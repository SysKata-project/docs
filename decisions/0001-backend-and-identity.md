# ADR 0001: Java/Quarkus API and self-hosted Keycloak

Status: accepted technology and installation scope; ongoing operations explicitly deferred.
Decision date: 2026-11-05.
Tracking issue: https://github.com/SysKata-project/docs/issues/2

## Context

The MVP needs a modular API for durable learning state and an identity provider
for the Flutter iOS and Android application. PostgreSQL and Flutter are existing
baseline decisions. Lab execution remains a separate trust boundary.

## Decision

Use Java with Quarkus for the application API. Use self-hosted Keycloak for
learner identity, with operations owned by SysKata. The project owner explicitly
selected both technologies on the decision date.

Develop and validate locally first. Run the API, Keycloak and PostgreSQL in the
local development environment; hosted deployment is explicitly deferred by the
project owner. This does not select a cloud provider or authorize infrastructure
spending. Initial installation into an existing administrator-accessible OpenShift
cluster is tracked by docs #5; ongoing release operations are deferred to docs #6.
Local development is not evidence of
production readiness or of OpenShift lab feasibility.

Preserve the modular API and PostgreSQL transaction boundaries described in
[the shared architecture](../architecture/learning-platform.md). Do not execute
learner commands on the API host.

## Consequences

SysKata owns Keycloak deployment, updates, availability, configuration and
recovery. Provider operation is part of the release responsibility, not an
external managed service guarantee. Identity and application data must both be
covered by the eventual deletion and restore procedures.

Quarkus supports bearer-token authentication through its OIDC extension; the
exact issuer, audience, mobile login flow and token lifecycle must be specified
in the identity contract before implementation.

## Remaining decisions

- Initial cluster installation is tracked in [docs #5](https://github.com/SysKata-project/docs/issues/5).
  Ongoing deployment, rollback and deployed-secret rotation policies/ownership
  are explicitly deferred to [docs #6](https://github.com/SysKata-project/docs/issues/6).
- Supported Java, Quarkus and Keycloak versions, pinned during scaffolding.
- Accepted local secrets, backup/restore and retention policies are recorded in
  [ADR 0003](0003-data-lifecycle-and-operations.md); deployed-secret rotation is
  deferred to docs #6.
- Mobile authentication contract and account deletion coordination.
- [Learning policy](0002-learning-policy.md) records the accepted behavior;
  implementation must assign and pin its policy version.
- The curriculum source baseline is OpenShift 4.22, as recorded in the
  [MVP plan](../plans/openshift-mvp.md) from the 2026-11-04 source review.
  This is not a verified runtime version. [labs #1](https://github.com/SysKata-project/labs/issues/1)
  owns verification on the available cluster, objective compatibility differences,
  access/isolation checks, session cost ceiling and concurrency. Cluster admin
  access does not establish safe learner privileges or a zero operating cost.

Issue #2 remains open pending review and merge of these decisions. Deferred
implementation choices above are tracked separately and are not claims of
implemented or validated capabilities.

## Reference

- [Quarkus OIDC bearer-token authentication](https://quarkus.io/guides/security-oidc-bearer-token-authentication/)
