2. Product Vision
2.1 Vision Statement
LiftHub is the fastest, most reliable way for a lifter to know exactly what they did last time — and to log what they're doing right now — without breaking focus on the workout itself.
2.2 What LiftHub Is
LiftHub is a single-purpose workout logger, not a fitness "super-app." Every screen exists to serve one of three moments in a user's gym session:

1. Before the workout — deciding what to do (routine selection).
2. During the workout — logging sets fast, with minimal cognitive load, while physically tired and time-constrained.
3. After the workout — seeing that the effort mattered (history, PRs, trends).

2.3 What LiftHub Is Not (V1)
LiftHub is not a social network, not a coaching platform, not a nutrition tracker, and not a gym management tool in V1. It does not try to retain users through gamification, streak-shaming, or social pressure. Retention is earned by being genuinely useful and fast, not by manufactured engagement loops.
Design Impact: This has a direct architectural consequence — no feature in V1 should introduce a dependency on real-time multi-user data (e.g., leaderboards, shared feeds), which keeps the Supabase schema simple (single-tenant-per-user reads for most of the app) and RLS policies straightforward for now. Multi-user read patterns are deferred to the Trainer/Owner roadmap.
2.4 The "During Workout" Principle (final — with logging-mode decision added)

The single highest-leverage design constraint in this entire product is this: a user is mid-set, possibly out of breath, and needs to log weight × reps in the fewest taps possible, with the previous session's numbers already visible for reference.

Every V1 feature decision should be evaluated against this principle first. If a feature makes the "log a set" flow slower or more cluttered to accommodate something else, that something else does not belong in V1 — this is the practical test we'll apply when scoping features in Section 9 (MVP Scope).

Logging mode decision: V1 is optimized primarily for live, set-by-set logging (log each set immediately after performing it) rather than after-the-fact bulk entry from memory. This is the dominant real-world usage pattern for workout trackers and produces more accurate data, which is essential to the app's core purpose (progressive overload tracking). Retroactive logging (e.g., a missed or forgotten session) is still supported — the same Workout Session screen handles both cases — but no dedicated bulk-entry UI is built for it in V1.

Design Impact: This implies the workout-session data model needs to support fast, optimistic local writes (log a set, see it immediately, sync in background) rather than waiting on a network round-trip per set — reinforcing the offline-first requirement flagged in Section 1. It also means the Workout Session screen is a single unified interface for both live and retroactive entry, with no separate "log past workout" flow in V1.
2.5 Long-Term Vision (Context Only — Not V1 Scope)
LiftHub eventually becomes a three-role ecosystem (Member, Trainer, Gym Owner), as described in the brief. V1 exists to prove the Member experience is excellent in isolation before any multi-role complexity is introduced. The vision matters here only insofar as it constrains V1 architecture — e.g., using a `role` field on the user/profile table from day one (even if only `member` is a valid value in V1) so future roles don't require a schema migration that touches every table.
Design Impact: Recommend a `profiles` table with a `role` enum (`member` for V1, `trainer`/`owner` reserved) from the start, and ownership/foreign-key patterns (`user_id` on every workout-related table) designed so that "which rows can Trainer X see for Client Y" is a straightforward RLS policy addition later, not a redesign.
2.6 AI-Agent Readability Note
Since this PRD is meant to make downstream AI-agent-assisted development easier, I'll carry a consistent discipline through every section:

* Explicit terminology — I'll define terms once (see future Glossary, Section 25) and use them consistently (e.g., always "workout session," never sometimes "workout" and sometimes "session" for the same concept).
* Explicit business rules, not implied ones (e.g., not "reasonable defaults" but the actual default values).
* Structured, table-driven specs where possible, since agents parse structured data more reliably than prose.
* Numbered, referenceable requirements in Sections 11+ so later docs (ERD, architecture) can cite back to a specific FR/NFR ID.

Look back into this section and tell me is this the final one or any changes are done, and also give me next sections too
