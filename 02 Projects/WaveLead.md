---
status: final-beta
updated: 2026-09-25
next-build: 2026-10-20
---

# WaveLead

#project

Growth & monetization platform for **WhatsApp Channels**. [wavelead.org](https://wavelead.org) · [github.com/joefebrian/wavelead](https://github.com/joefebrian/wavelead) (public). Product of [[02 Projects/P2P Labs|P2P Labs]]. **Not affiliated with Meta/WhatsApp.**

**Loop:** Discover → Follow Intent → Measure → Grow → Monetize  
**Sides:** channel owners · brands  
**Measures:** follow intent (clicks / 24h unique intent) — **not** confirmed followers.

## Phase — Final Beta
Feature development **frozen** for the month. Focus = traffic + finding issues. Resume development **2026-10-20**. Hotfixes only for money / security / data bugs. Weekly run-sheet: [[WaveLead Freeze Checklist]].

## Status board

| State | Items |
|-------|--------|
| **Complete** | Channel submission & discovery; owner dashboard; manual verification (free); fast verification ($1 one-time); channel approval; owner rate card; direct brand→owner sponsorship; marketplace booking; economics owner 90% / WaveLead 10%; brand campaign marketplace; campaign commitment 5% (separate from revenue); campaign funded-capacity enforcement; owner promotion / sponsored placement E2E; admin promotion rates; promotion CPM server-authoritative; provider-neutral promotion payment; promotion delivery (homepage/search/category/country/channel); promotion reporting; Brand Pro $15/30d manual renewal; Founding Lifetime $100; support chat core; GA4 foundation; security hardening major patch; transactional email code |
| **Yellow** | **SMTP production** — code done; set `SMTP_HOST`/`PORT`/`USER`/`PASS`/`FROM` secrets in prod; send one real email per path and confirm delivery · **SEO** — audit done; remediation committed in `6c3ff51` but commit says deploy not executed — confirm prod · **Weekly follower scheduler** — `POST /api/cron/whatsapp-refresh` + `CRON_SECRET` exists; needs platform cron (e.g. weekly Monday 03:00) · **Advanced admin reports** — deferred; domain reports exist (payment-health, ledger, Brand Pro report) |

## Architecture
Next.js **15.5.26** App Router + TypeScript + MongoDB + Yarn.  
UI → one API catch-all `app/api/[[...path]]/route.ts` (~2,500 lines) → ~80 services (`lib/services`) → ~20 repositories (only layer touching Mongo).  
Roles: `visitor < user < channel_owner < business < moderator < admin < super_admin` — re-read from DB every request (JWT = identity only).  
Payments provider-neutral (PayPal adapter live). Money: **USD cents** for marketplace/commercial; **USD micros** in promotion ledger (double-entry).

## Money streams (keep separate)
1. **Sponsorship marketplace** — 90/10, Payment Protection, 72h review + 72h settlement hold, mostly manual payouts.
2. **Campaign commitment** — 5% of budget; **not revenue**; campaign opens only when funded; applicants hand off into marketplace booking.
3. **Owner promotions CPM** — WaveLead ad inventory, admin-set CPM, **not** 90/10.
4. **Entitlements** — $1 fast verify · Brand Pro $15/30d · Founding Lifetime $100; prices snapshotted in `commercial_pricing_config` history.

## Known issues / watch list
- PayPal webhook concurrency shared across streams (duplicate captures; fee-null orders stuck in pending fee reconciliation)
- Rate limiter is single-node (Redis deferred)
- SMTP fails silently by design
- Claim vs $1 fast-verify concurrency
- Campaign commitment `finalization_mismatch` never counts as paid
- `/for-brands` copy stale (says sales-assisted; marketplace "coming later")
- No `/for-owners` page (404)
- Follower counts stale until cron wired
- README has outdated M06-era "no live marketplace" text
- 0 open GitHub issues/PRs as of 2026-09-23

## Next cycle backlog (from 2026-10-20)
1. SMTP verify + deliverability monitoring
2. Confirm SEO + security patches live
3. Wire weekly follower cron
4. Rewrite `/for-brands` + add `/for-owners`
5. Public campaign board + shortlist/reject emails
6. Campaign→booking handoff polish
7. Shared/Redis rate limiting
8. Advanced admin reports
9. Local IDR provider (Xendit/Midtrans)
10. Clearer creator payouts/receipts
11. README refresh
12. Consent/GA4 cleanup-on-revoke

## Positioning vs siblings
| Product | Role |
|---------|------|
| [[02 Projects/atlasnow\|AtlasNow]] | Multi-outlet WhatsApp Business CRM + Maps |
| **WaveLead** | WhatsApp Channels marketplace |
| [[02 Projects/AtlasNexus\|AtlasNexus]] | YouTube-first campaigns |

**Competitors:** Meta Promoted Channels (native) · FindChannels (directory) · Inceptoo (~30% cut) · Channelad / MindViewers (marketplaces)

## Guardrails
Do **not** claim confirmed followers, live revenue numbers, or Meta affiliation. Site states ~216 channels indexed (**site claim, not verified**).

## Links
- [[WaveLead Freeze Checklist]]
- [[WaveLead (archive 2026-09-25)]]
- [[02 Projects/P2P Labs|P2P Labs]] · [[02 Projects/atlasnow|AtlasNow]] · [[02 Projects/AtlasNexus|AtlasNexus]]
