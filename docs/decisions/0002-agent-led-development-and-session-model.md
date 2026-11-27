# ADR-0002: Agent-led development with one planning session and one session per feature

Date: 2026-11-27
Status: Accepted

## Context

FET is agent-led: agents write the code and Christian reviews. That worked, and this repo
keeps it. Christian also wants the pattern he uses at work: one coordinating session, and
one session per piece of work.

## Decision

1. Agents write the code. Christian reviews and merges. No agent merges, approves or pushes
   to `main`.
2. One **mind** session plans: the roadmap, specs, ADRs, Plan blocks and the brief for each
   feature session. It runs on the most capable model. It does not write feature code.
3. Each slice runs in its own **feature session**, with its own `implementer` and
   `reviewer` subagents, on its own branch. A second concurrent session gets its own
   worktree.
4. Feature sessions and their subagents run on Opus at medium effort.
5. The review loop is required before a PR and stops after 2 rounds. A third round needs
   Christian's answer.
6. The harness follows FET's shape: instructions in `AGENTS.md`, hard limits in
   `.claude/settings.json`, subagents in `.claude/agents/`, status derived from git and the
   JSON registers.

## Consequences

- The Plan block must be complete enough for a session that starts cold. Open questions get
  resolved in the mind session, before the hand-off.
- The mind owns the roadmap index. A feature session edits only its own slice, so parallel
  sessions do not conflict in that file.
- Planning costs more per token and happens once. Implementation costs less per token and
  happens many times.
- Enforcement by hooks and CI arrives in slices 0.2 and 0.3. Until then the rules in
  `AGENTS.md` are written rules only.
