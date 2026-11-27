# Doc structure

Where each kind of doc goes, and how long it can be.

## Where things go

| Path | Holds | Life |
| --- | --- | --- |
| `docs/roadmap/` | The index, the phase files, `slices.json`, later the chore and bug registers | Changes with every slice |
| `docs/specs/` | What a feature area does and why. One spec per area, numbered | Outlives the work |
| `docs/plans/` | Dated plans: sequencing, research results, a delivery order | Dies when the work ships |
| `docs/decisions/` | ADRs, numbered. One decision each | Permanent. Superseded, never edited away |
| `docs/conventions/` | How we work and how we write code | Changes with sign-off |
| `docs/reference/` | Lookup facts: the backend contract, domain rules | Kept current |
| `docs/design/` | Design screens by section, each with a `README.md` | Replaced on a new export |
| `docs/lessons.md` | Friction already paid for | Append only |

A spec and a plan are different docs. The spec holds what someone needs to understand the
feature. The plan holds the order of work. A line that a refactor would make false belongs
in a plan, not in a spec.

## Naming

- ADR: `NNNN-short-name.md`, 4 digits, next free number.
- Spec: `NNNN-short-name.md`, same rule.
- Plan: `YYYY-MM-DD-short-name.md`.
- Design screens: `NN-screen-name.png` inside the section folder, in screen order.

## Soft caps

A doc that you cannot read in one sitting is too long. The caps trigger a "should this
split?" decision. They are not a hard limit.

| Doc type | Soft cap (lines) |
| --- | --- |
| ADR | 200 |
| Convention | 300 |
| Spec | 400 |
| Plan | 600 |
| README or index | 150 |
| Reference, `AGENTS.md`, design section READMEs | exempt |

Over the cap: split the doc, or keep the narrative and link out to the data. Data lives in
one place (a JSON file, a reference table) and is never listed again in prose.

## Writing rules

- Short sentences, plain words, active voice.
- No em dashes. Use a period or a comma.
- Sentence-case headings.
- One idea per bullet.
- Name the source of a claim, or cut the claim.
