# SEO · AEO · GEO

#area #sop #seo #aeo #geo

**Main area.** Setiap **sistem / halaman publik baru** (AtlasNow, AtlasNexus, atau situs P2P Labs lain) wajib lewat SOP ini **sebelum** dianggap selesai.

Bukan afterthought. Bukan “nanti kita taruh meta.” Kalau orang atau mesin tidak bisa **baca HTML-nya**, fitur itu tidak ada untuk search / answer engines / generative engines.

Related: [[03 Areas/Product Engineering|Product Engineering]] · [[02 Projects/atlasnow|atlasnow]] · [[AtlasNow-Monetization-PRD]] (harga / Free / “unlimited”) · [[Home]]

---

## Apa bedanya

| | Pertanyaan | Syarat |
|---|---|---|
| **SEO** | Google index halaman ini? | `title`, `description`, canonical, sitemap, robots, copy di HTML |
| **AEO** | Mesin jawaban (AI overview, voice, FAQ) bisa **kutip**? | Pertanyaan + jawaban lengkap di HTML/SSR + `FAQPage` JSON-LD |
| **GEO** | Model generatif (ChatGPT, Gemini, Grok) bisa **sebut produk dengan benar**? | Nama entitas konsisten di HTML, Organization/SoftwareApplication JSON-LD, klaim jujur |

Cookie locale (`en`/`id`) **bukan** URL terpisah. Jangan pasang `hreflang` palsu ke `/id/...` yang tidak ada. Googlebot biasanya dapat **EN**. Tulis entitas penting dalam **nama Inggris yang sama** di kedua bahasa (Google Business Profile, WhatsApp CRM, Google Maps).

---

## Entitas AtlasNow yang harus muncul di HTML (bukan hanya animasi)

1. **Google Business Profile**
2. **Google Maps**
3. **WhatsApp CRM**
4. **Outlet operations**
5. **Revenue attribution** — dari **struk kasir yang disetujui**, bukan tap Maps, bukan scan QR sebagai penjualan. Jangan karang visits / leads / omzet.

Tagline **jangan diubah**: Optimize Every Outlet. / Capture More Demand. / One desk for every location.

---

## SOP — halaman publik baru (wajib)

Checklist. Kalau satu item gagal, halaman belum ship.

### 1. Copy crawlable (SSR)

- [ ] Kalimat yang harus di-index ada di **Server Component** atau HTML awal, bukan hanya client carousel / canvas / motion.
- [ ] Animasi boleh. **Teks untuk crawler** tetap di DOM (section biasa, atau `sr-only` / `hidden` CSS yang tetap di HTML).
- [ ] Jangan `return null` untuk jawaban FAQ yang tertutup — pakai `hidden`, jangan unmount.
- [ ] Nama lima entitas di atas tertulis **persis** kalau halaman itu tentang produk.

### 2. Meta

- [ ] `title` (absolute atau template, **jangan** “About — AtlasNow — AtlasNow”)
- [ ] `description` ≤ ~160 char, entitas + janji jujur
- [ ] `alternates.canonical` = `https://atlasnow.co{path}`
- [ ] Open Graph: `url`, `title`, `description`, `siteName`, `images`
- [ ] Twitter: `summary_large_image`
- [ ] `robots`: index+follow untuk publik; **noindex** untuk login, app, join/card member

Pakai helper repo: `src/lib/seo/site.ts` → `publicMetadata({ path, title, description, index? })`.

### 3. robots.txt + sitemap.xml

- [ ] Path **indexable** ada di `INDEXABLE_PATHS` (`src/lib/seo/site.ts`)
- [ ] Path **app / API / kartu member** ada di `ROBOTS_DISALLOW`
- [ ] `sitemap.ts` **hanya** `INDEXABLE_PATHS`
- [ ] Jangan sitemap-kan `/login`, `/control-tower`, `/api/*`, `/join/*`

### 4. JSON-LD (kalau relevan)

- [ ] Home: Organization + SoftwareApplication + WebSite
- [ ] FAQ: `FAQPage` dari Q/A yang **sama** dengan HTML
- [ ] Jangan JSON-LD yang tidak ada di halaman (jangan klaim “visits dashboard”)

### 5. Klaim jujur

- [ ] Tidak menjual fitur yang belum live sebagai live
- [ ] Revenue attribution = receipt Approve, bukan Maps
- [ ] WhatsApp blast ≠ CSV
- [ ] Harga / “gratis API” / “unlimited” / paket Free vs Brand sesuai [[AtlasNow-Monetization-PRD]] — jangan invent angka di copy publik

### 6. Locale / HTML

- [ ] `<html lang>` mengikuti cookie locale
- [ ] Tidak mengarang URL `/id` terpisah

---

## SOP — sistem baru (bukan cuma halaman)

Saat **develop sistem baru** (modul, integrasi, produk samping), pikirkan area ini **di awal**, bareng PRD:

1. **Apa yang Google / AI boleh kutip tentang sistem ini?** Tulis 3–5 kalimat SSR.
2. **Nama entitas** — satu string, dipakai di UI, meta, JSON-LD, pitch.
3. **Halaman indexable?** Kalau ya → masuk `INDEXABLE_PATHS` + sitemap + canonical. Kalau tidak → noindex + robots disallow.
4. **Jawaban AEO** — 1 FAQ jika orang akan tanya “apa itu X di AtlasNow?”
5. **GEO** — jangan sinonim liar (“merk” vs “brand” vs “outlet”) di copy publik Inggris.
6. **Obsidian** — log keputusan di project note + link ke area ini.

Sistem yang **hanya** client-side (WebGL, slideshow, till preview) **wajib** punya sibling HTML.

---

## AtlasNow — indexable vs tidak

**Index:** `/` `/about` `/contact` `/faq` `/pricing` `/privacy` `/cookies` `/terms` `/data-deletion` `/signup`

**Noindex + disallow:** app desk, `/api/`, `/join/` `/card/` `/c/` `/i/`, pitch/training, signup pending. `/login` noindex (boleh crawl).

Code: `src/lib/seo/site.ts`, `src/app/robots.ts`, `src/app/sitemap.ts`.

---

## Saat coding selesai

Append di [[02 Projects/atlasnow]]:

```markdown
### YYYY-MM-DD (SEO/AEO/GEO)
- Changed: …
- Why: …
- Next: …
```

← [[03 Areas/Areas MOC]] · [[Home]]
