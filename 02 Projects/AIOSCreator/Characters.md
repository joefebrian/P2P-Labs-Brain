# Character library

#project #decision

**Job of `/create/characters`:** build a **consistent AI influencer** — one recurring persona (face, body, vibe) that stays the same person across every still. Same job as “Build a consistent AI influencer with the AI Influencer Generator.” Not a one-off pretty picture. Not a collage of lookalikes.

Character is a **persist object**, not a third engine.

Still engines:
- **GPT Image 2 / Seedream 5.0 Pro** — paid cloud, ChatGPT-class plates. Key in Settings.
- **Z-Image Turbo** — local Apache, INT8 on 3060. Better photoreal than Klein. Prompt-only + **orang baru / perawakan sama** (img2img).
- **Qwen Image Edit 2511** — native Comfy edit. **Needs a reference photo.** INT8 + Lightning 4-step. Smoke ~2 min on 3060. Identity plate **768×960**. **Keep-face** = VAEEncode of the scaled plate + denoise 0.55. Empty latent + denoise 1 **drifts identity** (Lili 768 first pass = orang baru). Transform (new face, same build) stays denoise 1. Prompt-only auto-falls back to Z-Image.
- **Klein 4B** — local Apache, fast lock via ReferenceLatent. More AI-beauty.

Video = **Kling Motion Control 3.0** (cloud copy, 3–30s 1080p) / H3 I2V / **H3 I2V · long** (chunked 5s windows ≤60s, not native 60s denoise) / **H3 I2V · nudity** (NaughtyTimes) / LTX-2 / H3 R2V (local copy 2s) / **H3 R2V · nudity** (AfterMidnight) / Wan Animate 2 (crashed Windows) / Wan 5B / Hunyuan / Seedance. **TaoMate-H3** = streaming H3 on Hopper clusters only ([[TaoMate-H3]]) — auto-deploy if GPU qualifies, **never on this 3060**. Civitai “60s seamless” = Motion Director 6×10s T2V + SageAttention — we did **not** install Sage. NVIDIA = upscale only.

## Journey (influencer lock)

1. **Design the persona** — `/create/characters/new`: **AI influencer generator** (visual picks for build / eyes / hair + woman **breast library** 32–38 × A–DD, default **36B** + bespoke framework wardrobe / marks / makeup / other → clean studio portrait, no phone) or **upload** (lock as-is / new person same build).
2. **Lock identity** — the AFTER still on the right. That file is the influencer. Accept it before anything else.
3. **Same-person stills** — one pose/angle/expression per GEN, always from that identity. Front, side, smile, standing… each is a new shot of **her**, not a new girl.
4. **Continuity sheet** — assembled from those locked stills (ffmpeg grid). Never ask a model to paint a contact-sheet mosaic.
5. Commerce hold/glance stay UGC shots of the same person.

If a still changes face, hair identity, or body, it is a failed shot — do not keep it in the set.

## Object

`data/db/characters.json` + `data/media/characters/{id}-{slot}.png`

- `source`: `photo` | `transform` | `prompt`
- `identityUrl`
- `slots[]`: **sheet** (4:5 bible) + turnaround (front/3/4/side/back) + face + expressions + poses + costume + commerce (hold, glance)

## UI

- `/create/characters` library
- `/create/characters/new` wizard
- `/create/characters/[id]` identity + set
- MotionControl: picker from library identity + filled slots
- AI Studio **Avatar → LOCK**: pick library identity/slot first, or upload a one-off photo. Downstream stills + video use that `src`.

## Prompts

Local stills/motion: **no SFW filter**. Nude / NSFW OK for adult fictional characters and documented consenting adults. Operator prompt is passed through as written.

Still blocked (PRD): minors, CSAM, non-consensual intimate of a real person.

Cloud engines (GPT Image 2 / Seedream) follow *their* ToS — we cannot uncensor those APIs.

**Prompt enhance (PRD, not built):** LLM rewrite via OpenRouter `:free` before GEN. Opt-in. Stops sheet prompts drifting to cartoon. Spec [[Prompt-Enhance-PRD]].

## Not this sprint

Voice, rights registry (M04), R2V identity clip, VSA/Wan, prompt-enhance UI.

See [[02 Projects/AIOSCreator/GROK]] · [[02 Projects/AIOSCreator/H3-Motion-Profiles]] · [[Prompt-Enhance-PRD]]
