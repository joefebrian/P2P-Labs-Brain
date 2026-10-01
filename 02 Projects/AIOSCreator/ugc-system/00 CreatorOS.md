# UGC system → CreatorOS

#project

Pack: **enzoxmotion UGC System v2**. Source zip 2026-09-25.

Ini **aturan kreatif** untuk script + clip character. Bukan ganti identity lock.

## Mapping

| Pack | Di CreatorOS |
|---|---|
| SYSTEM.md lock creator + product | Character FACE/BODY + SKU still |
| HOOK_LIBRARY | `/api/jobs/script` hook |
| FORMATS.md | angle: review / unboxing / hold / talking / lifestyle → format terdekat |
| BATCHING.md | nanti: 1 still × N hook, bukan 1 klik 20 random clip |
| CREATOR_SCALING | roster character = talent wave |
| BRIEF template | Affiliate step 3 + Products |

## Hukum yang ikut ke video

- First frame harus ngomong sebelum VO panjang
- Product di cerita, bukan nempel di detik terakhir
- VO kedengaran orang, bukan brand
- Jangan invent klaim, review, angka
- Identity character **tidak** berubah antar take (SYSTEM §2)

## Files

- [[SYSTEM]]
- [[HOOK_LIBRARY]]
- [[FORMATS]]
- [[BATCHING]]
- [[CREATOR_SCALING]]
- [[CREATOR_BRIEF_TEMPLATE]]
- Code: `apps/AIOSCreator/docs/ugc-system/` + `lib/ugc-system.ts`
- Affiliate: `?tool=affiliate`
- Factory: `/create/ugc-factory`

## Links

- [[02 Projects/AIOSCreator]]
- [[02 Projects/AIOSCreator/design/00 Direction]]
