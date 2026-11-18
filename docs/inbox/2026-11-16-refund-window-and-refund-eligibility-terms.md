---
captured: 2026-11-16T15:25:10Z
source: cohort-005-project
status: open
tags: []
---

# Refund Window / Refund Eligibility terms and duplicated eligibility rules

Park: Refund Window / Refund Eligibility terms + duplicated eligibility rules (completion-limit bypass bug).

## Context

Came up while unifying refund/cancellation/chargeback language into **Refund Request** / **Refund** (see `CONTEXT.md`).
Proposed glossary terms, not yet agreed:

- **Refund Window**: 14 calendar days from the Purchase.
- **Refund Eligibility**: inside the Refund Window, under 50% of lessons completed, under 2 hours watched, and not a claimed team seat.

The eligibility rules exist twice and have drifted:

- `app/routes/courses.$slug.tsx` `getCancellationOffer` checks the 50% completion limit (`CANCEL_COMPLETION_LIMIT`).
- `app/routes/courses.$slug.refund.ts` action does not, so a direct POST bypasses it.
- The 14-day constant is defined in both files (`CANCEL_WINDOW_DAYS`, `REFUND_WINDOW_DAYS`).
- The watched-time query is copy-pasted in both files, and the offer checks a lower bound on the window that the action does not.
