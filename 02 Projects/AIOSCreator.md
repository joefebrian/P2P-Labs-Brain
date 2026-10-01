# AIOSCreator (CreatorOS)

#project

## Outcome
Local-first **AI Social Media Operating System**. Operator kasih product + character + akun + revenue goal → research → script → gen lokal unlimited → pack platform → official publish → attribution → mutate winner.

Public name: **CreatorOS**. GitHub: [joefebrian/AIOSCreator](https://github.com/joefebrian/AIOSCreator).

**Master kerangka = PRD v2.1** (`AI_Creator_Commerce_OS_Master_PRD_v2_1.docx`). IA unchanged from v2.0: HOME · Intelligence · Commerce · Create · Distribute · Grow · System. Delta only: [[02 Projects/AIOSCreator/PRD-v2.1-delta]] (NVIDIA stack + Grok terminal). Agent load: [[02 Projects/AIOSCreator/GROK]]. v3 notes stay constraints, not a second IA.

## Status
🟡 Active · **session focus** · M00 + **first local image** · `http://localhost:3000/create/studio`

## Paths
```
Notes:         02 Projects/AIOSCreator/ inside the synced vault
Mac vault:     /Users/joefebrian/Downloads/Working Desk/Obsidian/mygrok
Windows vault: C:\Users\USER\Documents\Obsidian\mygrok
App code:      C:\Users\USER\Grok\apps\AIOSCreator\   (Windows only, not in the vault)
GitHub notes:  https://github.com/joefebrian/P2P-Labs-Brain
GitHub app:    https://github.com/joefebrian/AIOSCreator
Master PRD:    [[02 Projects/AIOSCreator/PRD-v2.1-extracted]] (v2.1)
v2.0 extract:  [[02 Projects/AIOSCreator/PRD-v2-Master-extracted]]
v2.1 delta:    [[02 Projects/AIOSCreator/PRD-v2.1-delta]]
Grok OS:       [[02 Projects/AIOSCreator/GROK]]
v3 constraints:[[02 Projects/AIOSCreator/CreatorOS-PRD-v3-extracted]]
Design dir:    [[02 Projects/AIOSCreator/design/00 Direction]]
Motion control:[[02 Projects/AIOSCreator/design/2026-10-02 Motion Control]]
UGC system:    [[02 Projects/AIOSCreator/ugc-system/00 CreatorOS]]
UGC playbook:  [[UGC Playbook/00 UGC Playbook – Index]]
Factory 33:    [[02 Projects/AIOSCreator/design/2026-10-02 UGC Factory 33 templates]]

```

## This machine (local-max)
| | |
|---|---|
| GPU | NVIDIA RTX **3060 12GB** (driver 560.94) |
| RAM | **112 GB** |
| CPU | Dual Xeon E5-2696 v4 (44c / 88t) |
| ffmpeg | `C:\ffmpeg\bin` · 8.1.2 already on PATH |
| VRAM pack (PRD §18.2 + §33 T0) | 8–12GB → FLUX.2 Klein **4B** + Wan 2.2 **5B** @ 480p/720p draft. **No native 4K.** Broadcast off during generate. NVENC for encode. |

## Docker?
**Tidak. Jangan install Docker Desktop untuk Phase 0.**

Alasan (PRD §19 Local mode):
- Wedge = **GPU lokal**. ComfyUI + CUDA harus native Windows, bukan container.
- Docker Desktop makan RAM/VRAM lewat WSL2 — lawan “local-max”.
- Single-user local: **SQLite** allowed. Redis/Postgres = Hybrid later.
- ffmpeg sudah native.

Kalau nanti Hybrid (multi-seat / cloud control plane): Postgres + Redis via Docker **optional**, app + ComfyUI tetap native.

## Stack lock (local, no build yet)
| Layer | Local-max choice |
|---|---|
| Web UI | Next.js + React + TS + Tailwind + **shadcn/ui** (HeliosGen interaction, not kie.ai) |
| Desktop later | Tauri |
| API / BFF | TypeScript |
| AI/media worker | Python FastAPI → ComfyUI |
| DB | **SQLite** (single-user). Postgres only when Hybrid |
| Queue | In-process / SQLite jobs first. Redis+BullMQ = Hybrid |
| Storage | Local disk (`data/media`) |
| Video | ffmpeg native |
| Inference | ComfyUI native + pinned nodes |
| LLM (control plane) | SpaceXAI / xAI `XAI_API_KEY` · `https://api.x.ai/v1` · default `grok-4.5` — **server-side only** |

## HOME = seven modules (design SoT)

![[HOME-seven-modules]]

One engine, seven modules. Fake animation without a backing job = banned.

| # | Module | Job |
|---|---|---|
| 1 | Research | Intelligence decoded |
| 2 | Content Engine | Write → narrate · script · voiceover |
| 3 | Production Studio | Animation / B-roll · rendered |
| 4 | Distribution | Official APIs · IG / FB / TikTok / YouTube |
| 5 | Engagement | Reply → capture |
| 6 | Analytics | Score posts · winning hooks → Research |
| 7 | Monetization | Shop / affiliate / booked calls — no invented GMV |

Growth Engine = live pipeline + revenue chip. Reference: Structure Webworks.

## Money (locked)
- Local pixels = **no per-clip fee**. Hardware/VRAM/time are the limits.
- Paid later: cloud burst, 4K/8K upscale, seats, Autopilot, premium packs.
- Commerce P0: Amazon + TikTok Shop + Shopee. P1: YouTube Shopping tags, Meta shopping.
- North star: affiliate contribution profit / 1,000 AI-generated views.
- Official APIs only. Unofficial bots = product ban.

## Strict MVP (jangan overbuild)
AI Studio + ComfyUI + MotionControl + Character Library + Amazon/Shopee import + UGC script + AI voice + UGC video + resolution pipeline + **export pack** + YouTube Shorts official path + TikTok **Inbox Upload** + affiliate link.

Bukan MVP gate: Direct public TikTok, YouTube Shopping write-API, public For-You network, native 4K every job.

Milestones M00–M10: [[02 Projects/AIOSCreator/Local-dev-prep]]

## Ingested references (2026-09-02)

Take what’s good, don’t fork:

- Design: [[02 Projects/AIOSCreator/Design-lock]] — shadcn + HeliosGen UX. Ant Design = table/form patterns only.
- Logic: [[02 Projects/AIOSCreator/Logic-lock]] — MoneyPrinterTurbo = UGC factory stages. HunyuanVideo = not on 12GB; Wan 2.2 stays P0.

## Next actions
- [x] Ingest PRD v3.0 + HOME screenshot into vault
- [x] Lock Docker = no for local-max
- [x] Scaffold `apps/AIOSCreator` (no `npm install`, no build)
- [x] Git 2.55 + Node 22.19 + pnpm 11 + Python 3.12 + uv + ffmpeg on this PC
- [ ] Admin once: long paths + optional VS Build Tools (`apps/AIOSCreator/scripts/admin-once.ps1`)
- [ ] Joe: buka vault folder ini di Obsidian
- [x] **M00** HOME + Content Engine script job (xAI grok-4.6). Key in `.env.local` only.
- [x] Native ComfyUI on `:8188`. Image GEN = Klein / Z-Image / Qwen Edit. Motion generate = H3 I2V / Wan 5B / Hunyuan 1.5 480p. MotionControl copy = H3 R2V. ffmpeg = encode/export only.
- [x] PRD v2.1 ingested — delta NVIDIA + GROK.md. IA unchanged.
- [ ] Stability Matrix — **skipped**. Runtime is native ComfyUI.
- [x] Wan 5B native TI2V + Hunyuan 1.5 480p I2V distilled (no GGUF). NVENC encode still later.

## Decisions log
### 2026-09-02
- Project GitHub **AIOSCreator** = CreatorOS PRD v3.0.
- Develop **local-max** di PC ini (RTX 3060 12GB). Bukan Docker-first.
- SQLite + native ComfyUI + native ffmpeg. AtlasNow tetap paused.
- LLM control plane = SpaceXAI/xAI, bukan OpenAI default.
- Design: shadcn/ui + HeliosGen **canvas in AI Studio** (screenshot SoT [[Helios-canvas-ref]]). HOME stays PRD v2 IA. **No antd.**
- Logic: MPT stage machine for UGC Factory. HunyuanVideo not P0 (45–60GB). Wan 2.2 5B stays draft engine.
- **Generate engine P0:** skip Stability Matrix. Native ComfyUI `%LOCALAPPDATA%\Programs\ComfyUI`. First workflow = SD 1.5 `v1-5-pruned-emaonly.safetensors` 512×768. MotionControl node lives on Studio canvas; interim ffmpeg zoompan labeled `ffmpeg-camera-preview`. Wan Move/Mix later.

### 2026-09-05
- Changed: Dropped **ffmpeg camera preview** as a motion engine. Motion = H3 I2V / R2V. ffmpeg stays for NVENC / 4K export only.
- Why: Joe won’t use the 2s zoompan.

### 2026-09-05
- Changed: **Prompt enhance** masuk PRD only ([[Prompt-Enhance-PRD]]). OpenRouter `:free` = LLM rewrite, not image gen. Not built.
- Why: Joe parked the Pinggy/OpenRouter free-API idea before code.

### 2026-09-06
- Changed: Cloud motion **Seedance 2.5** via CometAPI (`POST /v1/videos`, model `seedance-2-5`, still as `input_reference`, poll `GET /v1/videos/{id}`). Key in Settings / `COMETAPI_KEY`. 720p 9:16 I2V 4–30s. Paid, their ToS. H3 R2V stays local default.
- Why: Joe gassed CometAPI Seedance 2.5 as a generate engine.

### 2026-09-05
- Changed: Gas **Wan 2.2 5B** native TI2V + **HunyuanVideo 1.5 480p I2V step-distilled fp8**. H3 R2V stays MotionControl. ffmpeg stays 4K export. No GGUF/city96. No EasyCache.
- Why: Joe gassed video generate + motion control on this 3060. Full Hunyuan 720p/GGUF still blocked.

### 2026-09-05
- Changed: Gas **LTX-2 19B distilled fp8** native Comfy (I2V + audio, 8-step, Gemma FP4 CPU). Not LTX Studio. Not LTX-2.3/2.5 (T1 16GB+). Not GGUF.
- Why: Joe: LTX Video / LTX-2.x is needed in the stack. Unique vs Wan/Hunyuan = native audio; unique vs H3 = faster 8-step official Comfy/NVIDIA path.

### 2026-09-05
- Changed: Gas **Wan Animate 2 INT8 ConvRot** as second MotionControl engine (native `WanAnimate2ToVideo`, LightX2V 6-step LCM, cache CPU). H3 R2V stays default (audio).
- Why: Joe asked for the best free motion-copy; Animate 2 is the 2026 SOTA body/face transfer. Framing must match. Silent.

### 2026-09-05
- Changed: Character **continuity sheet** is the standard set (4:5 bible). Production slots extract panels. Commerce hold/glance stay UGC.
- Why: Joe’s reference-sheet spec. One sheet first on T0.
- Also: Qwen Image Edit 2511 native Comfy live. Prompt-only falls back to Z-Image.
- Next: GEN sheet from a locked identity, then stills one-at-a-time.

### 2026-09-02 (generate wire)
- Changed: ComfyUI native + SD 1.5 + Studio Image/MotionControl GEN.
- Why: Joe asked SM? + pasang ComfyUI + 1 workflow image + kawat ke `/create/studio`.
- Next: FLUX Klein / Wan on 12GB; keep SM optional.

## Links
- [[02 Projects/AIOSCreator/Local-dev-prep]]
- [[02 Projects/AIOSCreator/CreatorOS-PRD-v3-extracted]]
- [[02 Projects/Projects MOC|Projects MOC]]
- [[03 Areas/YouTube & Content]]
- [[03 Areas/Affiliate & Monetization]]
- [[03 Areas/AI Systems]]
- [[03 Areas/SEO-AEO-GEO]]
- [[Home]]
