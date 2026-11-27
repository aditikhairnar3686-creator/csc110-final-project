# Steering Log
<!-- How YOU directed Claude. /checkpoint drafts an entry at the end of each task and asks you to correct it.
Be honest and specific. The best entries show a moment you changed Claude's direction.
You'll use these in your write-up and slides. Template:

## <date> — <task>
- **Goal:**
- **What I asked for:**
- **How I steered / corrected Claude:** (rejected an idea, caught a bug, asked for simpler code, gave an example...)
- **What I learned:**
- **Next:**
-->

## 2026-11-26 — Finish and submit proposal
- **Goal:** Finalize docs/01-proposal.md (Mile Marker road trip planner) and turn it in.
- **What I asked for:** To see the finished proposal, then whether I needed a git tag for it.
- **How I steered / corrected Claude:** Nothing to correct in this chat. I asked about the tag myself before committing.
- **What I learned:** Each deliverable needs a git tag (`proposal`, `plan-design-prototype`, `final`) so the instructor can see what I had on the due date.
- **Next:** /project-plan (due Mon Nov 30 with the class design and UI prototype).

## 2026-11-26 — Project plan
- **Goal:** Write docs/02-project-plan.md with every official requirement mapped to a feature.
- **What I asked for:** Ran /project-plan and answered three rounds of questions (12 questions) on rules, priorities and the demo.
- **How I steered / corrected Claude:** I first picked 1B (a leg counts toward the day you leave from), then changed my mind to 1A (the day you arrive). Claude updated D1. I accepted Claude's recommendations for the other 11 questions.
- **What I learned:** The requirements leave rules open (when a leg is "outdated", what "over budget" means, whether days can go backwards). I have to decide them and write them down in decisions.md so I can explain why.
- **Next:** /class-design (due Mon Nov 30 with the plan and UI prototype).

## 2026-11-27 — Class design
- **Goal:** Write docs/03-class-design.md (classes, diagram, where the rules live, save format).
- **What I asked for:** Ran /class-design and answered 4 design questions (Leg as its own class, String error messages, double money, edge cases). All four went with Claude's recommendations.
- **How I steered / corrected Claude:** Claude decided D16 (new stops are placed by day) without asking me, and flagged it for my confirmation. I approved it. I then asked Claude to check the design against the official requirements and keep it beginner-friendly so I can explain every method. That check found 4 problems in Claude's draft: setters that didn't validate, editing from a filtered list, a wrong setLeg signature in the diagram, and Move Up/Down at the ends of the list. Claude fixed them. I approved the new D17 rule (leg minutes 0–59).
- **What I learned:** Trip is the manager that owns the stops and enforces the rules. addStop returns a String so the program can report success or explain why a stop was rejected. Totals are calculated fresh, not stored, so they always stay correct.
- **Next:** /ui-prototype (due Mon Nov 30 with the plan and class design).
