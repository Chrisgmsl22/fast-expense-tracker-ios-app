# Agent workflow

How sessions and subagents divide the work in this repo. The rules are in
[`AGENTS.md`](../../AGENTS.md). This doc explains how to apply them.

## Operating model

Agents write the code. Christian reviews and merges. No agent merges, approves or pushes
to `main`.

There are 3 levels:

| Level | Who | Owns |
| --- | --- | --- |
| Mind | One planning session | The roadmap index, specs, ADRs, Plan blocks, the brief for each feature session |
| Feature session | One session per slice | One branch, one PR, its own subagents, its own review loop |
| Subagent | `implementer`, `reviewer` | One task inside one feature session |

Feature sessions and subagents run on Opus at medium effort
([ADR-0002](../decisions/0002-agent-led-development-and-session-model.md)).

## The mind

The mind plans. It does not write feature code.

- It keeps `docs/roadmap/README.md` current: what is active, what is available, what is
  blocked and on what.
- It writes the Plan block for a slice when the slice becomes next.
- It resolves open questions with Christian before a feature session starts.
- It tracks backend work in the FET repo that an iOS slice depends on.
- It hands each feature session a brief (below).

Docs-only changes that define the plan or the harness (ADRs, conventions, roadmap files)
can come from the mind. They still land through a PR.

## The brief for a feature session

A feature session starts with an empty context. The brief is short because the Plan block
holds the detail.

```
Slice: <id and name>
Branch: <feat|chore|docs>/<id>-<short-name>
Worktree: <path, or "canonical checkout">
Plan block: docs/roadmap/<phase file>#<anchor>
Read first: AGENTS.md, then the docs the Plan block names
Backend dependency: <FET item and its state, or none>
Done means: PR open with a clean review, link reported back
```

## The feature session

1. Read `AGENTS.md`, the Plan block and the docs it names.
2. Confirm that the Plan block has no open question. If it has one, stop and report.
3. Dispatch the `implementer` subagent with the item id and the Plan block location.
4. Check the hand-back: read `git diff`, do not trust the report alone.
5. Run the review loop (below).
6. Push the task branch. Open the PR with the template. Report the link.

A feature session edits only its own slice in the phase file. The "Currently active"
pointer in `docs/roadmap/README.md` belongs to the mind.

## The review loop

It is required before every PR.

1. Dispatch the `reviewer` subagent on the branch.
2. Fix every Critical and Important finding. Send the fix back to the `implementer`, or fix
   it in the feature session when it is a few lines.
3. Review again.
4. **Cap: 2 rounds.** If round 2 still has a Critical or Important finding, stop and report
   to Christian with the open findings. Do not run round 3 without his answer.

UI slices add a Simulator check against the screen in `docs/design/`. Unit tests do not
verify a screen.

## When not to use a subagent

- A change of a few lines that you already understand.
- A lookup where you know the file.
- A docs fix.

## Parallel work

One checkout holds one branch. A second concurrent feature session gets a worktree:

```
git worktree add ../fast-expense-tracker-ios-app-<short> -b <branch> origin/main
```

- Slices that run in parallel declare a file footprint in their Plan block. A slice that
  needs a file outside its footprint stops and reports.
- After the PR merges: `git worktree remove <path>`, then `git branch -d <branch>`.
- A worktree with uncommitted changes gets reported, never removed.

## Blockers

Flag a blocker or an unclear requirement at once, with a draft of the question for
Christian. Do not wait for the end of the session.

## Anti-patterns

- A feature session that plans the next slice. That is the mind's job.
- The mind writing feature code "because it is small".
- A PR opened before a clean review pass.
- A subagent report accepted without a look at the diff.
- A backend gap patched on the phone. If the API cannot do what the screen needs, the fix
  is a FET work item.
