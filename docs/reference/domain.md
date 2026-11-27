# Domain

The money rules that the app must respect. The full reference is FET's
[`domain-reference.md`](https://github.com/Chrisgmsl22/fast-expense-tracker/blob/main/docs/reference/domain-reference.md).
This file holds only what an iOS agent needs so that it does not break those rules.

## The app shows money. The server counts it.

The app never calculates a total, a split or a bucket. It sends what the user entered and
shows what the server returns.

## What the numbers mean

- The owner tracks in **MXN** and splits shared expenses with a partner.
- For each expense the server stores `actualExpenditure`:

  ```
  actualExpenditure = isShared ? amount × yourPercentage : amount
  ```

- **Totals use `actualExpenditure`, never `amount`.** It is stored, so an old expense keeps
  its split when the default percentage changes.
- The exception is a card's balance. A card was charged the full `amount`.
- Budget buckets follow a 50/25/25 rule: essentials, discretionary, savings. **Savings is
  its own bucket, not an essential.**

## What this means on screen

- A list row can show both numbers ("my share" and the full amount). Each comes from the
  server. Do not derive one from the other.
- The split slider in the Add form shows a preview of the share. Treat it as a preview. The
  stored value comes back from the server after the save.
- The global "amounts hidden" setting masks every money value in the app, including in
  widgets, notifications and screenshots for the App Store.

## Demo data

The design screens use invented data: November 2026, partner "Sam", a 68/32 split, MXN.
Use the same invented data in previews, fixtures and tests. Never use a real name, a real
amount or a real card.
