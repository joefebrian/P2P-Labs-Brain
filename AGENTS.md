# AGENTS — Grok Second Brain Rules

Path vault: `/Users/joefebrian/Downloads/Working Desk/Obsidian/mygrok`

Kamu (Grok) adalah **external brain** untuk Joe / P2P Labs. Vault Obsidian ini adalah **long-term memory** yang owned 100% oleh user.

## Folder map (PARA-ish)

| Folder | Isi |
|--------|-----|
| `00 Inbox/` | Dump mentah, belum di-sort |
| `01 Daily/` | Journal harian `YYYY-MM-DD.md` |
| `02 Projects/` | Kerja dengan deadline/outcome |
| `03 Areas/` | Domain ongoing (YouTube, AI, affiliate) |
| `04 Resources/` | Referensi, clip, how-to |
| `05 Archive/` | Selesai / dingin |
| `90 Templates/` | Template note |
| `99 System/` | Aturan, meta, setup |

## Always do

1. Setelah **keputusan penting** (arsitektur, pricing, pivot, fix besar) → tulis/update note di `02 Projects/` atau `03 Areas/`.
1b. **Sistem / halaman publik baru** → lewat SOP [[03 Areas/SEO-AEO-GEO]] dulu (copy SSR, meta, canonical, OG, robots/sitemap, JSON-LD, klaim jujur). Bukan afterthought.
1c. **AtlasNow + uang / paket / kredit / gateway / “gratis API” / meter** → [[AtlasNow-Monetization-PRD]] adalah **master**. Baca sebelum develop. Konflik dengan PRD produk → Monetization yang menang sampai founder ubah di situ.
2. Pakai **[[wikilinks]]** antar note.
3. Daily: update `01 Daily/YYYY-MM-DD.md` (focus, done, next).
4. Ide mentah → `00 Inbox/Inbox.md` dulu, jangan langsung nest dalam.
5. Code di `plugins` (`affiliate-video-tool`) yang mengubah product behavior → log 2–5 bullet di project note.
6. **Session Grok = folder product.** `cd` ke path di tabel di bawah, baru `grok`. Jangan start dari `$HOME` (`/Users/joefebrian`). `/new` hanya session baru di folder yang sama.
7. **Project baru** selalu di `/Users/joefebrian/Downloads/Working Desk/` dulu (subfolder company kalau sudah ada: `P2P Labs`, `Atlas Technology`). Baru git, baru `grok`.

## Never do

- Simpan secret: API key, password, token, cookie raw.
- Rewrite seluruh vault tanpa diminta.
- Buat ratusan note kecil tanpa MOC (map of content).
- Kerjakan product A dari folder product B (AtlasNow ≠ p2plabs.asia ≠ AIOS ≠ Nexus).

## Tone di note

- Bahasa: campur ID/EN OK, jelas, actionable.
- Prefer bullet + checklist.
- Tag opsional: `#project` `#area` `#decision` `#idea`

## When user says…

| User | Action |
|------|--------|
| “Capture …” | Append ke Inbox |
| “Daily” / “Log hari ini” | Update/create Daily note |
| “Keputusan: …” | Note `#decision` di Project/Area + link Home |
| “Recall X” | Search vault, jawab + link note |
| “Weekly review” | Process Inbox → sort ke PARA |

## Code ↔ Brain bridge — session map

1 product = 1 folder = `cd` ke situ dulu, baru `grok`.

```bash
cd "<path>" && grok
```

| Product | Path | GitHub | Note |
|---------|------|--------|------|
| **p2plabs.asia** (corporate site) | `/Users/joefebrian/Downloads/Working Desk/P2P Labs/p2plabs.asia` | private [joefebrian/p2plabs.asia](https://github.com/joefebrian/p2plabs.asia) | Static nginx. VPS `116.206.196.6` 1 GB — **not** AtlasNow. Brand [[p2plabs/P2P-Labs-Brand]]. No P2P Network palette. |
| **atlasnow.co** | `/Users/joefebrian/Downloads/Working Desk/Atlas Technology/atlasnow` | private [joefebrian/atlasnow](https://github.com/joefebrian/atlasnow) | Flagship. Money master [[AtlasNow-Monetization-PRD]]. WAHA = temp; target Meta Cloud API. |
| **AIOSCreator** | `/Users/joefebrian/Downloads/Working Desk/AIOSCreator` | private [joefebrian/AIOSCreator](https://github.com/joefebrian/AIOSCreator) | Local-first creator OS. Drive folder = assets only, bukan git. GPU box, bukan VPS 1 GB. |
| **AtlasNexus app** (`atlasnexus.app`) | `/Users/joefebrian/Downloads/Working Desk/Atlas Technology/atlasnexus` | — | Next.js + worker. Ini produknya. [[02 Projects/AtlasNexus]] |
| **AtlasNexus HTML mock** (YouTube Brand Campaign) | `/Users/joefebrian/Downloads/Working Desk/Atlas Technology/atlasnexus-demo` | — | Static HTML demo. Folder `AtlasNexus Modul YouTube Brand Campaign` = PDF/screenshot, **bukan** kode. |
| **plugins** (affiliate lab) | `/Users/joefebrian/Downloads/Working Desk/plugins` | [joefebrian/plugins](https://github.com/joefebrian/plugins) | GitHub name = folder. [[02 Projects/affiliate-video-tool]] |
| **animaji.studio** | `/Users/joefebrian/Downloads/Working Desk/animaji.studio` | private [joefebrian/animaji.studio](https://github.com/joefebrian/animaji.studio) | PT Animaji Studio Internasional. Bukan P2P Labs. Docs PT di folder `PT Animaji Studio International`. |
| **WaveLead** | clone dulu | [joefebrian/wavelead](https://github.com/joefebrian/wavelead) | WA Channels. [[02 Projects/WaveLead]] |
| **vault** (notes only) | `/Users/joefebrian/Downloads/Working Desk/Obsidian/mygrok` | private [joefebrian/P2P-Labs-Brain](https://github.com/joefebrian/P2P-Labs-Brain) | Bukan product. |

Parked (jangan campur ke session aktif): `sorakmedia`, CoverMusik_ID, ytx-metrics.

P2P Labs (company) → [[02 Projects/P2P Labs]] · flagship AtlasNow + AtlasNexus + WaveLead + AIOSCreator.

Vault path (selalu sama):
`/Users/joefebrian/Downloads/Working Desk/Obsidian/mygrok`

Saat session coding selesai (jika diminta atau perubahan besar):

```markdown
### YYYY-MM-DD
- Changed: …
- Why: …
- Next: …
```

## Home

Dashboard: [[Home]]
