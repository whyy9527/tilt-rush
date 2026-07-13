# Tilt Rush Issues

This directory is the repository's canonical issue ledger. It records actionable work, decisions, acceptance criteria, verification evidence, and outcomes close to the code.

## Naming

- Assign the next four-digit ID by adding one to the highest existing ID.
- Use `issues/NNNN-short-slug.md` for a small issue.
- Use `issues/NNNN-short-slug/NNNN-short-slug.md` when the issue owns screenshots, reports, recordings, research, or other companion artifacts.
- Keep the ID and path stable. Lifecycle state belongs in the first non-empty line, not in the filename or directory name.
- `issues/README.md` and companion artifacts are never issue candidates; only the numbered main issue markdown files participate in the lifecycle.

## Status

The first non-empty line is the source of truth:

- `🟡 # ...` — open and actionable.
- `📌 # ...` — picked for active work; excluded from general selection.
- `⌛️ # ...` — waiting for a named human decision, authorization, external event, or evidence trigger.
- `✅ # ...` — closed with resolution and verification recorded.

Any issue without a terminal `✅`, waiting `⌛️`, or reserved `📌` prefix is treated as actionable. A prose status such as “blocked”, “skipped”, or “deprecated” does not close an issue.

## Required Shape

```markdown
🟡 # <short title>

Created: YYYY-MM-DD
Source: <request, observation, parent issue, or evidence>

## Goal

<one measurable outcome>

## Context

<why this matters and what is true now>

## Scope

- ...

## Non-goals

- ...

## Acceptance Criteria

- [ ] ...

## Verification

- `<command or manual flow>` — <expected evidence>
```

An issue must describe one chosen solution. Alternatives and research can explain the decision, but implementation scope must not contain multiple competing paths.

## Lifecycle

1. **Capture:** create or update the issue from observed evidence. Reuse an issue only when the problem, owner, and verification path are still the same.
2. **Clarify:** define the smallest independently verifiable slice, its non-goals, and acceptance criteria before implementation.
3. **Pick:** change the first line to `📌` when work starts. Work on one issue at a time unless dependencies explicitly require otherwise.
4. **Implement:** keep code, tests, and issue evidence aligned. Scope expansion becomes a new numbered issue rather than an ever-growing checklist.
5. **Verify:** exercise the complete player-visible flow. For game changes, record automated state checks and screenshots where they materially prove the result.
6. **Close:** change the first line to `✅` only after the goal is achieved and verified. Add the following section:

```markdown
## Resolution

- Closed at: YYYY-MM-DD HH:mm <timezone>
- Commit: <hash>
- Verification:
  - `<command or manual flow>` — passed
- Notes: <outcome and residual risk, or "none">
```

If work cannot proceed without a decision or external trigger, change the first line to `⌛️` and add `## Waiting Decision` with the owner, exact question or trigger, and notification date. Do not use waiting merely because work is difficult or large.

Closed issues stay in place. Do not move them to a `done` or `archive` directory. When follow-up work has a different scope or verification path, create a new issue and leave only a short link in the parent.
