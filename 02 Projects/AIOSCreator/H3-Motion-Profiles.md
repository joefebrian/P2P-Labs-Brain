# MiniMax H3 — motion profiles (lock, do not build yet)

#decision #project

Source: community 24-run 5090 bench (1MP · 8 steps · 16:9 · native speech · RIFE 2× · RTX 2× upscale · LoRA 0.75) + Comfy-Org native H3 + Kijai FastVideo VSA (experimental).  
Not a 3060 number. **T0 default stays pruned INT8 ConvRot + official I2V/R2V graphs.**

Related: [[GROK]] · [[PRD-v2.1-delta]] · [[Local-dev-prep]]

## What we take (product)

1. **H3 is a profile stack, not one checkpoint.** Operator picks a *lane* (draft / identity / quality), not a filename.
2. **Audio is a first-class fail.** Echo on non-VSA trunks is a ship-blocker for YouTube/UGC. Listen before calling a clip “done.”
3. **Identity and background are different jobs.** Ref2VA Acc 8-step can lock a face and still warp furniture. Product still / set plate from Klein; motion should not restyle the room unless the operator asked.
4. **Post is not generate.** RIFE 2× (fps) + RTX/RealESRGAN 2× (spatial) sit in the **export** lane. Do not label interpolated/upscaled as native 4K or native 48fps. NVIDIA = encoder/upscale, not the generator ([[PRD-v2.1-delta]]).
5. **LoRA at 0.75, not 1.0.** Bench: turbo/acc stacks are ~same wall time (~140s on 5090). Quality and warp differ. Default strength 0.75 until we measure on 3060.
6. **Never mix trunks.** FL2VA LoRA on Ref2VA UNET (or reverse) applies clean and looks silently wrong. Pair FL2V turbo with fl2va weights; Ref2V turbo / Ref2VA Acc with ref2va weights.
7. **8 steps is a quality lane, not T0 proof.** Official native graph is ~20 steps. Turbo/Acc/VSA 4–8 step = later. Don’t advertise 5090 1:25 as this PC.

## Lanes (later picker — not wired)

| Lane | When | Diffusion | LoRA | Post | T0 3060 |
|---|---|---|---|---|---|
| **Draft** | iterate prompt / still | pruned **INT8 ConvRot** FL2VA or Ref2VA (what we download now) | off | none | **P0** — 480×864 · 124f · offload |
| **Identity** | character + motion ref | **Ref2VA** INT8 | Ref2V Turbo 4-step @ 0.75 *or* Ref2VA Acc 8-step @ 0.75 | optional RIFE | after Draft proven; Acc if face slips, watch furniture warp |
| **UGC quality** | influencer / YT, audio matters | **FastVideo VSA** (Kijai experimental) if Comfy core + kitchen land | FL2V Turbo 8-step @ 0.75 only on FL2VA trunk | RIFE 2× then RealESRGAN/NVENC | **not P0** — extra kernel, extra weight, 5090-shaped |
| **Forbidden as default** | — | BF16 (~61GB), native 1MP denoise on 12GB, “RTX 2× = 4K generate” | LoRA 1.0 | Chrome VSR as export | never |

FP8 Scaled: skip on 3060 (Ampere, no FP8 HW). INT8 ConvRot stays the T0 trunk.

## TaoMate-H3 (Hopper cluster only)

Streaming 5s-chunk H3 + audio. **Not a 3060 / Comfy lane.** Auto-install iff GPU inventory says Hopper SM90+ and ≥4×80GB. Spec: [[TaoMate-H3]]. Do not clone on this PC.

## Do not build this sprint

- **Kablex ComfyUI-Ref2VA-VSA custom node** — kitchen CUDA is present on this Comfy 0.34, but **`sol_attn` is not in capabilities**. Their patch fails closed without that kernel. Do not git-clone unpinned.
- FastVideo VSA full checkpoint / 1344×768 (their peak ~13.5GB — over 12GB at that res)
- Ref2VA Acc PDD custom node (`ComfyUI-MiniMax-H3-PDD-Acc`)
- RIFE interpolation node
- Mixing FL2V turbo LoRA onto Ref2VA UNET (or reverse)

## What we took from Kablex (2026-09-07)

Kablex = Ref2VA INT8 + LightX2V **4-step turbo LoRA** + `MiniMaxH3SigmaShift(12,3)` + euler/simple + (optional) VSA gate transplant.

Already on this PC: Ref2VA INT8, CLIP NVFP4, both VAEs, native `MiniMaxH3ReferenceToVideo` + `MiniMaxH3SigmaShift`.

**Wired now:** turbo LoRA path on R2V when the **rank-21** file `minimax_h3_ref2v_turbo_4step_v0.1_comfyui_resized_avg_rank_21_bf16.safetensors` is in `models/loras`. CLIP stays **cpu**. Res stays **448×800**. SaveVideo stays string `mp4/h264` (their nested format broke us once).

**OOM lesson (2026-09-07):**
- Official LightX2V full BF16 LoRA (~1.87GB) → OOM sample 0/4 on 2s 448×800.
- SVD rank-21 (~312MB) on a **fresh** Comfy → still OOM ~6 min in, same 0/4.
- Dense 20-step R2V without LoRA is the only 12GB path that has completed (2s, 512 plate).
- Turbo is **opt-in** `CREATOROS_H3_TURBO=1`. Default stays 20-step dense.
- R2V now lanczos-scales the identity to 448×800 before the Ref2VA node so the 768 plate doesn’t inflate prefix tokens.

**Still gated:** VSA until a Comfy kitchen build exposes `sol_attn`. Then pin Kablex at `92e3f835` — do not `git pull` main.

## Copy

- Allowed: “local H3, native stereo, draft on 3060; quality lane later.”
- Forbidden: “5090 85s is our speed”; “VSA is official MiniMax”; “RIFE+RTX = native 4K.”
