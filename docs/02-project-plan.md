# Project Plan: Mile Marker (Road Trip Planner)

Rules and their reasons are in `docs/decisions.md` (D1–D9). Words are defined in `docs/glossary.md`.

## Requirements → features
| Requirement (official) | Feature(s) | Priority |
|---|---|---|
| Set a trip budget and daily travel-time limit | F1 Trip settings | Must |
| Add, edit, remove stops (name, day, category, cost) | F2 Stop editing | Must |
| Reorder stops | F3 Reorder (Move Up / Move Down) | Must |
| Enter distance and travel time between consecutive stops | F4 Legs | Must |
| Reject negative values and connections to missing stops | F4 Legs (validation), F2 | Must |
| Flag outdated estimates when stops change | F4 Legs (status), F2, F3 | Must |
| Search stops by name | F5 Search & filter | Must |
| Filter stops by day or category | F5 Search & filter | Must |
| Total distance, travel time, planned cost, remaining budget | F6 Summary | Must |
| Flag trip over budget and days over the travel-time limit | F6 Summary | Must |
| Clearly show when estimates are incomplete | F6 Summary, F4 | Must |
| Save and reopen with stops, order, legs, budget, limit intact | F7 Save & load | Must |
| Fictional / hand-entered estimates only | F4 (typed in by user), F7 sample file | Must |
| (All projects) clear messages for bad input | F1, F2, F3, F4 | Must |
| (All projects) data stays consistent when things change | F2, F3, F4 | Must |

## Rules I decided
- **Leg** = the drive *from the previous stop to this stop*. The first stop has no leg. (D2)
- A leg's drive time counts toward the **day of the stop you arrive at**. (D1)
- Leg status: **CURRENT** (counted), **OUTDATED** (previous stop changed because of add/remove/reorder; old numbers shown, not counted), **MISSING** (never entered; new stops start here). (D2)
- Editing only a stop's name, cost, or category does **not** make a leg outdated. (D8)
- Totals add only CURRENT legs; if any leg is OUTDATED or MISSING, show "⚠ Incomplete: X outdated, Y missing". (D3)
- Distance in miles (decimal OK, ≥ 0). Drive time entered as hours + minutes, stored as whole minutes (≥ 0). (D4)
- Over budget = planned cost **>** budget (equal is OK). Remaining budget may be negative. (D4)
- A day is over the limit when its total drive minutes **>** the daily limit. (D4)
- Trip has a number of days (sample: 7). A stop's day must be 1 to that number. (D5)
- Day numbers never go backwards in the stop list. Adds, edits, or moves that break this are rejected. (D6)
- Categories: Food, Sightseeing, Lodging, Activity, Other (fixed list). (D7)
- Stop name not blank and unique (ignoring capitals). Cost ≥ 0. Budget ≥ 0. Daily limit > 0. (D8)
- A leg can only be entered for a stop that exists and is not the first stop ("connection to a missing stop" is rejected). (D2)
- Save button writes `data/trip.txt`; app loads it on start; missing file → empty trip + friendly message. (D9)

## Features by priority
### Must (needed for requirements)
- [ ] F1 Trip settings: budget, daily drive limit, number of days
- [ ] F2 Add / edit / remove stops, with validation
- [ ] F3 Reorder stops (Move Up / Move Down)
- [ ] F4 Legs: enter distance + time; CURRENT / OUTDATED / MISSING status
- [ ] F5 Search by name; filter by day or category
- [ ] F6 Summary: totals, remaining budget, over-budget flag, over-limit days, incomplete warning
- [ ] F7 Save / load `data/trip.txt` + sample San Diego → LA → SF → Las Vegas trip
### Should (makes it good)
- [ ] Confirm box before removing a stop
- [ ] Color: red for over-limit days / over budget, yellow for outdated legs
### Could (stretch)
- [ ] Printable day-by-day itinerary screen (only after feature freeze is safe)

## Build order
| When | Build | Done? |
|---|---|---|
| by Mon Nov 30 | Plan, class design, clickable HTML prototype (`docs/02`–`04`) | ☐ |
| Nov 30 – Dec 2 | Model + rules with tests: `Stop`, leg fields/status, `Trip` (F1, F2, F3, F4 rules). Main window showing the stop list; add/edit/remove (F2) | ☐ |
| Dec 2 – Dec 4 | Reorder buttons (F3), leg entry dialog (F4), summary panel (F6) | ☐ |
| Dec 4 – Dec 7 | Search & filter (F5), save/load + sample data file (F7). **Mon Dec 7 = feature freeze** | ☐ |
| Dec 7 – Dec 9 | Should items if time, bug fixes, test from a fresh download, write-up, slides, demo practice | ☐ |

## Risks
| Risk | What I'll do about it |
|---|---|
| Can't explain the code in Q&A (my biggest worry) | Run `/explain-it` after each feature; answer every "Check yourself" question myself |
| OUTDATED logic gets confusing | Keep all leg-status rules in `Trip`, with 1–3 tests each, before any UI |
| Running out of Claude usage | One feature per chat, `/checkpoint` + `/clear` after each |
| App doesn't compile from a fresh download | Clone the repo into a new folder and run `bash run.sh` before Dec 9 |
| Falling behind over the break | Musts first; Should/Could only after Dec 7 freeze is safe |

## Manual test checklist
| # | Do this | Expect this | Pass? |
|---|---|---|---|
| 1 | Set budget to −50 | Error: budget can't be negative; old value kept | ☐ |
| 2 | Set daily limit to 6h 0m | Summary shows limit 6h 0m | ☐ |
| 3 | Add stop "Santa Barbara", Day 2, Sightseeing, $25 | Stop appears in list; planned cost +$25; its leg shows MISSING | ☐ |
| 4 | Add a stop with blank name, or cost −10, or day 9 | Clear error message; nothing added | ☐ |
| 5 | Add a second stop named "las vegas" | Error: name already used | ☐ |
| 6 | Edit a stop's cost from $25 to $40 | Planned cost updates; its leg status unchanged | ☐ |
| 7 | Remove a middle stop | Stop gone; the next stop's leg becomes OUTDATED | ☐ |
| 8 | Move a stop up past the stop before it (same day) | Order changes; affected legs become OUTDATED | ☐ |
| 9 | Move a Day 3 stop above a Day 2 stop | Error: days can't go backwards; order unchanged | ☐ |
| 10 | Enter leg LA → Santa Barbara: 95 mi, 1h 45m | Leg shows CURRENT; totals increase | ☐ |
| 11 | Enter a leg with −20 miles or −5 minutes | Error message; leg unchanged | ☐ |
| 12 | Try to enter a leg for the first stop | Rejected: first stop has no previous stop | ☐ |
| 13 | Make one leg OUTDATED | Summary shows "⚠ Incomplete: 1 outdated…"; that leg not in totals | ☐ |
| 14 | Search "vegas" | Only stops with "vegas" in the name show (any capitals) | ☐ |
| 15 | Filter Day 3, then filter Food | Only Day 3 stops, then only Food stops show | ☐ |
| 16 | Add a $300 stop so cost > budget | "Over budget" flag; remaining budget negative | ☐ |
| 17 | Make one day's legs total more than the limit | That day flagged over the limit | ☐ |
| 18 | Save, close, run again | Same stops, order, legs + statuses, budget, limit, days | ☐ |
| 19 | Rename `data/trip.txt`, start the app | Friendly message; empty trip; no crash | ☐ |

## Demo story (about 4 min)
1. Open the app: the 7-day San Diego → LA → SF → Las Vegas trip loads.
2. Add "Santa Barbara" between LA and SF: the SF leg turns OUTDATED and the incomplete warning appears.
3. Enter the new legs: the warning goes away and totals update.
4. Filter to Day 3, then search "Vegas".
5. Add "Vegas show $300": the trip goes over budget and the warning shows.
6. Try a negative distance: error message.
7. Save, close, reopen: everything is still there.
