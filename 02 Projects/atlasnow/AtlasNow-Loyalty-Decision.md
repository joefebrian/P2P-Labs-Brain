---
title: AtlasNow — Loyalty modes decision
aliases:
  - Stamp card
  - Top spender monthly
company: P2P Labs
product: AtlasNow
document_type: decision
version: 1.1.0
date: 2026-08-28
status: locked-in-chat
tags:
  - atlasnow
  - decision
  - loyalty
  - stamp
  - top-spender
related:
  - "[[AtlasNow-WhatsApp-Decision]]"
  - "[[AtlasNow-Direction-PRD]]"
  - "[[AtlasNow-Tenancy-Decision]]"
  - "[[AtlasNow-PRD]]"
  - "[[AtlasNow-Loyalty-QR-Stamp-Logic]]"
---

# Loyalty: stamp + monthly top spender (locked 2026-08-25)

> [!success] Decision
> Each **brand** runs loyalty on its **HQ Cloud API WhatsApp** (same member record). Two modes, both optional, both configurable. An **agency** may set this for brands it parents. Super Admin does not impose another agency’s program.

Brand **picks which programs to turn on**: stamp only, top spender only, or both. They are not the same engine.

## Mode 1 — Stamp card

| Setting | Rule |
|---|---|
| Stamp rewards | **Beberapa baris.** Contoh: 5 stamp → es kopi, 10 stamp → tumbler. Tiap baris = stamp count + teks hadiah. Goal kartu = stamp **tertinggi**. |
| Min belanja per stamp | Brand-set. **1 struk yang lolos min = 1 stamp** (bukan per item). Min `0` = setiap struk valid dapat 1. |
| Klaim (opsi A, 2026-08-25) | Tiap hadiah bisa ditukar **sekali** setelah stamp cukup. Hadiah 5 **tidak** mengosongkan kartu. Kartu baru kosong **hanya setelah hadiah tertinggi** ditukar. Kalau 5 dan 10 sudah tercapai, kasir tukar yang kecil dulu. |
| Kartu penuh | Count ≥ stamp tertinggi. Tidak nambah stamp sampai hadiah tertinggi ditukar. HQ WA kabari hadiah yang sudah bisa diklaim. Pelanggan tunjuk HP; **kasir Redeem per hadiah di Atlas**. |
| Hangus | **Bukan default 30 hari.** Brand pilih: **lifetime** (progress tidak kedaluwarsa) **atau** 1 / 2 tahun sejak **stamp pertama** di kartu itu. |
| Refund | **Tidak ada alur batal.** Struk keluar = transaksi valid. Tidak tarik stamp. |
| Who punches | Intake sources below. |

Not points. Progress on HQ member (`phone` + `tenantId`).

## Mode 2 — Top spender (monthly) — separate program

| Setting | Rule |
|---|---|
| On/off | Brand activates independently from stamp. |
| Scope | Brand pilih: **satu cabang** **atau** **seluruh merek** (terpusat). |
| Period | **Per bulan** (timezone merek). |
| Aturan | Brand isi: **nominal min** dan **hadiah per juara** (juara 1 / 2 / 3, tiap baris hadiah sendiri). Ranking only uses events **with amount**. Juara 1 **hanya** dapat hadiah juara 1, bukan kumulatif. |
| Pemenang | HQ kirim info ke pemenang. Pelanggan bisa `Status Spender` / `RANKING` ke nomor HQ. |
| Redeem | Kasir/admin **Redeem** hadiah juara itu. Setelah Redeem = **sudah diklaim**, tidak klaim ganda. Bulan berikutnya hitung baru. |
| Refund | Sama: struk valid, tidak void. |

## Who configures

| Actor | Can set loyalty for |
|---|---|
| Brand (standalone or under agency) | Itself |
| Agency | Only brands with that agency as parent |
| Super Admin | Does not overwrite another agency’s program. May view in platform hat. |

## Data honesty (same as PRD)

- No invented visits, spend, or revenue.
- A stamp without a recorded event is not a stamp.
- Top spender without amounts is empty — UI says **no spend data**, not Rp 0 as a ranking fact.
- Branch WhatsApp **monitor** threads do not add stamps by themselves.

## WhatsApp (HQ official only)

- Punch / spend recorded in Atlas → optional notify on **HQ Cloud API**.
- “You got a stamp / card complete / monthly winner” = template. Promo wording = **Marketing**. Dry receipt of a purchase they just made may be **Utility**.
- Blast list remains HQ opt-in. Completing a card does not license blasting a branch-only phone.

## Amendment 2026-08-28 — foto struk, auto kalau cocok

Founder chat. Spec: AtlasNow repo `docs/superpowers/specs/2026-08-28-receipt-photo-auto-approve-design.md`. **Not built.**

Amends the pipes below: OCR is no longer “always human.” Form pipe **requires a photo**. Auto-Approve **only** when the photo matches.

| Topic | Lock |
|---|---|
| Nomor di kasir | **Satu kolom:** No. transaksi / No. Struk / No. Invoice (nama mesin beda, nomor yang sama). Shipped. |
| Foto | Wajib kirim. Tanpa foto tidak masuk. |
| Auto default | Ya, jika **match**: HP ada di buku member merek ini, `trx_id` unik = nomor di foto, Rp = Rp di foto, tembus min. HP cetak di kertas = bonus, bukan syarat. |
| Tidak kebaca / beda | Bukan auto. Kasir boleh ketik dari kertas; foto tetap nempel; **antrian HQ**. |
| Mode audit | Setting merek “Kantor cek semua” — match tetap antri manusia. Preventive. |
| Pintu kasir | Utama — biar till gampang. |
| Pintu tamu | Boleh unggah (kartu stamp dan/atau foto ke WA HQ) dengan **syarat match yang sama**. Lebih lemah terhadap foto lama; unique trx + audit = rem. Default off sampai pintu kasir live. |
| POS API | Gelombang belakangan. Webhook/API bertanda tangan: HP + trx + Rp + outlet → auto tanpa foto. Jangan janji Moka/Majoo sebelum token asli. |

Stamp tetap event yang tercatat. Super Admin tidak cap merek orang. JOIN poster tetap daftar.

## Intake sources (settings, per brand)

Kasir bertanya: punya nomor member / mau daftar? Nomor HP itu ID member HQ. Setting merek memilih **satu atau lebih** pipa:

| Pipa | Di setting | Approve manusia? |
|---|---|---|
| **Form Atlas + foto** | Selalu ada. Foto wajib. Satu kolom nomor + Rp wajib | **Tidak** jika OCR **MATCH**. **Ya** jika buram, mismatch, atau mode audit |
| **POS sync** (Moka, Majoo, …) | Connector per merek, outlet POS → lokasi Atlas. Partnership / API resmi, bukan scrape | **Tidak wajib** jika webhook bertanda tangan + `trx_id` unik + ada HP. Boleh tetap antri jika merek mau review |
| **OCR struk** | Bagian dari form (bukan pipa terpisah). Baca nomor + Rp dari foto | Auto hanya pada MATCH. Thermal/blur = UNREADABLE → antrian HQ, bukan tebak stamp |
| **Tamu unggah** (PWA / WA HQ) | Toggle merek, default off sampai form+foto kasir live | Sama: MATCH auto, else HQ |
| **WA cabang terdaftar** | Nomor WA outlet **wajib terdaftar + confirmed** di menu Atlas lokasi itu. Hanya nomor itu yang boleh kirim intake ke HQ. Nomor lain diabaikan | Ya (staf cabang, bukan tamu) |

POS belum live sampai partnership/API token merek itu ada. UI setting: Moka / Majoo / Lainnya = **Coming, connect when ready** — jangan janji sync palsu.

**POS happy path:** kasir isi/pilih pelanggan di Moka/Majoo → transaksi tutup → Atlas terima ticket (HP, total, trx id, outlet) → stamp/spend → HQ WA ke pelanggan. Member baru = calon member HQ (tetap opt-in WA terpisah untuk blast).

**OCR (amended 2026-08-28):** baca nomor + Rp dari foto. **Sumber kebenaran = kertas.** Auto hanya jika kertas = yang diketik (atau yang terbaca di pintu tamu) **dan** `trx_id` unik + member ada. Bukan tebak stamp dari foto buram.

## Cabang → validasi → pelanggan (locked)

Business flow (yes):

1. Kasir cabang input **nomor HP** (= ID member), **satu nomor struk** (transaksi / struk / invoice — nama mesin), **nominal**, **foto kertas**.
2. Atlas **validasi**: format HP, member ada, `trx_id` unik, foto ada, OCR match nomor+Rp, tembus min. **MATCH + audit off** → Approve sistem (stamp hidup). Selain itu **admin web merek** Approve / Tolak. Super Admin platform tidak cap. Stamp dan WA ke pelanggan **hanya setelah Approve** (sistem atau manusia).
3. Stamp dan/atau amount tercatat di member HQ (bukan di nomor cabang).
4. Nomor **HQ Cloud API** mengirim ke **nomor pelanggan** (bukan membalas ke HP kasir).

Pipa:

| Pipa | Kapan |
|---|---|
| **Atlas form** (disarankan) | Kasir login cabang. Tidak campur inbox pelanggan. |
| WA cabang → nomor HQ | Hanya jika nomor pengirim = **WA terdaftar + confirmed** di outlet Atlas itu. Format kaku, contoh `STAMP 0812xxxx TRX 12345` + foto invoice. Pengirim tidak terdaftar → **abaikan** (bukan antrian stamp). |

Bukan: pelanggan di-blast dari nomor toko. Bukan: invoice tanpa `trx_id` (dobel stamp). Bukan: kirim ke HP yang belum opt-in HQ kecuali template **utility** sah untuk transaksi itu. Bukan: Super Admin atlasnow.co yang cap stamp merek orang.

**Antrian validasi (web merek)**

| Langkah | Siapa |
|---|---|
| Submit HP + trx + invoice | Kasir / staff cabang (form Atlas atau WA whitelist) |
| Approve / Tolak | Admin merek (atau admin agency untuk merek itu) di web Atlas |
| Setelah Approve | Stamp/spend tercatat + nomor HQ kirim ke pelanggan |
| Tolak | Tidak ada stamp; alasan boleh dikirim ke cabang, bukan spam ke pelanggan |

Auto-format (08→62, duplikat trx) menolak **sebelum** antrian. **MATCH** = kertas setuju dengan angka kasir; itu yang boleh auto. Manusia tetap putuskan yang buram, beda, atau merek yang nyalain audit.

## Self-serve on HQ chat (locked)

Customer messages the **HQ** number. Atlas replies as a **loyalty agent** (scripted from the database). Not a free LLM inventing counts.

| Inbound (examples) | Reply |
|---|---|
| `Status Stamp`, `CEK STAMP`, `STAMP` | Stamps / N, min belanja, hadiah, status kartu (jalan / penuh / **sudah di-redeem**). If no card: `DAFTAR`. |
| `TUKAR` | Kartu penuh + belum redeem → “tunjukkan ke kasir”. Sudah redeem → “hadiah sudah dipakai”. |
| `Status Spender` / `RANKING` | If program on: standing bulan ini / “kamu pemenang, belum/sudah redeem”. No amount data → jujur “belum ada data belanja”. |

Customer chat **opens the 24h service window**.

### HQ auto-reply copy (locked 2026-08-27)

Brand staff (or the parent agency for that brand) edit the **words** HQ sends. Counts still come from the database — never invent stamps.

**Where:** AtlasNow → **Settings → Loyalty** (pick the brand) → **WhatsApp HQ auto-reply**.

**Keywords live today:**

| Customer types | Reply |
|---|---|
| `Stamp` / `Info Stamp` | **Menu / poin program** (editable box “When they type Stamp”). Lists what they can ask. |
| `Status Stamp` / `Cek Stamp` / `kartu stamp` | Live card (off / expired / progress / claim / complete). |

| Box in settings | When it sends | Placeholders (keep these so numbers stay true) |
|---|---|---|
| Stamp program off | Stamp card toggle is off | none |
| Card expired | Hangus 1 / 2 year | none |
| Card in progress | Has stamps, next gift not reached | `{count}` `{goal}` `{min}` `{next_stamps}` `{next_reward}` `{kasir}` |
| Gift ready to redeem | A tier is claimable | `{count}` `{goal}` `{gifts}` `{hint}` `{kasir}` |
| Card complete | Goal reached, no next tier | `{count}` `{goal}` `{min}` `{kasir}` |

Empty box = Atlas default (Indonesian, merchant-plain). Tutorial: change copy here, Save, then chat `Status Stamp` on the HQ Cloud number. Super Admin does not overwrite another agency’s wording.

`TUKAR` and `Status Spender` replies: same settings page later — not live yet.

Customer chat **opens the 24h service window**.

### v1: how the member shows the stamp card (locked 2026-08-26)

No member-app QR yet. Two ways, both live when HQ Cloud is connected (desk lookup works without it):

1. **Customer chats HQ** `Status Stamp` / `Cek Stamp` / `kartu stamp`. Atlas replies with count/goal/next gift from the database. That inbound opens the 24h service window, so the reply is **not a marketing template** (low / usually no conversation charge vs blast).
2. **Kasir ketik HP** on Loyalty → Cek member, then Redeem.

**Stamp card image (locked 2026-08-27, logo-only 2026-08-27):** upload is **one brand mark**, not a finished poster. Atlas composites the logo (`contain`, never crop) on a 1080×1350 ink canvas and writes live `{count} / {goal}` at the bottom. Rec: **square PNG 1080×1080** (min 512×512), max ~1.5 MB, JPG/PNG/WebP. Example: P2P Labs uses AtlasNow `public/brand/mark.png` (1064×1064). `Status Stamp` sends that JPEG + caption inside the 24h service window (`type: image`). No upload → default Atlas card. Menu keyword `Stamp` stays text.

**Settings UI (locked 2026-08-27):** **Settings → Loyalty**. Brand picker **top right**. Then four tabs (not one long page): **Membership QR** | **Birthday gift** | **Stamp card** | **Top spender**. Stamp tab is two columns (rules left, logo + preview right) + auto-reply grid.

**Join page (locked 2026-08-27):** public `/join/{key}` is one Atlas template (judul/field belum CMS). Customize = **brand name + brand logo**. Email **wajib**. Logo: square 512×512 (min 256), max 1.5 MB upload; Atlas compresses to WebP 512. Upload at **Brands → New / brand detail**, **Settings → Brand mark**, or **signup** (kind=brand). Payment-after-signup profile later. Not Settings → Branding (that is AtlasNow chrome).

**Customers book (locked 2026-08-27):** Potential (HQ/branch chat, no QR) ≠ Prospect (filled QR) ≠ Member (first qualifying approved receipt). Same phone merges. Table headers English. Click row for name / phone / email / birthday.

Member QR (kasir scans the phone) stays later — [[AtlasNow-Loyalty-QR-Stamp-Logic]]. JOIN poster is still daftar-only.

Router: loyalty keywords first → then AI/FAQ if enabled → else human inbox.

## Reports ranking (locked 2026-08-27)

**Reports → loyalty month** shows two customer boards, both from **approved receipts this month** (not visits, not lifetime card unless labeled):

| Board | Ranked by | When it shows |
|---|---|---|
| Stamp ranking | Stamp count this month (top 20) | Stamp card on |
| Top spender | Qualifying spend this month (top 20; gift column only on prize ranks) | Top spender on |

Same member can appear on both. Phone is masked (`•••` last 4).

## Redeem is the source of truth

Staff **Redeem** in Atlas (brand/cabang). That flag is what stops reuse. Chat `TUKAR` only tells the customer what to do — it does **not** mark used by itself.

## WA send after Approve (clarified)

Approve menyimpan stamp/hadiah di database **dulu**. Lalu Atlas minta Meta kirim WA. Kadang Meta/nomor gagal (salah format, nomor tidak WA, gangguan). **Stamp tetap sah.** Antrian “gagal kirim” + retry. Bukan rollback stamp.

## Cloud API number = nomor bisnis WABA

Bukan WA pribadi, bukan QR WAHA/WA Web. Satu nomor **WhatsApp Business Platform** (Cloud API) per merek = HQ. Nomor itu biasanya **tidak** dipakai di app WA biasa bersamaan. Tidak boleh nomor yang sama Cloud API + WAHA.

## Fraud (locked)

| Guard | Rule |
|---|---|
| `trx_id` unik per merek | Submit ganda / foto struk yang sama dengan trx sama → tolak |
| 1 struk lolos min = 1 stamp | Tidak numuk stamp dari satu invoice |
| Redeem sekali | Status `redeemed` tidak bisa Redeem lagi |
| Form + foto MATCH | Auto (kecuali mode audit) |
| Form + foto buram/beda | Antrian HQ |
| Tamu unggah | Sama dengan form; toggle merek |
| WA cabang staf | Antrian HQ (whitelist nomor outlet) |
| POS | Hanya webhook/API bertanda tangan; tanpa HP → skip |
| HP staf | Tolak jika nomor pelanggan = nomor akun staf cabang itu |
| WA cabang | Hanya nomor **terdaftar + confirmed** di menu outlet Atlas yang boleh kirim ke HQ. Satu outlet, nomor yang di-confirm. Bukan HP kasir liar |
| Blast | HP dari kasir/POS tidak otomatis opt-in promo |
| Super Admin | Tidak cap stamp merek orang |

## Not in this lock

- Points wallet, paid membership tiers, multi-brand shared stamps.
- Live Moka/Majoo tokens before a signed partnership (settings stub only).
- OCR auto **without** a match on nomor+Rp (blur guess). Match-gated auto is in the 2026-08-28 amendment.
- AI inventing stamp counts or rewards.
- **QR stamp collection** — locked as **membership first, then member QR (kasir scan)**. Join QR stays daftar-only. See [[AtlasNow-Loyalty-QR-Stamp-Logic]]. Not shipped.
