# Roadmap

The "where are we" index. The planning session owns this file. A feature session edits only
its own slice in a phase file.

## Currently active

**Phase 0: Foundation.** Slice 0.1 is in review.

| Next | Blocked on |
| --- | --- |
| 0.2 Session hooks and status scripts | 0.1 merged |
| 0.3 Tech stack, Xcode project, CI | 0.1 merged, and Christian's answers to [ADR-0004](../decisions/0004-tech-stack.md) |
| FET CHORE-42 (other repo) | Nothing. It can start now |

## Phases

| Phase | Name | Design section | Needs from FET | State |
| --- | --- | --- | --- | --- |
| 0 | [Foundation](./phase-0-foundation.md) | n/a | Nothing | Active |
| 1 | Sign in and session | `01-sign-in-and-onboarding` screens 1 to 6 | CHORE-42, identity route, client contract | Not sliced |
| 2 | Expenses and add | `03-expenses-and-add` | `/api/v1` expenses, categories, cards, movements | Not sliced |
| 3 | Dashboard | `02-dashboard` | `/api/v1` dashboard summary, category detail, budgets | Not sliced |
| 4 | Money | `04-money` | `/api/v1` income, settlement, card balances | Not sliced |
| 5 | Settings and onboarding | `05-settings`, `01-sign-in-and-onboarding` screens 7 to 15 | `/api/v1` settings, account, onboarding | Not sliced |
| 6 | App Store release | `06-app-store` | A privacy policy page | Not sliced |

A phase gets its slices when it becomes next. Within a phase, screens with the badge Kept
or Adjusted come first. Screens with the badge New wait for their backend feature. Screens
with the badge Proposal wait for a decision from Christian.

## Backend track

Work in the [FET repo](https://github.com/Chrisgmsl22/fast-expense-tracker) that this app
waits on. The state lives in FET's registers. This table is a pointer.

| Order | FET item | What | State on 2026-11-27 |
| --- | --- | --- | --- |
| 1 | CHORE-42 | OAuth 2.1 provider, consent page, iOS client entry | Open |
| 2 | `fet-feat-mobile-auth-contract` | Identity route and the written client contract | Not started |
| 3 | `fet-feat-api-v1` | Data routes and the OpenAPI document | Not registered. Needs a route design |

Details: [`backend-contract.md`](../reference/backend-contract.md).

## Registers

| File | Holds |
| --- | --- |
| [`slices.json`](./slices.json) | Every slice: id, phase, title, type, dependencies |
| `chores.json`, `bugs.json` | Added when the first chore or bug exists |

Slice status is not stored. From slice 0.2 on, a script derives it from git and the
registers, the same way FET does (FET ADR-0008). Until then, this file is the status.

## Design briefs

The design READMEs tag screens with a brief number. The numbers come from the FET design
canvas. This list is read from the screen names, so check the section README before you
rely on a line.

| Brief | Feature |
| --- | --- |
| 1 | Global "amounts hidden" privacy toggle |
| 2 | Recurring expenses |
| 3 | Multi-currency |
| 4 | Add button and optimistic rows, offline state |
| 5 | Weekly summary |
| 6 | Category management |
| 7 | Card balances, archive, points redemption |
| 8 | Plan the month, due payments |
| 9 | Show full amounts on a category |
| 10 | Account: change password, delete account |
| 11 | Privacy policy |
| 12 | Partial reimbursement |
| 13 | Native sign-in, consent, session ended |
