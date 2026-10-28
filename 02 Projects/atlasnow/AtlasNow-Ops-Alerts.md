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

## Recovery runbook (2026-10-28)

Host `srv1756392`, public IP `76.13.198.28`. SSH alias `atlasnow`. If the operator network cannot reach port 22, the authorized relay is `ssh -o ProxyCommand='ssh p2plabs nc %h %p' atlasnow`. Do not open extra forwarding. Do not reboot or restore a dump to clear a health check.

No Biznet console credential is stored here. The guest agent on this VM is Hostinger's (`.hstgr-` telemetry). Provider power logs are not on the VM.

| Scenario | Detection | Diagnose | Safe action | Needs approval | After |
|---|---|---|---|---|---|
| VPS unavailable | External HTTPS fails from two networks | Provider console power state. Do not infer power from one client timeout. | If the console shows Running, inspect from the console. If it shows Stopped, start it there. | Power on, reboot, rebuild | SSH, `uptime`, `docker ps`, HTTPS 200 |
| SSH down, site up | Port 22 timeout while 443 answers | `fail2ban-client status sshd`, UFW. Compare from `116.206.196.6`. | Unban one address only if the jail lists it. | Firewall reset | Key login from the operator network |
| Caddy down | TCP 443 accepts and returns no TLS, or HTTP not 308 | `docker logs --tail 50 atlasnow-caddy-1` | `docker start atlasnow-caddy-1` if the container is exited | Caddyfile or DNS edit | Certificate dates, `https://atlasnow.co/` 200 |
| Atlas unhealthy | Caddy up, `/` not 200, container not healthy | `docker logs --tail 80 atlasnow-atlas-1` | Recreate only `atlas` from the current image, `--no-build --no-deps` | New image build | Health, login page, webhook 401 unsigned |
| Postgres down | Atlas logs database errors | `docker ps`, disk `df -h` | `docker start atlasnow-postgres-1` if exited | Restore a dump | App health, migration table readable |
| WAHA down | QR or inbox for WAHA locations fails | `docker logs --tail 50 atlasnow-waha-1`, memory | Start the existing container. Do not raise the 6-session cap. | Image change | Container up, memory under 2 GB |
| Meta webhook failures | App error log, Meta delivery errors | Signed empty POST stays 200 and does not add messages. Subscriptions stay on `/api/webhooks/whatsapp`. | Fix the app only after a failed signed fixture. | Callback change | GET challenge matches, unsigned POST is 401 |
| Coexistence disconnect | `account_update` / `PARTNER_REMOVED` | Connector `needs_attention`, phone row still on the same workspace | Leave the number in place. Automation stays paused. | Re-onboarding | Owner repeats Embedded Signup. Do not call Deregister. |

Rollback image: `atlasnow-atlas:rollback-pre-coexistence-b31` (`sha256:89aacc333206c10e9ea709fde7fd85951d68fb76fb18d41ef831bf2bad872ed7`). Latest dump before B3.1: `/root/atlasnow-backups/atlasnow-20261028-pre-coexistence-b31.dump`. Restoring it drops data written after 09:19 UTC on 2026-10-28. Docker is enabled and the four containers use `unless-stopped`. There is no external uptime monitor. Add one only after the operator names the alert destination.
