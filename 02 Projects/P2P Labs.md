# P2P Labs

#project

## Outcome
Creator Economy SaaS Operating System — music, video, image, affiliate, API integrations.

## Status
🟡 Active (strategy + product)

## Context
- Role Grok di config: CEO / founder co-pilot
- Fokus: music_video_image_affiliate + API integration
- Swarm agents di `~/.grok/config.toml` (trend, YT, TikTok, Meta, affiliate, dll.)
- **Flagship products:** [[02 Projects/atlasnow|AtlasNow]] (`atlasnow.co`) + [[02 Projects/AtlasNexus|AtlasNexus]] (`atlasnexus.app`) + [[02 Projects/WaveLead|WaveLead]] (WhatsApp Channel discovery / follow intent · [repo](https://github.com/joefebrian/wavelead))
- **Internal lab:** [[02 Projects/affiliate-video-tool|affiliate-video-tool]]
- **Public site:** https://p2plabs.asia on its **own** VPS (not AtlasNow)
- **Brand (locked 2026-09-02):** [[p2plabs/P2P-Labs-Brand|P2P-Labs-Brand]] · [[p2plabs/P2P-Labs-Design-System|design system]] · PDF in `02 Projects/p2plabs/`

## Ops — p2plabs.asia VPS (2026-09-01)

| | |
|---|---|
| IP | `116.206.196.6` |
| SSH | `ssh p2plabs` · user `p2p-labs` · key `~/.ssh/p2p-labs.pem` |
| Size | 1 vCPU · 1 GB RAM · 60 GB · Ubuntu 26.04 · Asia/Jakarta |
| Stack | nginx static only + 2 GB swap + UFW + fail2ban + Let’s Encrypt |
| Do not | Docker, Node, Postgres, AtlasNow, Sorak, mix `.env` from `76.13.198.28` |

HTTPS live 2026-09-02: https://p2plabs.asia (Let’s Encrypt, renews via certbot.timer). DNS A `@` = `116.206.196.6`.

### 2026-09-02 (People to Prosperity + light site)
- Changed: Public meaning locked to **People to Prosperity** (memakmurkan orang). Second P may also be Performance / Partner / People to People. No P2P Network on the site (later a service). Horizontal logo from Shared Drive. Holding page rebuilt light (white/neutral, purple CTA). Live on https://p2plabs.asia.
- Why: Joe: not People·Partners·2 as the lead; highlight Prosperity; no dark backgrounds; logo file given.
- Next: Tweak copy if the four P-reads need different weight.

### 2026-09-02 (flagship product cards)
- Changed: p2plabs.asia now has dedicated Flagship cards for **AtlasNow** and **AtlasNexus**. Services/Labs/Jakarta sit under “Around the products”. JSON-LD Organization + two SoftwareApplication. Live.
- Why: Joe: keduanya produk andalan P2P Labs, minta card khusus.
- Next: Copy tweak if Joe wants different product weight. AtlasNow coding still paused.

### 2026-09-02 (editorial rebuild)
- Changed: p2plabs.asia rebuilt to Awesomic layout language (36px cards, hairline borders, 64px display, sticky nav, 80px rhythm) with **P2P Labs colour only** — navy `#0B0F2B`, purple CTA `#652DFF`, lime accent `#A6FF1A`, canvas `#F3F4F8`. No zinc, no orange, no P2P Network palette.
- Why: Joe: previous cards looked amateur; pasted Awesomic style ref and asked colours swapped to Labs guidelines.
- Next: Visual tweak if Joe wants product screenshots instead of geometry in the flagship cards.

### 2026-09-02 (Awesomic-faithful rebuild)
- Changed: Holding page rebuilt to match Awesomic homepage composition (white canvas, 3-line display + gray word, pill capture, stats row, overflowing photo cards). Colour still Labs: navy / purple CTA / lime chip. Prosperity stays locked (not rotated). Product stills from live atlasnow.co / atlasnexus.app.
- Why: Joe: previous pass was jauh banget from the style ref.
- Next: Wait for Joe's eye. Don't invent stats or client logos.

Password login is **off**. Provider panel password was pasted in chat — rotate it there; it is not stored on disk.

## Next actions
- [ ] Align AtlasNexus roadmap dengan capability dari affiliate-video-tool
- [ ] Definisikan 1 wedge GTM (mis. brand campaign + product detect)
- [ ] Satu source of truth: keputusan produk dicatat di AtlasNexus note

## Decisions log
### 2026-08-04
- Second brain vault di Obsidian `mygrok` dihubungkan ke Grok.
- AtlasNexus masuk vault sebagai project utama (sebelumnya hanya di browser).

## Links
- [[p2plabs/P2P-Labs-Brand]]
- [[p2plabs/P2P-Labs-Design-System]]
- [[02 Projects/atlasnow|AtlasNow]]
- [[02 Projects/AtlasNexus|AtlasNexus]]
- [[02 Projects/affiliate-video-tool|affiliate-video-tool]]
- [[03 Areas/Affiliate & Monetization|Affiliate]]
- [[Home]]

