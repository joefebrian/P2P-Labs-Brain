# Prompt enhance (LLM) — PRD

#decision #project

Status: **spec only. Not built.** Joe 2026-09-05: masuk PRD dulu.

Source: [OpenRouter free models / “unlimited tokens”](https://pinggy.io/blog/free_ai_model_apis_unlimited_tokens_openrouter/) — honest read: **$0/token, not unlimited requests**.

See [[Characters]] · [[PRD-v2.1-delta]] · [[GROK]] · Settings LLM already has OpenRouter free.

## What it is

Cloud **LLM rewrite** of the operator prompt **before** Comfy still/motion. Not a generator. Not an image API.

Use: stop Qwen reading “character reference sheet” as a cartoon bible; expand “orang baru, perawakan sama”; UGC hook/script later.

## What it is not

- Not Z-Image / Qwen / Klein / H3 (those stay local Comfy).
- Not GPT Image 2 / Seedream (paid image APIs).
- Not “unlimited”. Caps: **20 req/min**, **50 req/day** unpaid, **1000/day** after ≥ $10 credits ever purchased.
- Not a production SLA. Free `:free` models rotate, throttle at peak, can vanish.
- Not for stealth models (Owl Alpha etc.) on real-person / customer data — providers may log prompts.

## Control plane

- OpenAI-compatible: `https://openrouter.ai/api/v1` · key in Settings (`data/db/llm-providers.json`, gitignored).
- Default route: `openrouter/free` (auto-pick $0) **or** explicit `:free` IDs with a **fallback list** (do not hardcode one model).
- Prefer for enhance: instruction-following chat. Optional later: Gemma 4 `:free` if we pass a thumbnail (multimodal).
- LLM is not locked to xAI. OpenRouter free is valid Phase 0.

## Product rules

1. **Opt-in.** Button “Enhance” on identity / sheet / slot textarea. Never silent rewrite.
2. **1 click = 1 request.** Show remaining-day is optional; fail with the OpenRouter error if 429.
3. Output lands in the **same textarea**. Operator edits again, then GEN. Comfy still gets the final string.
4. System prompt must: keep identity lock law, keep wardrobe, **photoreal PHOTO not illustration/cartoon/3D/anime** for sheets, no invented GMV, adult fictional OK (local gen is uncensored; cloud LLM may still refuse NSFW — then show the error, don’t swap engine).
5. Lineage: store `llm_model`, `llm_provider`, original prompt vs enhanced, job id.
6. Rights: same preflight as generate. Don’t send real-person intimate refs to stealth/free endpoints that log.

## UI (when built)

- Characters identity + continuity sheet + slot prompts.
- Studio text nodes: later.
- Copy under button: “LLM rewrite · OpenRouter free · not the image engine.”

## Tickets (not this sprint)

- PE-01 Settings already has key → wire `enhancePrompt(text, kind)` using active LLM.
- PE-02 Fallback `models[]` array on OpenRouter.
- PE-03 Enhance on `/create/characters/[id]` sheet + identity.
- PE-04 Don’t call enhance inside Autopilot without a daily cap.

## Out of scope

Local LLM on this 3060. Paid Claude/GPT-5 for enhance. Image-to-prompt as a separate product until Gemma path is proven.
