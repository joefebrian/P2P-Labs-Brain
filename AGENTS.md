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
5. Code di `affiliate-video-tool` yang mengubah product behavior → log 2–5 bullet di project note.

## Never do

- Simpan secret: API key, password, token, cookie raw.
- Rewrite seluruh vault tanpa diminta.
- Buat ratusan note kecil tanpa MOC (map of content).

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

## Code ↔ Brain bridge

Repo / product penting:

- **atlasnow** → [[02 Projects/atlasnow]] · repo `/Users/joefebrian/Downloads/Working Desk/Atlas Technology/atlasnow`
  - **Money master:** [[AtlasNow-Monetization-PRD]]
  - Docs: `02 Projects/atlasnow/AtlasNow-PRD.md`, `AtlasNow-Blueprint.md`, `Blueprint-Tech-Tasks.md`
  - WAHA = temp prototype; target Meta WhatsApp Cloud API
- AtlasNexus (SaaS) → [[02 Projects/AtlasNexus]]
- `/Users/joefebrian/affiliate-video-tool` → [[02 Projects/affiliate-video-tool]]
- P2P Labs (company) → [[02 Projects/P2P Labs]]
  - Site: https://p2plabs.asia · VPS `116.206.196.6` · **not** AtlasNow
  - Brand: [[p2plabs/P2P-Labs-Brand]] · UI: [[p2plabs/P2P-Labs-Design-System]]
  - Do not mix P2P **Network** cyan/pink palette into Labs corporate

Vault path (selalu sama antar session):
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
