6. Target Users
   6.1 Primary User Segment (V1)
   Attribute	Description
   Who	Beginner-to-intermediate gym-goers
   Training frequency	3–6 days per week
   Training style	Structured resistance training with defined exercises, sets, reps, and weight — not purely improvisational
   Primary motivation	Getting stronger / visible progress over time (progressive overload), not just "staying active"
   Current tool	Notes app, paper notebook, spreadsheet, or memory (per Section 3)
   Tech comfort	Comfortable with everyday mobile apps; no assumption of advanced fitness-app experience
   Key frustration	Losing track of previous performance; friction in existing tools mid-workout

6.2 Explicitly Excluded From V1 Targeting
Excluded Group	Why
Coaches / personal trainers	Trainer role is post-V1 (Section 2.5); V1 has no multi-client management
Gym owners / gym staff	Owner role is post-V1; no gym-management features exist
Competitive powerlifters with highly specialized programming (e.g., percentage-based periodization, RPE autoregulation)	Their needs (complex programming logic, coach-prescribed periodized plans) add significant complexity for a small, demanding niche — explicitly deferred per the brief's Non-Goals
Users primarily seeking nutrition/meal tracking	Explicit non-goal (Section 10 will formalize this)
Complete fitness beginners with no structured routine at all	Not excluded from using the app, but V1's exercise library and routine-builder assume the user already knows what a "routine" and "set/rep" structure is — onboarding does not teach someone how to train from zero. Worth flagging as a scoping boundary.

Design Impact: Because V1 assumes users already understand basic training structure, onboarding (Section 14/15) does not need to include educational content about what a "set," "rep," or "routine" means — this simplifies first-run UX and keeps scope tight, but it's a deliberate exclusion worth being explicit about.

6.3 Geographic / Platform Assumptions
Assumption	Note
No geographic targeting restriction	App is generally usable anywhere; no region-locked content
Mobile-only (Flutter, iOS + Android)	No web or desktop client in V1
Units	Must support both metric (kg) and imperial (lb) — not a US-only or region-only assumption (ties to Settings → Unit Preferences from the original feature list)

