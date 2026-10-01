Part of [[00 UGC Playbook – Index]].

# Katalog 33 template UGC Factory

Tanggal salinan: 2026-10-02. Ini salinan dari kode yang sedang jalan, buat dibaca dan dianalisa. Bukan spec baru.

Sumber:

- `apps/web/lib/ugc-factory-recipes.ts` — 33 resep di papan UGC Factory (14 faceless, 6 slideshow, 13 talent).
- `apps/web/lib/ugc-factory-pack.ts` — peta id resep ke id format naskah.
- `apps/web/lib/ugc-script.ts` — hint dan teks struktur yang dikirim ke penulis naskah.
- `apps/web/lib/ugc-factory-board.ts` — cek `needs` waktu draft dan waktu tulis naskah.
- `apps/web/lib/meta-branded.ts` — pemilih template dari branded content.

Dua lapis, jangan dicampur:

1. **Resep papan** (`F01`–`T13`). Ini yang kelihatan sebagai 33 recipes. Isinya nama, kebutuhan (`needs`), dan daftar beat.
2. **Format naskah**. Setiap resep menunjuk satu format. Teks format itu yang mengisi hook, visual, dan CTA. `T03` dan `T13` menunjuk format yang sama: `talking`.

Hitungan beat di resep: faceless dan talent mostly 5. Pengecualian: `F12` punya 6, `T02` punya 4. Slideshow selalu 6. Teks format slideshow menulis "8 stills". Teks format video menulis slot 0–2s / 2–6s / 6–10s / 10–14s.

## Index

| Id | Keluarga | Nama | Beat | Butuh | Format naskah |
| --- | --- | --- | --- | --- | --- |
| F01 | Faceless | Proof-first | 5 | evidence | proof-first |
| F02 | Faceless | Screen-record | 5 | screen | screen-record |
| F03 | Faceless | Pack / hero | 5 | photo | pack-hero |
| F04 | Faceless | Before / after | 5 | before-after | before-after |
| F05 | Faceless | Problem to payoff | 5 | photo | problem-payoff |
| F06 | Faceless | A vs B | 5 | comparison | comparison |
| F07 | Faceless | Unbox | 5 | packaging | unboxing |
| F08 | Faceless | What's in the box | 5 | components | whats-in-box |
| F09 | Faceless | How-to | 5 | instructions | how-to |
| F10 | Faceless | Hands-only | 5 | photo | hands-only |
| F11 | Faceless | Satisfying | 5 | photo | satisfying |
| F12 | Faceless | Test | 6 | test | test |
| F13 | Faceless | Stop-scroll | 5 | photo | stop-scroll |
| F14 | Faceless | Restock | 5 | photo | restock |
| S01 | Slideshow | Discovery | 6 | photo | slides-discovery |
| S02 | Slideshow | List | 6 | four-points | slides-list |
| S03 | Slideshow | Story | 6 | photo | slides-story |
| S04 | Slideshow | FAQ | 6 | faq | slides-faq |
| S05 | Slideshow | Mistakes | 6 | instructions | slides-mistakes |
| S06 | Slideshow | Rank | 6 | comparison | slides-ranking |
| T01 | Talent | Unbox talk | 5 | talent, packaging | unbox-talk |
| T02 | Talent | Hold | 4 | talent, photo | hold |
| T03 | Talent | Talking | 5 | talent, voice | talking |
| T04 | Talent | Lifestyle | 5 | talent, photo | lifestyle |
| T05 | Talent | I found this | 5 | talent, photo | i-found-this |
| T06 | Talent | Comment reply | 5 | talent, comment-or-faq | comment-reply |
| T07 | Talent | Review | 5 | talent, photo | review |
| T08 | Talent | GRWM | 5 | talent, wearable | grwm |
| T09 | Talent | Beauty GRWM | 5 | talent, instructions | beauty-grwm |
| T10 | Talent | POV | 5 | talent, photo | pov |
| T11 | Talent | Day in the life | 5 | talent, photo | day-in-life |
| T12 | Talent | Shopping haul | 5 | talent, components | haul |
| T13 | Talent | Demo product | 5 | talent, instructions | talking |

`T13` tidak punya teks format sendiri. Penulis naskah menerima struktur `talking`, sama dengan `T03`.

## Cara `needs` dicek

- `photo` terpenuhi kalau SKU punya gambar, atau ada still fashion yang dipilih, atau `supplied` memuat `photo`.
- `talent` terpenuhi kalau talent source-nya `NEW` atau `FASHION_LOOK`, atau `supplied` memuat `talent`. Resep talent tanpa itu ditandai belum siap.
- `evidence`, `test`, `before-after`, `comparison`, `screen`, `components`, `instructions`, `four-points`, `faq`, `comment-or-faq`, `wearable`, `voice`, `packaging` terpenuhi hanya kalau kunci itu ada di `supplied`. Foto SKU tidak mengisi kunci-kunci ini.
- Kalau yang kurang termasuk `evidence`, `test`, atau `before-after`, kode bloknya `MISSING_EVIDENCE`. Kekurangan lain jadi `MISSING_ASSET`.
- Fakta produk kosong juga memblok (`product-facts`).
- Resep yang `needs`-nya `packaging`, dan naskahnya menyebut buka kotak sementara packaging belum terpasok, kena blok `ASSUMED_PACKAGING`. `F03` butuhnya `photo`, jadi kalimat kotak di F03 tidak kena blok itu.
- Resep faceless menambah catatan review: wajah yang kelihatan di frame akhir memblok approval.
- Setiap draft juga membawa catatan review: placement profile masih `NEEDS_VERIFICATION`.

## Saran dari jenis SKU

Pemilih ini ada di `suggestFactoryFormats`. Operator tetap bisa pilih template lain.

| Jenis SKU | Format yang disarankan | Resep papan |
| --- | --- | --- |
| Makeup | beauty-grwm, review, before-after | T09, T07, F04 |
| Skincare | beauty-grwm, before-after, proof-first | T09, F04, F01 |
| Shoes | unbox-talk, haul, grwm | T01, T12, T08 |
| Garment | haul, grwm, hold | T12, T08, T02 |
| Gadget | pack-hero, unbox-talk, how-to, proof-first | F03, T01, F09, F01 |
| App | screen-record, proof-first, slides-list | F02, F01, S02 |
| Food | satisfying, proof-first, review | F11, F01, T07 |
| Other | pack-hero, unbox-talk, review | F03, T01, T07 |

Jenis SKU dibaca dari judul, fitur, dan `objectKind`. Makeup menang sebelum skincare. Kata shoe/sneaker/gazelle mengalahkan `objectKind` garment.

## Saran dari Meta branded content

Dari jumlah postingan berlabel partnership, bukan dari likes atau views:

- Reel paling banyak, dan ada minimal satu: `T03` Talking.
- Story lebih banyak dari post, dan ada minimal satu: `T04` Lifestyle.
- Ada post: `S01` Discovery.
- Tidak ada yang ketiganya: `F03` Pack / hero.

## Faceless

### F01 Proof-first

- Butuh: `evidence`
- Beat: Supported result, Context, Process, Supporting detail, CTA
- Format: `proof-first`. Hint: Result first, then how.

Faceless. THIS SKU’s result/use in frame 1 — not a laptop SaaS demo. HOOK 0–2s spoken: one-line surprise about the result. Visual: finished output / product doing the thing, readable. 2–6s: the input/problem, then THIS SKU being used. 6–10s: output again, one listing-true detail that makes it believable. 10–14s: hold on the product. CTA: link below, affiliate. No invented results.

### F02 Screen-record

- Butuh: `screen`
- Beat: Source screen, Step, Step, Detail, CTA
- Format: `screen-record`. Hint: This SKU’s UI only.

Crop THIS SKU’s real screen/UI. No fake dashboard. HOOK 0–2s spoken: one line over the result already on screen. Visual: UI result first, readable. 2–6s: 2–4 taps/scrolls through the real flow. 6–10s: zoom the feature that creates the payoff. 10–14s: final output. CTA overlay + link below. Voiceover only if it adds info. No invented screens.

### F03 Pack / hero

- Butuh: `photo`
- Beat: Hero, Packaging detail, Product, Visible benefit, CTA
- Format: `pack-hero`. Hint: SKU full, no face.
- Default form Create Production adalah template ini.

Faceless pack/hero. No face. Hands ok. HOOK 0–2s spoken: name THIS SKU in one breath. Visual: pack or hero fills 9:16, logo/color readable. 2–6s: slow turn / hands lift, pockets or included pieces from the listing. 6–10s: one listing-true detail in close-up. 10–14s: hero hold. CTA: link below, affiliate. Do not invent extra accessories.

### F04 Before / after

- Butuh: `before-after`
- Beat: Start state, Problem, Process, End state, CTA
- Format: `before-after`. Hint: Only if listing-true.

Only if the listing supports a real before/after. Do not fabricate. HOOK 0–2s spoken: name the problem. Visual: before state, no SKU yet. 2–6s: THIS SKU / process in frame. 6–10s: after state. One listing-true change that caused it. 10–14s: product readable. CTA: link below. No fake ‘30-day glow’ unless listed.

### F05 Problem to payoff

- Butuh: `photo`
- Beat: Problem, Consequence, Mechanism, Demo, CTA
- Format: `problem-payoff`. Hint: Pain, mechanism, result.

Faceless. HOOK 0–2s spoken: specific pain, not a slogan. Visual: the annoying old way. 2–6s: why the usual method sucks, then THIS SKU’s mechanism from the listing. 6–10s: it working. Payoff/result only if listing-true. 10–14s: product readable. CTA: link below, affiliate.

### F06 A vs B

- Butuh: `comparison`
- Beat: Setup, A, B, Criteria, CTA
- Format: `comparison`. Hint: Same input, two options.

Same input, same rules. HOOK 0–2s spoken: we’re testing A vs B. Visual: side-by-side setup, THIS SKU is one side. 2–6s: option A. 6–10s: option B (this SKU). 10–14s: reveal + one listing-true conclusion. No fake winner stats or invented scores. CTA: link below.

### F07 Unbox

- Butuh: `packaging`
- Beat: Closed pack, Open, Reveal, Detail, CTA
- Format: `unboxing`. Hint: Hands, pack, contents.

Faceless hands. No talking head. HOOK 0–2s spoken: one line as the box hits the table. Visual: closed pack of THIS SKU, readable. 2–6s: open. 6–10s: lay out only what the listing includes. 10–14s: hero of the main item. CTA: link below. No extra gifts invented.

### F08 What's in the box

- Butuh: `components`
- Beat: Packaging, Contents, Each part, Setup, CTA
- Format: `whats-in-box`. Hint: Kit layout.

Top-down kit. Faceless. HOOK 0–2s spoken: what’s actually in here. Visual: closed pack, then layout. 2–6s / 6–10s / 10–14s: name each included piece from the listing, one at a time. No extras. CTA: link below.

### F09 How-to

- Butuh: `instructions`
- Beat: Goal, Prep, Steps, Result, CTA
- Format: `how-to`. Hint: 2–4 real steps.

Hands + THIS SKU. No face required. One job from the listing. HOOK 0–2s spoken: I’m gonna show you how to [job]. Visual: SKU + the job setup. 2–6s: step 1–2. 6–10s: step 3. 10–14s: done / result. CTA: link below. No invented steps.

### F10 Hands-only

- Butuh: `photo`
- Beat: Pick up, Detail, Use, Close, CTA
- Format: `hands-only`. Hint: Hands + SKU, no face.

Only hands and THIS SKU. HOOK 0–2s: texture/use in frame, one spoken line. 2–6s / 6–10s: satisfying use from listing (buttons, zip, clip). 10–14s: product readable. CTA: link below. No talking head.

### F11 Satisfying

- Butuh: `photo`
- Beat: Detail, Repeatable motion, Close detail, Payoff, CTA
- Format: `satisfying`. Hint: Click / peel / texture.

ASMR-adjacent. First frame = texture of THIS SKU. HOOK 0–2s spoken: almost none, or one whisper line. Visual: peel/click/pack tight. 2–10s: repeat the satisfying action. 10–14s: full product. CTA overlay. No fake slime if the SKU isn’t that.

### F12 Test

- Butuh: `test`
- Beat: Question, Setup, Run, Result, Limit, CTA
- Format: `test`. Hint: Does it actually…
- Satu-satunya resep faceless dengan 6 beat.

One test that the listing actually claims. HOOK 0–2s spoken: does it actually [claim]? Visual: the test setup + THIS SKU. 2–6s: the attempt. 6–10s: what happened (no invented pass/fail numbers). 10–14s: product readable. CTA: link below.

### F13 Stop-scroll

- Butuh: `photo`
- Beat: Opening detail, Context, Product, Benefit, CTA
- Format: `stop-scroll`. Hint: Weird first frame.

Odd first frame of THIS SKU (extreme close-up, odd angle). HOOK 0–2s spoken: wait what is that. Visual: pattern interrupt, product still identifiable. 2–6s: pull back, name the SKU. 6–10s: one use. 10–14s: readable hero. CTA: link below.

### F14 Restock

- Butuh: `photo`
- Beat: Storage, Fill, Use, Result, CTA
- Format: `restock`. Hint: Shelf / desk drop.

Faceless. Product lands on desk/shelf. HOOK 0–2s spoken: restocking this. Visual: THIS SKU dropping into place, readable. 2–6s: identify. 6–10s: one use. 10–14s: tidy shelf. CTA: link below.

## Slideshow

Penulis naskah memotong beat slideshow di 6, dan menambah beat `CTA` kalau kurang dari 6. Teks format di bawah menulis 8 stills.

### S01 Discovery

- Butuh: `photo`
- Beat: Hook, Problem, Find the product, Main feature, Supporting use, CTA
- Format: `slides-discovery`. Hint: Then I found…

8 stills, one thought each, 5–14 words. 1 curiosity hook + strongest visual. 2 old problem. 3 then I found…. 4 THIS SKU. 5 strongest listing feature. 6 second proof. 7 who it’s for. 8 CTA + affiliate. Not every slide an ad.

### S02 List

- Butuh: `four-points`
- Beat: Title, Point 1, Point 2, Point 3, Point 4, CTA
- Format: `slides-list`. Hint: 3–5 things.

8 stills. Slide 1: 3/5 things hook. 2–5: items. 6: THIS SKU earns one slot from listing facts. 7 summary. 8 CTA. Do not make every slide a disguised ad.

### S03 Story

- Butuh: `photo`
- Beat: Open, Context, Problem, Action, Change, CTA
- Format: `slides-story`. Hint: Tension → payoff.

8 stills: 1 tension hook. 2 context. 3 failure. 4 turning point. 5 THIS SKU. 6 what changed (listing-true). 7 result. 8 CTA.

### S04 FAQ

- Butuh: `faq`
- Beat: Open, Question 1, Question 2, Question 3, Question 4, CTA
- Format: `slides-faq`. Hint: One Q per slide.

8 stills. Real listing FAQs only. One question per slide, THIS SKU answers. No fake comments, no fake review counts. Last slide CTA.

### S05 Mistakes

- Butuh: `instructions`
- Beat: Open, Mistake 1, Mistake 2, Mistake 3, Better way, CTA
- Format: `slides-mistakes`. Hint: Stop doing X.

8 stills: mistakes people make in this category. THIS SKU is the fix on later slides, from listing facts. Last slide CTA. No invented ‘everyone does this’ stats.

### S06 Rank

- Butuh: `comparison`
- Beat: Criteria, Fourth, Third, Second, First, CTA
- Format: `slides-ranking`. Hint: Best → skip.

8 stills ranking options. THIS SKU earns a slot from listing facts. No fake #1. Last slide CTA + affiliate.

## Talent

Talent di factory adalah throwaway, bukan karakter roster. Wardrobe masih di `factoryWardrobe`: pakaian sehari-hari, bukan outfit character library. Beauty GRWM memakai camisole atau tee di vanity. Unbox talk dan haul untuk sepatu atau garment memakai lounge di kasur.

### T01 Unbox talk

- Butuh: `talent`, `packaging`
- Beat: Open, Talk while opening, Reveal, Detail, CTA
- Format: `unbox-talk`. Hint: GRWM haul: box → pull → hold to lens → CTA.

Bedroom/sunlit haul, throwaway talent (not a roster face). Title like “[SKU] haul / GRWM”. HOOK 0–2s spoken: Get ready with me — these JUST came and I’m obsessed. Visual: she sits on the bed, closed box of THIS SKU in frame 1, shocked/happy hands. 2–6s: open the box, pull the exact product. Spoken + visual name only listing-true details (material, color, sole, stripes, laces, what’s in the box). 6–10s: hold SKU to the lens / close-up. Talk feel/fit/how it goes with outfits ONLY if those claims are in the listing — no invented sizing or ‘sell out’. 10–14s: quick mirror or on-body if shoes/clothes, else detail hold. CTA: lean into camera. Link below. Disclosure affiliate. Do not copy another brand’s unbox (no Adidas/Gazelle unless that is the SKU).

### T02 Hold

- Butuh: `talent`, `photo`
- Beat: In hand, Detail, One confirmed benefit, CTA
- Format: `hold`. Hint: Throwaway + SKU.
- Satu-satunya resep talent dengan 4 beat.

Throwaway talent, not a roster face. HOOK 0–2s spoken: look at this. Visual: she holds THIS SKU to camera, readable from frame 1. 2–6s: turn it, one listing detail. 6–10s: how you’d use it (listing-true). 10–14s: hold closer. CTA: lean in, link below, affiliate.

### T03 Talking

- Butuh: `talent`, `voice`
- Beat: Hook, Explain, B-roll, Benefit, CTA
- Format: `talking`. Hint: To camera.

Throwaway talking head. Conversational, not testimonial-speak. SKU in frame the whole time. HOOK 0–2s spoken: mid-thought one-liner naming THIS SKU. Visual: face + product. 2–6s: old way. 6–10s: one listing feature. 10–14s: why it helps. CTA: link below, affiliate. No ‘changed my life’.

### T04 Lifestyle

- Butuh: `talent`, `photo`
- Beat: Day scene, Use, Detail, Payoff, CTA
- Format: `lifestyle`. Hint: In use.

Throwaway talent using THIS SKU in a real beat (desk, kitchen, commute) — not bolted on at the end. HOOK 0–2s spoken: situation, not a slogan. Visual: she’s already using it. 2–10s: the use, one listing detail. 10–14s: product readable. CTA: link below.

### T05 I found this

- Butuh: `talent`, `photo`
- Beat: Discovery, Why it fits, Demo, Detail, CTA
- Format: `i-found-this`. Hint: Mid-thought.

Already mid-thought. Conversational. HOOK 0–2s spoken: I found this. Visual: natural creator shot, THIS SKU nearby. 2–6s: old frustration. 6–10s: show product + main listing feature. 10–14s: why it’s useful. CTA: link below. No scripted testimonial.

### T06 Comment reply

- Butuh: `talent`, `comment-or-faq`
- Beat: Question, Answer, Demo, Detail, CTA
- Format: `comment-reply`. Hint: On-screen question.

On-screen question from a listing FAQ — not a fake comment with likes. HOOK 0–2s spoken: answering that. Visual: question overlay + talent + THIS SKU. 2–10s: demo the answer. 10–14s: one extra listing detail. CTA: link below.

### T07 Review

- Butuh: `talent`, `photo`
- Beat: Criteria, Feature, Demo, Known limit, CTA
- Format: `review`. Hint: First-use honest.

First-use review. Listing facts only. No star counts, GMV, or ‘changed my life’. HOOK 0–2s spoken: first time using THIS SKU. Visual: unbox or hold. 2–6s: what you notice (listing-true). 6–10s: who it’s for. 10–14s: honest caveat if listing has one, else product readable. CTA: link below, affiliate.

### T08 GRWM

- Butuh: `talent`, `wearable`
- Beat: Getting ready, Put on, Detail, Final look, CTA
- Format: `grwm`. Hint: Get-ready with this SKU.

Get-ready-with-me. THIS SKU is the object (put on / grab), not a 4-brand beauty vlog unless the SKU is beauty — then use Beauty GRWM. Throwaway talent. HOOK 0–2s spoken: get ready with me. Visual: bedroom/vanity, THIS SKU on the table. 2–6s: pick it up. 6–10s: put it on or use it. 10–14s: mirror. CTA: link below. Listing details only.

### T09 Beauty GRWM

- Butuh: `talent`, `instructions`
- Beat: Prep, Apply, Texture, Finish, CTA
- Format: `beauty-grwm`. Hint: Makeup/skincare try-on on face.

Beauty Get Ready With Me — try-on on the face, not an unbox. Warm sunlit vanity, throwaway talent. Only for makeup/skincare SKUs. THIS SKU is the product she applies (lipstick, serum, mascara…). Do not invent a full routine of other brands. Other steps stay generic or skip. HOOK 0–2s spoken: get ready with me. Visual: vanity, THIS SKU in hand or on the table, she looks to camera. 2–6s: prep, then apply THIS SKU to face/skin. 6–10s: blend/finish, listing-true texture/shade only — no invented ingredients. 10–14s: mirror close-up of the result on her. CTA: lean in, link below, affiliate. Trendy lifestyle, not a studio ad. Not a shoebox unbox.

### T10 POV

- Butuh: `talent`, `photo`
- Beat: POV setup, Interact, Detail, Use, CTA
- Format: `pov`. Hint: Camera is the user.

POV: viewer’s hands/eyes. Hook is the situation, not a brand slogan. HOOK 0–2s spoken: POV you just [situation]. Visual: first-person, THIS SKU entering frame. 2–10s: use it first-person. 10–14s: result. CTA: link below.

### T11 Day in the life

- Butuh: `talent`, `photo`
- Beat: Morning, Context, Use the product, Next context, CTA
- Format: `day-in-life`. Hint: One beat of the day.

One real moment, not a 24h montage. HOOK 0–2s spoken: a time of day. Visual: talent in that beat, THIS SKU already there. 2–10s: the use. 10–14s: product readable. CTA: link below. Don’t invent a whole day of products.

### T12 Shopping haul

- Butuh: `talent`, `components`
- Beat: Preview, Item, Detail, Summary, CTA
- Format: `haul`. Hint: The one keep.

Haul energy, but THIS SKU is the keep. Don’t invent a pile of other brands. HOOK 0–2s spoken: haul just landed / the one I kept. Visual: bags/box, THIS SKU. 2–6s: pull it. 6–10s: why it stayed (listing-true). 10–14s: hold to camera. CTA: link below, affiliate.

### T13 Demo product

- Butuh: `talent`, `instructions`
- Beat: Goal, Setup, Main step, Detail, CTA
- Format yang dikirim ke penulis: `talking`, sama dengan T03. Hint dan teksnya ikut T03 di atas.
- Beat resep ini (Goal, Setup, Main step, Detail, CTA) tidak muncul di teks format `talking`.
