# PRD v2.1 — delta vs v2.0

#decision

Source: [[AI_Creator_Commerce_OS_Master_PRD_v2_1]] · extracted [[PRD-v2.1-extracted]]  
Canonical agent files: [[GROK]] · [[GROK_TERMINAL_INSTRUCTIONS_CreatorOS]]

IA, modules A–J, commerce loop, Amazon-first, official APIs, rights preflight, Autopilot gates = **unchanged from v2.0**. Only take this page as “what’s new.”

## Version lock
- Document version **2.1** · 2 Sep 2026
- Changelog: NVIDIA RTX Local Creator Stack as first-class runtime; NVIDIA-owned free software vs open-source generation; Grok terminal operating instructions

## New locked decisions
- NVIDIA software = **free capability layer** (driver / encoder / filters / precision). **Not** an official unlimited NVIDIA generator.
- Local generation stays **ComfyUI + approved open weights** (Flux Schnell/Klein, Qwen, Wan, LTX; Hunyuan later). Flux Dev = non-commercial unless licensed.
- Default RTX stack: Studio Driver + ComfyUI (FP8 on 40-series, NVFP4 on 50-series, GGUF/offload below) + NVENC encode + Broadcast optional.
- Game Ready driver only if the PC is dual-use gaming.

## This PC = T0 (RTX 3060 12GB)
- Image yes (Klein / Schnell / Qwen). Video = short quantized Wan/LTX only, heavy offload.
- Broadcast **off** during generate.
- NVENC for final encode when present (this PC has NVENC).
- Do not promise 4K native. Do not label Chrome RTX Video as export.

## §33 NVIDIA — what we may use
| Use | Component | Not this |
|---|---|---|
| Workstation | NVIDIA App | Not CreatorOS UI |
| Driver | Studio Driver | Not required to start inference |
| Capture | ShadowPlay | Not an NLE |
| Mic/cam | Broadcast 2.2 | Not TTS |
| Watch upscale | RTX VSR | Never “export 4K from Chrome” |
| Export upscale | Comfy RTX Video node only | |
| Encode | NVENC H.264/HEVC/AV1 | Not generation |
| Precision | NVFP4 / FP8 / GGUF | Not a quality promise |
| Operator helper | G-Assist | Not Script/Growth agent |
| Optional RAG | ChatRTX | Not product claims |
| Dead | NVIDIA Canvas | Do not mention in setup |

Cost: GPU-seconds + electricity. **No NVIDIA per-generation fee.**

## New tickets (P0 first)
NV-001 GPU inventory · NV-002 Settings NVIDIA card · NV-004 NVENC encode · NV-005 precision router · NV-008 no NVIDIA token cost · NV-009 load GROK.md before code.

NVS-01 probe nvidia-smi · NVS-03 gpu_tier + precision_policy · NVS-04 NVENC or log fallback · NVS-05 fail closed on VRAM · NVS-06 never market G-Assist as generator · NVS-07 lineage stores gpu/driver/precision/encoder · NVS-08 copy: local has no NVIDIA token.

## §34 Grok terminal
Load [[GROK]] before CreatorOS implementation. Product is the commerce OS, not a motion toy. Swarm only in product/strategy mode; implementation = ship the ticket.

## H3 motion profiles (Sep 2026, not built)

Community 5090 bench is **reference, not T0 SLA**. Lock: [[H3-Motion-Profiles]].

- T0 generate = Comfy-Org pruned **INT8 ConvRot** FL2VA / Ref2VA. Not BF16, not 1MP native, not FastVideo VSA.
- Later lanes: Identity (Ref2VA + turbo/acc LoRA @ 0.75) · UGC quality (VSA only after core lands) · Export (RIFE fps + RealESRGAN/NVENC spatial).
- Audio echo = fail the clip. Don’t mix FL2VA LoRA onto Ref2VA trunk.
- 5090 85–218s @ 1MP/8-step is their card. 3060 = minutes + RAM offload.

## TaoMate-H3 (streaming MiniMax H3 — not this PC)

Lock: [[TaoMate-H3]]. Repo [TaoLiveAIGC/TaoMate-H3](https://github.com/TaoLiveAIGC/TaoMate-H3).

- **Auto-deploy** only on Linux Hopper SM90+, **≥4 GPUs × ≥80GB**, CUDA 12.8 / PyTorch 2.8. Validated 8×H20 96GB.
- Else hide the engine. No clone, no hopper FlashAttention build, no LoRA pull.
- **T0 3060 Windows: do not build.** Joe 2026-09-13.

## Prompt enhance (LLM, not built)

Cloud rewrite of operator prompts **before** Comfy. Spec: [[Prompt-Enhance-PRD]].

- OpenRouter `:free` = LLM only. $0/token, **request-capped** (50/day unpaid, 1000/day after $10 credits).
- Opt-in Enhance button. Output back to textarea. Image engines stay local.
- Not this sprint. Fallback model list when we build — free IDs rotate.

## Copy rules
- Allowed: unlimited gens on **your GPU**; cost is electricity/time. NVIDIA = engine room, open models paint.
- Forbidden: “NVIDIA unlimited official Sora”; “RTX Video exports 4K from Chrome”; “G-Assist writes scripts.”
