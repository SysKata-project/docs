# ADR 0002: Guided completion and independent skill evidence

Status: learning-policy decisions accepted; implementation must preserve and version these rules.
Decision date: 2026-11-05.
Tracking issue: https://github.com/SysKata-project/docs/issues/2

## Context

The pilot needs explicit completion and remediation rules without equating
progress through lessons with independent competence.

## Decision

Guided lesson completion unlocks the next lesson. Track independent skill
evidence separately. The project owner selected this behavior on the decision
date. Hints and answer reveals must remain visible in the evidence used for
review and skill reporting; guided success must not be reported as independent
success. XP is motivational feedback, not a mastery measure.

Unlocking remains subject to the destination lesson's other prerequisites.
This choice does not waive the requirement to complete real lab checkpoints.

## Completion and remediation

The project owner approved the following rules on 2026-11-05:

- Lesson completion requires a correct response covering every lesson objective.
- Hints and answer reveals are allowed. A correct response after assistance may
  satisfy completion, but remains assisted evidence rather than independent
  skill evidence.
- Viewing a revealed answer alone does not satisfy an objective; the learner
  must submit a correct response.
- Revisit mistakes later in the same session for remediation. Do not mark the
  lesson complete while any objective lacks a qualifying correct response.

The session implementation must specify deterministic remediation ordering and
preserve pending remediation when a learner resumes an interrupted session.

## Completion XP

The project owner approved equal completion XP for guided and independent
lesson completion on 2026-11-05. Hints or reveals do not reduce the lesson
completion award. Independent skill evidence remains separate from XP, and
assisted completion must not be presented as independent mastery.

The project owner approved the following award on 2026-11-05:

- Award 10 XP on a learner's first completion of a lesson.
- Retries and replays grant no additional lesson-completion XP.
- Apply the same award to guided and independent completion.

Persist the completion award atomically with confirmed completion and enforce
one award per learner and stable lesson ID. Request retries, concurrent
submissions and content-version updates must not duplicate the award.

## Review XP

The project owner approved 5 XP for completing due review of a skill, limited
to once per learner, skill and day, on 2026-11-05. Award per qualifying skill,
not per attempt or HTTP request. Repeated practice of that skill on the same
day does not grant another review award. A session covering multiple qualifying
skills may award 5 XP for each skill within its daily limit.

Persist review rewards atomically with confirmed review completion and enforce
the daily uniqueness constraint using the learner-local day and timezone
transition rules below.

The project owner confirmed that a correct response completes a due-skill
review and qualifies for its 5 XP award, subject to the daily limit. Hints and
reveals are allowed; viewing an answer alone is not completion. Assisted success
resets the next review to 1 day and remains assisted evidence. A mistake does
not complete the review or earn its XP; subsequent successful remediation may
complete it, but must not advance the interval as if it were a later scheduled
review. Preserve eligibility from the issued due-review instance when a mistake
reschedules the skill, so remediation can still complete that review.

## Lab-checkpoint XP

The project owner approved 25 XP on a learner's first successful completion of
each lab checkpoint on 2026-11-05. Resets and replays grant no additional
lab-completion XP.

Award only after a trusted assessment confirms successful completion. Persist
the award atomically with confirmed progress and enforce one award per learner
and stable checkpoint ID. Duplicate results, resets, replays and content-version
updates must not duplicate the award. Infrastructure failures do not qualify
as successful completion or count as learner mistakes.

## Review intervals

The project owner approved this deterministic per-skill schedule on 2026-11-05:

- Schedule the first review 1 day after initial qualifying skill completion.
- Independent success on that review schedules the next review 7 days later.
- The next independent success schedules review 15 days later. Subsequent
  independent successes retain the 15-day interval.
- A mistake or assisted success resets the skill to the 1-day interval; after
  that reset, independent review successes again advance to 7 and then 15 days.

Intervals are gaps from the qualifying result, not offsets from the original
lesson date. Hint/reveal usage must distinguish assisted from independent
success. Infrastructure errors do not count as mistakes or reset the schedule.
The policy must be versioned and duplicate result delivery must not advance
the schedule twice. Same-session remediation must not be counted as a later
scheduled review to accelerate interval advancement.

These intervals are a pilot product policy to evaluate with learner evidence,
not a claim of a universally optimal learning schedule.

The project owner confirmed that review intervals use elapsed time: 1, 7 or
15 times 24 hours after the server-confirmed qualifying result. Persist the
due instant in UTC. Timezone changes and daylight-saving transitions do not
move an already scheduled review; the learner's timezone affects only its
display and the separate daily goal, streak and review-XP accounting rules.

## Daily goal and qualifying practice

The project owner selected one completed lesson as the daily goal and
requirement for streak credit on 2026-11-05. Guided completion qualifies under
the accepted lesson-completion rules. Due-skill reviews and lab checkpoints
alone do not satisfy this daily goal or grant streak credit; their XP policies
remain unchanged.

The project owner confirmed that completing a previously finished lesson also
qualifies for the daily goal and streak on 2026-11-05. A replay must satisfy the
same lesson-completion criteria; merely reopening a completed lesson does not
qualify. Replays grant no additional lesson-completion XP. Replayed delivery of
the same completion event must not count as a new completion on another day.

The project owner confirmed on 2026-11-05 that a missed day resets the current
streak to zero while preserving the learner's longest streak. Treat a day as
missed only after that day has ended without a qualifying lesson completion;
an unfinished current day is not yet a missed day. The next qualifying day
starts a new current streak of one.

## Learner-local days

The project owner confirmed on 2026-11-05 that daily goals, streaks and daily
review-XP limits use the learner's chosen timezone. Each day runs from local
midnight, inclusive, to the next local midnight, exclusive.

Store a named IANA timezone rather than a fixed UTC offset so daylight-saving
transitions follow the chosen timezone. A local day may therefore be shorter
or longer than 24 hours. Use server-confirmed completion timestamps to assign
qualifying events to a local date. Persist the timezone and credited date with
the event so retries do not recalculate or duplicate historical credit.

## Timezone changes

The project owner approved the following transition policy on 2026-11-05:

- A requested timezone change takes effect at the next midnight in the
  previously active timezone. Keep using that timezone until the effective
  instant.
- Preserve previously credited dates, rewards and streak history; do not
  reinterpret past events in the new timezone.
- Prevent a second review-XP award for the same skill during the transition.
  Carry the outgoing day's per-skill award guard through the first partial
  local day in the new timezone, until its next midnight. A skill not already
  rewarded may still receive its single qualifying award during that period.

Persist the old/new timezone and effective instant so retries apply the change
once. The project owner confirmed that the partial transition day preserves
the current streak without increasing or breaking it. Normal streak counting
resumes at the next midnight in the new timezone, when the first full qualifying
day begins. A completion during the partial transition day does not pre-credit
that next full day. Skipped or repeated calendar-date labels caused by the
change must not independently reset or increase the streak.


## Assistance evidence per attempt

The project owner rejected carrying an assisted classification automatically
across all retries of an exercise instance. Each new attempt begins without
assistance and remains independent unless the learner requests a hint or reveal
on that attempt. Assistance on an earlier attempt does not automatically make a
later attempt assisted, even when both use the same exercise instance.

Record hint and reveal usage separately for each attempt and retain the prior
attempt history. Resuming an existing attempt after closing the app preserves
its assistance state; recovery or request replay is not a new attempt. A
correct response without assistance on a new attempt is independent under this
product policy, while the prior exposure remains available in the evidence.

This classification does not bypass the review schedule: same-session
remediation still cannot advance intervals as a later scheduled review.

Assign a policy version before implementation and pin it to learning sessions
and their results.
