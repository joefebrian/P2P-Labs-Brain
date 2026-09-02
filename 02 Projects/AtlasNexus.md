# AtlasNexus

#project

## Outcome
Platform creator economy: brand ↔ creator campaigns (YouTube-first), discovery, contracts, monitoring post-campaign.

## Status
🟡 Active (product live / demo) · **session focus: switched from AtlasNow**

## Paths
```
Repo (local): /Users/joefebrian/Downloads/Working Desk/artifacts/atlasnexus
HTML demo:    /Users/joefebrian/Downloads/Working Desk/artifacts/atlas-nexus-demo
Live app:     https://atlasnexus.app
```

```bash
cd "/Users/joefebrian/Downloads/Working Desk/artifacts/atlasnexus"
# docker compose up --build   # postgres + stack
# cd web && npm run dev       # Next app (check port vs AtlasNow :3000)
```

## URLs
- App: `https://atlasnexus.app` (orgs, campaigns, modules)
- Related internal tool: [[02 Projects/affiliate-video-tool|affiliate-video-tool]]
- Sibling product (parked): [[02 Projects/atlasnow|atlasnow]]

## Product map (dari sidebar app)

### Core modules
| Module | Fungsi singkat |
|--------|----------------|
| YouTube Brand | Brand / demo YouTube surface |
| Creator Discovery | Cari & shortlist creator |
| Create Campaign | Buat campaign |
| Drafts | Campaign draft |
| Running | Campaign live |
| Monitoring & Post-Campaign | Tracking + wrap-up |
| Creator Applications | Aplikasi creator |
| Browse Campaigns | Browse (creator side) |
| My Applications | Aplikasi saya |

### Entities
- Organizations
- Channels
- Contracts

### Access control
- Users
- Invitations

### Settings
- Account
- Creator Suites Management
- Pages
- YouTube API

## How it relates

```
AtlasNexus (SaaS product)
    ↑ productizes
affiliate-video-tool (internal ops / R&D)
    ↓ feeds ideas into
P2P Labs (company / vision)
```

- **affiliate-video-tool** = lab internal (scan brand/product, storage, multi-AI)  
- **AtlasNexus** = produk user-facing (campaign lifecycle)  
- Fitur “YouTube Brand Scan / product detect” di tool internal bisa jadi **capability** AtlasNexus ke depan

## Next actions
- [ ] Tulis 1-pager positioning AtlasNexus vs competitor
- [ ] Map fitur tool internal → roadmap module AtlasNexus (mana yang di-productize dulu)
- [ ] Catat stack/deploy AtlasNexus (repo path, env) di note ini saat ready
- [ ] Link Organizations / campaign model ke keputusan produk

## Decisions log
### 2026-09-02
- Public: AtlasNexus is a **flagship product card** on https://p2plabs.asia/#products (with AtlasNow). Company site, not the app.

### 2026-08-11
- Context switch from AtlasNow → AtlasNexus (park GBP write work until “balik atlasnow”)
- Local repo found under `artifacts/atlasnexus` (Next `web/` + Python `worker/` + docker postgres)

### 2026-08-04
- Vault second brain: AtlasNexus ditambahkan sebagai project utama (sebelumnya cuma di browser, belum di brain).

## Links
- [[02 Projects/Projects MOC|Projects MOC]]
- [[02 Projects/P2P Labs|P2P Labs]]
- [[02 Projects/affiliate-video-tool|affiliate-video-tool]]
- [[03 Areas/YouTube & Content|YouTube & Content]]
- [[03 Areas/Affiliate & Monetization|Affiliate]]
- [[Home]]
