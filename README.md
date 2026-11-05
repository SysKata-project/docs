# SysKata documentation

SysKata helps learners build a daily technical practice habit through short lessons and hands-on challenges, primarily oriented toward Red Hat certification paths. Its aim is practical competence for performance-based exams and on-the-job administration.

## Product principles

- Make progress manageable through focused daily sessions.
- Teach Linux administration, automation, and related technologies through practice.
- Explain mistakes promptly and reinforce weak skills through review.
- Make progress visible through learning paths, daily goals, streaks, and milestones.
- Increase challenge gradually, from commands to realistic administrative tasks.

## Component map

| Repository | Owns |
| --- | --- |
| [app](https://github.com/SysKata-project/app) | Flutter application for iOS and Android; learner interface and interaction design |
| [api](https://github.com/SysKata-project/api) | Application state, progression, sessions, and review scheduling |
| [labs](https://github.com/SysKata-project/labs) | Practice environment lifecycle and assessment execution |
| [content](https://github.com/SysKata-project/content) | Authored learning paths, lessons, exercises, and assessment criteria |
| [.github](https://github.com/SysKata-project/.github) | Public organization profile |

The proposed flow is: a learner selects a lesson in the Flutter app; the API tracks the session, grades knowledge exercises, and requests an isolated environment from the lab service only for hands-on tasks; lab assessments produce results; the API records progress and returns feedback. Versioned content supplies the learning material and assessment criteria. Contracts are to be designed before integration.

## Mobile application

The [app repository](https://github.com/SysKata-project/app) owns a shared Flutter/Dart application for iOS and Android. Its planned experience combines short daily lessons, a visible learning path, immediate feedback, targeted review, daily goals, streaks, and achievement milestones with Kata as the practice companion. Hands-on Linux tasks execute in remote labs accessed through the app.

See the [product specification](https://github.com/SysKata-project/app/blob/main/docs/product.md), [architecture](https://github.com/SysKata-project/app/blob/main/docs/architecture.md), and [implementation roadmap](https://github.com/SysKata-project/app/blob/main/docs/roadmap.md). These documents describe planned behavior; no runnable mobile app is available yet.

## Proposed first milestone

1. Deliver the OpenShift pilot slice aligned to DO180 and DO280 public objectives.
2. Define the content format and author an original lesson with a practical challenge.
3. Provision a disposable lab and assess observable task outcomes.
4. Deliver a complete learner flow with explanatory feedback and saved progress.
5. Add daily goals and review before expanding the curriculum.

## Decisions still open

The learner application will use Flutter and Dart for iOS and Android. The MVP baseline uses PostgreSQL, a modular Java/Quarkus API, self-hosted Keycloak and versioned content bundles. Development starts locally; hosted deployment is deferred. The initial journey is OpenShift aligned to DO180/DO280. Hosted operations, lab isolation implementation and verified runtime compatibility remain open. See [ADR 0001](decisions/0001-backend-and-identity.md) for accepted choices and remaining decisions.

## Contributing

Open an issue describing the learner need, proposed behavior, and affected components. Keep cross-component contracts and product decisions here; keep implementation documentation with the owning component. Avoid committing secrets or learner data.

## Implementation design

- [Runtime and identity decisions](decisions/0001-backend-and-identity.md)
- [Learning policy](decisions/0002-learning-policy.md)
- [Data lifecycle and operations](decisions/0003-data-lifecycle-and-operations.md)
- [Credential-free local configuration example](configuration/.env.example)
- [Learning architecture](architecture/learning-platform.md)
- [OpenShift MVP plan](plans/openshift-mvp.md)
- [Cross-repository issue backlog](plans/mvp-backlog.md)

## Status

Planning scaffold only. This README describes intended behavior, not implemented capabilities.

## License

Copyright 2026 SysKata contributors.

This repository, including its code, documentation, and learning content, is licensed under the [Apache License 2.0](LICENSE).
