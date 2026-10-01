# TaoMate-H3 — streaming H3 (PRD, not this PC)

#decision #project

Source: [TaoLiveAIGC/TaoMate-H3](https://github.com/TaoLiveAIGC/TaoMate-H3) · HF [TaoLiveAIGC/TaoMate-H3](https://huggingface.co/TaoLiveAIGC/TaoMate-H3)  
Powered by MiniMax H3 FL2VA. Alibaba TaoLive AIGC. License = MiniMax H3 Community License.

Related: [[GROK]] · [[PRD-v2.1-delta]] · [[H3-Motion-Profiles]]

## What it is

Low-latency **streaming audio+video** runtime on MiniMax H3. 5s chunks, 3-step LoRA, KV-cache continuity, 480p / 768p / 1080p. Not a Comfy node. Not T0 3060.

Validated: **8 × NVIDIA H20 96GB** (Hopper SM90), Linux, CUDA 12.8, PyTorch 2.8, TP2 + Ulysses. Also `--gpus 4`. Peak DiT ~31 GB **per GPU** in their 8×H20 bench.

## Auto-deploy (product)

On boot / GPU inventory (NV-001 / NVS-01):

1. Probe `nvidia-smi` + compute capability.
2. **Install + wire TaoMate-H3** only if **all** of:
   - Linux (not Windows Phase 0)
   - Hopper **SM 9.0+** (H100 / H200 / H20 / GB200 class). Not Ampere, not Ada, not 3060/4090.
   - **≥ 4** GPUs, each **≥ 80 GB** VRAM
   - CUDA **12.8** + PyTorch **2.8** stack available
3. Else: engine **hidden**. No clone, no `flash-attention/hopper` build, no LoRA download, no vLLM.

Fail closed. Do not “try INT8 on 3060.” This is a **multi-Hopper node** lane.

## This PC (T0 RTX 3060 12GB SM 8.6 Ampere, Windows)

**Do not build. Do not clone. Do not pip install.**  
Joe 2026-09-13: masuk PRD + auto-deploy on compatible GPUs only.

T0 H3 stays Comfy pruned INT8 FL2VA / Ref2VA + chunked I2V.

## When it does deploy

- New motion engine: **H3 stream (TaoMate)** — 5s-aligned duration, 480/768/1088 short-edge.
- NVIDIA still = encoder/upscale only. TaoMate paints.
- Do not advertise 8×H20 17s first-playable as 3060 speed.
- Pin git SHA + LoRA (`adapter_model.safetensors` rank 128 step-3000 EMA) when we wire. No unpinned `git pull`.

## Copy

- Allowed: “streaming H3 on Hopper nodes (4–8× H20-class); auto-on if the box qualifies.”
- Forbidden: “TaoMate on 3060”; “11× faster H3 on this PC.”
