# fast-expense-tracker-ios-app

The native iOS app for Fast Expense Tracker (FET). Swift, one iPhone target. It reads and
writes the same data as the web app through the FET backend. **Agent-led**: agents write the
code, Christian reviews. The quality bar is the same as a production repo.

The repo is **public**. Everything that lands here is world-readable. Real financial data
lives in the FET database and stays there. It never goes into this repo, a fixture, a
screenshot or a log. Test data is invented.

## Orient

1. Read [`docs/roadmap/README.md`](./docs/roadmap/README.md). It says where we are and which
   work is available.
2. Read the active phase file that it points at.
3. Run `git fetch origin` and `git status -sb`. Report a dirty tree or a stale branch before
   you do anything else.

Session-start status hooks are slice 0.2. Until that slice ships, steps 1 to 3 are manual.

## Two repos

| Repo | Holds | Rule |
| --- | --- | --- |
| This repo | The Swift app, its docs, its design screens | Work here |
| [`fast-expense-tracker`](https://github.com/Chrisgmsl22/fast-expense-tracker) | The backend: login, `/api/v1`, all money rules | Backend work is a FET work item, in the FET repo, under FET's own `AGENTS.md` |

The phone never calculates money. The server stores `actualExpenditure` and the app shows
it. See [`docs/reference/domain.md`](./docs/reference/domain.md).

How the app logs in and calls the API:
[`docs/reference/backend-contract.md`](./docs/reference/backend-contract.md). Read it before
any work on networking or auth.

## Sessions and models

Christian runs this repo with one planning session and one session per feature
([ADR-0002](./docs/decisions/0002-agent-led-development-and-session-model.md)).

| Session | Does | Does not |
| --- | --- | --- |
| **Mind** (planning) | Plans, specs, ADRs, slices, briefs for feature sessions, the roadmap index | Feature code |
| **Feature session** | One slice on one branch, with its own `implementer` and `reviewer` subagents | Another session's slice, the roadmap index |

Feature sessions and their subagents run on Opus at medium effort. A feature session starts
cold, so everything it needs is in the slice's Plan block and the docs that block names.

## How work flows

One **slice** (or chore, or bug) per branch, per PR.

1. Pick from available work only. Never take a slice that another session owns.
2. Branch off current `main`: `feat/`, `chore/` or `docs/` plus the item id.
3. Implement with tests. Delegate to the `implementer` subagent by default.
4. **Review loop.** Run the `reviewer` subagent. Fix every Critical and Important finding,
   then review again. The loop stops after 2 rounds: if round 2 is not clean, report to
   Christian instead of running round 3.
5. UI slices include a check in the iOS Simulator against the screen in `docs/design/`.
6. Slice lifecycle before the PR: tick the tasks, copy the Plan block into the PR
   description, delete the Plan block. One commit, same PR.

Details: [`agent-workflow.md`](./docs/conventions/agent-workflow.md) ·
[`slice-planning.md`](./docs/conventions/slice-planning.md) ·
[`pr-strategy.md`](./docs/conventions/pr-strategy.md)

**Verify a subagent's work before you build on it.** A "done" report with an empty
`git diff` means that it wrote nothing.

**Parallel work needs real isolation.** Two sessions in one checkout share a HEAD and an
index. Each concurrent feature session gets its own worktree:
`git worktree add ../fast-expense-tracker-ios-app-<short> -b <branch> origin/main`.
A worktree that holds uncommitted changes gets reported, never removed.

## Rules

**Write the code.** Routine work needs no permission. Pick up the item and ship it.

**Commit, push and open the PR for authorized work.** Push only to the task branch, after
the checks and the review pass.

**Never merge or approve a pull request, and never push to `main`.** Opening the PR is
yours. Merging is Christian's, always. "Ship it" means finish the PR and hand over the
link. Never enable auto-merge. Never force-push. Never rewrite a pushed branch.

Ask for sign-off in the conversation before you:

- **Edit the rules.** `AGENTS.md`, `.claude/**`, `.gitignore`, `docs/decisions/**`,
  `docs/conventions/**`.
- **Expand a slice past its Scope (in).** Report the extra work as a follow-up.
- **Add a dependency.** A new Swift package needs an ADR or a line in the Plan block.

Always:

- **Land through a PR off `main`.** Every change, docs included.
- **Keep secrets out.** No token, key, password or real host credential in code, docs,
  fixtures, logs or screenshots. The app's OAuth client is public and has no secret.
- **Use invented data** in fixtures, previews, tests and screenshots.
- **Reach the network only through URLs already named in committed code or docs.**
- **Fix the failing check.** Do not skip it with `--no-verify`.
- **Keep the Xcode project generated.** Edit `project.yml`, not the `.xcodeproj`
  (applies once slice 0.3 ships).

Found a secret in the repo? Stop. Tell Christian before you touch history.

## PR and task titles

- Use `ios-<type>-<short-name>` for every PR title, for example `ios-feat-add-expense-sheet`.
- Types: `feat`, `chore`, `bug`, `docs`.
- Keep the session title the same as the PR title.

## GitHub access

- `gh` has two logins on this machine. The Blend host is the default. This repo's remote is
  `github.com`, so `gh` picks the personal login when you run it inside the repo.
- Outside the repo, set `GH_HOST=github.com` for that command.
- The token is in the keychain. Never print it. Never write it to a file.
- All commit, push, approval and merge limits above still apply.

## Conventions

| Area | Doc |
| --- | --- |
| Sessions, subagents, review loop | [`agent-workflow.md`](./docs/conventions/agent-workflow.md) |
| How to plan a slice | [`slice-planning.md`](./docs/conventions/slice-planning.md) |
| PR shape, commits, branches | [`pr-strategy.md`](./docs/conventions/pr-strategy.md) |
| Where each doc goes, and how long | [`doc-structure.md`](./docs/conventions/doc-structure.md) |
| Design screens and badges | [`docs/design/README.md`](./docs/design/README.md) |

Swift architecture, coding and testing conventions arrive with slice 0.3, after the tech
stack ADR is accepted. Until then, no Swift code.

Write an ADR in [`docs/decisions/`](./docs/decisions/) for a non-obvious trade-off, a
deferral or an architectural call. Append to [`docs/lessons.md`](./docs/lessons.md) when a
slice hits friction that a note would have prevented.

## Harness

| Layer | Lives in | State |
| --- | --- | --- |
| Instructions | `AGENTS.md` (`CLAUDE.md` is a symlink to it) | Here |
| Hard boundaries | `permissions.deny` in `.claude/settings.json` | Here |
| Subagents | `.claude/agents/` | Here |
| Session status lines, guards | `.claude/hooks/`, `scripts/` | Slice 0.2 |
| Must-not-merge checks | `.github/workflows/ci.yml` | Slice 0.3 |
