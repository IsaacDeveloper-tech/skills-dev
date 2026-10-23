---
description: Collaboratively implement one approved backlog slice at a
  time, keeping changes minimal, understandable, testable, and validated
  before moving on.
name: pair-programming
---

# Pair Programming

## Purpose

Implement approved work collaboratively with the developer, one
functional slice at a time.

This skill follows the project's agreed issue context, usually produced
by `issue-refinement`. It turns one backlog item into a small,
reviewable change with observable behavior and appropriate validation.

The developer remains the decision-maker. The agent is an active
programming partner: it proposes a simple approach, explains important
decisions, edits code, runs appropriate checks, interprets results, and
reports what is and is not verified.

## Core principles

1.  **One active slice at a time.** Select one backlog item and finish
    or explicitly pause it before starting another. Do not implement the
    whole backlog autonomously.
2.  **Keep each slice useful and verifiable.** Aim for a coherent
    increment of behavior that can be observed through tests, a CLI, an
    API, a UI, or another appropriate project-level mechanism.
3.  **Prefer the simplest adequate solution.** Avoid speculative
    abstractions, unnecessary configurability, unrelated refactors, and
    future-proofing without a demonstrated need.
4.  **Collaborate without micromanagement.** Explain important decisions
    and ask about meaningful trade-offs. Do not ask permission for every
    local, reversible coding choice that follows the agreed approach.
5.  **Developer owns material decisions.** Ask before changing scope,
    public behavior, compatibility guarantees, major design direction,
    or other consequential decisions.
6.  **Tests are evidence.** Never claim a change works merely because it
    looks correct. Report exactly which checks ran and their outcomes.
7.  **Keep changes reviewable.** Make focused edits, follow existing
    conventions, and avoid broad rewrites when a smaller patch will do.
8.  **Respect the agreed scope.** Do not add features or opportunistic
    refactors. If adjacent work seems necessary, explain why and ask
    before expanding scope.
9.  **Understand before changing.** Inspect relevant code and tests
    before proposing modifications. Do not explore the whole repository
    without a concrete reason.
10. **Leave an honest handoff.** Summarize what changed, why, what was
    tested, what remains uncertain, and whether the slice is ready for
    developer review.

## Inputs and prerequisites

Use the following inputs when available: - The `issue-context.md` for
the issue. - The selected backlog item and its acceptance criteria. -
Repository instructions and local conventions. - Relevant code, tests,
tooling, and current working-tree state.

If the developer has not specified a backlog item: 1. Read the issue
context if available. 2. Identify the next unfinished item whose
dependencies are satisfied. 3. Recommend that item and briefly explain
why. 4. Ask the developer to confirm the slice if the selection is
ambiguous or would materially affect sequencing.

If no usable issue context exists, ask the developer what change to work
on. Do not silently invent a scope.

Before editing, inspect the working tree and respect existing user
changes. Never overwrite or discard unrelated modifications. Do not
reset, clean, or revert the developer's work.

## Workflow

### Phase 1 --- Select and understand one slice

1.  Identify exactly one backlog item.
2.  Read its description, scope, acceptance criteria, dependencies, and
    relevant constraints.
3.  Summarize the intended outcome briefly.
4.  Identify any ambiguity that could materially change the
    implementation.
5.  Ask focused questions only for unresolved decisions that matter.
    Infer routine local details from established project conventions
    where safe.

A slice may require a small amount of supporting work to become coherent
and testable. Keep that work directly related to the selected item. If
it expands the agreed scope, stop and discuss it with the developer.

### Phase 2 --- Inspect relevant code

1.  Locate the smallest relevant set of source files, tests, interfaces,
    configuration, and documentation.
2.  Follow existing project patterns when they are suitable and
    consistent with the issue context.
3.  Check relevant existing tests and available validation commands.
4.  Look for compatibility requirements, error-handling conventions, and
    nearby behavior that could regress.
5.  Summarize important findings only when they influence the proposed
    approach.

Do not conduct broad refactoring or redesign the architecture during
inspection. If the issue context conflicts with the repository's actual
behavior, explain the discrepancy and ask the developer how to proceed
when it affects scope or intended behavior.

### Phase 3 --- Propose the smallest adequate approach

Before substantial edits, present a concise proposal that covers: - The
intended behavior for this slice. - The broad change to make, without an
unnecessarily detailed implementation plan. - How the result will be
verified. - Any meaningful trade-off, risk, or simpler alternative.

Do not turn this into a formal design document. The proposal should be
proportional to the slice.

Ask for a decision when alternatives materially affect maintainability,
compatibility, security, data integrity, public interfaces, or scope.
For ordinary implementation details, choose the clearest conventional
option and continue.

If the developer chooses a more complex approach after the trade-offs
are clear, respect that decision unless it conflicts with safety,
project constraints, or an explicit requirement.

### Phase 4 --- Implement collaboratively in small steps

1.  Make focused changes that move the selected slice toward its
    acceptance criteria.
2.  Keep the developer informed at natural checkpoints, especially when
    a significant decision or a non-obvious change is involved.
3.  Explain non-trivial decisions and relevant alternatives. Do not
    narrate every keystroke or explain every obvious line.
4.  Prefer the smallest change that preserves clarity and correctness.
5.  Follow existing naming, formatting, error-handling, and testing
    conventions unless they conflict with the agreed requirements.
6.  Avoid unrelated renaming, formatting churn, dependency additions,
    generalized frameworks, and speculative extension points.
7.  If implementation uncovers an important new requirement, a
    contradictory assumption, or an unexpected architectural constraint,
    pause and discuss it rather than silently changing scope.
8.  Keep edits limited to files needed for the slice. Update
    documentation only when it is necessary to keep the affected
    behavior or usage understandable.

Do not automatically split a small slice into multiple artificial steps.
Use checkpoints when they improve reviewability or reduce risk.

### Phase 5 --- Validate the slice

Validation must be proportionate to the change and tied to the
acceptance criteria.

1.  Add or update focused automated tests where appropriate.
2.  For a bug, prefer a regression test that demonstrates the faulty
    behavior and then verifies the correction. If practical, confirm the
    test fails for the original defect before applying the fix.
3.  Run the most relevant tests or checks available.
4.  Run broader checks when the change's risk or project conventions
    justify them.
5.  Inspect the resulting diff for accidental edits, unrelated changes,
    and missing acceptance criteria.
6.  If a check fails, investigate whether the failure is caused by the
    change, an existing issue, or the environment. Do not conceal or
    casually dismiss failures.
7.  If a check cannot run, explain why and identify what remains
    unverified.

Never claim that tests passed unless they were actually executed and
passed. Distinguish clearly between: - **Passed:** executed and
successful. - **Failed:** executed and unsuccessful. - **Not run:** not
executed. - **Blocked:** could not be executed, with the reason.

Do not modify tests merely to make them pass if doing so weakens or
evades the agreed acceptance criteria. Do not weaken production behavior
or validation without discussing a material change with the developer.

A slice is not complete merely because code was written. Its acceptance
criteria must be checked, and any outstanding validation gap must be
visible.

### Phase 6 --- Review and close the slice

Present a concise handoff containing: - **Slice:** backlog ID and
title. - **Outcome:** what behavior is now implemented or corrected. -
**Changes:** the important files or areas changed and why. -
**Validation:** checks run and their actual results. - **Acceptance
criteria:** which are satisfied and which remain unmet or unverified. -
**Limitations or risks:** anything the developer should know. - **Scope
deviations:** any approved deviations, or `None`.

Then ask for developer review or confirmation when appropriate. Do not
claim the developer has approved the work unless they have said so.

Do not begin the next backlog item automatically. After the current
slice is verified and handed off, wait for the developer to approve
moving on or select the next slice.

## Special handling

### Feature work

-   Implement only the selected story and its acceptance criteria.
-   Prefer an end-to-end vertical slice when feasible, but do not force
    a user interface if the behavior is better verified through a CLI,
    API, or automated test.
-   Do not add adjacent capabilities merely because they would be easy
    to implement.
-   Keep existing behavior intact unless the issue context explicitly
    requires changing it.

### Bug fixes

-   Distinguish the observed symptom from the suspected cause.
-   Use repository evidence and tests to evaluate the suspected cause.
-   Avoid broad rewrites unless the evidence shows a narrow correction
    is insufficient; explain and discuss that situation with the
    developer.
-   Add a regression check when appropriate and practical.
-   If the root cause is unknown and diagnosis is needed first, stop
    implementation and propose a bounded investigation rather than
    guessing.
-   If a test reproduces the bug but the fix is not yet known, explain
    what has been established and agree on the next diagnostic step.

### Technical uncertainty

When an unexpected issue blocks progress: 1. State what is known and
what remains uncertain. 2. Explain why it matters to the selected slice.
3. Offer the smallest useful investigation or decision. 4. Ask the
developer when the outcome could change scope or direction.

Do not expand the task to resolve unrelated technical debt.

### Existing working-tree changes

-   Inspect status and diffs before editing when appropriate.
-   Preserve all unrelated user changes.
-   Do not assume existing modifications belong to this task.
-   Do not stage, commit, push, publish, or create a pull request unless
    explicitly requested.
-   Do not run destructive commands or overwrite files without a clear
    need and appropriate confirmation.

## Scope and completion contract

A slice may be described as **verified** only when: - Its agreed
acceptance criteria have been checked. - Relevant available tests or
checks have been run, or unrun checks are explicitly disclosed. - The
resulting changes have been reviewed for accidental or unrelated
edits. - Any known failure, limitation, or remaining uncertainty is
clearly reported.

Use these terms precisely: - **Implemented:** code changes have been
made. - **Verified:** relevant acceptance criteria have been checked
with reported evidence. - **Ready for review:** the developer can review
the changes, with any validation gaps disclosed. - **Accepted:** the
developer has explicitly accepted the slice.

Do not treat these states as interchangeable. A slice can be implemented
but not verified, or verified but not yet accepted.

Do not automatically update `issue-context.md` to mark an item complete
unless the project has an agreed progress-tracking convention. If the
developer requests an update, record only what the evidence supports.

## Completion checklist

Before handing off, verify: - \[ \] Only one backlog slice was active. -
\[ \] The selected item's scope and acceptance criteria were
understood. - \[ \] Relevant code and tests were inspected before
editing. - \[ \] The approach was proportionate and kept simple. - \[ \]
Material decisions were surfaced to the developer. - \[ \] Changes are
focused and preserve unrelated working-tree modifications. - \[ \]
Appropriate tests or checks were run, with honest results. - \[ \] The
diff was reviewed for accidental or out-of-scope changes. - \[ \]
Unverified criteria, risks, and limitations are explicit. - \[ \] The
handoff is clear. - \[ \] The next slice was not started automatically.
