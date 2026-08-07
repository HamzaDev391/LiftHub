4. Goals
   4.1 Product Goals (V1)
   ID	Goal	Rationale
   G1	Enable a user to log a complete workout session (multiple exercises, multiple sets each) in under the time it takes to do the workout itself, with minimal UI friction.	Directly addresses the core problem (3.4) — speed and low cognitive load during logging.
   G2	Surface the user's previous performance for an exercise automatically, at the moment they're about to log a new set.	Enables informed progressive-overload decisions in real time, per 3.2.
   G3	Give users a reliable, structured historical record of every workout they've logged.	Replaces the "memory" and "paper notebook" failure modes in 3.1.
   G4	Automatically compute and surface personal records (PRs) and basic progress trends without manual calculation.	Removes the spreadsheet failure mode (manual formula maintenance) and gives users a sense of tangible progress.
   G5	Work reliably with poor or no gym wifi/cellular connectivity.	Gyms are frequently dead zones; this is a functional requirement, not a nice-to-have — reinforced by the offline-first decision in Section 2.
   G6	Ship a V1 focused enough to actually reach the Play Store and App Store, rather than stall in scope creep.	Stated project goal — a narrow, shippable V1 beats a broad, unfinished one.
   G7	Produce an architecture and data model that supports future Trainer/Owner roles without requiring a rebuild.	Long-term vision (2.5) — avoid technical debt that blocks the product roadmap.

4.2 Engineering / Portfolio Goals (V1)

These sit alongside product goals since this is a flagship portfolio project, not just a business deliverable.

ID	Goal
EG1	Demonstrate professional-grade Flutter architecture (clean separation of concerns, testable code, feature-based structure).
EG2	Demonstrate a properly normalized, RLS-secured Supabase/PostgreSQL schema.
EG3	Produce documentation (this PRD, future ERD, architecture docs) detailed enough for another engineer or an AI coding agent to work from with minimal back-and-forth.
EG4	Ship to both major app stores, satisfying their respective review/compliance requirements.

4.3 Non-Goals of This Section

Goals here are intentionally about the product working well for a single lifter. Goals related to business monetization, growth/acquisition, or multi-role functionality are explicitly out of scope for V1 and are not listed here — see Section 10 (Explicit Non-Goals) and Section 23 (Future Roadmap).

