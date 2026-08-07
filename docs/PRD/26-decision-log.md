26. Decision Log

This section records accepted product decisions that resolve previously open questions or establish new rules during PRD development.

## Decision Entries

### DL-001

Date: 2026-08-07
Status: Accepted
Related Sections: 11.3 (FR-EXLIB-04), 6.2, 10, 15.4
Decision: Members can create custom exercises in V1.
Rationale: Real users inevitably need gym-specific exercise variations not covered by any preset library; blocking this breaks the core logging flow (P1/P3).
Alternatives Considered: Built-in library only (rejected — too restrictive for real-world gym equipment variation).
Design Impact: Custom exercises are private per-user (FR-EXLIB-05, BR-03); no shared/public custom exercise library in V1.

### DL-002

Date: 2026-08-07
Status: Accepted
Related Sections: 11.7 (FR-PR-03), 16.2, 18 (EC-09)
Decision: Estimated 1RM uses the Epley formula: 1RM = weight × (1 + reps/30).
Rationale: Industry-standard default, simple to implement and explain.
Alternatives Considered: Brzycki formula (rejected — no material advantage for V1 use case).
Design Impact: See DL-011 for the applicable rep-range cap on this formula.

### DL-003

Date: 2026-08-07
Status: Accepted
Related Sections: 11.8 (FR-STAT-04), 16.3
Decision: Streak = number of consecutive calendar weeks in which the Member logged at least one finished Workout Session. A week with zero finished sessions breaks the streak.
Rationale: Simplest to compute and simplest for a user to understand; avoids ambiguity of rolling-window definitions.
Alternatives Considered: Rolling 7-day window (rejected — harder to communicate to the user, ambiguous "week" boundary); daily-requirement streak (rejected — conflicts with P6, unrealistic for a 3–6x/week training pattern).
Design Impact: Streak calculation needs only session `finished_at` timestamps grouped by calendar week — no additional schema beyond session records.

### DL-004

Date: 2026-08-07
Status: Accepted
Related Sections: 12.2 (NFR-REL-03), 17 (BR-01), 18 (EC-06)
Decision: Offline sync conflicts resolve via last-write-wins at the session level (not field-level merge), based on most recent local modification timestamp.
Rationale: Simpler solution per P8; BR-01 (one active session at a time per user) makes true concurrent conflicts rare in practice.
Alternatives Considered: Field-level merge (rejected — meaningfully more complex for low expected conflict frequency).
Design Impact: Architecture doc must implement session-level `updated_at`/`modified_at` comparison during sync reconciliation.

### DL-005

Date: 2026-08-07
Status: Accepted
Related Sections: 11.5 (FR-SESS-07)
Decision: Workout notes exist at the exercise level only in V1, not at the session/workout level.
Rationale: No clear use case for session-level notes yet; keeps the data model simpler and can be added later without schema pain.
Alternatives Considered: Both levels (rejected — added scope with no validated demand).
Design Impact: None — confirms existing FR-SESS-07 behavior; no FR changes needed.

### DL-006

Date: 2026-08-07
Status: Accepted
Related Sections: 17 (BR-05, new BR-09), 16.1, 18 (EC-07)
Decision: User-generated/user-owned content with historical dependencies (custom exercises, abandoned sessions) is soft-deleted rather than hard-deleted, applied as a uniform V1-wide pattern rather than decided per feature.
Rationale: Preserves historical session/PR integrity; a single consistent rule is easier for an AI coding agent to implement correctly than per-feature exceptions.
Alternatives Considered: Hard delete with cascade (rejected — would corrupt past session records, per BR-05's original concern); block deletion entirely (rejected — overly restrictive for the user).
Design Impact: Exception — full account deletion (FR-SET-03/BR-06) still performs actual hard deletion, required for App Store/Play Store compliance (NFR-SEC-04). Soft-delete applies to individual content items, not full-account deletion.

### DL-007

Date: 2026-08-07
Status: Accepted
Related Sections: 17 (BR-08), 11.8
Decision: Deleted/abandoned sessions never count toward Statistics or Personal Records, regardless of what data they contained.
Rationale: Extends the existing BR-08 principle (only finished sessions count) to also cover the deletion/abandonment case explicitly, per P9 (explicit over implicit).
Alternatives Considered: None — this is a direct extension of an already-accepted rule.
Design Impact: Stats/PR queries must filter on session state = finished AND not soft-deleted.

### DL-008

Date: 2026-08-07
Status: Accepted
Related Sections: 11.7 (FR-PR-02), 16.2
Decision: PRs are recomputed immediately on every set create/edit/delete event, not batched at session end.
Rationale: This was already the specified behavior in FR-PR-02/16.2; OQ-10 is resolved by confirming existing behavior, not changing it.
Alternatives Considered: Batch recomputation at session finish (rejected — delays PR feedback, which conflicts with FR-PR-05's "indicated at the moment it's set").
Design Impact: None — no FR changes required.

### DL-009

Date: 2026-08-07
Status: Accepted
Related Sections: 17 (BR-02), 11.5 (new FR-SESS-14), 16.2
Decision: Members can edit sets within a finished session (not just an active one), to correct data-entry mistakes noticed after the fact. Editing a finished session's sets triggers the same PR/Statistics recalculation as editing an active session.
Rationale: Data-entry mistakes aren't limited to mid-workout; blocking post-finish edits would leave users unable to fix known errors.
Alternatives Considered: Immutable finished sessions (rejected — too restrictive, no clear reason to block correction).
Design Impact: New FR-SESS-14 added. PR/stat recalculation logic must trigger on finished-session edits, not just active-session edits.

### DL-010

Date: 2026-08-07
Status: Accepted
Related Sections: 11.2 (FR-PROF-04)
Decision: Fitness goal values = Build Muscle, Lose Fat, Get Stronger, General Fitness. Experience level values = Beginner, Intermediate, Advanced.
Rationale: Standard, sufficient categories for V1 personalization; avoids over-engineering a taxonomy with no validated need for more granularity.
Alternatives Considered: None proposed beyond these.
Design Impact: ERD enum values for `fitness_goal` and `experience_level` fields are now fixed.

### DL-011

Date: 2026-08-07
Status: Accepted
Related Sections: 18 (EC-02, EC-09)
Decision: (a) A set with 0 reps is invalid and blocked from saving (hard validation rule). (b) Estimated 1RM is computed and displayed only for sets with ≤15 reps; sets above that are excluded from 1RM display.
Rationale: (a) 0 reps isn't a meaningful data point, consistent with EC-01 allowing 0/null weight but not 0 reps. (b) The Epley formula becomes unreliable at high rep counts; a wildly inaccurate estimate is worse than no estimate.
Alternatives Considered: Allowing 0-rep sets as a placeholder (rejected — no meaningful use case); showing 1RM regardless with a caveat label (rejected — adds UI complexity for a number to be distrusted anyway).
Design Impact: Set validation logic must enforce reps ≥ 1. PR calculation logic must exclude sets >15 reps from 1RM computation specifically (Max Weight and Max Volume PRs are unaffected by this cap).

