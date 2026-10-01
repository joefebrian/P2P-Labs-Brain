---
tags: [ugc-playbook, moc, index]
sample_count: 1025
videos_analysed: 889
---
# UGC Playbook – Index

Map of content for the AIOSCreator UGC script and style playbook. It is built from a frame-by-frame and transcript study of the Drive folder of UGC sample ads, blended with current platform guidance. Written so that people **and** the `grok` CLI / UGC Factory can generate scripts from it.

## Start here
1. [[01 How to Write a UGC Script]]: the master method and fill-in template
2. [[04 Style Selection Guide]]: which of the 24 styles to use for which product and goal
3. [[02 Hook Library]]: 203 real hooks, categorised
4. [[03 CTA & Offer Library]]: 65 real CTAs plus offer-device statistics
5. [[05 AIOSCreator Script Generator Spec]]: JSON schema and rules for machine generation
6. [[06 AIOSCreator Factory 33 Templates]]: the 33 recipes currently wired in UGC Factory

## Styles (24)
- [[Styles/AI - Cartoon Style|AI - Cartoon Style]] (42 files · median 63.5 s)
- [[Styles/App Walkthrough|App Walkthrough]] (12 files · median 29.5 s)
- [[Styles/B-Roll + Voiceover|B-Roll + Voiceover]] (160 files · median 34.5 s)
- [[Styles/Before & After|Before & After]] (59 files · median 38.5 s)
- [[Styles/Comment Response|Comment Response]] (66 files · median 36.9 s)
- [[Styles/Founder-led|Founder-led]] (22 files · median 47.2 s)
- [[Styles/Green Screen|Green Screen]] (34 files · median 38.6 s)
- [[Styles/Listicle|Listicle]] (75 files · median 49.6 s)
- [[Styles/Live Reaction|Live Reaction]] (14 files · median 57.6 s)
- [[Styles/Motion Graphics|Motion Graphics]] (12 files · median 8.6 s)
- [[Styles/Myth Bust|Myth Bust]] (5 files · median 49.1 s)
- [[Styles/POV|POV]] (24 files · median 20.4 s)
- [[Styles/Problem - Solution|Problem / Solution]] (102 files · median 42.3 s)
- [[Styles/Product Demo|Product Demo]] (53 files · median 35.9 s)
- [[Styles/Rage Bait|Rage Bait]] (19 files · median 51.6 s)
- [[Styles/Skit|Skit]] (37 files · median 47.4 s)
- [[Styles/Storytelling|Storytelling]] (12 files · median 61.4 s)
- [[Styles/Street Interview|Street Interview]] (14 files · median 45.5 s)
- [[Styles/Testimonial|Testimonial]] (53 files · median 36.7 s)
- [[Styles/Ultra Cinematic|Ultra Cinematic]] (39 files · median 29.1 s)
- [[Styles/Unboxing|Unboxing]] (20 files · median 34.2 s)
- [[Styles/Voiceless|Voiceless]] (69 files · median 15.6 s)
- [[Styles/Whiteboard Explainer|Whiteboard Explainer]] (7 files · median 42.9 s)
- [[Styles/Yapping|Yapping]] (75 files · median 42.8 s)

## Headline findings (data)
1. **Vertical and short-to-mid length.** 86% of the 889 analysed videos are 9:16. Median length is 38.0 s (IQR 25.5–53.6 s). Short formats (Motion Graphics about 8.6 s, POV about 20.4 s) and long advertorials (AI Cartoon about 63.5 s, Storytelling about 61.4 s) sit at the extremes.
2. **The hook is double-channelled.** 84% show readable hook text in the first 3 s (OCR, a conservative lower bound). The spoken hook is one sentence that ends by about 3 s, and 33% of speaking videos say 'you/your' in the first 3 s.
3. **Fast talk, frequent cuts.** The median pace is 187.5 words per minute of runtime (213.5 inside speech segments) (median 131.0 words per video), with about 3.6 detected scene cuts per 10 s, i.e. a visual change every ~3 s.
4. **Product early in short ads, late in advertorials.** The brand is first spoken at a median of 10.8 s overall. App Walkthrough is at 6.5 s, while the AI Cartoon advertorials are at 25.8 s.
5. **Offers are stacked.** Across all videos: urgency language 21%, guarantee/risk-free 10%, price anchors 11%, % off 7%, scarcity 6%, free gift 3%. 48% of speaking videos close with an explicit verbal CTA.
6. **Sound-off matters.** 19% of videos have fewer than 15 spoken words (Voiceless, Motion Graphics, POV, many Ultra Cinematic). For these, on-screen text is the script.
7. **The library is DTC-heavy.** It is dominated by supplements, apparel/shapewear, beauty, food, travel and cookware brands (Supplements & wellness 284, Apparel & shapewear 166, Beauty & skincare 126, Travel & accessories 106, Food & beverage 75). Software and creator tools (Canva, Motion, Linktree, Calm, Remini, Hormozi/Acquisition.com) appear mainly in App Walkthrough, Problem/Solution, Skit, POV, Testimonial and Founder-led. Those are the closest templates for AIOSCreator.

## Dataset & method
- Source: Google Drive folder with 1025 files across 24 style folders (911 mp4 videos, 114 images). No scripts or text files existed in the folder.
- Processed: 889 videos (transcript with word timestamps via faster-whisper `small`; ffprobe metadata; keyframes at 0/1/3 s then every 5 s; tesseract OCR; ffmpeg scene-cut detection). Skipped 22 exact-size duplicates (listed in `Data/skipped_duplicates.csv`). Failed: 0. Images OCR'd: 114.
- Keyframe contact sheets for about 10 videos per style (all videos where fewer) were reviewed by eye to describe the visual style.
- Caveats: there is no performance data (views/CTR/ROAS), so 'strongest' means best-crafted, not proven winners. OCR is noisy on stylised captions. Cut counts are estimates (threshold 0.30). Some non-English/misdetected transcripts were re-run with forced English.

## Data files
- `Data/per_video_summary.csv`: one row per video (style, file, duration, word count, wpm, hook text, CTA text, brand, category, offers…)
- `Data/style_stats.csv`: per-style aggregates
- `Data/images_summary.csv`: static image ads with dimensions and OCR
- `Data/skipped_duplicates.csv`

## All styles at a glance
| Style | Files | Videos analysed | Median length (s) | wpm (runtime) | Cuts/10 s | Low-speech | Verbal CTA | Top categories |
|---|---|---|---|---|---|---|---|---|
| [[Styles/AI - Cartoon Style|AI - Cartoon Style]] | 42 | 42 | 63.5 | 169.2 | 3.3 | 5% | 62% | Supplements & wellness, Pet |
| [[Styles/App Walkthrough|App Walkthrough]] | 12 | 11 | 29.5 | 228.1 | 2.7 | 36% | 86% | Software, apps & info, Apparel & shapewear |
| [[Styles/B-Roll + Voiceover|B-Roll + Voiceover]] | 160 | 156 | 34.5 | 191.9 | 5.0 | 3% | 51% | Beauty & skincare, Apparel & shapewear |
| [[Styles/Before & After|Before & After]] | 59 | 37 | 38.5 | 178.2 | 3.7 | 30% | 58% | Beauty & skincare, Apparel & shapewear |
| [[Styles/Comment Response|Comment Response]] | 66 | 46 | 36.9 | 195.8 | 2.3 | 24% | 46% | Food & beverage, Supplements & wellness |
| [[Styles/Founder-led|Founder-led]] | 22 | 19 | 47.2 | 196.1 | 6.0 | 0% | 26% | Beauty & skincare, Supplements & wellness |
| [[Styles/Green Screen|Green Screen]] | 34 | 31 | 38.6 | 198.7 | 2.9 | 3% | 50% | Supplements & wellness, Beauty & skincare |
| [[Styles/Listicle|Listicle]] | 75 | 58 | 49.6 | 173.8 | 3.5 | 14% | 68% | Apparel & shapewear, Supplements & wellness |
| [[Styles/Live Reaction|Live Reaction]] | 14 | 14 | 57.6 | 162.8 | 2.4 | 0% | 29% | Apparel & shapewear, Food & beverage |
| [[Styles/Motion Graphics|Motion Graphics]] | 12 | 12 | 8.6 | 155.2 | 0.0 | 83% | 50% | Supplements & wellness, Travel & accessories |
| [[Styles/Myth Bust|Myth Bust]] | 5 | 5 | 49.1 | 192.6 | 3.7 | 0% | 80% | Supplements & wellness, Apparel & shapewear |
| [[Styles/POV|POV]] | 24 | 23 | 20.4 | 198.0 | 2.3 | 43% | 46% | Beauty & skincare, Supplements & wellness |
| [[Styles/Problem - Solution|Problem / Solution]] | 102 | 87 | 42.3 | 195.8 | 3.9 | 3% | 44% | Apparel & shapewear, Supplements & wellness |
| [[Styles/Product Demo|Product Demo]] | 53 | 50 | 35.9 | 180.4 | 3.7 | 14% | 47% | Apparel & shapewear, Supplements & wellness |
| [[Styles/Rage Bait|Rage Bait]] | 19 | 17 | 51.6 | 176.3 | 3.4 | 12% | 60% | Travel & accessories, Apparel & shapewear |
| [[Styles/Skit|Skit]] | 37 | 32 | 47.4 | 195.4 | 3.7 | 12% | 57% | Supplements & wellness, Food & beverage |
| [[Styles/Storytelling|Storytelling]] | 12 | 12 | 61.4 | 203.4 | 4.1 | 0% | 50% | Travel & accessories, Supplements & wellness |
| [[Styles/Street Interview|Street Interview]] | 14 | 14 | 45.5 | 233.5 | 4.7 | 0% | 57% | Food & beverage, Supplements & wellness |
| [[Styles/Testimonial|Testimonial]] | 53 | 19 | 36.7 | 190.2 | 2.6 | 32% | 46% | Supplements & wellness, Travel & accessories |
| [[Styles/Ultra Cinematic|Ultra Cinematic]] | 39 | 39 | 29.1 | 160.2 | 5.7 | 36% | 20% | Supplements & wellness, Home & kitchen |
| [[Styles/Unboxing|Unboxing]] | 20 | 20 | 34.2 | 173.8 | 3.3 | 40% | 50% | Home & kitchen, Other/unclassified |
| [[Styles/Voiceless|Voiceless]] | 69 | 66 | 15.6 | 63.0 | 3.5 | 97% | 0% | Supplements & wellness, Apparel & shapewear |
| [[Styles/Whiteboard Explainer|Whiteboard Explainer]] | 7 | 5 | 42.9 | 188.0 | 3.6 | 0% | 40% | Supplements & wellness, Food & beverage |
| [[Styles/Yapping|Yapping]] | 75 | 74 | 42.8 | 198.9 | 0.5 | 0% | 24% | Supplements & wellness, Other/unclassified |