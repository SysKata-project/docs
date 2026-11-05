# OpenShift MVP scope and release gates

Status: planned; initial path selected on 2026-11-04. This is a bounded first release, not complete coverage of either course.

## Learning baseline

The first journey is OpenShift with DO180-aligned foundations followed by DO280-aligned administration. Use original SysKata lessons and tasks mapped to public objectives, not copied course books, lab solutions or exam questions. SysKata is independent of Red Hat; completion does not claim certification readiness.

The public course pages reviewed on 2026-11-04 both reference OpenShift Container Platform 4.22. Record this as the curriculum source baseline; actual lab compatibility remains unverified until the environment issue passes. Preserve source URL, review date, target platform and explicit supported runtime version in content. If provider availability requires a different release, document the objective delta before publishing that content.

- [DO180 public outline](https://www.redhat.com/en/services/training/red-hat-openshift-administration-i-operating-a-production-cluster)
- [DO280 public outline](https://www.redhat.com/en/services/training/red-hat-openshift-administration-ii-configuring-a-production-cluster)

## Pilot learning slice

| Stage | Original SysKata lessons | Practical checkpoint |
| --- | --- | --- |
| Foundations / DO180 alignment | Cluster/resource orientation; oc queries and project context; deployments and troubleshooting; services and routes | Deploy a provided application in an isolated project, expose it, diagnose and fix a failing rollout |
| Administration / DO280 alignment | Declarative manifests; namespace-scoped authorization; resource budgets and workload separation | Apply a manifest, grant a supplied identity a scoped role, configure a quota and demonstrate permitted/denied access |

Target seven short lessons, each with an explanation, measurable skills, 3–5 knowledge/command exercises, misconception feedback, hints and version-matched documentation references. Deliver two real lab scenarios, one per stage, on the same lifecycle/assessment implementation. Duration estimates for labs are separate from 3–7 minute lessons.

Provide controlled prerequisite evidence for the second stage: completing the foundations slice unlocks only the pilot administration lessons, not an assertion of full DO180 mastery. Preconfigured identities enable scoped RBAC practice without exposing cluster-wide identity configuration.

Map the broader course objectives in content and explicitly mark non-pilot areas as planned. Storage, reliability, expanded update scenarios, cluster identity, advanced networking, Operators, security constraints and cluster updates belong to later curriculum expansion. Do not grant shared-cluster administrator privileges to implement those topics quickly.

## Delivery order

1. Record backend/auth/hosting decisions; define contracts, content schema and lab feasibility.
2. Build API persistence/auth, content compiler, Flutter foundation and lab lifecycle.
3. Connect deterministic sessions and grading to original foundations content and the first lab.
4. Add the administration slice and second lab, review/daily goals/streaks and cross-device recovery.
5. Run staging acceptance on both mobile platforms and pilot with learners.

A cross-repository issue index records exact dependencies and release gates. Work can begin with contract fixtures before all services are runnable.

## Release acceptance

- Sign in, enroll, finish both pilot stages, receive useful incorrect-answer feedback and complete two assessed lab scenarios.
- Progress resumes after restart and on a second device; retries/concurrent requests cannot duplicate outcomes or rewards.
- Assessment infrastructure failure is retryable and does not penalize the learner.
- New content activation does not change active-session grading; rollback and old-bundle availability are exercised.
- Labs enforce scoped credentials, expiry, resource limits, cleanup and cross-learner isolation.
- Basic due review, daily goals and learner-local streaks work; XP and skill mastery remain distinct.
- iOS/Android builds, accessibility, terminal keyboard behavior, account deletion and database restore are verified.
- All content identifies source baseline and actually tested lab versions. No claim of complete DO180/DO280 coverage.

## Deferred

Redis, microservice decomposition, ML personalization, offline lesson completion, lives/gifting, payments, leaderboards and full course coverage. Record later work separately from MVP blocking issues.
