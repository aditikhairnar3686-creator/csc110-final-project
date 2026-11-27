# Decisions
<!-- Claude adds entries during /grill-me and planning. Only the "why did you do it that way?" decisions.
Newest at the bottom. Template:

## D<number>: <short title>
**Decided:** what we chose.
**Why:** the reason, in 1-2 sentences.
**Other options:** what we didn't pick (optional).
-->

## D1: A leg's drive time counts toward the day you arrive
**Decided:** The drive between two stops counts toward the day number of the stop you are driving TO.
**Why:** You drive in the morning and arrive at that day's stop, and the leg is stored on that same stop, so it is simple to explain and to code.
**Other options:** Count it toward the day of the stop you leave from (first picked, then changed).

## D2: Each stop owns the leg from its previous stop; changes mark it OUTDATED
**Decided:** Every stop except the first holds one leg ("from the previous stop") with a status: CURRENT, OUTDATED, or MISSING. If a stop's previous stop changes (add, remove, reorder), its leg becomes OUTDATED: old numbers stay visible but are not used. A new stop's leg starts MISSING.
**Why:** The requirement says to flag outdated estimates, not delete them, and keeping old numbers makes them quick to fix.
**Other options:** Delete old numbers (back to MISSING); store legs in a separate list keyed by stop pairs.

## D3: Totals use only CURRENT legs and warn when incomplete
**Decided:** Total distance/time add only CURRENT legs. If any leg is OUTDATED or MISSING, the summary shows a warning like "Incomplete: 2 outdated, 1 missing".
**Why:** You still get useful numbers, and the warning satisfies "clearly show when estimates are incomplete".
**Other options:** Hide totals until every leg is filled in.

## D4: Units and "over" rules
**Decided:** Distance in miles (decimal allowed). Drive time entered as hours + minutes, stored as whole minutes (`int`). Over budget = planned cost > budget (equal is OK); remaining budget may be negative. A day is over the limit when its drive minutes > the daily limit.
**Why:** Whole minutes keep the math simple; "greater than" is the normal meaning of "over".

## D5: The trip has a set number of days
**Decided:** A trip has a day count (sample trip: 7). A stop's day must be from 1 to that count; anything else is rejected with a message.
**Why:** Gives a clear, testable rule, and the per-day travel-time check needs a known set of days.
**Other options:** Allow any day number of 1 or more.

## D6: Day numbers never go backwards in the stop list
**Decided:** Any add, edit, or reorder that would put a stop with a higher day before a stop with a lower day is rejected with a clear error.
**Why:** Keeps the plan making sense and is one simple rule to test.
**Other options:** Allow it with a warning; treat order and day as unrelated.

## D7: Categories are a fixed list
**Decided:** Food, Sightseeing, Lodging, Activity, Other, stored as `String` constants and picked from a dropdown.
**Why:** Filtering by category only works if the spelling is always identical.
**Other options:** Free-text categories.

## D8: Stop and trip validation rules
**Decided:** Stop name not blank; no duplicate names (ignoring capitals); cost >= 0; budget >= 0; daily limit > 0 minutes. Editing a stop's name, cost, or category does not make a leg OUTDATED; only order changes (add, remove, reorder) do.
**Why:** Unique names keep search results and messages clear; flagging legs only when the drive could have changed avoids false warnings.

## D9: Save with a button; load on start
**Decided:** A Save button writes `data/trip.txt`. The app loads that file when it starts; if it is missing, it starts an empty trip with a friendly message instead of crashing.
**Why:** Saving is visible in the demo ("save, close, reopen") and easier to explain than auto-save.
**Other options:** Save automatically after every change.

## D10: Leg is its own class, held by Stop
**Decided:** A `Leg` class (miles, minutes, status), and each `Stop` holds one `Leg` object.
**Why:** Keeps `Stop` small, puts the leg-status logic in one place, and shows an object holding another object.
**Other options:** Put `legMiles`, `legMinutes`, `legStatus` straight on `Stop`.

## D11: Rule methods return a String message
**Decided:** `Trip` methods that can be rejected return a `String`: `""` means it worked, anything else is the error to show.
**Why:** The rule writes its own message, so it lives in the model and can be tested. Exceptions aren't covered in CSC110 yet.
**Other options:** Return `boolean` and let the UI write the message.

## D12: Money is a double in dollars
**Decided:** Costs and budget are `double` dollars, shown with 2 decimals.
**Why:** Easiest to read and explain; precision is fine at this scale.
**Other options:** `int` cents; `int` whole dollars.

## D13: The first stop's leg is ignored
**Decided:** Whatever stop is first has its leg shown as "—", and it isn't counted in totals or the incomplete warning. If that stop later stops being first, the normal OUTDATED/MISSING rule applies.
**Why:** There is no previous stop to drive from, so the leg means nothing.

## D14: Can't lower the number of days below a stop's day
**Decided:** Changing the trip from 7 days to 5 is rejected if any stop is on day 6 or 7 ("move it first").
**Why:** Same "reject, don't break data" idea as D5 and D6.

## D15: Stop names can't contain "|"
**Decided:** Names containing `|` are rejected.
**Why:** `|` separates fields in the save file, so allowing it would corrupt the file.

## D16: A new stop is placed by its day
**Decided:** `addStop` inserts the new stop after the last stop with the same or an earlier day. Move Up/Down then fine-tune order within a day (they only swap stops with the same day).
**Why:** Appending to the end would break D6 for most new stops (e.g. adding a Day 2 stop to a 7-day trip), and it avoids needing a position picker.
**Other options:** Insert after the selected stop; always append to the end.

## D17: Leg minutes must be 0–59
**Decided:** When entering a leg, hours must be ≥ 0 and minutes must be from 0 to 59 (e.g. 1h 90m is rejected; type 2h 30m).
**Why:** Catches typos and keeps hours + minutes meaning one clear thing.
**Other options:** Allow any minutes ≥ 0 and convert them.
