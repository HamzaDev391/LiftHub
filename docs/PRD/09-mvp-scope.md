9. MVP Scope
   9.1 Scoping Method

Every candidate feature from the brief's "Planned V1 Features" list is run through this test, derived from Sections 2.4 and 8 (P3):

Does this feature directly serve logging a workout, viewing history, or tracking progress for a single Member? And does it avoid adding friction to the live-logging flow (P1)?

If yes to the first and it passes the second → In Scope.
If it's adjacent-but-not-core, or adds meaningful complexity for uncertain value → Deferred, with reasoning.

9.2 In-Scope V1 Features
Feature Area	Included	Notes
Authentication	Email/password, Google Sign-In	Supabase Auth handles both natively
User Profile	Name, height, weight, fitness goal, experience level, preferred units	Needed for personalization and unit display (kg/lb)
Exercise Library	Built-in exercises, muscle groups, equipment, instructions	Core dependency for routines and logging — can't log a set without an exercise to log it against
Workout Templates (Routines)	Create, edit, delete, duplicate	Directly serves "before the workout" (2.2)
Workout Session	Start workout, log sets (weight, reps), previous performance shown, workout timer, rest timer, exercise notes	Core of the app — the "during workout" moment
Workout History	Previous workouts, previous sets	Core "after the workout" value (G3)
Personal Records	Highest weight, estimated 1RM, highest volume	Automatic computation, no manual entry — ties to G4
Statistics	Workout frequency, weekly volume, streaks, total workouts, exercise frequency	Supports Persona B (Sara) without cluttering the primary flow for Persona A (Ahmed) — see 9.4 on presentation
Settings	Dark mode, unit preferences, delete account	Baseline expectations for a production app

9.3 Features Requiring a Scoping Decision (Called Out From the Original List)
Feature	Recommendation	Reasoning
Export data	Defer to post-V1, unless you object	The brief listed this as "if appropriate for MVP" — it doesn't serve logging, history, or progress directly (fails the 9.1 test), and export formats/destinations (CSV? PDF? email?) add real scope. It's a good V1.1 feature once core logging is proven.
Streaks (under Statistics)	Include, but as passive display only — not a notification or pressure mechanic	Conflicts on the surface with P6 (no manufactured engagement), but a passive streak count (like a stat, not a push notification nagging you not to break it) is informational, not manipulative. I'd draw the line at: show it if asked, never push it at the user.

9.4 Statistics Presentation — Simple vs. Expanded

Flagged in Section 7's Design Impact: Ahmed (beginner) and Sara (intermediate) want different depths of stats. Recommendation for V1: a single Statistics screen with a simple default view (frequency, streak, total workouts) and an expandable/secondary section for volume trends and exercise-frequency breakdowns. This avoids building two separate screens (added complexity, P8) while still respecting P1's "don't overload the primary experience" for Ahmed-like users.

Open Question: Should experience level (from Section 6.2/Profile) auto-adjust which stats view is default, or should it always default to "simple" for everyone and let the user expand manually? I'd lean toward the latter (simpler, no hidden personalization logic) — flagging for your call.

9.5 Explicitly Out of MVP Scope

Deferred to Section 10 (Explicit Non-Goals) for the full list and reasoning — this section only covers features that were in the original "Planned V1 Features" list but didn't make the cut (Export Data, per 9.3).

