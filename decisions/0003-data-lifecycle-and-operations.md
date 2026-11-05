# ADR 0003: Data lifecycle and operational responsibilities

Status: data lifecycle, backup/restore and local secrets policies accepted; ongoing release operations explicitly deferred.
Decision date: 2026-11-05.
Tracking issue: https://github.com/SysKata-project/docs/issues/2

## Account deletion

The project owner approved the following policy on 2026-11-05:

- Disable account access immediately when an authenticated account-deletion
  request is accepted.
- Permanently delete the learner's active account data within 30 days of the
  accepted request.
- Define backup retention separately; the active-data deadline does not imply
  that existing backup copies have already expired.

Apply deletion across the application database, self-hosted Keycloak and other
active stores containing learner account data. Disable API access and revoke
identity sessions; access enforcement must not depend solely on existing access
tokens expiring. Terminate active learner lab/terminal access and include their
learner-linked data in cleanup.

Make deletion jobs retryable and track the original request deadline so retries
do not extend the 30-day limit. Retain only the minimal operational evidence
needed to verify deletion or prevent restoration of deleted accounts, under a
separately defined retention policy. Never include credentials or learner
answers in deletion logs.

## Backup retention and restore

The project owner approved a 30-day backup retention limit on 2026-11-05.
Expire backup copies no later than 30 days after their creation, including
replicas and exported copies managed by SysKata. Copying or restoring a backup
must not restart its retention period.

Before making restored services accessible, reapply all account deletions
accepted since the restored snapshot. Keep restored API, identity and lab access
unavailable until deleted accounts and their associated active data have been
removed and the result verified. If deletion evidence is unavailable or cannot
be reconciled, do not reopen access.

Maintain minimal deletion evidence independently of the snapshot being restored
so restoring an older backup cannot erase knowledge of subsequent deletions.
Its retention period is defined below; restrict access to deletion and restore
operators/services. Backup expiry is separate from the accepted deadline for
deleting active account data.

## Learning history and progress retention

The project owner confirmed on 2026-11-05 that learning history and progress
are retained while the account remains active, until the learner requests
account deletion. This includes attempts, skill evidence, completion history,
review schedules, XP and streak records needed to preserve the learning journey.

An accepted account-deletion request overrides this retention rule: disable
access immediately and delete the associated active data within 30 days, as
specified above. Backup copies remain subject to the separate 30-day expiry
and restore-reconciliation rules. This decision does not set retention periods
for operational logs or deletion evidence.

## Operational log retention

The project owner approved a 30-day retention limit for operational logs on
2026-11-05. Expire logs no later than 30 days after the logged event, including
copies exported to logging systems. Copying or exporting logs must not restart
their retention period.

Exclude credentials, tokens and learner answers from logs. Apply this rule to
application, identity, lab and gateway logging, including request/error traces;
do not log raw request bodies, authentication headers or terminal transcripts
that could contain those values. Use bounded, redacted operational metadata
and correlation IDs for troubleshooting.

Deletion evidence follows its separately defined policy rather than being
implicitly retained as ordinary operational logs.

## Deletion evidence retention

The project owner approved retaining minimal deletion records until 30 days
after deletion completes. Extend retention only while a backup or restore could
still reintroduce the account, then remove the record once both conditions are
satisfied: the 30-day period has elapsed and no such recovery risk remains.

Keep pending deletion records until deletion is verified complete; do not start
the post-completion retention period merely when the request is accepted.
Store only identifiers needed to match restored records, request/completion
timestamps and deletion status. Exclude credentials, tokens, learner answers
and unnecessary profile data. Restrict access to authorized deletion and
restore operators/services and keep this evidence independent of restored
application snapshots.

Track and review any retention extension with its recovery-related reason.
An extension does not authorize keeping backups beyond their 30-day limit or
retaining unrelated learner data.

## Backup and restore ownership

The project owner confirmed that SysKata's deployment operator owns daily
automated backups and a monthly restore test for application and Keycloak data.
The operator must monitor backup failures, verify retention expiry and record
restore-test results without exposing learner data or credentials.

Run restore tests in an isolated environment. Verify application and identity
data recovery, reapply account deletions and check access controls before any
restored service becomes accessible. Include the independent deletion evidence
in recovery planning; do not replace it with an older snapshot during restore.

The operator role must be assigned before a shared deployment stores learner
data. Implement the automated backup schedule and restore procedure as part of
deployment work, and supply verification evidence at the staging release gate.
This ownership decision does not claim that backups or restore tests already
exist in the current local development scaffold.

## Remaining decisions

The project owner limited current cluster work to initial installation.
Ongoing deployment, rollback and deployed-secret rotation policies and
ownership are deferred to [docs #6](https://github.com/SysKata-project/docs/issues/6).
Do not infer ownership of those activities from the operator's accepted backup
and restore responsibilities, which remain unchanged. Initial installation is
tracked by [docs #5](https://github.com/SysKata-project/docs/issues/5).

## Local secrets handling

The project owner approved keeping local development secrets in a Git-ignored
`.env` file and committing only placeholder values in `.env.example`.
Each developer supplies their own local values; do not distribute populated
files through Git, issues, logs or documentation. Keep local secrets distinct
from deployed credentials and restrict filesystem access to the developer.

See the [configuration example](../configuration/.env.example). Its variable
names are illustrative inputs for the eventual local launcher; they are not
yet a runnable Quarkus or Keycloak configuration. The implementation must map
them explicitly and reject missing secret values rather than use defaults.
No populated `.env` file is created as part of this decision.
