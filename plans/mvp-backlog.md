# OpenShift implementation backlog

Status: all issues open when created on 2026-11-04. Documentation does not imply working software.

Coordination: https://github.com/SysKata-project/docs/issues/1

## MVP delivery issues

| Repository | Issue | Depends on |
| --- | --- | --- |
| docs | [Record runtime, identity, hosting and learning-policy decisions](https://github.com/SysKata-project/docs/issues/2) | Start now |
| content | [Define versioned content schemas and assessment fixtures](https://github.com/SysKata-project/content/issues/1) | Start now |
| api | [Publish OpenAPI contracts and shared learning fixtures](https://github.com/SysKata-project/api/issues/1) | [docs#2](https://github.com/SysKata-project/docs/issues/2), [content#1](https://github.com/SysKata-project/content/issues/1) |
| labs | [Validate OpenShift runtime, isolation and operating budget](https://github.com/SysKata-project/labs/issues/1) | Start now |
| content | [Compile and publish immutable content bundles](https://github.com/SysKata-project/content/issues/2) | [content#1](https://github.com/SysKata-project/content/issues/1) |
| content | [Map the OpenShift DO180 and DO280 journey and prerequisites](https://github.com/SysKata-project/content/issues/3) | [content#1](https://github.com/SysKata-project/content/issues/1) |
| content | [Author DO180-aligned foundations lessons and checkpoint](https://github.com/SysKata-project/content/issues/4) | [content#3](https://github.com/SysKata-project/content/issues/3), [content#2](https://github.com/SysKata-project/content/issues/2), [labs#1](https://github.com/SysKata-project/labs/issues/1) |
| content | [Author DO280-aligned administration lessons and checkpoint](https://github.com/SysKata-project/content/issues/5) | [content#3](https://github.com/SysKata-project/content/issues/3), [content#2](https://github.com/SysKata-project/content/issues/2), [labs#1](https://github.com/SysKata-project/labs/issues/1) |
| api | [Implement authentication, PostgreSQL persistence and service foundation](https://github.com/SysKata-project/api/issues/2) | [docs#2](https://github.com/SysKata-project/docs/issues/2), [api#1](https://github.com/SysKata-project/api/issues/1) |
| api | [Serve versioned journeys and deterministic learning sessions](https://github.com/SysKata-project/api/issues/3) | [api#2](https://github.com/SysKata-project/api/issues/2), [content#2](https://github.com/SysKata-project/content/issues/2), [content#3](https://github.com/SysKata-project/content/issues/3) |
| api | [Grade attempts and commit progress exactly once](https://github.com/SysKata-project/api/issues/4) | [api#3](https://github.com/SysKata-project/api/issues/3) |
| labs | [Implement scoped OpenShift lab sessions and terminal gateway](https://github.com/SysKata-project/labs/issues/2) | [labs#1](https://github.com/SysKata-project/labs/issues/1), [api#1](https://github.com/SysKata-project/api/issues/1) |
| labs | [Implement outcome-based assessment for both OpenShift checkpoints](https://github.com/SysKata-project/labs/issues/3) | [labs#2](https://github.com/SysKata-project/labs/issues/2), [content#4](https://github.com/SysKata-project/content/issues/4), [content#5](https://github.com/SysKata-project/content/issues/5) |
| api | [Orchestrate asynchronous labs and deduplicate assessment results](https://github.com/SysKata-project/api/issues/5) | [api#4](https://github.com/SysKata-project/api/issues/4), [labs#2](https://github.com/SysKata-project/labs/issues/2), [labs#3](https://github.com/SysKata-project/labs/issues/3) |
| api | [Implement skill review, daily goals and streaks](https://github.com/SysKata-project/api/issues/6) | [api#4](https://github.com/SysKata-project/api/issues/4), [docs#2](https://github.com/SysKata-project/docs/issues/2) |
| app | [Scaffold Flutter iOS and Android with typed service adapters](https://github.com/SysKata-project/app/issues/1) | [api#1](https://github.com/SysKata-project/api/issues/1) |
| app | [Render the OpenShift journey, exercises and feedback](https://github.com/SysKata-project/app/issues/2) | [app#1](https://github.com/SysKata-project/app/issues/1), [content#4](https://github.com/SysKata-project/content/issues/4), [content#5](https://github.com/SysKata-project/content/issues/5), [api#4](https://github.com/SysKata-project/api/issues/4) |
| app | [Implement sign-in and durable session recovery](https://github.com/SysKata-project/app/issues/3) | [app#1](https://github.com/SysKata-project/app/issues/1), [api#4](https://github.com/SysKata-project/api/issues/4), [api#2](https://github.com/SysKata-project/api/issues/2) |
| app | [Integrate OpenShift terminal and asynchronous assessment](https://github.com/SysKata-project/app/issues/4) | [app#1](https://github.com/SysKata-project/app/issues/1), [api#5](https://github.com/SysKata-project/api/issues/5) |
| app | [Show review, daily goals and confirmed progress](https://github.com/SysKata-project/app/issues/5) | [app#2](https://github.com/SysKata-project/app/issues/2), [app#3](https://github.com/SysKata-project/app/issues/3), [api#6](https://github.com/SysKata-project/api/issues/6) |
| docs | [Validate staging integration and pilot release readiness](https://github.com/SysKata-project/docs/issues/3) | [api#5](https://github.com/SysKata-project/api/issues/5), [api#6](https://github.com/SysKata-project/api/issues/6), [app#2](https://github.com/SysKata-project/app/issues/2), [app#3](https://github.com/SysKata-project/app/issues/3), [app#4](https://github.com/SysKata-project/app/issues/4), [app#5](https://github.com/SysKata-project/app/issues/5), [content#2](https://github.com/SysKata-project/content/issues/2) |

## Deferred work

- [[Later] Expand validated DO180 and DO280 objective coverage](https://github.com/SysKata-project/content/issues/6)
- [[Later] Design optional challenge lives and attributable gifts](https://github.com/SysKata-project/api/issues/7)

## Starting points

Begin with runtime/policy decisions (docs #2), content schema (content #1) and OpenShift feasibility (labs #1). Formal API contracts follow the decisions/schema; mobile adapters can then use fixtures while implementation proceeds. The release gate is docs #3.

Redis, ML personalization and further service decomposition require measured justification and are not MVP dependencies.
