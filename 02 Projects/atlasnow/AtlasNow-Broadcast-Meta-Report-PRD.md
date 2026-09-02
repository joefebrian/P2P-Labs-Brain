---
title: AtlasNow — Broadcast report (Meta statuses)
aliases:
  - Blast report
  - WA delivered read
company: P2P Labs
product: AtlasNow
document_type: prd
version: 0.1.0
date: 2026-09-01
status: draft-for-founder-review
tags:
  - atlasnow
  - broadcast
  - whatsapp
  - meta
related:
  - "[[AtlasNow-WhatsApp-Decision]]"
  - "[[AtlasNow-Monetization-PRD]]"
  - "[[AtlasNow-PRD]]"
---

# AtlasNow — Broadcast report (Meta only)

> **Hanya angka yang Meta kirim lewat Cloud API.** Bukan visit toko, bukan omzet, bukan “klik link Google.”
>
> Spec: AtlasNow repo `docs/superpowers/specs/2026-09-01-broadcast-meta-status-report-design.md`. Joe: **gas** 2026-09-02 — built (History tab).

## Kenapa

Halaman Broadcast sekarang cuma kirim. “Terkirim N / gagal F” lalu hilang. Webhook `delivered` / `read` **diabaikan**. Joe minta report **dikirim / dibaca / action** di halaman itu, dari data Meta dulu.

## Tempat

Tab baru di **Broadcast**: **History / Riwayat**. Bukan menu Reports (itu stamp + outlet).

## Yang Meta kasih

| Kolom | Artinya | Jujur |
|---|---|---|
| Terkirim (`sent`) | Sudah keluar dari server Meta | Tick 1 |
| Sampai HP (`delivered`) | Masuk HP | Tick 2 abu. Kalau langsung dibaca, Meta kadang **tidak** kirim `delivered` — kita hitung delivered = delivered **atau** read |
| Dibaca (`read`) | Chat dibuka | Tick 2 biru. **Hanya** jika pelanggan nyala read receipt. Bukan 100% orang |
| Gagal (`failed`) | Meta tolak / tidak sampai | Kode error Meta (bukan karangan) |
| **Action** | Orang **nulis balik** ke HQ **atau** tap tombol quick-reply template | Satu-satunya “action” yang Meta kirim. Bukan klik URL, bukan datang ke toko |

**Bukan Meta (tidak di wave 1):**

- Klik tombol **URL** / “buka maps” pada template
- Datang ke cabang, stamp, belanja
- Persen “open rate” seperti email

## H-2 ultah

Kiriman `birthday_greeting` otomatis ikut History (sumber **Birthday H-2**). Tetap status Meta yang sama.

## Uang

Chip kategori Meta (`marketing` / `utility` / `service` / …) boleh tampil sebagai **label Meta**. Bukan tagihan AtlasNow. [[AtlasNow-Monetization-PRD]] tetap master. Jangan debit kredit dari webhook ini.

## Sukses

Kirim template ke 10 nomor → History: 10 attempted, lalu terisi sent / sampai / baca / gagal dari webhook. Tiga orang balas HQ atau tap tombol → **Action = 3**. Tidak ada klaim “3 orang masuk gerai.”
