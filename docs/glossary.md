# Glossary
<!-- Your project's own words, agreed once so you and Claude mean the same thing. Claude adds terms
during /grill-me. Format:

**Term**: one or two sentences saying what it IS.
_Avoid_: other words that mean the same thing (so we always use one name).
-->

**Trip**: The whole plan: a budget, a daily drive-time limit, and an ordered list of stops.
_Avoid_: journey, route, itinerary (itinerary is only the stretch-goal printout).

**Stop**: One place on the trip, with a name, day number, category, and activity cost.
_Avoid_: destination, location, waypoint.

**Leg**: The drive from the previous stop to this stop: distance (miles), drive time (minutes), and a status. The first stop has no leg.
_Avoid_: segment, connection, route, travel estimate (use "leg" in code).

**Leg status**: CURRENT (numbers are up to date and counted), OUTDATED (the stops around it changed, so the numbers are shown but not counted), or MISSING (no numbers entered yet).

**First stop**: Whatever stop is at the top of the list right now. It has no leg that counts (D13).
_Avoid_: start, origin.

**Planned cost**: The sum of every stop's cost. Remaining budget = budget − planned cost.
_Avoid_: total spent, expenses.
