# UGC Factory + Character Affiliate — lock

2026-09-27: Factory pindah ke menu **UGC Generator** bersama Fashion Motion. Isi Factory belum dirombak. Catatan menu: [[02 Projects/AIOSCreator/design/2026-09-27 UGC Generator]].

#decision

Status: 🟢 lock · 2026-09-25

Goal: affiliator volume. Bukan “satu character jadi influencer.” Dua mesin, dua jenis akun.

## Dua permukaan (jangan dicampur)

| | **UGC Factory** `/create/ugc-factory` | **Character Affiliate** `workspace?tool=affiliate` |
|---|---|---|
| Siapa | Faceless + **talent buang** (bukan roster) | Talent bernama (Kim, Aoi, Lili) |
| Output | Image **dan** video, 9:16 | Image on-model **dan** video |
| Engine still | Qwen 2.1 default | Generate/Try-on yang sudah lock |
| Script | enzoxmotion, **satu angle/format per Write** | enzoxmotion, satu angle per Write |
| Simpan orang | **Tidak** ke `/create/characters` | Wajib Character row |

AI Creator (Generate / Clone / Try-on / Face swap / Edit still) **tetap di Character**. Factory tidak jadi studio rias.

## Factory — tiga mode output

1. **Faceless** — SKU, tangan, pack, UI. Tidak ada muka.
2. **Slideshow 8 slide · 9:16** — Photo Mode TikTok. Qwen 2.1 per slide. Bukan 16:9. Enzoxmotion formats 7–9 (discovery / list / story).
3. **Talent buang** — talking / hold / lifestyle untuk akun random niche (contoh “Daily Home Gadget”). Generate orang **sekali pakai**, file di `media/factory/{niche}/`, **bukan** Character library.

Chip Factory (ganti 5 chip on-model):

Faceless: Proof-first · Screen-record · Pack/hero · Before/after  
Slideshow: Discovery 8 · List 8 · Story 8  
Talent buang: Hold · Talking · Lifestyle (hanya mode ini)

Satu yang terpilih → satu script. Bukan 12 konsep.

## Character Affiliate

- enzoxmotion **di-wire di sini** (sudah: Write script).
- Alur: SKU → still lock (headshot/3/4/full/on-model) → Write → **Generate clip di bar**.
- Image + video boleh. Fokus affiliate, bukan photoshoot baru (itu Generate image).
- Angle on-model: review / unboxing / hold / talking / lifestyle.

## Kenapa slideshow di Factory, bukan Character

Photo Mode 2026: distribusi sering 5–6× video untuk stills+teks; gadget/home = faceless-primary (bukti visual di frame 1). Character affiliate = trust muka yang sama. Slideshow massal = Factory.

## Talent buang vs Character

- Character = cast tetap, FACE lock, Complete set, akun sosial terhubung.
- Talent buang = wajah baru per batch niche, tidak Update/Delete character, tidak Complete set.
- Jangan “Create character” diam-diam. Kalau suatu saat satu wajah menang, **promote** ke Character (aksi terpisah).

## I2V (Factory clip)

Picker, bukan hardcode Wan Prime:

| Engine | Pakai kalau |
|---|---|
| **Wan 3.0** (std; Prime fallback ke std) | faceless / product still, DashScope ada |
| **Seedance 2.5** | character+SKU refs, Higgsfield credited (2.0 tidak di catalog kita — 2.5 yang hidup) |
| **Grok Imagine Video** | talking/talent buang, key `imagine-video` |

Default: Wan 3.0. Slideshow 8 **bukan** I2V dulu — Photo Mode = 8 still Qwen 2.1. I2V opsional “Ken Burns” belakangan.

Clip prompt = gabungan `visual` per beat (bukan dump VO).

## Script — wajib HOOK, VO tidak ngulang hook

UI + JSON (bukan blob 4 field):

```
HOOK    0–2s   spoken + visual   (wajib, tidak boleh kosong)
BEAT    2–6s   spoken + visual   pain / old way
BEAT    6–11s  spoken + visual   mechanism / proof
CTA     11–15s spoken + visual + disclosure + URL
```

`voiceover` audio = spoken diurut, **hook sekali**. Contoh bag tote:

- 0–2 HOOK spoken: “I finally stopped carrying three different bags.”
- 2–6: “Work tote on weekdays, tiny purse on weekends — neither did both.”
- 6–11: “Structured base, hidden slips — phone, wallet, bottle, still slim.”
- 11–15 CTA: “Everyday uniform — link below. Affiliate.”

Yang sekarang jelek: hook = kalimat penuh, VO **mengulang kalimat itu** lalu lanjut. Display harus **timeline**, bukan Title/Hook/VO/CTA bertumpuk.

Write LLM harus isi `hook.spoken`, `hook.visual`, `beats[].spoken/visual`, `cta.*`. Kalau hook kosong → tolak.

## Write = script (satu objek)

Timeline itu **naskah**, bukan prompt engine.
- `spoken` → VoiceStudio
- `visual` → brief Qwen 2.1 (slide atau first frame) **dan** prompt I2V
Slideshow **punya script yang sama**. 8 slide = HOOK + beats dipecah ke 8 kartu (slide 1 = hook visual+teks, slide 8 = CTA). Bukan naskah terpisah.

## Satu run (Factory) — cabang setelah Write

```
SKU → satu format → Write (timeline)
                    ├─ Slideshow 8 → Qwen 2.1 × 8 still → [VO opsional] → download
                    └─ Clip        → Qwen 2.1 × 1 first frame → I2V (Wan/Seedance/Grok)
                                     → VO mux → download
```

**Script ≠ T2V.** Write wajib: itu naskah (HOOK + spoken + visual). Bukan “ketik paragraf → model video”.

**Tidak ada T2V kosong:** clip **selalu** dari still (foto SKU / Qwen first-frame / plate character). Wan, Seedance, Grok Video di Factory = I2V. Teks script mengarahkan gerak + VO, **bukan** mengganti gambar produk. Tanpa still, tas di listing bisa jadi tas lain di clip.

Character Affiliate: script sama; still boleh sudah ada di strip → I2V tanpa generate Qwen lagi.

Urutan clip: **image dulu, baru video, baru VO** (VO bisa sebelum mux, tetap after script). Slideshow berhenti di image.

Batch 12 / scaling 5–15 creator = fase 2 (BATCHING.md). Jangan di tombol yang sama.

## Bukti luar (arah, bukan SLA)

- TikTok Shop 2026: demo + Photo Mode slideshow dari foto listing yang sama. Video kalau *motion* adalah bukti; slideshow kalau urutan stills (warna, fit, 3 alasan).
- Photo Mode vs video (creator study): views ~6×, save ~8× — distribusi, bukan jaminan GMV.
- Gadget/home: faceless-primary, first frame = alat melakukan klaimnya. 83% winning shorts masih ada manusia di frame; 65% tanpa kata terucap → **tangan + produk** sering cukup, talking-head bukan wajib.

## Out of scope sekarang

- 16:9 YouTube long
- Auto-post 30 video/hari (Shop US cap 30 shoppable video / 60 photo)
- Masafy LoRA / numuk H3
- Simpan talent buang ke roster Character

## Links

- [[02 Projects/AIOSCreator/ugc-system/00 CreatorOS]]
- [[02 Projects/AIOSCreator/design/00 Direction]]
