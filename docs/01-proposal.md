# Project Proposal

**Name:** Aditi Khairnar
**Project:** Road Trip Planner
**App name:** Mile Marker
**Repo link:** https://github.com/aditikhairnar3686-creator/csc110-final-project

## My idea in two sentences
Mile Marker is for a traveler planning a multi-day road trip who wants to know if the trip fits their
budget and how much driving they can handle each day. They add the stops, enter the distance and drive
time between them, and the app shows totals and warns them when something goes over the limit.

## My twist / theme
My sample trip is a real one along the West Coast and into the desert: **San Diego → Los Angeles →
San Francisco → Las Vegas**, over **7 days**. The demo data will use these cities and the kinds of things I'd actually
do in each one.

## Requirements checklist
Official requirements for the Road Trip Planner (from `docs/reference/project-ideas.md`):

- [ ] Set a trip budget and a daily travel-time limit
- [ ] Add, edit, remove, and reorder stops (each stop has a name, day number, category, and activity cost)
- [ ] Enter distance and travel time between consecutive stops
- [ ] Reject negative distance/time values and connections to missing stops
- [ ] When stops change, flag outdated travel estimates instead of using them as current
- [ ] Search stops by name
- [ ] Filter stops by day or by category
- [ ] Show total distance, total travel time, planned cost, and remaining budget
- [ ] Flag a trip that is over budget, and days that are over the travel-time limit
- [ ] Clearly show when travel estimates are incomplete
- [ ] Save and reopen the trip with stops, order, travel estimates, budget, and daily limit intact
- [ ] Use fictional or hand-entered travel estimates (no live maps, bookings, or route optimization)

Every project also needs: data in classes/objects and `ArrayList`s, data that stays consistent when
things change, clear messages for bad input, search/filter, calculated summaries, and save and reopen.

## The 60-second demo I imagine
I open Mile Marker and my saved San Diego → LA → SF → Las Vegas trip loads. I add a new stop, and the
total cost and remaining budget update right away. The travel estimate next to the changed stop gets
flagged "outdated". Then I go over budget on purpose so the class sees the warning. I save, close the
app, reopen it, and everything is still there.

## One stretch goal (if time allows)
A printable day-by-day itinerary screen that lists each day's stops, drive time, and cost.

## My biggest worry
Explaining the code in the Q&A. I want to understand every class well enough to answer questions
about it myself.
