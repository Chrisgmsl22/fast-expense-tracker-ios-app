# Slice planning

How to plan a vertical slice before any code. Small PRs need a clear scope first. The
lifecycle is the same as in FET.

## When to plan

Plan a slice when it becomes next. Do not plan slices that are weeks away. Their context
goes stale.

## Where the plan lives

In the phase file under `docs/roadmap/`, below the slice's task list. A Plan block exists
only while its slice is in flight.

**The Plan block is deleted in the same PR that ships the slice.** The PR description is
its permanent home. `main` never holds a stale Plan block.

Each slice that runs in parallel has its own Plan block and its own branch. A feature
session edits only its own block.

## Full Plan or Light Plan

Use a **Full Plan** when the slice:

- touches auth, tokens, the Keychain or any secret handling
- sets a pattern that later slices copy (a Foundation slice)
- adds a dependency
- changes many files or has an open design question
- implements a screen with the badge **Proposal**

Use a **Light Plan** when the slice follows a pattern that already exists in the repo, or
is polish, or is a bug fix with a known cause.

### Full Plan template

```markdown
#### N.M: [Slice name] [PR]

##### Plan

**Design screens**

- The files in `docs/design/` this slice implements.

**Scope (in)**

- What this PR touches, to file level where known.

**Scope (out)**

- What waits for a later slice.

**Backend dependency**

- The `/api/v1` endpoints this slice calls, and the state of each. "None" if it uses mock data.

**Design decisions**

- The calls made here. Link the ADR for a large one.

**Acceptance criteria**

- Checkable statements. "Tests pass" is fine. "Code is clean" is not.

**Open questions**

- Resolve all of these before any code.

##### Tasks

- [ ] ...
```

### Light Plan template

```markdown
#### N.M: [Slice name] [PR]

**Scope**: [one sentence on the outcome for the user]
**Design screens**: [files, or n/a]
**Out** (optional): [what is deferred]

##### Tasks

- [ ] ...
```

## Rules of thumb

- **Scope (out) matters as much as Scope (in).** A named exclusion keeps the PR small.
- **One slice, one concern.** Two unrelated items in Scope (in) are two slices.
- **Open questions block code.**
- **A design badge sets the risk.** Kept and Adjusted screens have a web twin to compare
  with. New screens need the backend feature to exist. Proposal screens need a decision
  from Christian first.

## The cycle

1. The slice becomes next. The mind writes the Plan block.
2. The mind resolves the open questions with Christian.
3. A feature session implements it (see [`agent-workflow.md`](./agent-workflow.md)).
4. Checks pass locally.
5. The review loop passes.
6. Cleanup, in one commit in the slice's PR: tick the tasks, copy the Plan block into the
   PR description, delete the Plan block, mark the slice shipped in its own section.
7. The feature session opens the PR and reports the link.
8. Christian merges.
9. If the slice hit friction that a note would have prevented, append to `docs/lessons.md`.
10. The mind updates `docs/roadmap/README.md`.

## What a good slice looks like

- One concern: one screen, one flow, one client module.
- A reviewer can hold the whole change in mind in 30 minutes.
- Tests included.
- Mergeable alone. It does not need an unmerged sibling PR.
