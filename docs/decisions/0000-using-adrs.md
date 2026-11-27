# ADR-0000: We record decisions as ADRs

Date: 2026-11-27
Status: Accepted

## Context

Agents start each session with no memory of earlier ones. A decision that lives only in a
conversation gets made again, often differently.

## Decision

Each non-obvious trade-off, deferral or architectural call gets one short file in
`docs/decisions/`, numbered in order. The format is Context, Decision, Consequences.

- Status is one of: Proposed, Accepted, Superseded by ADR-NNNN.
- A Proposed ADR is a question for Christian. Agents do not build on it until it is Accepted.
- An accepted ADR is not edited to change its decision. A new ADR supersedes it. That needs
  sign-off first.

## Consequences

- A new session can find why something is the way it is.
- A decision made in the FET repo that binds this repo gets an ADR here that links to the
  FET one. It is not copied.
