---
title: AtlasNow — Monetization PRD
aliases:
  - AtlasNow Monetization
  - AtlasNow Pricing
company: P2P Labs
product: AtlasNow
document_type: prd
version: 0.2.0
date: 2026-08-29
status: draft-for-founder-review
depends_on:
  - "[[AtlasNow-Blueprint]]"
  - "[[AtlasNow-PRD]]"
tags:
  - atlasnow
  - monetization
  - pricing
  - packaging
---

# AtlasNow — Monetization PRD

> [!danger] MASTER — money
> **Dokumen ini master** untuk apa pun yang menyentuh uang, paket, meter, kredit, gateway, invoice, atau klaim harga — termasuk fitur baru.
>
> - Mau ship blast, Cloud, OCR, Free vs Brand, Creem, Xendit, `/pricing`, copy “unlimited”? **Baca ini dulu — termasuk fitur yang kelihatannya “bukan billing”.** Kalau konflik, **PRD ini yang menang** sampai founder mengubahnya di sini.
> - [[AtlasNow-PRD]] = apa yang software boleh *ada*. **Ini** = apa yang boleh *dijual*, *diukur*, *ditagih*.
> - Jangan invent meter, harga, atau “gratis API” di kode / landing / pitch yang tidak ada di sini.
> - Angka IDR bertanda **DRAFT** sampai founder mengunci. Yang sudah locked direction: Free vs paid APIs, credits PAYG, rail ID vs luar, PayPal bukan primary.

> [!important] Status
> **2026-08-29:** Situs publik sudah punya `/pricing` sebagai **Free + One brand + Several brands**, angka masih “kami pasang / we’ll quote”. Bukan self-serve checkout. §15–17 = **credits + pay-as-you-go** (WhatsApp blast dan pemakaian berbayar lain). Gateway: invoice IDR tetap default; **Creem.io** kandidat kartu/kredit; PayPal bukan rail utama.

**Product language = English** untuk nama paket. Penjelasan operasional boleh ID.

| Item | Decision |
|---|---|
| Owner | P2P Labs founder |
| Sells | P2P Labs |
| Product | AtlasNow |
| Managed brand | P2P Local Growth — Powered by AtlasNow |
| Buyer today | Multi-location brand HQ, sold and operated by P2P |
| Not yet | Self-serve checkout, public IDR table, other agencies as resellers |
| Source of truth | **This PRD is master for money.** [[AtlasNow-PRD]] for product scope. [[AtlasNow-Blueprint]] §15–16 for thesis. |

## 1. What we sell

AtlasNow is sold as a **Local Demand-to-Action Control Tower** — software plus, when the client wants it, P2P operating the tower.

We sell:

- a working location graph (every branch in one list);
- Google listing, review, and (when connected) search/ads visibility;
- one inbox for WhatsApp and Facebook Messenger per mapped branch;
- actions with an owner and a deadline.

We do **not** sell:

- guaranteed Maps rank;
- guaranteed revenue or “incremental sales”;
- a visit count we invented from a directions tap;
- official WhatsApp Cloud until Meta approves that path;
- other people’s Facebook or Google logins.

Money follows **locations and channels that are actually connected**, not seats and not vanity dashboard logins.

## 2. Who pays

| Role | Who | Pays? |
|---|---|---|
| Economic buyer | Brand HQ (marketing / ops lead) | Yes — invoice to the brand |
| Operator | P2P Labs (agency tenant in the app) | No — we are the vendor |
| Brand staff | Client Admin / branch PIC | No extra seat fee in MVP |
| End customer who DMs a Page | Shopper | Never |

One AtlasNow **client tenant** = one brand = one bill.  
One **active location** = one branch the client asked us to run this month.

P2P’s own workspace (demo, internal Page tests) is **not billable**.

> Later (not this PRD): another agency could license AtlasNow. That is a second motion. Do not design reseller margins until the first five brand invoices are real.

## 3. Go-to-market motion (locked)

```mermaid
flowchart LR
    A["Leakage audit"] --> B["90-day paid pilot"]
    B --> C["Monthly Control"]
    C --> D["Add-ons"]
```

1. **Audit** — paid, time-boxed, even if they do not stay. See Blueprint §16 entry offer.
2. **Pilot** — 90 days, 10–20 locations, Control + optional Conversation.
3. **Retain** — monthly Control on the active location set.
4. **Expand** — Conversation, Convert, then Revenue when the product can prove it.

Public site (2026-08-29): **Free** = membership desk without Meta/Google APIs (hook). Paid Brand/Group = quote after follow-up, then APIs. Internal demo logins stay internal. Free is **not** free WhatsApp blast.

## 4. Packages

Names are English. They match Blueprint §15.

| SKU | What the client is buying | When we may sell it |
|---|---|---|
| **Foundation** | One-time setup: location graph, access, mapping, data-health cleanup | Now (with every new brand) |
| **Control** | Platform + monitoring per *active* location: listings, reviews, leakage, actions | Now — this is the core subscription |
| **Growth Ops** | P2P people run the tower (weekly sprint, replies drafted, listing fixes) | Now — managed retainer, not software |
| **Conversation** | WhatsApp + Messenger inbox on mapped branches | Sell as **beta**: WAHA unofficial, Meta app still unpublished until Live |
| **Convert** | Vouchers / local ads ops | After Convert Lite in product PRD is real |
| **Revenue** | POS / booking match, verified attributed revenue | Revenue 2.0 only |

### 4.1 Control includes

- Tenant + users for that brand (no per-seat charge).
- Location list, Maps import, readiness.
- Google Business Profile connect (brand’s own login).
- Reviews inbox + reply.
- Control Tower / leakage / actions that exist in the build.
- Privacy, terms, and data-deletion pages.

### 4.2 Control does **not** include

- P2P doing the weekly work (that is Growth Ops).
- A WhatsApp number or Facebook Page (the brand brings those).
- Ads spend (ads budget is the brand’s, paid to Google/Meta).
- Hosting the brand’s website.

### 4.3 Conversation includes (beta)

- One mapped WhatsApp session **or** one mapped Facebook Page per location, in the Atlas inbox.
- Webhook ingest. Monitor first; send/reply in-product only when that feature exists.
- Honest identity: phone only if WhatsApp sent a phone; Messenger stays a platform id.

### 4.4 Conversation sales rule

Do not invoice Conversation as “official WhatsApp Business API” while the pipe is WAHA.  
Do not promise live Messenger DMs until the Meta app is **Live** and the Page is subscribed.  
Write the invoice line as **Conversation (beta) — inbox for connected chats**.

## 5. What we meter

| Meter | Definition | Bill? |
|---|---|---|
| **Client tenant** | One brand workspace | Base platform fee |
| **Active location** | `Location.status = ACTIVE` and the client wants it in the monthly set | Per location / month |
| **Connected chat channel** | ACTIVE mapping `WAHA` or `FACEBOOK` / `INSTAGRAM` on that location | Conversation add-on / channel / month |
| **Seat** | A login | No (MVP) |
| **Message volume (inbound)** | Customer wrote first, 24h service window | No. Care replies are not PAYG. |
| **WhatsApp credits** | Billed Cloud **template** sends (blast / utility / auth outside the free window) | Yes — PAYG wallet, §16 |
| **Other usage** | Anything we pay a vendor per use (future OCR overage, extra WABA, etc.) | Yes — same wallet or a named meter, §17 |
| **Google / Meta API quota** | Their tokens | No — they own the accounts |

Archived locations drop off the next invoice.  
A location that is ACTIVE but has no Google and no chat still counts if the client asked us to keep it on the list.

## 6. Price architecture (locked)

```text
Monthly invoice
  = Base platform          (one per brand)
  + Control × active locations
  + Conversation × connected chat channels     (if any)
  + Growth Ops retainer                        (if any)
  + Convert / Ads ops                          (if any)
  + pass-through ads spend                     (never marked up as “Atlas revenue”)
```

Plus, at the start:

```text
One-time
  = Foundation setup
  and/or paid Leakage Audit
```

Performance fee is **allowed only** when:

- the outcome is verified (redemption or matched transaction — see product PRD §1.2);
- the formula is in the SOW *before* the campaign;
- we never take a cut of “directions” or star-rating movement.

## 7. Draft IDR bands — founder must lock

> [!warning] DRAFT
> Angka ini usulan supaya ada titik mulai. **Bukan** komitmen sales. Ganti atau hapus sebelum invoice pertama.

Assumes beachhead 20–200 locations, F&B / retail, billed monthly, IDR, exclude VAT.

| Line | DRAFT band | Notes |
|---|---|---|
| Leakage audit (one brand) | IDR 15–40 jt | Scales with outlet count; 1–2 week delivery |
| Foundation setup | IDR 8–25 jt | Waived or reduced if they just paid a full audit |
| Base platform / month | IDR 3–7 jt | One brand tenant |
| Control / active location / month | IDR 150–350 rb | Volume break at 50 and 100 locations |
| Conversation / connected channel / month | IDR 75–150 rb | Beta. Cap or discount if both WA + FB on same store |
| Growth Ops retainer / month | IDR 12–40 jt | People, not software. Scope in SOW (hours or stores) |
| 90-day pilot | 70–80% of (base + Control × cohort) | Cohort = 10–20 stores, not the whole chain |

**Worked example (DRAFT only):** 40 active locations, Control only, no chat add-on.

`5 jt base + 40 × 250 rb = IDR 15 jt / month`  
plus Foundation in month 1.

Founder lock checklist (do not publish until ticked):

- [ ] Base platform IDR
- [ ] Control per location IDR + volume breaks
- [ ] Conversation per channel IDR
- [ ] Audit / Foundation IDR
- [ ] Pilot discount rule
- [ ] VAT and invoice legal name (P2P Labs)

## 8. Contracts and billing ops

| Topic | MVP rule |
|---|---|
| How they pay | **Now:** invoice (IDR transfer). **Later:** Creem for card / credit packs (see §15). Not PayPal as primary. |
| Cycle | Monthly in advance, after the pilot. |
| Pilot | One invoice up front for 90 days. |
| Currency | IDR unless the SOW says otherwise. |
| Start date | First day an active location is live in Atlas **or** SOW start — whichever the SOW names. |
| Churn | 30-day notice. Location count is the last locked list before notice. |
| Downgrade | Client can archive locations; next invoice shrinks. |
| Failed payment | Soft-off: read-only after 14 days overdue. Do not delete their data. |
| Who invoices | P2P Labs ops. Not the app. |

No billing module in AtlasNow for this release. A spreadsheet + invoice is enough. Build `BillingAccount` in software only after the third paying brand.

## 9. Website and sales claims

atlasnow.co **must not** show:

- a price table, until §7 is locked;
- “increase revenue by X%”;
- “official WhatsApp partner” while on WAHA;
- customer logos we do not have written permission to use.

atlasnow.co **may** show:

- the brand tagline (*Optimize Every Outlet. Capture More Demand.*);
- what the product does, in plain language;
- Privacy / Terms / Data deletion;
- a “talk to P2P Labs” path (email), not a self-serve upgrade.

## 10. Cost we must cover (so the fee is not fantasy)

These are vendor costs, not client line items:

| Cost | Why it matters |
|---|---|
| Singapore VPS (app + Postgres + WAHA) | Always-on inbox. Serverless will drop WhatsApp sessions. |
| Domain + email | atlasnow.co, invoices, legal pages |
| Meta / Google apps | Free to register; staff time is not |
| WAHA / unofficial WA risk | Do not scale Conversation SKU past a handful of numbers without a Cloud API plan |
| P2P analyst time | Only billed if they bought Growth Ops |

Control pricing should stay profitable **without** assuming Growth Ops hours. If a brand is “Control only” and still eats 10 hours/week, that is a packaging miss — move them to Growth Ops or raise Control.

## 11. Success metrics (money)

| Metric | First useful target |
|---|---|
| Paying brands | 1 in 90 days after founder lock, 3 in 6 months |
| Billable active locations | ≥ 20 on the first retain |
| Pilot → retain | ≥ 50% of pilots |
| Gross margin on Control-only | Positive after VPS + one analyst-day/month |
| Conversation beta incidents | Track WAHA disconnects; if > weekly, stop selling new Conversation lines |

Do not put these numbers on the marketing site.

## 12. Open decisions (founder)

1. Confirm or replace the DRAFT IDR bands in §7.
2. Does P2P ever sell Control **without** Growth Ops, or is every first deal managed?
3. Minimum location count (Blueprint ICP says 20 — is a 8-outlet friend-and-family deal allowed?).
4. When Meta is Live: keep Conversation as add-on, or fold one Page into Control?
5. Legal entity and tax on the invoice.
6. Creem vs stay invoice-only for credit packs (§15).
7. Credit pack sizes and Atlas margin on Meta WhatsApp rates (§16).
8. Does Free ever get a tiny care-only Cloud number, or is Cloud always paid Brand?

Until (1) or (7) is checked, engineering does **not** wire Creem or debit credits in production. `/pricing` copy may stay “we’ll quote.”

**Execution (2026-08-29):** public `/pricing` = Free + quote, no card checkout. No Creem/Stripe in the app yet. Resume credits + gateway after founder locks §7 bands **or** credit pack IDR in §16, and at least one brand SOW or self-serve top-up is real.

## 13. Relationship to other docs

| Doc | Owns |
|---|---|
| **This PRD (master money)** | Packages, meters, credits, rails, what we refuse to sell or give away |
| [[AtlasNow-PRD]] | What the software may claim and ship |
| [[AtlasNow-Blueprint]] §15–16 | Why the ladder exists, ICP, audit offer |
| [[03 Areas/SEO-AEO-GEO]] | Crawlable claims — must not contradict this PRD |
| Website / landing / pitch | Story. Prices and “unlimited” only if this PRD allows |

### Before you develop anything

Bukan hanya tiket billing. **Setiap** fitur, halaman, copy, atau integrasi baru lewat gate ini dulu:

1. Does it cost us per use (Meta, Google, compute)? → wallet / PAYG here, or it is not billed.
2. Does it need Cloud / GBP? → not on Free (§3 / public pricing).
3. Does it take money from a customer? → rail A IDR or rail B Creem (§15.3), never a third silent gateway.
4. Would copy say “free / unlimited / included”? → check this PRD first.

If the answer is not in this file, **add it here** (founder lock) — don’t hide it in a random ticket. Product PRD may describe the feature; **this file decides whether we charge, meter, or give it away.**

## 15. Payment rails (2026-08-29)

Three different jobs. Do not force one vendor onto all three.

| Job | Who pays | Rail | Why |
|---|---|---|---|
| Brand retainer (Control / Growth Ops) | Indonesian HQ | **IDR transfer + invoice** | Cheapest. Brands already pay vendors this way. ~0% gateway. |
| Self-serve software / credit top-up (later) | Brand on a card, maybe not ID | **Creem** (candidate) | Merchant of Record, subscriptions + one-time products, usage-shaped top-ups, Next.js-friendly. Indonesia is on Creem’s merchant payout list. |
| “Everyone has PayPal” | — | **Not primary** | See fee math below. Holds and FX eat local deals. |

### 15.1 Creem — can we use it?

**Yes, as a later rail — not the only rail.**

Creem is a **Merchant of Record** (they are the legal seller, they collect/remit VAT/GST). Headline **3.9% + US$0.40** per successful transaction, no monthly fee. Product currency today is **USD and EUR**, not IDR. Payouts 1st and 15th, min US$50 / €50. Bank payout fee **US$7 / €7 or 1%**, whichever is higher. Funds can sit 7–12 days for risk. Extra: revenue splits +2%, affiliates +2%, abandoned-cart recovery +5%, USDC payout 2%. Chargebacks exist (plan on a flat dispute fee).

Fit for AtlasNow:

- Good: card checkout for **credit packs** and later self-serve Brand.
- Good: they claim usage-based billing — maps to PAYG credits.
- Bad as the **only** gateway: Indonesian F&B HQ wants **IDR invoice**, not a USD checkout.
- P2P Labs (Indonesia) can be a Creem merchant in principle — confirm KYC as **business** PT, payout account name must match.

Do not mix Sorak (or any other product) API keys onto Atlas Creem. Separate Creem store.

### 15.2 Is Creem cheaper than PayPal?

**Sometimes. Not always. Not vs local transfer.**

| | Creem | PayPal (typical merchant, international) | IDR bank transfer |
|---|---|---|---|
| Headline | 3.9% + $0.40 | ~3.5% + fixed domestic; **~4.4% + fixed + FX 3–4%** when cross-border | ~0% |
| Tax | Included (they are MoR) | You are the seller; VAT is your problem | Your invoice |
| Extra | Payout 7 USD/1%; splits/affiliates extra | Holds, disputes, account freezes | Admin time |
| Currency we charge | USD / EUR | Many, messy FX | **IDR** |
| $20 credit pack all-in (intl card) | ~**5.9%** ($1.18) | often **7–9%+** after FX | n/a |

Worked intuition:

- **Local brand, IDR 15 jt/month retainer** → transfer wins. Creem or PayPal would burn hundreds of ribu for no reason.
- **US$20–100 credit pack on a foreign card** → Creem is usually **cheaper than PayPal international**, and cheaper than Paddle/Lemon Squeezy (5–7%). vs **Stripe raw** (2.9%+$0.30) Creem looks more expensive **until** you add Stripe Tax + FX + you filing VAT — then Creem’s 3.9% is the all-in MoR number.
- **Do not tell sales “Creem is always cheaper than PayPal.”** Say: cheaper than PayPal **for international cards on digital checkout**; **not** cheaper than transfer.

**Founder lock:** Creem = candidate for credits + later self-serve. Invoice = default for retainers. PayPal = do not build unless a specific buyer requires it.

### 15.3 Scheme — Indonesia vs luar (locked direction)

Split by **who pays** (billing entity / NPWP / invoice address), **not** where the outlets are. A Bali chain owned by a Singapore holding = luar. A Jakarta PT with 3 KL stores = Indonesia.

One brand tenant = **one rail**. Do not mix IDR transfer and Creem on the same bill.

```text
Paying entity
  ├─ Indonesia  →  Rail A  IDR
  └─ not ID     →  Rail B  USD (Creem)
```

| | **Rail A — Indonesia** | **Rail B — luar** |
|---|---|---|
| Who | PT / CV / personal with ID bank | Foreign co. / foreign card |
| Currency they pay | **IDR** | **USD** (Creem; EUR if we add it) |
| Brand / Group monthly | Invoice P2P Labs + **bank transfer** | Creem **subscription** (later) |
| WhatsApp credit packs | Invoice now. Later: **Xendit/Midtrans** (VA, QRIS, e-wallet) if we want self-serve IDR | Creem **one-time** pack |
| Tax | PPN 11% on *our* invoice | Creem is MoR — they collect/remit |
| Gateway fee | ~0% | 3.9% + $0.40 (+ payout 7 USD or 1%) |
| PayPal | No | No |

**Wallet (credits) is always IDR inside AtlasNow.** Meta’s rate card is IDR. If they paid USD on Creem, we credit the wallet at a **locked FX on that top-up** (show the rate on the receipt). Burn is still Meta IDR + Atlas fee. Do not keep a second USD balance.

**Now (no app checkout):** both rails can be invoice — IDR transfer for A, USD wire/Wise for B — until Creem is live.

**Do not:** send an Indonesian HQ to Creem USD checkout “because we have it.” They eat FX twice.

**Later IDR self-serve:** Xendit or Midtrans, not Creem. Creem has no IDR product currency.

Open: exact Xendit vs Midtrans when we build IDR top-up. Not blocking.

## 16. WhatsApp credits (PAYG)

This is the blast / template money. It is **not** the Brand subscription.

Code already knows Meta’s per-message card (`src/lib/broadcast/rates.ts`, effective **1 July 2026**, IDR). Indonesia examples on that card:

| Kind | Meta IDR / message (ID dest.) | Atlas default add-on (DRAFT) |
|---|---|---|
| Session (customer wrote, 24h) | 0 (service window) | 0 — **do not sell this as credits** |
| Utility | 356.65 | + IDR 90 + marginPct |
| Authentication | 356.65 | + IDR 90 + marginPct |
| Marketing (blast) | 586.33 | + IDR 150 + marginPct |

PPN 11% is an **estimate on our invoice**, not a Meta line. `marginPct` default 0 until founder locks.

### 16.1 What a credit is

| Rule | Decision |
|---|---|
| Unit | **1 WhatsApp credit** = **1 billed Cloud template send** that Meta would charge (utility / marketing / auth). |
| Session reply | **0 credits.** If they wrote first and we answer inside the window, that is the product, not PAYG. |
| Destination | Burn is **by recipient market** on Meta’s card, not “1 credit = 1 message worldwide.” Display estimated IDR before send. |
| Failed send | Meta did not bill → **do not debit**. Debit only on accepted Cloud send. |
| STOP / opt-out | Still required. Credits never allow a CSV blast. Only HQ Cloud, only people who chatted or opted in. |
| Who holds the wallet | **Brand tenant** (one brand). Group desk spends the **active brand’s** wallet. |
| Free plan | **Cannot** connect Cloud, **cannot** buy or spend credits. |
| Brand / Group | Cloud connected → wallet + top-up. |

Do not invent a second “SMS credit” until we actually send SMS.

### 16.2 What the merchant sees

Settings → Broadcast (already has fee config):

- Balance in **IDR equivalent** and **est. marketing sends left** (because that’s what they care about).
- Before a blast: `N numbers × (Meta + Atlas + PPN est.) = total`. Block send if wallet < total.
- After: ledger line per campaign, not per mystery debit.

HQ inbox care replies: no wallet prompt.

### 16.3 Packs (DRAFT — founder lock)

Top-up is a **one-time product** (Creem later, invoice now).

| Pack (DRAFT) | Pay | Rough marketing sends (ID) |
|---|---|---|
| Starter | IDR 250 rb | ~300 |
| Desk | IDR 1 jt | ~1 200 |
| Chain | IDR 5 jt | ~6 000 |

Exact send count = `floor(pack / (metaMarketing + atlasMarketing) / 1.11)` once bands lock. **Do not print pack IDR on atlasnow.co until locked.**

Unused credits: no expiry in MVP (founder can add 12-month expiry later). No cash refund; remaining credits survive brand pause, die if tenant is deleted after the data-deletion process.

### 16.4 Cost stack we must cover

```text
Customer pays pack
  → (optional) Creem 3.9% + $0.40 if card
  → wallet credited in IDR
  → each billed send:
        Meta rate (by market + category)
      + Atlas flat (DEFAULT_ATLAS_FEES)
      + Atlas marginPct
      + PPN est. on our invoice if we must
```

If wallet is prepaid, we **buy Meta traffic from the WABA** as we send. Never let a brand run a blast that would overdraw — Cloud bill hits P2P’s / the WABA owner’s Meta invoice. **Hard block > overdraft.**

WABA ownership: brand’s number, brand’s Meta bill **or** P2P’s WABA with pass-through. Pick one per tenant in the SOW. Credits still work either way: if Meta bills the brand directly, Atlas fee is our only take and credits may be “Atlas fee only.” If P2P’s WABA, credits must cover **Meta + Atlas**.

## 17. Pay-as-you-go for any metered use

Same pattern as WhatsApp. Do not invent a new checkout per feature.

```text
Feature is PAYG
  → named meter
  → debit the brand wallet (or a dedicated bucket)
  → block when empty
  → top-up = same pack / invoice / Creem SKU
```

| Meter (now / next) | PAYG? | Notes |
|---|---|---|
| WhatsApp template blast | **Now (design)** | §16 |
| WhatsApp session / HQ reply | No | Product |
| Stamp / join / receipt photo | No on Free/Brand software | That’s the desk |
| Extra Cloud WABA | Later | Per-number, not per-message |
| OCR overage | Later | Only if Tesseract/VPS actually hurts |
| Google / Meta API quota | No | Their tokens |
| Ads spend | Never as Atlas PAYG | Brand pays Google/Meta |

**Product rule:** if we pay a vendor per use, the brand pre-pays credits. If we don’t pay per use, don’t fake a meter.

## 18. Non-goals of this document

- Paying Meta or Google **ads spend** on behalf of the client.
- Equity, fundraising, or P2P Labs P&L.
- Reseller / white-label price book (still later).
- Using PayPal as the default rail.

Credits, Creem, and usage meters **are** in scope of this PRD from 0.2.0 — product build stays parked until founder lock on pack prices.
