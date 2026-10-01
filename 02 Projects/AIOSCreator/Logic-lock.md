# AIOSCreator — Logic lock (MPT + Hunyuan)

#decision

Locked 2026-09-02. GPU this PC = RTX **3060 12GB**. PRD workflow registry still wins: FLUX.2 Klein 4B + Wan 2.2 5B @ 480p/720p draft.

## MoneyPrinterTurbo — take the factory, not the product

Repo: https://github.com/harry0703/MoneyPrinterTurbo · MIT · Python FastAPI + ffmpeg.

Pipeline we **copy as stages** (maps 1:1 to HOME modules 2–4):

```
topic / product URL
  → script (LLM)
  → voice (TTS)
  → visuals (local gen, not stock-first)
  → captions
  → BGM (licensed per platform — PRD)
  → ffmpeg assemble 9:16 / 16:9 / 1:1
  → export pack  → official publish
```

Code shape to mirror later (`app/services`, `app/controllers`): script / voice / material / subtitle / concat as **separate services**, one orchestrator, durable job.

**Take**
- Stage machine + batch + job history
- Edge TTS as **free local-ish voice** fallback (no key)
- Aspect SKUs 9:16 1080×1920, 16:9, 1:1
- Caption style knobs (font, stroke, position)
- LLM gateway already lists **xAI Grok** — we use SpaceXAI/`XAI_API_KEY` as default, not OpenAI
- Custom script / custom voice / custom clips at each stage (operator override)

**Leave**
- Pexels/Pixabay as default visual (PRD = local gen + product UGC, stock is optional B-roll)
- Docker / docker-compose (Phase 0 native)
- “One-click unofficial social bots” if any path is unofficial — PRD bans that
- Cloud video APIs (Seedance, MiniMax H3, WaveSpeed) as P0 — those are budgeted `closed_*`
- Merging their WebUI — our HOME is seven-module OS

MPT is a **short-video factory**. AIOSCreator is a **social-commerce OS**. Factory becomes UGC Factory module, not the whole app.

## HunyuanVideo — quality reference, not the 12GB engine

Repo: https://github.com/Tencent-Hunyuan/HunyuanVideo · 13B DiT · ComfyUI native exists.

Official VRAM (batch 1):

| Setting | Peak |
|---|---|
| 720×1280 × 129f | **60 GB** |
| 544×960 × 129f | **45 GB** |

This PC has **12 GB**. Stock HunyuanVideo **will not run**. Do not download 13B weights for M00–M02.

**Take**
- Architecture ideas: 3D VAE, prompt-rewrite before sample, dual-stream→single-stream
- ComfyUI node as a **P2 workflow** if a 12GB path exists later: HunyuanVideo-1.5, HunyuanVideoGP, GGUF/city96, TeaCache
- I2V / Avatar / Custom as future MotionControl cousins — not MVP
- License is **Tencent “other”** — read before any commercial ship. Not Apache-2.0.

**Leave (Phase 0)**
- Default T2V engine
- Multi-GPU xDiT
- Linux-only conda stack as our runtime (we are Windows native + ComfyUI)

P0 video stays **Wan 2.2 5B** (and Wan Animate for MotionControl). Hunyuan = optional later adapter, same as Kling/Veo: behind a workflow id, honest ETA, VRAM gate.

**2026-09-05 override (Joe gas):** T0 12GB path is live — native **HunyuanVideo 1.5 480p I2V step-distilled fp8** (8-step, no GGUF, no EasyCache). Stock 720p / 13B / GGUF still blocked. MotionControl copy = MiniMax H3 R2V, not Wan Animate.

## Orchestrator (ours)

```
Web/API → rights preflight → workflow router
  → local worker → ComfyUI (Wan/FLUX)  OR  ffmpeg factory (MPT-style)
  → master + derivatives + lineage
```

Generation timeout ≠ HTTP timeout (HeliosGen job poller). Idempotent publish (PRD).

## Links
- [[02 Projects/AIOSCreator]]
- [[02 Projects/AIOSCreator/Design-lock]]
- [[AtlasNow-Monetization-PRD]] is **not** money master here — CreatorOS PRD is.
