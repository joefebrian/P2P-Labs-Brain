---
title: AtlasNow — WhatsApp HQ vs branch decision
aliases:
  - HQ Cloud API
  - Branch monitor only
  - Loyalty WhatsApp number
company: P2P Labs
product: AtlasNow
document_type: decision
version: 1.0.0
date: 2026-08-25
status: locked-in-chat
tags:
  - atlasnow
  - decision
  - whatsapp
  - cloud-api
  - loyalty
related:
  - "[[AtlasNow-Direction-PRD]]"
  - "[[AtlasNow-Ops-Alerts]]"
  - "[[AtlasNow-PRD]]"
  - "[[AtlasNow-Blueprint]]"
  - "[[AtlasNow-Loyalty-Decision]]"
---

# WhatsApp: HQ official vs branch monitor (locked 2026-08-25)

> [!success] Decision
> **One official HQ number per brand** on **WhatsApp Cloud API** (Meta). That number is for **blast + loyalty + HQ inbox**.
> **Branch numbers are not used to reply from Atlas.** For now they are **monitor-only**: ingest chats for analysis and reporting later.

## Two jobs, two kinds of number

| Number | Legal path | Atlas may send? | What it is for |
|---|---|---|---|
| **HQ / brand** (1 per merk) | **Official Cloud API** | **Yes** — templates, loyalty, blast, HQ replies | Member list, opt-in, promo, stamp / top-spender later |
| **Cabang** | WAHA (unofficial) for now | **No** | Watch conversations. Taxonomy, SLA, unanswered, reporting. Staff still reply on the **phone**, not Atlas |

Not 31 blast senders. Not “every cashier lives in Atlas”.

## Hard rules

1. Blast and loyalty **only** on the HQ Cloud API number.
2. Audience = people who **wrote to / opted in on that HQ number**. Branch chats **do not** become HQ blast list.
3. Atlas **must not** send on a branch WAHA session (hide composer / blast on those threads).
4. `STOP` / `UNSUB` on HQ drops them from blast immediately.
5. No CSV dump of branch phones into Cloud API.
6. Same number cannot be Cloud API **and** WAHA. HQ is official only.

## Loyalty sits on the HQ number

The official HQ WhatsApp **is** the loyalty channel:

- Inbound to HQ → **calon member**
- Keyword / form (`DAFTAR`, etc.) → `optInAt`
- Later: stamp card + monthly top spender **on this same contact** — see [[AtlasNow-Loyalty-Decision]]
- Blast = Cloud API **template** to opted-in HQ contacts (outside 24h) or session message inside 24h

Branch chat can still create a customer record for **analytics**, tagged with location, but that record is **not blastable** until they opt in on HQ.

## Branch monitor (honest)

“Monitor only” still needs a **live** unofficial session to receive messages (WAHA WEBJS = Chromium). VPS cap remains **6 live numbers** — see [[AtlasNow-Ops-Alerts]].

Wave A build order:

1. **HQ Cloud API** (send + receive + loyalty/blast) — this is the product.
2. **Branch observe** later / few stores only — ingest, no reply. Do not connect 31 cabang.

If a brand never connects cabang WAHA, HQ Cloud API still stands alone.

## Official spec (reference, not an SDK)

Meta OpenAPI for WhatsApp Business Messaging (generate-SDK / field lookup later — templates, media, errors). Do **not** npm-install this into AtlasNow.

- Repo: https://github.com/facebook/openapi
- Spec file: https://github.com/facebook/openapi/blob/main/business-messaging-api_v23.0.yaml
- Human docs: https://developers.facebook.com/documentation/business-messaging/whatsapp/overview
- Get started (WABA / phone number ID / system user token): https://developers.facebook.com/docs/whatsapp/cloud-api/get-started/

Atlas HQ webhook: `https://atlasnow.co/api/webhooks/whatsapp`

## What this is not

- Not IG/FB DMs (Meta App still unpublished).
- Not blasting from cabang numbers.
- Not using unofficial WAHA to send HQ promo (ban + policy).
- Not inventing visits/revenue from chat volume.
