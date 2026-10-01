---
status: freeze-runsheet
updated: 2026-09-25
freeze-through: 2026-10-19
related: "[[WaveLead]]"
---

# WaveLead Freeze Checklist

#project

Weekly run-sheet for the **Final Beta freeze** through **2026-10-19**. Parent: [[WaveLead]].

> **No feature work during freeze.** Hotfixes only for money / security / data bugs. Resume development **2026-10-20**.

## Week of _______________

_Copy this section each week (or duplicate the note) and tick boxes._

### Money & payments
- [ ] Admin **payment-health** looks sane
- [ ] Ledger sanity check (marketplace + promotion)
- [ ] Any **fee-null** / `pending_fee_reconciliation` orders?
- [ ] Duplicate captures?
- [ ] Refunds status (if any)

### Marketplace ops
- [ ] Orders stuck past **72h review** SLA
- [ ] Orders stuck past **72h settlement** hold
- [ ] Payout requests waiting

### Campaigns
- [ ] Commitments stuck / not opening when funded
- [ ] Any `finalization_mismatch` (never counts as paid)

### Promotions
- [ ] Spend vs funded budget
- [ ] Delivery anomalies (homepage / search / category / country / channel)

### Email
- [ ] SMTP: sent vs `send_failed` / `smtp_not_configured` **per path**
- [ ] If secrets missing: note which path failed silently

### Supply & trust
- [ ] New submissions / claims queue
- [ ] Fast-verify activations
- [ ] Follower data staleness (cron still unwired?)

### Traffic
- [ ] GA4: `sign_up`, `channel_submission_*`, `booking_*`, `campaign_*`, `checkout_started`
- [ ] Top landing pages
- [ ] `/for-brands` behavior (stale copy watch)
- [ ] `search_used`

### Security / stability
- [ ] Errors / 500s
- [ ] Rate-limit hits
- [ ] Auth anomalies

### Bug diary

| Date | Area | What happened | Severity | Repro | Fix in Oct 20 cycle? |
|------|------|---------------|----------|-------|----------------------|
| | | | | | |
| | | | | | |
| | | | | | |

---

## Carry into Oct 20 backlog
_Items discovered during freeze that should land on the ranked next-cycle list in [[WaveLead]]:_

- [ ]
- [ ]
- [ ]

## Notes
- Money streams stay separate: marketplace 90/10 · campaign commitment 5% (not revenue) · promotions CPM · entitlements.
- Do not invent follower / revenue metrics; measure **follow intent** only.
- Archive of pre-freeze note: [[WaveLead (archive 2026-09-25)]]
