# UGC Generator

#decision

Status: 🟢 slice shipped · 2026-09-27

Menu baru di sidebar. UGC Factory **belum** dirombak. Fashion Motion adalah isi pertama.

## Problem

Factory dan fashion video campur di satu menu. Joe mau satu rumah **UGC Generator**. Factory mulai diganti 28 Sep 2026 mengikuti PRD UGC Factory v1.0 dan Script Bible v0.1. Layar utamanya My Productions. Katalog 33 resep. Enam market tidak otomatis jadi enam video. Yapping belum dipakai sebagai retrieval. Render provider dari board baru masih ditahan.

## User flow

1. Sidebar **UGC Generator** → **Fashion Motion** (`/create/ugc-generator/fashion`). Layar default adalah **My Videos**, bukan wizard lima langkah.
2. Kartu horizontal: checkbox, produk, preview, status, satu tindakan. Klik bagian kartu membuka drawer. Board tetap pegang search, filter, selection, dan scroll.
3. Batch Create, Apply Preset, Generate Looks, Review Looks (Approve & Next), Assign Motion, Generate Videos, Review Videos, Download Approved.
4. Motion butuh still yang sudah di-approve dan video referensi. Tidak ada fallback Wan I2V.
5. Antrean batch tersimpan di `data/db/ugc-fashion.json`. Menutup browser tidak menghapus rencana. Dispatch ke Qwen/Kling untuk batch massal masih ditahan.
6. File sungguhan, kalau ada, tetap di `data/media/UGC_Fashion/`, bukan Character dan bukan Motion library.

## Keputusan

- Menu: **UGC Factory** + **Fashion Motion** di bawah UGC Generator.
- Satu project = satu look, maksimal 4 item, satu orang dewasa.
- Prompt disusun aplikasi dari produk + karakter + style. Joe tidak wajib nulis prompt.
- Vendor tidak jadi nama menu.

## Out of scope

- Rombak total UGC Factory.
- Ledger biaya, upload video, player trim, dan dispatch provider untuk antrean 40/60. Checklist review dan export daftar approved sudah ada. Export belum berupa zip file video.
- Posting / checkout marketplace.

## Cara cek

- [ ] Sidebar ada grup UGC Generator, dua item.
- [ ] My Videos kosong punya Create Look.
- [ ] Tambah 1–4 SKU, Generate Look, still muncul di kartu.
- [ ] Approve, Generate Video, file tidak muncul di MotionControl.

## Yang jadi

- Menu + dashboard My Videos + workspace look/still/motion.
- Media `UGC_Fashion` / `AIOSCreator-UGC_Fashion-…`.
- PRD penuh (registry, biaya, review checklist) belum.

## Links

- [[02 Projects/AIOSCreator/design/00 Direction]]
- [[02 Projects/AIOSCreator/design/2026-09-25 UGC Factory lock]]
- [[02 Projects/AIOSCreator]]
