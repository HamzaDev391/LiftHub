8. Product Principles

These are the standing design rules the team (human or AI agent) should apply when making judgment calls not explicitly covered elsewhere in this PRD.

# Principle	What It Means in Practice

P1	Speed beats completeness during a workout.	If a screen is used during an active session, minimize taps, fields, and decisions. Push optional detail (notes, RPE, etc.) behind secondary interaction, never in the primary flow.
P2	Show, don't require, historical context.	Previous performance is always visible where relevant (Section 2.4/G2) but never blocks progress — a user can log a set with zero reference to history if they choose.
P3	One thing done well beats many things done adequately.	Directly from the brief's philosophy. When scoping a feature, ask "does this serve logging, history, or progress?" If not, it's out of V1 (Section 10).
P4	Offline is not an edge case — it's a primary case.	Gym connectivity is unreliable by default, not exceptionally. Every core flow (start session, log set, finish session) must work with zero connectivity and sync later without data loss.
P5	Never lose a logged set.	Data loss during an active workout is the single worst failure mode possible for this app — worse than a crash, worse than a slow sync. Local-first writes with guaranteed persistence take priority over real-time sync guarantees.
P6	No manufactured engagement.	No streak-shaming, no guilt notifications, no gamified pressure mechanics (2.3). Retention comes from utility, not psychological hooks.
P7	Design for one role now, architect for three later.	Every schema/architecture decision should ask "does this block future Trainer/Owner roles?" without actually building for those roles now (2.5).
P8	Prefer the simpler solution unless there's a compelling reason otherwise.	Directly from the brief. Default to boring, proven patterns; complexity must justify itself with clear user or architectural value.
P9	Explicit over implicit, everywhere.	Business rules, defaults, and edge-case behavior are stated outright in this document, not left to inference — supports the AI-agent-readability goal (2.6).

Design Impact: P5 in particular has a concrete architectural consequence beyond what's already noted: it implies local persistence (e.g., a local SQLite/drift store on-device) is not just a "nice to have" for offline support but a hard requirement — the app should never hold an in-progress workout only in volatile app memory. Worth flagging clearly for the future architecture doc.

