# ADR-0003: Plans, specs, slices and design screens live in this repo

Date: 2026-11-27
Status: Accepted

## Context

Christian's work setup keeps specs in a company wiki. This is a personal, public project.
Its docs must be readable by any agent that clones the repo, with no access to anything
else.

## Decision

1. Specs, plans, ADRs, the roadmap and the conventions live under `docs/`. Nothing about
   this project goes to a company system.
2. The design screens live under `docs/design/`, in the section folders of the export:
   sign in and onboarding, dashboard, expenses and add, money, settings, App Store. Each
   section keeps its `README.md`, which gives every screen a badge and the reason for each
   change.
3. The Claude Design source files stay in `docs/design/source/`, so the designs can be
   edited later.
4. A new export replaces a section folder in one PR. Screens are not edited by hand.

## Consequences

- A slice's Plan block names its screens by path.
- The PNG files add about 19 MB to the repo. That is acceptable for 103 screens. If exports
  become frequent, we revisit (Git LFS, or a release asset).
- The screens show invented demo data, so they are safe in a public repo. A screenshot of
  the real app with real data never goes here.
