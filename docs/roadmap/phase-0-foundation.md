# Phase 0: Foundation

Get the repo ready for agent-led work before any feature. Plan:
[`2026-11-27-foundation-plan.md`](../plans/2026-11-27-foundation-plan.md).

**Done when:** a feature session that starts cold can pick a slice, build it, pass checks
in CI and open a PR, with the session-start lines telling it where things stand.

## Slices

#### 0.1: Harness docs and design screens [PR]

**Scope**: The instructions, limits, subagents, conventions, first ADRs, roadmap, backend
contract and the 103 design screens are in the repo.

##### Tasks

- [x] `AGENTS.md` with the `CLAUDE.md` symlink
- [x] `.claude/settings.json` deny rules, `implementer` and `reviewer` subagents
- [x] Conventions: agent workflow, slice planning, PR strategy, doc structure
- [x] ADR-0000 to ADR-0003 accepted, ADR-0004 proposed
- [x] Roadmap index, `slices.json`, this file
- [x] Backend contract and domain reference
- [x] Design screens under `docs/design/`
- [x] PR template

#### 0.2: Session hooks and status scripts

Type: Foundation. Depends on 0.1.

Port FET's derived status to this repo, so each session starts with the state.

##### Tasks

- [ ] `scripts/roadmap-status` derives each slice's state from git and `slices.json`
- [ ] `.claude/hooks/` for branch status, roadmap status and worktree status at session start
- [ ] `scripts/session-context.sh` prints the same lines for a tool with no hook runner
- [ ] A Bash guard hook for the limits that a deny pattern cannot express
- [ ] A subagent hand-back hook that prints the changed paths
- [ ] Tests for the hook verdicts against a throwaway repo
- [ ] `chores.json` and `bugs.json` with their status scripts

Open question for the Plan block: which language for the status scripts. FET uses
TypeScript, and this repo has no Node toolchain. Bash with `jq`, or Swift scripts.

#### 0.3: Tech stack, Xcode project, CI

Type: Foundation. Depends on 0.1 and on Christian's answers to
[ADR-0004](../decisions/0004-tech-stack.md).

##### Tasks

- [ ] ADR-0004 accepted, with its Consequences written
- [ ] `project.yml` and an app target that builds and shows one empty screen
- [ ] A unit test target and a UI test target, each with one passing test
- [ ] `docs/conventions/architecture.md`, `swift.md` and `testing.md`
- [ ] Lint and format config
- [ ] `.github/workflows/ci.yml`: build, test, lint, a secret scan
- [ ] Protect `main`: require the CI check and a PR (Christian's step, in the GitHub settings)

#### 0.4: Design tokens and base components

Type: Foundation. Depends on 0.3.

##### Tasks

- [ ] Colors, type sizes and spacing read from the screens in `docs/design/`, as one token file
- [ ] The card, bucket and category color systems, the same values as FET
- [ ] Base components that many screens share: money text with the hidden state, list row, sheet header, primary button
- [ ] A preview catalog that shows each component with invented data
- [ ] `docs/specs/0001-design-system.md`
