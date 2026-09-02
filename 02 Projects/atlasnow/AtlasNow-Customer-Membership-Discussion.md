---
title: AtlasNow — Customers + membership invite (open discussion)
company: P2P Labs
product: AtlasNow
document_type: discussion
date: 2026-08-25
status: locked-in-chat
tags:
  - atlasnow
  - discussion
  - customers
  - membership
  - qr
  - birthday
related:
  - "[[AtlasNow-Loyalty-Decision]]"
  - "[[AtlasNow-WhatsApp-Decision]]"
  - "[[AtlasNow-Direction-PRD]]"
---

# Customers → member (diskusi, belum dikunci)

Bukan keputusan. Jangan implement sebelum Joe lock. Recall file ini tiap sesi berikutnya.

## Yang sudah ada (fakta, bukan opini)

- Menu **Customers** = `WaContact` yang punya nomor, dari chat WhatsApp cabang/HQ. Buku HP. Bukan master member.
- Loyalty stamp/spender pakai **HP + merek** terpisah (bukan join ke Customers).
- Chat cabang **bukan** daftar blast. Blast / promo HQ hanya setelah opt-in di nomor HQ. Lihat [[AtlasNow-WhatsApp-Decision]].
- A/B/C (member = stamp saja / stamp+blast / wajib chat HQ dulu) **belum dijawab**. Joe minta diskusi dulu.

## Usul yang sedang dibahas (2026-08-25)

Kasir tanya mau daftar → **bukan cuma ketik HP**. Atlas **provide QR** ke form pengisian data pelanggan.

Field v1 (sementara itu dulu):

| Field | Wajib? |
|---|---|
| No. telp | Ya (ID member) |
| Nama | Ya kalau sempat / form QR |
| Tanggal lahir | Ya untuk program ultah |
| Email | **Ya** (locked 2026-08-27 — join form) |
| Provinsi + kota/kabupaten | **Ya** if phone is +62 / 08 (Indonesia). Dropdowns from Atlas wilayah list. |

Tanggal lahir → reward loyalty ulang tahun. H-2 bisa broadcast (diskon/voucher). Broadcast H-2 **nanti** lewat HQ Cloud API; data DOB boleh disimpan sekarang.

Struk belanja hari itu tetap boleh masuk antrian stamp pakai HP yang sama.

## Arah yang disarankan (belum lock)

- QR = isi **profil** (HP, nama, DOB, email). Stamp **tetap kasir** (HP + no. trx + invoice) — QR tidak mengganti antrian Approve.
- Satu orang = satu HP per merek. Submit ulang = update profil, bukan member dobel.
- URL Atlas, public, no login. Contoh arah: `https://atlasnow.co/join/{brand}?outlet={cabang}` + QR PNG unduh per cabang.
- Ultah = program terpisah dari stamp/top spender. Klaim sekali setahun di kasir. H-2 kirim hanya setelah HQ Cloud hidup + template + izin WA (centang di form, bukan diam-diam dari chat cabang).

## Terkunci di chat

| Item | Isi | Kapan |
|---|---|---|
| QR placement | **No. 3** — kasir **dan** meja/pintu/standing. Pelanggan bebas isi dari mana (scan di bayar, di meja, atau foto QR dikerjain belakangan). | 2026-08-25 |
| Aktivasi member | Isi form **bukan** member aktif. Aktif **hanya jika pernah ada transaksi** yang lolos antrian Approve. Tanpa itu: tidak redeem, tidak H-2 ultah, tidak dianggap member jalan. | 2026-08-25 |
| Urutan | **Daftar dulu, baru struk.** Tidak ada “struk dulu, QR belakangan”. Struk loyalty **wajib** nomor member yang sudah ada (calon). HP yang belum isi form = membership tidak valid, struk ditolak. | 2026-08-25 |
| Ultah kunjungan pertama | **A** — setelah struk pertama Approve, boleh redeem ultah di kunjungan yang sama. **B ditolak**: struk sudah nyimpen no. member; kalau member belum valid, struk itu tidak sah. | 2026-08-25 |
| Min belanja | **Setting per merek** (bukan angka Atlas). Default **0** = kopi kecil pun mengaktifkan. Brand boleh isi nominal sendiri. Struk di bawah min = **bukan transaksi valid**: member tetap calon, tidak stamp, tidak redeem. | 2026-08-25 |
| QR scope | **Setting merek:** `Satu merek` (terpusat) **atau** `Per cabang`. HQ bisa challenge antar outlet / lihat pertumbuhan per outlet. | 2026-08-25 |
| Challenge / hitungan | Leaderboard HQ = **member aktif baru** (struk pertama yang tembus min), di cabang **kasir Approve**. Isi QR calon tidak dihitung “menang”. Kalau QR per cabang, first-touch signup tetap dicatat terpisah. | 2026-08-25 |
| Izin WA H-2 ultah | Centang di form daftar. **Tidak wajib** untuk jadi member. Tanpa centang: aktif + stamp + redeem kasir tetap jalan, **tidak** dikirimi H-2. Bukan izin blast promo umum (itu belakangan / nomor HQ). | 2026-08-25 |

OTP / “kasir centang HP cocok” **tidak** jadi gerbang utama — bukti = form dulu + struk Approve yang tembus min merek.

## Menu Customers (locked 2026-08-27)

One people book. Same phone = one row. Stamp still gates **membership**.

| Status (EN / ID) | How they got here | Membership |
|---|---|---|
| **Potential / Potensi** | Chat HQ or a branch. Never filled join QR. | Not a member. Cannot stamp. |
| **Prospect / Calon** | Filled join QR (name, phone, email, DOB). | Calon until first qualifying **approved** receipt. |
| **Member** | First qualifying approved receipt (brand min). | Aktif. Stamp card + birthday gift can apply. |

If they filled QR **and** chatted: still one row. Source = Join QR. Detail lists HQ/branch threads.

**Secret inbound (locked 2026-08-27):** pairing / verification copy (“Don’t share it”, kode WhatsApp, pairing code) is **not** a customer. Skip ingest (do not store the body). Already-saved code-only chats stay out of the people book. Never log or display the code. Real chat or a join QR still counts.

Table headers stay **English** in both locales (Phone, Name, Status, Source…). Row click opens profile (phone, name, email, birthday). Export ≠ blast list.

## Belum dikunci

- Min belanja aktivasi = field yang sama dengan min stamp yang sudah ada, atau angka terpisah.
- Copy persis checkbox: **“Boleh kirim ucapan ulang tahun via WhatsApp”** (2026-08-25, lock).
- Blast promo umum (bukan ultah) — A/B/C lama. belum.
