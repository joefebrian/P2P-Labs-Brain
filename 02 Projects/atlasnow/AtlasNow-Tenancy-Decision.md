---
title: AtlasNow — Multi-agency tenancy decision
aliases:
  - Tenancy decision
  - Super Admin vs Agency vs standalone brand
company: P2P Labs
product: AtlasNow
document_type: decision
version: 1.0.0
date: 2026-08-24
status: locked-in-chat
tags:
  - atlasnow
  - decision
  - tenancy
related:
  - "[[AtlasNow-PRD]]"
  - "[[AtlasNow-Blueprint]]"
  - "[[AtlasNow-Monetization-PRD]]"
---

# Multi-agency tenancy (locked 2026-08-24)

Product spec in repo: `docs/superpowers/specs/2026-08-24-multi-agency-tenancy-design.md`

> [!success] Decision
> AtlasNow is a **platform of groups**, plus **standalone brands**. Super Admin (atlasnow.co) is not the same as a group admin.

> [!success] Locked 2026-08-27 (founder chat) — words, not schema
> **Buyer** = executive owner + operations lead of a **multi-outlet brand**. That is one `CLIENT` + many locations. They do **not** need a Group.
> **Group** (UI) = the parent that can own/run **many brands**. Same tenant type as today’s `AGENCY`. Owner-run holding and agency-run portfolio are the **same shape**. Optional layer.
> Do **not** call this **multitenant** in product copy. AtlasNow already *is* multi-tenant. Do not add a fourth tenant type. Keep `AGENCY` / `CLIENT` in code until a rename migration is worth it.

## Who is who

| Actor | Sees | Does |
|---|---|---|
| **Super Admin** (atlasnow.co, one login) | All groups + standalone brands | Switcher: **Platform** / **P2P** / **any group**. Can operate inside a group. Approves new group, standalone signup, upgrade-to-group. |
| **Group** (code: `AGENCY`) | Only brands with that group as parent | Add those brands, follow-up *their* brand logins. Cannot see other groups or other people’s standalone brands. Agency-run or owner-run — same screens. |
| **Brand** (code: `CLIENT`) | That one merk, **many outlets** | Not a group. Can **apply** to become a group. First merk stays the same brand. This is the economic buyer. |

## Hard no

- Super Admin does **not** attach a standalone brand to someone else’s agency.
- Agency 1 does **not** inspect Agency 2.
- Signup does **not** drop people into the dashboard. Login stays off until follow-up.
- Do **not** build billing in this phase.

## Upgrade

Standalone brand **applies** → Super Admin **approves** (today, a person). New agency workspace; existing brand becomes brand #1 under it. Later, when monetization ships, paid agency feature can **auto-approve**.

## Data (approach 1)

- Keep tenant types `AGENCY` and `CLIENT`.
- Brand: optional `agencyId`. Null = standalone.
- `p2p-labs` = **P2P agency** (Super Admin’s second hat).
- Existing VPS brands → parent **P2P**, not standalone.
- New self-serve after ship → standalone until they upgrade.

## Phases

1. **Now (build):** isolation, switcher, two signup doors, follow-up split, upgrade request, nav by workspace kind.
2. **Later:** per-agency change log (who changed what) + WhatsApp disconnect (and system events) in that log and/or notification.
3. **Later:** monetization — **per merk** + **WhatsApp number**, subscription **by feature**. Parked in [[AtlasNow-Monetization-PRD]] until tenancy is live.
4. **Later:** white-label mobile per agency / brand — same `tenantId` walls. A branded app must not list another agency’s merks. See [[AtlasNow-Direction-PRD]] §6.

## Why not other shapes

- Not “everyone is an account holder with a brand list” — agency vs one-merk menus would blur.
- Not a deep parent-child tree — too heavy for current queries.
- Not Super Admin = current `isAgencyStaff` (sees all clients). That is the bug this decision removes.
