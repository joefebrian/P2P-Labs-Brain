# Locked this arc (Studio + Character workspace)

#decision

Status: 🟢 lock · 2026-09-25

Cuplikan keputusan yang sudah hidup di code. Jangan diutak-atik tanpa brainstorm lagi.

## Character

- Generate image: FACE lock = headshot. BODY = front atau 3/4 dari framing prompt.
- Clone Image = Muse Image 1.0. Prompt operator = pose + latar.
- Face swap = ReActor. Workspace = wajah. Image 2 = pose character lain. Hasil masuk library character yang terbuka.
- Edit still = freestyle. **Tidak ada** accordion Framing / Camera body / Art / Architecture / Landscape / Weather. Image 2/3/4 = extra (orang, tempat, objek). Prompt = mereka ngapain.
- Complete set = headshot + 3/4 + full. Slot kosong harus keisi — Lili 3/4 sudah di-gen 2026-09-25.
- Adult chips: Nude · studio, Lingerie, Boudoir, Sheer slip, After shower, Bath towel, Open robe, Tiny bikini, Body oil, In bed. Bukan Theme/Title.
- Camera workspace: **Framing** (crop/angle) vs **Camera body** (iPhone, Leica, Sony…).

## Studio

- UserRound: 1 plate **atau** 2 plates → 1 image (headshot | full body sheet).
- Plus (Compose): SKU library **atau** upload image → product + compose ter-wire.
- Prompt order: Camera → Place → Light → Style. Present nampilin Camera dari node.
- I2V first frame = character atau compose still, **bukan** pack SKU.
- Seedance 2.5: character + upload = reference-to-video `@Image1` `@Image2`.
- Wan: first_frame only (tidak mix reference_image). Prime fallback ke std kalau key `wan3_base`.
- Grok Imagine Video: key `XAI_VIDEO_API_KEY` / account `imagine-video`, terpisah dari stills.
- Download `?download=1`: strip C2PA/EXIF + delogo pill AI. Master di library utuh.

## Links

- [[02 Projects/AIOSCreator/design/00 Direction]]
- [[02 Projects/AIOSCreator/Design-lock]]
