# PR strategy

## Goal

Small PRs that Christian can review in one sitting. He is the only human reviewer, so the
size of a PR is the limit on how fast work lands.

## Rules of thumb

- One slice, one branch, one PR.
- Slice vertically: one user flow from screen to network, not "all the models" then "all
  the views".
- A refactor and a feature are 2 PRs.
- Docs-only changes also land through a PR.

## Branching

| Prefix | Use |
| --- | --- |
| `feat/<id>-<short-name>` | A roadmap slice |
| `chore/<id>-<short-name>` | Tooling, harness, cleanup |
| `docs/<short-name>` | Docs only |

Branch off current `origin/main`. Never push to `main`. Never force-push. On a pushed
branch, add a commit. Do not amend or rebase it.

## Commits

- Conventional Commits: `feat(scope): subject`, `fix`, `chore`, `docs`, `test`, `refactor`.
- Subject of 72 characters or fewer, imperative mood, readable alone.
- No body by default. Add 1 to 3 lines only when the reason is not visible in the diff.
- Do not restate the diff.

## Pull requests

- Title: `ios-<type>-<short-name>`, for example `ios-feat-sign-in-sheet`.
- Body: the template in `.github/PULL_REQUEST_TEMPLATE.md`. For a slice, the Scope sections
  come from its Plan block.
- UI changes include a Simulator screenshot next to the design screen. Invented data only.
- Fill "Backend dependency" when the PR needs a FET endpoint. State if that endpoint is
  merged and deployed.

## Before you call a PR ready

1. Refresh `origin/main` and confirm that the branch includes it.
2. Confirm that GitHub reports the PR mergeable and that the required checks pass.
3. Confirm that the review loop ended with a clean pass.
4. If a check is pending, name it. Do not ask Christian to find it in the PR page.

Agents open PRs. Christian merges them. No agent merges, approves or enables auto-merge.
