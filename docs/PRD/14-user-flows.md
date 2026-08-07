14. User Flows
    High-level flow descriptions for the core paths. Detailed screen-by-screen wireframe-level flows belong in a future UX doc, but these establish the required navigational logic an engineer or AI agent needs before building screens (Section 15).

14.1 Flow: First-Time Onboarding
App Launch (no session)
→ Sign Up (email/password OR Google) [FR-AUTH-01, FR-AUTH-02]
→ Profile creation (optional fields — can skip) [FR-PROF-05]
→ Home / Dashboard

Key rule: Profile completion is never a blocking gate (FR-PROF-05, P1) — user can reach Home and start a session immediately after signup.

14.2 Flow: Starting and Completing a Workout Session (Core Loop)
Home / Dashboard
→ [Option A] Select a saved Routine → Start Session (pre-loaded exercises) [FR-SESS-01]
→ [Option B] Start Freeform Session (no routine) [FR-ROUT-07]
→ Active Session screen:
→ Add/select exercise
→ View previous performance for that exercise (auto-shown) [FR-SESS-04]
→ Log set (weight, reps) [FR-SESS-03]
→ (Rest timer triggers) [FR-SESS-06]
→ Repeat: log next set / add next exercise
→ (Optional) Add note to exercise [FR-SESS-07]
→ Finish Session [FR-SESS-08]
→ Session Summary (PRs hit this session, if any) [FR-PR-05]
→ Return to Home

Key rule: Every step from "Active Session screen" onward must function with zero connectivity (FR-SESS-11, NFR-REL-02).

14.3 Flow: Reviewing Progress
Home / Dashboard
→ History tab → List of past sessions [FR-HIST-01]
→ Tap a session → Full session detail [FR-HIST-02]
→ OR: Statistics tab → Simple view (default) [FR-STAT-03]
→ Expand → Volume trends / exercise frequency
→ OR: From within a session/exercise, view that exercise's full history + PR [FR-HIST-03, FR-PR-04]

14.4 Flow: Recovering an Interrupted Session
App reopened after crash/force-close during active session
→ App detects an in-progress (unfinished) session exists locally [FR-SESS-12]
→ User is returned directly to that Active Session screen, with all previously logged sets intact
→ User can continue logging, or explicitly finish/discard the session [FR-SESS-08, FR-SESS-13]

Key rule: This flow must never silently discard an in-progress session — recovery is the default behavior, not an edge case (P5).

