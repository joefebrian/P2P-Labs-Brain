---
title: AtlasNow — Support help desk (Radit)
aliases:
  - Radit
  - Help desk
company: P2P Labs
product: AtlasNow
document_type: prd
version: 0.1.0
date: 2026-09-01
status: draft-for-founder-review
tags:
  - atlasnow
  - support
  - help-desk
related:
  - "[[AtlasNow-PRD]]"
  - "[[AtlasNow-Monetization-PRD]]"
  - "[[AtlasNow-Direction-PRD]]"
---

# AtlasNow — Support help desk (Radit)

> **P2P bantu orang yang pakai AtlasNow, atau yang akan pakai.** Bukan bot tamu merek. Bukan inbox WhatsApp HQ. Bukan AI.
>
> Spec teknis: AtlasNow repo `docs/superpowers/specs/2026-09-01-support-radit-helpdesk-design.md`. Joe: **gas** 2026-09-01 — built. Screenshot attach belum.

## Locked (Joe 2026-09-01)

| | |
|---|---|
| Agen | Manusia. Nama tampilan **Radit**. |
| Siapa nanya | Prospek di situs atlasnow.co **dan** client yang sudah login (halaman mana pun, termasuk error). |
| Antrian | Satu percakapan. Selesaikan dulu, baru yang berikutnya. |
| 10 menit | Milik **client**. Radit sudah balas, client diam 10 menit → close. |
| Close | Sarankan email **hello@atlasnow.co**. |
| Seen | Pesan client **Not seen yet** sampai Radit buka convo. Lalu **Seen**. |
| Menu | Super Admin → **Help desk**. Simpan percakapan. Bukan menu Inbox merek. |
| Jam | **09:00–17:00 Asia/Jakarta.** Di luar jam, kotak **mati** — tidak ngetik, tidak antre. **Diisi form email support** (form `/contact` yang sama, ke hello@). Jam bisa diubah di Super Admin. |

## Bukan ini

- Auto-reply di nomor WA merek (janji publik “bukan chatbot tamu” tetap).
- Campur chat support dengan chat pelanggan Vilo / cabang.
- Fin-style AI (health check, republish).
- Produk berbayar / kredit. Ini kerjaan P2P, bukan paket.
- Widget di website **toko** client.

Form `/contact` tetap ada. Di luar jam, **kotak chat itu yang jadi form itu** — bukan antrian Radit, bukan mailbox kedua.

## Jam buka

Default **09:00–17:00** setiap hari, jam **Jakarta** (bukan jam HP pengunjung). Super Admin bisa ganti jam, hari, atau matikan chat sama sekali.

Di luar jam: kotak masih kelihatan, chat mati, **form support** di dalam kotak (nama, email, pesan → hello@atlasnow.co). Tidak masuk antrian Help desk.

Pukul 17:00: tidak ada antrian baru. Yang sudah nunggu tetap di list untuk 09:00. Percakapan yang **sedang** dibalas Radit boleh diselesaikan dulu. Lembur = geser jam Close di setting, bukan tombol rahasia.

## Alur (pendek)

1. Joe nulis di kotak (situs atau dalam desk).
2. Masuk antrian. Tulisan Joe: **Not seen yet** sampai Radit buka.
3. Kalau Radit masih bantu orang lain: Joe lihat nomor antrian.
4. Radit buka → **Seen** → ketik.
5. Joe diam 10 menit setelah balasan Radit → close + “email hello@atlasnow.co”.
6. Joe nulis lagi setelah close → percakapan **baru**, antre lagi.

Timer 10 menit **tidak** jalan kalau Radit belum pernah balas.

## Uang

Tidak dijual. Tidak debit kredit WhatsApp. [[AtlasNow-Monetization-PRD]] tidak berubah.
