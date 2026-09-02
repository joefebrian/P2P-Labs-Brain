---
title: AtlasNow — Ops alerts (VPS)
aliases:
  - WAHA 6 session cap
  - VPS 8GB WhatsApp limit
company: P2P Labs
product: AtlasNow
document_type: alert
version: 1.0.0
date: 2026-08-25
status: active
tags:
  - atlasnow
  - ops
  - alert
  - waha
  - vps
related:
  - "[[AtlasNow-Direction-PRD]]"
  - "[[AtlasNow-PRD]]"
---

# AtlasNow — Ops alerts

> [!danger] WhatsApp live cap — VPS 8 GB (locked 2026-08-24)
> **Maks 6 nomor hidup** di VPS ini (`WAHA_MAX_LIVE_SESSIONS=6`).
> Cabang ke-7 **ditolak** sampai ada nomor yang di-Disconnect.
>
> Setiap nomor Connected = **satu Chromium** yang tetap hidup supaya inbox jalan.
> 31 cabang Connected = OOM lagi (login Network error / 502).
>
> **Operasi:** konek cabang ramai dulu, **satu-satu**, maks 6. Jangan reconnect semua QR sekaligus.
>
> **Nanti (bukan sekarang):** naik mesin, pindah **GOWS** (tanpa browser), atau **WhatsApp Cloud API**.

## Why this exists

Incident 2026-08-24: 31 WAHA WEBJS sessions → ~236 Chrome processes → RAM ~50 MB free → load >200 → `POST /api/auth/login` timeout/502. UI showed **Network error** because the body was not JSON.

Software guards now:

- Connect is **explicit** (no auto QR, no auto-start on location save).
- Unscanned QR is **stopped after 2 minutes** or Cancel.
- Hard cap **6** live `STARTING | SCAN_QR_CODE | WORKING | FAILED` sessions.
- WAHA container `mem_limit: 2g`, does **not** auto-restart all sessions on boot.

## Hostinger VPS (current)

| Item | Value |
|---|---|
| Host | `srv1756392` · `76.13.198.28` · atlasnow.co |
| Size | 2 vCPU · 8 GB RAM · 96 GB disk |
| Public ports | 22 (SSH), 80/443 (Cloudflare ranges only) |
| Stack | Caddy → Atlas (Next) → Postgres 16 + WAHA |
| Do not | Mix Sorak keys onto Atlas; delete Sorak files; commit `.env` |

## Headroom (rule of thumb)

| Live WA numbers | Expected extra RAM | Notes |
|---:|---|---|
| 0 | WAHA idle ~0.5 GB | Xvfb + node, no Chrome |
| 1–6 | ~0.2 GB Chrome each | Cap. Stay here. |
| 7+ | Rejected in product | Or host dies. |
| 31 | OOM | Already happened. |

## Host hardening (2026-08-25)

Done on `srv1756392` — Sorak files **not** deleted.

| Control | Setting |
|---|---|
| Swap | 2 GB file (OOM safety; login survived last time only after killing Chrome) |
| swappiness | 10 |
| SSH | key only (`PasswordAuthentication no`, `PermitRootLogin prohibit-password`) |
| fail2ban | sshd jail, 4 tries / 10 min → 1 h ban |
| UFW | 22 rate-limited; 80/443 Cloudflare ranges only |
| php-fpm 8.2 | **stopped** (Sorak leftover process; `/var/www/sorakmedia*` kept) |
| Docker caps | Atlas 1.5 GB · Postgres 768 MB · Caddy 128 MB · WAHA 2 GB / 400 PIDs |
| Postgres | `shared_buffers=256MB`, `max_connections=50` |
| Caddy | HSTS, nosniff, frame deny, 10 MB body cap |
| App | Login 8/15 min per IP · signup 5/hour per IP · no `X-Powered-By` |
