5. Success Metrics
   5.1 On Metrics for a V1 Portfolio Product

Worth naming directly: typical startup PRDs lean heavily on growth/business metrics (DAU, retention curves, CAC, etc.), which assume a launched product with real user acquisition. For LiftHub V1, that framing is premature — there's no user base yet, and manufacturing vanity metrics for a document like this would just be noise. Instead, I'd recommend defining success primarily in terms of product-quality and usage-quality metrics you can actually observe once the app is in your own hands (and a small test group's), with lightweight placeholders for growth metrics once it's live. Flagging this as a deliberate scoping choice rather than an oversight.

5.2 Core Usage Metrics (Post-Launch, Measurable)
Metric	Target (Directional)	Why It Matters
Time to log a single set	< 5 seconds from tap to confirmed save	Directly tests G1/the "During Workout" principle (2.4).
Time to complete full session logging (relative to actual workout duration)	Logging overhead should feel negligible to the user (qualitative check, not a hard number in V1)	Tests G1 at the session level.
% of workout sessions logged with zero sync/data-loss issues	100% (non-negotiable — data loss is a trust-breaking failure for this app)	Tests G5, offline reliability.
App crash-free session rate	> 99%	Baseline mobile app quality bar; also an app-store review-quality signal.
Weekly active logging (self-tracked, post-launch)	N/A for V1 spec — deferred to post-launch analytics setup	Real retention signal, but requires a live user base to mean anything.

5.3 Product-Quality Metrics (Pre-Launch, Verifiable During Development)
Metric	Target
Core "start workout → log all sets → finish workout" flow	Completable in a single unbroken flow with no dead ends or required navigation away from the active session screen
Previous-performance data visibility	Visible without requiring a tap/navigation, at the point of logging a new set (per G2)
Offline logging	A full workout session can be logged with zero network connectivity and syncs correctly once connectivity returns
PR/stat computation correctness	100% accurate against manually verified test cases (no silently wrong math — this erodes trust fast)

5.4 Engineering Success Metrics
Metric	Target
RLS policy coverage	Every table containing user data has RLS enabled and tested — no accidental cross-user data exposure
Test coverage on core logic (PR calculation, volume calculation, sync logic)	Meaningful automated test coverage — not necessarily a % target, but no untested critical-path business logic
App store review	Passes both Google Play and Apple App Store review on first or second submission (no major compliance rework)

5.5 Explicitly Deferred Metrics

Not defined in V1 because they require a live product and user base:

Retention curves (D1/D7/D30)
User acquisition cost / channel performance
Monetization metrics (irrelevant — no monetization in V1 per Non-Goals)
Net Promoter Score / qualitative satisfaction surveys

These belong in a post-launch measurement plan, not this PRD.

