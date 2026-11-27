# Lessons

Friction that a note would have prevented. Read it before work in an area it covers. Append
an entry when a slice pays for something twice, or when a setup step costs far more than
its size.

FET keeps its own log at
[`docs/lessons.md`](https://github.com/Chrisgmsl22/fast-expense-tracker/blob/main/docs/lessons.md).
Its entries on parallel agents and subagent dispatch apply here too.

## Entry format

```markdown
## YYYY-MM-DD: <short title>

**Area**: <auth | networking | Xcode | CI | parallel agents | subagents | ...>
**What happened**: <1 to 3 lines>
**Rule**: <what to do next time, as an instruction>
```

## Entries

## 2026-11-27: Read the backend at `origin/main`, not at the local checkout

**Area**: backend contract
**What happened**: The local FET checkout was 98 commits behind. It still showed the old
login system and none of the Better Auth work.
**Rule**: Before you state what the backend has, run `git fetch` in the FET checkout and
read `origin/main`, or read the file on GitHub. Write the commit you checked into
`docs/reference/backend-contract.md`.
