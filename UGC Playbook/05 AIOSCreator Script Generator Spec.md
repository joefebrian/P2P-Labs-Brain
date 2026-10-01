---
tags: [ugc-playbook, aioscreator, spec, script-generator]
title: AIOSCreator Script Generator Spec
version: 1.0
sample_count: 889
---
# AIOSCreator Script Generator Spec

Machine-readable contract that **UGC Factory**, **Faceless VO**, **Winner Hooks**, **Characters**, **MotionControl**, **ShortDrama** and the `grok` CLI use to generate short-form UGC scripts. Every number below comes from the 889-video study (see [[00 UGC Playbook – Index]]) unless marked *(web)*.

Related: [[01 How to Write a UGC Script]] · [[02 Hook Library]] · [[03 CTA & Offer Library]] · [[04 Style Selection Guide]]

## 1. Generation procedure (for the model)
1. Read the **brief** (§2). If `style` is empty, choose one with [[04 Style Selection Guide]] (goal × product type × assets available).
2. Open `Styles/<style>.md`. Use its **beat map** and **timing** as the skeleton, and its **hook formulas** as the starting point.
3. Write 3–5 **hook variants** (§5). Each variant must work on three channels at once: spoken line, on-screen text and first visual. Keep the body the same across the variants so they can be A/B tested *(web: TikTok recommends testing opening variations with the body held constant)*.
4. Fill in the beats. Name the product or show it in the first 3–8 s for short ads (median brand mention in the study: B-Roll+VO about 5 s, Product Demo about 4 s). Long advertorial styles (AI Cartoon, Storytelling) may delay the reveal to about 40–50% of the runtime.
5. Add proof (at least one of: demo, number, review/social proof, authority, guarantee) and **one** CTA. Offer devices come from [[03 CTA & Offer Library]], and you may only use the ones the brief says are true.
6. Add the disclosure (§7) and run the checks (§8). Output **only** JSON that validates against §3, optionally followed by a Markdown render.

## 2. Input brief schema
```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "$id": "aioscreator.brief.v1",
  "type": "object",
  "required": ["product", "goal", "platforms"],
  "properties": {
    "product": {
      "type": "object",
      "required": ["name", "category", "one_liner"],
      "properties": {
        "name": {"type": "string"},
        "category": {"type": "string", "description": "e.g. saas_app, ai_tool, info_product, supplement, skincare, apparel, gadget, food_bev, home, pet"},
        "one_liner": {"type": "string"},
        "key_benefits": {"type": "array", "items": {"type": "string"}, "maxItems": 5},
        "proof_points": {"type": "array", "items": {"type": "string"}, "description": "ONLY true, substantiated claims: numbers, reviews, awards, demos"},
        "offer": {"type": "object", "properties": {
          "discount": {"type": "string"}, "code": {"type": "string"}, "trial": {"type": "string"},
          "guarantee": {"type": "string"}, "bonus": {"type": "string"}, "deadline": {"type": "string"}}},
        "price": {"type": "string"},
        "objections": {"type": "array", "items": {"type": "string"}}
      }
    },
    "audience": {"type": "object", "properties": {
      "persona": {"type": "string"}, "pain_points": {"type": "array", "items": {"type": "string"}},
      "awareness": {"enum": ["unaware", "problem_aware", "solution_aware", "product_aware", "most_aware"]}}},
    "goal": {"enum": ["awareness", "consideration", "conversion", "retargeting", "affiliate_sale", "app_install", "lead"]},
    "platforms": {"type": "array", "items": {"enum": ["tiktok", "reels", "yt_shorts"]}},
    "style": {"type": "string", "description": "One of the 24 style names in Styles/, or empty to auto-select"},
    "talent": {"enum": ["on_camera_creator", "founder", "faceless_vo", "ai_avatar", "ai_cartoon_character", "multi_actor"]},
    "target_duration_s": {"type": "integer", "minimum": 7, "maximum": 180},
    "affiliate": {"type": "boolean", "description": "If true, add the commission disclosure"},
    "language": {"type": "string", "default": "en"},
    "num_hook_variants": {"type": "integer", "default": 3}
  }
}
```

## 3. Output: script object schema
```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "$id": "aioscreator.script.v1",
  "type": "object",
  "required": ["style", "title", "duration_s", "aspect_ratio", "hook_variants", "beats", "cta", "compliance"],
  "properties": {
    "style": {"type": "string"},
    "framework": {"enum": ["HPSPC", "PAS", "AIDA", "BAB", "LISTICLE", "QA_OBJECTION", "STORY_ARC", "DEMO_LOOP", "SKIT_TWIST", "MYTH_TRUTH"],
      "description": "HPSPC = Hook-Problem-Solution-Proof-CTA (the default)"},
    "title": {"type": "string"},
    "duration_s": {"type": "number"},
    "aspect_ratio": {"const": "9:16"},
    "resolution": {"type": "string", "default": "1080x1920"},
    "target_wpm": {"type": "integer", "description": "Words per minute of runtime. Default = style median from §4 (corpus median 187.5); 0 for voiceless"},
    "talent": {"type": "string"},
    "persona_notes": {"type": "string"},
    "hook_variants": {
      "type": "array", "minItems": 1,
      "items": {"type": "object", "required": ["id", "hook_type", "vo", "on_screen_text", "visual"],
        "properties": {
          "id": {"type": "string"},
          "hook_type": {"enum": ["callout", "question", "bold_claim", "negative_warning", "curiosity_gap", "result_first", "comment_reply", "pov", "listicle_number", "story_open", "authority_stat", "price_shock", "relatable_moment", "personified_problem", "myth"]},
          "vo": {"type": "string", "description": "Spoken line, at most about 12 words (fits within 3 s)"},
          "on_screen_text": {"type": "string", "description": "At most 8 words; may differ from the VO"},
          "visual": {"type": "string", "description": "The first frame / first motion; must show something in motion or the problem or result"},
          "source_pattern": {"type": "string", "description": "Hook Library formula id, e.g. H-CALLOUT-03"}}}
    },
    "beats": {
      "type": "array", "minItems": 3,
      "items": {"type": "object", "required": ["beat", "start_s", "end_s", "vo", "on_screen_text", "shot"],
        "properties": {
          "beat": {"enum": ["hook", "problem", "agitate", "reveal", "solution", "demo", "proof", "objection", "offer", "cta", "twist", "story", "reason_1", "reason_2", "reason_3", "reason_4", "reason_5", "before", "after", "bridge"]},
          "start_s": {"type": "number"}, "end_s": {"type": "number"},
          "vo": {"type": "string"},
          "on_screen_text": {"type": "string"},
          "shot": {"type": "object", "properties": {
            "type": {"enum": ["talking_head", "screen_recording", "product_closeup", "b_roll", "green_screen", "split_screen", "pov_handheld", "whiteboard", "motion_graphic", "ai_generated", "street", "reaction_pip", "unboxing_hands"]},
            "framing": {"type": "string"}, "setting": {"type": "string"},
            "b_roll": {"type": "array", "items": {"type": "string"}},
            "motion_control": {"type": "string", "description": "Camera move / MotionControl preset"},
            "sfx_music": {"type": "string"}}},
          "cut_every_s": {"type": "number", "description": "Target cut interval; the study median is about 2-4 s per cut"}}}
    },
    "cta": {"type": "object", "required": ["vo", "on_screen_text"],
      "properties": {"vo": {"type": "string"}, "on_screen_text": {"type": "string"},
        "offer_devices": {"type": "array", "items": {"enum": ["percent_off", "promo_code", "free_trial", "free_shipping", "free_gift", "bundle", "guarantee", "scarcity", "deadline", "price_anchor", "social_proof"]}},
        "placement_s": {"type": "number"}}},
    "captions": {"type": "object", "properties": {
      "style": {"enum": ["word_by_word_bold", "tiktok_native_box", "headline_top", "none"]},
      "safe_zone": {"type": "string", "default": "keep text out of the top 14% and bottom 35% (web: Meta Reels safe zone)"}}},
    "compliance": {"type": "object", "required": ["disclosure_vo", "disclosure_text", "claims_checked"],
      "properties": {"disclosure_vo": {"type": "string"}, "disclosure_text": {"type": "string"},
        "claims_checked": {"type": "boolean"}, "ai_generated_label": {"type": "boolean"}}},
    "production_notes": {"type": "string"},
    "module_routing": {"type": "object", "description": "Which AIOSCreator modules render which parts",
      "properties": {"ugc_factory": {"type": "boolean"}, "faceless_vo": {"type": "boolean"}, "characters": {"type": "boolean"},
        "motion_control": {"type": "boolean"}, "short_drama": {"type": "boolean"}, "winner_hooks": {"type": "boolean"}}}
  }
}
```

## 4. Style → default parameters (from the data)
| Style | Framework | Default length (s) | Talent | Cuts / 10 s | Note |
|---|---|---|---|---|---|
| [[Styles/AI - Cartoon Style|AI - Cartoon Style]] | PAS | 63.5 (IQR 55.4–89.3) | ai_cartoon_character | 3.3 | 169.2 wpm |
| [[Styles/App Walkthrough|App Walkthrough]] | DEMO_LOOP | 29.5 (IQR 18.2–39.1) | on_camera_creator | 2.7 | 228.1 wpm |
| [[Styles/B-Roll + Voiceover|B-Roll + Voiceover]] | HPSPC | 34.5 (IQR 27.0–47.1) | faceless_vo | 5.0 | 191.9 wpm |
| [[Styles/Before & After|Before & After]] | BAB | 38.5 (IQR 18.8–45.5) | on_camera_creator | 3.7 | 178.2 wpm |
| [[Styles/Comment Response|Comment Response]] | QA_OBJECTION | 36.9 (IQR 26.7–50.8) | on_camera_creator | 2.3 | 195.8 wpm |
| [[Styles/Founder-led|Founder-led]] | STORY_ARC | 47.2 (IQR 34.0–56.4) | founder | 6.0 | 196.1 wpm |
| [[Styles/Green Screen|Green Screen]] | HPSPC | 38.6 (IQR 31.6–51.2) | on_camera_creator | 2.9 | 198.7 wpm |
| [[Styles/Listicle|Listicle]] | LISTICLE | 49.6 (IQR 31.4–72.3) | on_camera_creator | 3.5 | 173.8 wpm |
| [[Styles/Live Reaction|Live Reaction]] | HPSPC | 57.6 (IQR 44.2–79.4) | multi_actor | 2.4 | 162.8 wpm |
| [[Styles/Motion Graphics|Motion Graphics]] | AIDA | 8.6 (IQR 7.7–10.3) | faceless_vo | 0.0 | text-led, low VO |
| [[Styles/Myth Bust|Myth Bust]] | MYTH_TRUTH | 49.1 (IQR 44.8–89.5) | on_camera_creator | 3.7 | 192.6 wpm |
| [[Styles/POV|POV]] | HPSPC | 20.4 (IQR 14.2–46.0) | on_camera_creator | 2.3 | 198.0 wpm |
| [[Styles/Problem - Solution|Problem / Solution]] | PAS | 42.3 (IQR 33.2–51.2) | on_camera_creator | 3.9 | 195.8 wpm |
| [[Styles/Product Demo|Product Demo]] | DEMO_LOOP | 35.9 (IQR 26.2–43.7) | on_camera_creator | 3.7 | 180.4 wpm |
| [[Styles/Rage Bait|Rage Bait]] | PAS | 51.6 (IQR 34.8–61.9) | on_camera_creator | 3.4 | 176.3 wpm |
| [[Styles/Skit|Skit]] | SKIT_TWIST | 47.4 (IQR 30.3–65.6) | multi_actor | 3.7 | 195.4 wpm |
| [[Styles/Storytelling|Storytelling]] | STORY_ARC | 61.4 (IQR 52.2–80.0) | on_camera_creator | 4.1 | 203.4 wpm |
| [[Styles/Street Interview|Street Interview]] | HPSPC | 45.5 (IQR 35.6–55.9) | multi_actor | 4.7 | 233.5 wpm |
| [[Styles/Testimonial|Testimonial]] | STORY_ARC | 36.7 (IQR 24.6–55.5) | on_camera_creator | 2.6 | 190.2 wpm |
| [[Styles/Ultra Cinematic|Ultra Cinematic]] | AIDA | 29.1 (IQR 14.9–47.7) | faceless_vo | 5.7 | 160.2 wpm |
| [[Styles/Unboxing|Unboxing]] | DEMO_LOOP | 34.2 (IQR 23.3–38.5) | on_camera_creator | 3.3 | 173.8 wpm |
| [[Styles/Voiceless|Voiceless]] | HPSPC | 15.6 (IQR 11.1–25.6) | faceless_vo | 3.5 | text-led, low VO |
| [[Styles/Whiteboard Explainer|Whiteboard Explainer]] | AIDA | 42.9 (IQR 42.6–52.3) | on_camera_creator | 3.6 | 188.0 wpm |
| [[Styles/Yapping|Yapping]] | STORY_ARC | 42.8 (IQR 36.0–55.1) | on_camera_creator | 0.5 | 198.9 wpm |

## 5. Hook rules (enforced)
- The spoken hook ends by **3.0 s** (about 8–12 words at the corpus pace). The on-screen hook appears in **frame 0** and is **8 words or fewer**. 84% of the study videos showed readable hook text in 0–3 s.
- The hook must name a **who** (callout), a **pain**, a **result**, or a **curiosity gap**. Use [[02 Hook Library]] formula ids.
- The first frame shows motion, the product, the problem, or the result. Never open on a static logo.
- Generate `num_hook_variants` hooks of **different** `hook_type`s.

## 6. Pacing rules
- Talking styles: budget words as duration × style wpm ÷ 60. Corpus median = 187.5 words per minute of runtime (213.5 inside speech segments; fast, native UGC delivery). For AI voices, 170–190 wpm stays intelligible.
- Voiceless / Motion Graphics: 0 VO. Each on-screen text card stays up for at least 1.5 s, at 5–10 words per second maximum *(web)*.
- Cut or visual change every 2–4 s (median 3.6 scene cuts per 10 s across the corpus; faster in B-Roll and Listicle).

## 7. Compliance block (always)
- If `affiliate=true`: `disclosure_vo` = "I earn a commission if you buy through my link." and `disclosure_text` = "#ad · affiliate link". Put both **in the video**, not only in the caption *(web: FTC)*.
- Only use claims from `proof_points`. No medical or income guarantees. Label AI avatars and characters as AI-generated where the platform requires it (several AI-Cartoon samples carry an "AI generated" label).

## 8. Self-check before output
- [ ] Hook ≤ 3 s, and the text hook is in frame 0
- [ ] Product shown or named by 8 s (unless the style is a long advertorial)
- [ ] At least one proof beat
- [ ] Exactly one primary CTA, and the offer is true
- [ ] Beat timings are contiguous and add up to `duration_s`
- [ ] VO word count ≈ duration × target_wpm / 60
- [ ] Disclosure present if the brief is affiliate

## 9. Example output (App Walkthrough, for an AIOSCreator-type affiliate tool)
```json
{
  "style": "App Walkthrough",
  "framework": "DEMO_LOOP",
  "title": "AIOSCreator · App Walkthrough · 'my 5-minute content week'",
  "duration_s": 30,
  "aspect_ratio": "9:16",
  "resolution": "1080x1920",
  "target_wpm": 190,
  "talent": "on_camera_creator",
  "persona_notes": "TikTok Shop affiliate, 20s–30s, posts daily, hates scripting",
  "hook_variants": [
    {
      "id": "A",
      "hook_type": "result_first",
      "vo": "Here's my setup that writes a week of TikTok scripts before my coffee's done.",
      "on_screen_text": "My 5-minute content week",
      "visual": "Creator lifts coffee; laptop shows a full script list",
      "source_pattern": "App Walkthrough formula 1"
    },
    {
      "id": "B",
      "hook_type": "callout",
      "vo": "If you're a TikTok Shop affiliate still writing scripts at midnight, watch this.",
      "on_screen_text": "Affiliates: stop scripting at midnight",
      "visual": "Clock 11:58pm, blank doc",
      "source_pattern": "H-CALLOUT"
    },
    {
      "id": "C",
      "hook_type": "curiosity_gap",
      "vo": "What experienced affiliates won't tell you about their scripts.",
      "on_screen_text": "Their secret isn't talent",
      "visual": "Creator leans into lens",
      "source_pattern": "App Walkthrough formula 4"
    }
  ],
  "beats": [
    {
      "beat": "hook",
      "start_s": 0,
      "end_s": 3,
      "vo": "(hook variant)",
      "on_screen_text": "(hook variant)",
      "shot": {
        "type": "talking_head",
        "framing": "medium close-up",
        "setting": "desk"
      },
      "cut_every_s": 3
    },
    {
      "beat": "solution",
      "start_s": 3,
      "end_s": 6,
      "vo": "It's called AIOSCreator, and it runs right on my laptop.",
      "on_screen_text": "AIOSCreator (local-first)",
      "shot": {
        "type": "screen_recording",
        "b_roll": [
          "dashboard launch"
        ]
      },
      "cut_every_s": 3
    },
    {
      "beat": "demo",
      "start_s": 6,
      "end_s": 12,
      "vo": "I paste the product link and it pulls the benefits and reviews for me.",
      "on_screen_text": "1. Paste link",
      "shot": {
        "type": "screen_recording",
        "b_roll": [
          "link paste → product card"
        ],
        "motion_control": "slow push-in on cursor"
      },
      "cut_every_s": 2.5
    },
    {
      "beat": "demo",
      "start_s": 12,
      "end_s": 18,
      "vo": "UGC Factory writes scripts in whatever style I want: problem-solution, POV, listicle.",
      "on_screen_text": "2. Pick a style",
      "shot": {
        "type": "screen_recording",
        "b_roll": [
          "style grid → script cards"
        ]
      },
      "cut_every_s": 2.5
    },
    {
      "beat": "demo",
      "start_s": 18,
      "end_s": 24,
      "vo": "Winner Hooks gives me three openers per script, and Faceless VO reads them if I'm not filming.",
      "on_screen_text": "3. Hooks + voice",
      "shot": {
        "type": "screen_recording",
        "b_roll": [
          "hook list",
          "audio waveform"
        ]
      },
      "cut_every_s": 3
    },
    {
      "beat": "proof",
      "start_s": 24,
      "end_s": 28,
      "vo": "That used to be my whole Sunday. Now it's {N} minutes.",
      "on_screen_text": "{X} hrs → {N} min",
      "shot": {
        "type": "b_roll",
        "b_roll": [
          "calendar full of scheduled posts"
        ]
      },
      "cut_every_s": 4
    },
    {
      "beat": "cta",
      "start_s": 28,
      "end_s": 30,
      "vo": "Link's below. {Trial/offer}. I earn a commission if you use it.",
      "on_screen_text": "Try AIOSCreator · #ad · affiliate link",
      "shot": {
        "type": "talking_head"
      }
    }
  ],
  "cta": {
    "vo": "Link's below. {Trial/offer}.",
    "on_screen_text": "Try AIOSCreator · link below",
    "offer_devices": [
      "free_trial"
    ],
    "placement_s": 28
  },
  "captions": {
    "style": "tiktok_native_box",
    "safe_zone": "top 14% / bottom 35% clear"
  },
  "compliance": {
    "disclosure_vo": "I earn a commission if you use my link.",
    "disclosure_text": "#ad · affiliate link",
    "claims_checked": false,
    "ai_generated_label": false
  },
  "production_notes": "Replace {N}/{X}/{Trial} with verified facts before rendering. Screen recording at 110–130% zoom on taps.",
  "module_routing": {
    "ugc_factory": true,
    "faceless_vo": false,
    "characters": false,
    "motion_control": true,
    "short_drama": false,
    "winner_hooks": true
  }
}
```
