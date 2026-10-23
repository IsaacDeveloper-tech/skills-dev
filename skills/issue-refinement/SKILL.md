---
description: Refine a feature request or bug report through a
  developer-led conversation, define minimal agreed scope, and create a
  structured issue-context.md without implementing or designing the
  technical solution.
name: issue-refinement
---

# Issue Refinement

## Purpose

Turn an incoming ticket, issue, or informal problem description into a
clear, reviewable, developer-approved definition of work.

This skill defines **what should be achieved**, not **how to implement
it**. It must not implement the issue, edit application code, design a
detailed technical architecture, or decompose the work into
implementation-level tasks.

Create one `issue-context.md` document per issue, using the matching
template in `templates/`.

## Core principles

1.  **Developer owns the scope.** Ask about meaningful ambiguity. Never
    silently make functional decisions on the developer's behalf.
2.  **Prefer the simplest adequate outcome.** Recommend the smallest
    change that satisfies the stated need. Explain the trade-off when
    suggesting a simpler alternative.
3.  **Respect explicit choices.** If the developer understands the
    trade-off and chooses a broader solution, accept that choice and
    update the scope. Do not repeatedly argue for simplicity.
4.  **Separate facts from assumptions.** Label unverified claims and
    unknowns. Do not invent requirements, causes, reproduction steps, or
    evidence.
5.  **Keep the work reviewable.** Backlog items should be independently
    understandable, have observable outcomes, and avoid unnecessary
    granularity.
6.  **Inspect gradually.** Understand the ticket and ask initial
    clarifying questions before exploring the repository. Inspect only
    relevant code, tests, configuration, or documentation when technical
    evidence is needed.
7.  **No silent scope expansion.** Any newly discovered requirement or
    proposed scope change must be explained and approved by the
    developer before being added.
8.  **No implementation.** Do not edit production code, tests,
    configuration, or other project implementation files. The only file
    this skill creates or updates is the agreed issue context document.
9.  **No premature technical plan.** Do not prescribe classes,
    functions, modules, file-by-file changes, algorithms, or
    implementation task breakdowns. Record technical constraints or
    confirmed findings only when they materially affect the scope.
10. **Be concise and conversational.** Ask one focused question at a
    time by default. Combine questions only when they are tightly
    related and easier to answer together. Do not ask about details
    already provided.

## Workflow

### Phase 1 --- Understand the incoming issue

1.  Read the ticket or issue supplied by the developer.
2.  Classify it as:
    -   `Feature`: new or intentionally changed capability.
    -   `Bug`: existing behavior differs from the expected behavior.
    -   `Unclear`: insufficient information to classify safely.
3.  Summarize your current understanding in a few sentences.
4.  Identify the most consequential gaps or ambiguities.
5.  Start with the highest-value clarification. Do not inspect the whole
    repository at this stage.

If the issue mixes a feature and a bug, ask whether the developer wants
one combined issue or separate issues. Recommend separating them when
they have distinct goals or can be reviewed independently, but accept
the developer's decision.

### Phase 2 --- Clarify and agree on scope

For a feature, clarify only what is relevant: - Who or what is the
actor, and what outcome is needed? - What behavior is included? - What
is explicitly excluded? - What should happen in important edge cases? -
What constraints, compatibility needs, or externally visible behavior
matter? - How will the developer recognize that the feature works?

For a bug, clarify only what is relevant: - What behavior was
observed? - What behavior was expected? - What is the impact and who or
what is affected? - Can it be reproduced? If so, under what conditions
and steps? - What evidence exists, and what is still unknown? - What
observable conditions would demonstrate a correction? - What behavior
must remain unchanged?

Do not mechanically ask every question. Ask only what is necessary for a
useful, testable definition. If the developer does not know an answer,
record it as unknown and decide whether investigation is needed.

### Phase 3 --- Recommend simplicity

When the proposed scope appears unnecessarily complex: 1. State the
specific source of complexity. 2. Offer a simpler alternative. 3.
Explain what the alternative would and would not deliver. 4. Ask for the
developer's decision when the choice affects scope or expected behavior.

Examples of unnecessary complexity include speculative extensibility,
configuration options without a demonstrated need, unrelated
refactoring, support for hypothetical use cases, and multiple
abstractions for a single straightforward behavior.

Do not reject a requirement merely because it is more complex. If the
developer explicitly chooses it after understanding the trade-off,
include it in the agreed scope.

### Phase 4 --- Inspect the repository when justified

Only begin repository inspection after the issue is understood well
enough to make the inspection purposeful, or when a specific question
cannot be answered from the conversation.

1.  Look for relevant, existing project guidance and conventions.
2.  Inspect the smallest relevant set of files, tests, interfaces, or
    configuration.
3.  Use evidence to answer a specific question: feasibility, current
    behavior, an existing constraint, or a likely regression boundary.
4.  Summarize relevant findings to the developer when they affect scope
    or confidence.
5.  If inspection reveals a new functional decision, ask the developer
    rather than deciding unilaterally.
6.  If the evidence is insufficient, state that clearly. Do not claim
    the root cause is confirmed without evidence.

Do not run broad repository exploration just because it is available. Do
not modify code or run commands that change project state. Read-only
inspection and non-mutating checks are allowed when useful.

For a bug whose root cause is unknown, do not force a root-cause guess.
If the next meaningful step is diagnosis, create a bounded investigation
backlog item with a clear question to answer and a concrete expected
outcome.

### Phase 5 --- Build the backlog

This skill produces **functional backlog items**, not implementation
tasks.

For features: - Use the user-story form exactly:
`Como <actor>, quiero <acción> para que <beneficio>.` - Give each story
a stable ID: `F-01`, `F-02`, and so on. - Add observable acceptance
criteria to every story. - Keep stories small enough to understand and
review, but do not split them into trivial fragments. - Order items
where sequence matters and state dependencies only when real. - Do not
invent technical subtasks. A purely technical concern may be recorded as
a constraint or note, but detailed implementation planning belongs to a
later skill.

For bugs: - Use IDs `B-01`, `B-02`, and so on. - Mark each item as
`Correction` or `Investigation`. - For a correction, define the behavior
to correct and acceptance criteria. - For an investigation, define the
unknown to resolve, the evidence or answer needed, and the decision that
the result should enable. - Add a regression-validation expectation
where appropriate. - Do not require a root-cause diagnosis before it is
evidenced.

Every backlog item must trace to the agreed scope. If no meaningful
backlog can be written because a critical decision remains unresolved,
record the open question and set the document status to
`Needs clarification` rather than pretending it is ready.

### Phase 6 --- Review the proposed context

Before writing the file: 1. Present a concise summary of the proposed
scope and backlog. 2. Ask the developer to confirm or correct it. 3.
Incorporate their feedback. 4. Do not mark the document
`Ready for implementation` while a scope-critical question remains
unresolved.

Developer confirmation is required before the final context is
considered agreed. If the developer asks to proceed despite non-critical
unknowns, record them explicitly and explain any limitation in
readiness.

### Phase 7 --- Write the output document

1.  Check whether the repository already has an agreed convention for
    issue-context files. Prefer an existing convention when clear.
2.  If no convention exists, use
    `docs/issues/<issue-slug>/issue-context.md`. Use a short, lowercase,
    hyphenated slug based on the issue title. If that path would
    conflict with existing work, ask the developer where to save it.
3.  Read the matching template: `templates/feature.md` or
    `templates/bug.md`.
4.  Generate exactly one `issue-context.md` for this issue, filling the
    relevant template. Do not leave instructional placeholders in the
    final document.
5.  Preserve uncertainty and distinguish confirmed facts, assumptions,
    and open questions.
6.  Report the path and a brief summary of the contents.
7.  Stop. Do not begin implementation or create technical implementation
    plans.

## Output contract

The output must use the matching template and preserve its section
headings unless a section is genuinely not applicable. If a section is
not applicable, write `Not applicable` with a brief reason rather than
silently omitting a required section.

All generated documents must: - Use Markdown. - State the issue type,
title, and status. - Make in-scope and out-of-scope behavior explicit. -
Include a backlog with stable item IDs. - Include observable acceptance
criteria. - Record material constraints, decisions, and unresolved
questions. - Avoid speculative requirements and implementation-level
task breakdowns.

Use only these status values: - `Needs clarification`: a critical scope
or expected-behavior question remains unresolved. -
`Needs investigation`: diagnosis or evidence gathering is required
before a reliable correction or scope decision can be made. -
`Ready for implementation`: the developer has agreed the scope and the
work is sufficiently defined to be handed to a separate planning or
implementation process.

For a feature, use the feature template. For a bug, use the bug
template. Do not combine both formats into one backlog. If the ticket
genuinely contains both types of work, clarify whether to split it or
which type should be the primary issue before producing the output.

## Completion checklist

Before finishing, verify: - \[ \] The issue type is appropriate. - \[ \]
Scope and exclusions are explicit. - \[ \] Simpler alternatives were
considered where useful. - \[ \] Developer decisions were respected. -
\[ \] Repository inspection, if performed, was targeted and read-only. -
\[ \] Unknowns are clearly labelled. - \[ \] Every backlog item traces
to the agreed issue. - \[ \] Feature items use the required user-story
form. - \[ \] Bug items distinguish correction from investigation. - \[
\] Acceptance criteria are observable. - \[ \] No implementation tasks
or code changes were added. - \[ \] The output path and status are
correct.
