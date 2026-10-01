P2P LABS  ·  CREATOROS
MASTER PRODUCT REQUIREMENTS DOCUMENT
CreatorOS
Local-first AI Social Media Operating System
Unlimited local image and video generation at the highest resolution the operator hardware can finish. Official social distribution. Monetization through shop, affiliate, and platform payouts — not through metering pixels.
Document version
3.0  —  replaces Master PRD v2.0 (2 Sep 2026)
Status
Master PRD — Product + Engineering + GTM
Date
2 September 2026
Working name
CreatorOS (replaceable codename)
Deployment
Local-first  ·  Hybrid target  ·  optional Cloud
Primary outcome
Attributable social-commerce profit from AI-produced content
Wedge
Unlimited local generation. No per-clip application fee.
Money
TikTok Shop · YouTube Shopping / Amazon tags · Shopee · affiliate · Rewards
Non-goal
A new public social network competing with TikTok / Instagram
PRODUCT PROMISE (LOCKED)
Give CreatorOS products, characters, accounts and a revenue goal. It generates unlimited local images and video at the highest resolution the machine can finish, packages platform-native derivatives, publishes through official APIs, and scales the combinations that actually make shop and affiliate money. Do not print “unlimited 4K” in the promise sentence.
0. Document Control and Locked Decisions
0.1 Version history
Version
Date
Summary
1.0
31 Aug 2026
Free Motion Control product concept.
1.5
2 Sep 2026
Local ComfyUI, character rights, consent-aware adult workflows.
2.0
2 Sep 2026
Unified MotionControl + Helios-style studio + UGC affiliate + social loop.
3.0
2 Sep 2026
Pivot lock: local social OS, unlimited local gen wedge, social-commerce monetization, official-API hostility, resolution doctrine, anti-slop publish caps.
0.2 What changed from v2.0 and why
The root product is still an AI Creator Commerce OS. v3.0 makes the social-workspace feel first-class and kills the idea of building a public For-You network.
Generation is the acquisition wedge, not the business model. Local pixels are free. Paid features buy leverage: cloud burst, 4K/8K upscale, seats, Autopilot, premium packs.
“Highest resolution” is a pipeline (draft → winner → hero), not a single toggle. Social platforms get 1080×1920 derivatives. 4K lives in the local library.
Distribution is official-API only. TikTok Inbox Upload and YouTube private-until-audit are the MVP paths. Unofficial bots are a product ban.
YouTube is dual-track: Short for reach, long-form companion for clickable affiliate links and watch hours. Shorts description URLs do not click.
Anti-slop gates are MVP, not Phase 5. Unlimited generation is allowed. Unlimited identical publication will get YouTube channels demonetized under the 16 Jul 2026 inauthentic-content policy.
Commerce provider order for this user (WIB / SEA-relevant): Amazon + TikTok Shop + Shopee as P0. YouTube Shopping tags and Meta shopping as P1.
2026 generation stack updated: FLUX.2 Klein 4B, Wan 2.2, Wan 2.7, LTX-2.5, Wan Animate Move/Mix, optional closed-model adapters. Wan 3.0 is treated as a Comfy partner/API node until open weights are confirmed.
0.3 Locked product decisions
Decision
Lock
Product class
Local-first AI Social Media Operating System. Not a TikTok clone. Not a Fediverse app. Not a credit-metered gen studio.
Local social meaning
1) Local gen + local asset ownership. 2) Workspace that feels like running a network (live pipeline, internal feed, multi-account, inbox). 3) Official publish APIs. 4) ActivityPub/PeerTube = Phase 6 adapter only.
Unlimited
No per-generation application fee on local compute. Hardware, VRAM, electricity and time remain real limits.
Highest resolution
Draft 480p/720p → QA → winner 1080p → paid/hero 4K/8K upscale. Social default publish = 1080×1920 H.264 30fps.
Master vs derivative
One local master per ContentAsset. Per-platform derivatives with their own encode, audio strategy and disclosure pack.
Money
Social commerce first: Shop GMV, affiliate EPC, YouTube Shopping tags, Creator Rewards on ≥61s TikToks. SaaS seats are secondary.
Paid features that are OK
Cloud GPU burst, 4K/8K queue, multi-workspace seats, Autopilot, premium motion/character packs, priority closed-model routing, extra social seats.
Paid features that are NOT OK
Per local generation. Watermark on local export. Resolution lock on local renders. Fake “unlimited” that silently queues for hours.
Publish rule
Official APIs or export pack. Never unofficial mobile automation. Never scrape Creative Center. Never use TikTok Research API commercially.
TikTok MVP
Inbox Upload (video.upload) first. Direct Post behind feature flag until Content Posting audit clears.
YouTube MVP
Data API v3 resumable upload. Short + long-form companion. Shopping = Studio handoff. No Content API for Shopping (sunset 18 Aug 2026).
Anti-slop
Default 3–5 public YouTube posts/channel/day. Diversity gate. Scale Winner mutates one variable. Human approval default ON.
AIGC labels
TikTok is_aigc=true default. YouTube containsSyntheticMedia=true on photoreal. C2PA embed is opt-in Developer Mode only.
Music
Per-platform licensed audio. No trending TikTok Sounds burned into commercial or YouTube renders.
Rights
Permission is a data object. Non-consensual intimate generation is not a supported mode.
ComfyUI role
Local inference runtime. CreatorOS owns objects, rights, jobs, lineage, routing.
HeliosGen role
UX and local-workflow reference. Not merged as the product.
North star
Affiliate contribution profit per 1,000 AI-generated content views.
1. Executive Summary
CreatorOS is a local-first operating system for social-commerce content. An operator gives it products, persistent AI creators, social accounts and a revenue goal. The system researches opportunities, writes platform-native scripts, generates images and video on local GPUs at no per-clip fee, transfers motion onto characters, packages platform derivatives, publishes through official APIs or export packs, measures what made money, and mutates only the winning combinations.
This is not another generator. Generation is one stage. Every asset is tied to product, creator, hook, motion, workflow, account, campaign and revenue. The moat is the accumulated relationship between those objects — Creative DNA — not the foundation model of the week.
1.1 Why this product exists in September 2026
Cloud gen studios (Runway, Pika, Kling, Veo, Higgsfield) meter credits. Runway Gen-4.5 is about $1.44 per 5 seconds. Affiliate operators who need 250+ pieces a month cannot live there.
CapCut / Dreamina win finishing and templates. They do not own commerce attribution or a closed learning loop.
UGC ad factories (Creatify, MakeUGC, Arcads, HeyGen) sell avatar ads. Cloud only. No local ownership. No Creative DNA.
Fediverse clones (Pixelfed ~1.2M users, PeerTube, Loops) have no shop loop. Building a public For-You network is a different company with moderation, CSAM, music-rights and network-effect costs we will not pay in MVP.
The gap nobody owns as one product: unlimited local gen + official multi-platform publish + shop/affiliate attribution + winner mutation.
1.2 2026 market facts this PRD is built on
Fact
Number
Why it matters
TikTok Shop GMV 2026
$112.2B global; US $20.6–23.4B
Primary commerce surface. Creators/affiliates drive ~42%.
LIVE share of Shop GMV
~26%, CVR ~7.8%
Talking-demo format matters. LIVE ingest is not an MVP API.
Creator brand spend 2026
$32.6B; creators keep >$21B
Money is in creator-owned commerce, not only ads-share.
YouTube Shopping × Amazon
Live 27 Aug 2026
Tags beat description links by >110% clicks. Shorts URLs do not click.
YT Shopping floor
500 subscribers (Mar 2026)
Commerce is available far below YPP ads.
YPP ads cliff
1 Feb 2027: 8k hours or 20M Shorts views / 90d
Do not optimize new channels for Shorts ads.
Shopee × YT / IG
SEA live Sep 2026
P0 provider for WIB / SEA operators.
Nano engagement
10.3% ER vs mega 1–2%
Volume of nano UGC beats celebrity deals.
Local Wan 2.2 720p / 5s
2–4 min on 16GB; ~$0 on owned GPU
Unlimited local is economically real.
Wan 2.7 4K on 16GB
15–30+ min / clip, impractical
Never promise native 4K on every job.
1.3 Core operating loop
Market intelligence → product opportunity → content strategy → local AI / UGC production → MotionControl / edit → platform packager → official publish or export → engagement → shop / affiliate / rewards event → analytics → Creative DNA extraction → controlled mutation → next batch.
2. Problem, Vision and Product Thesis
2.1 Problems
Social-commerce teams run research, scripting, generation, editing, publishing and analytics in disconnected tools. Learnings die in spreadsheets.
Most AI video products optimize for pretty frames. They do not know whether the content sold.
Cloud generation makes high-volume UGC expensive. “Unlimited” cloud plans are credit cliffs or low-res relaxed queues. Runway retired Unlimited for new customers in June 2026.
Local ComfyUI is powerful and cheap, and almost unusable as a business system: no product object, no rights preflight, no lineage, no publish compliance, no attribution.
Official social APIs are usable and hostile. Unaudited TikTok Direct Post is private. Unverified YouTube projects stay private. Shorts description links do not click. Music does not travel across platforms.
Platforms are punishing AI slop. YouTube’s 16 Jul 2026 inauthentic-content policy demonetizes generic templated mass production at channel level. Unlimited publication of clones is how we die.
2.2 Vision
An operator sits in one local-first workspace that feels like a live social network control room — research, write, film, publish, engage, learn, convert — and the system compounds toward affiliate profit, GMV, leads or booked calls inside explicit budgets, rights and approval rules.
2.3 Product thesis
THESIS
The moat is not the underlying generation model. The moat is the accumulated relationship between Product Data + Creator Identity + Creative DNA + Distribution Context + Performance Data + Revenue Attribution. Local unlimited generation is how we get enough at-bats. Official social commerce is how those at-bats pay.
3. Goals, Non-Goals and Success Metrics
3.1 Product goals
From a product URL + creator profile, produce a platform pack: TikTok cuts, YouTube Short, YouTube companion, IG Reel + carousel, FB/Threads/WA Status derivatives.
Run unlimited local image/video jobs with no per-clip application fee. Route by VRAM. Draft cheap, upscale winners.
Keep persistent AI creator identity, voice and motion reusable across hundreds of outputs.
Publish through official APIs where audited and allowed. Otherwise deliver an export pack that a human can finish in the native app.
Attribute shop/affiliate/rewards revenue down to creative components. Scale only winners.
Autopilot only after attribution quality exists, and never as silent public posting.
3.2 Non-goals for MVP
Building a new foundation video model.
Building a public social network, ActivityPub server, or For-You recommendation graph.
Supporting every affiliate network at launch.
Fully autonomous public posting on every platform.
Native 4K on every generation.
Unlimited free cloud GPU.
High-end NLE replacement for Premiere / CapCut desktop.
TikTok Research API, Creative Center scraping, unofficial posting bots.
YouTube Content API for Shopping (sunset 18 Aug 2026).
Sora API (winds down 24 Sep 2026).
AI-persona expert content in health, legal, finance or politics.
3.3 North star and KPI hierarchy
Metric
Definition
Why it matters
North star
Affiliate contribution profit / 1,000 AI-generated views
Ties reach, conversion and generation cost.
Content profit
Attributed commission + Shop GMV commission + Rewards − gen cost − paid boost
Primary creative economics.
EPC
Affiliate earnings / affiliate clicks
Commerce efficiency.
Shop GMV attributed
Orders × price from Shop / Shopping / Shopee APIs
Volume surface.
Winner rate
% of published items above configured threshold after min sample
Learning quality.
Generation success
Usable outputs / submitted jobs
Production reliability. Beta target ≥90%.
Cost per usable video
AI + GPU + processing / usable outputs
Unit economics. Local target ≈ electricity only.
Publish compliance
% of posts with correct AIGC + commercial disclosure + music strategy
Account survival metric.
Diversity pass rate
% of scheduled posts that pass anti-slop gate first try
YPP / spam survival.
4. Users and Jobs-to-be-Done
Persona
Primary job
Key needs
Affiliate operator
Turn product URLs into profitable volume
Import, score, 3-pack UGC, links, publish, attribution
AI creator network operator
Run persistent AI creators across niches
Identity, voice, motion library, account portfolio
Social manager
Plan and ship platform-native content
Calendar, approval, quotas, export fallback
Performance marketer
Find combinations that make money
Creative DNA, experiments, Scale Winner
Local AI power user
Generate privately at hardware max
ComfyUI, model manager, offline, no per-clip fee
Agency / brand team
Operate client workspaces
Isolation, roles, cost/revenue, approval
4.1 Core jobs
When I find a product, give me a platform pack today so I can test demand.
When something wins, tell me why and mutate one variable.
When I create an AI creator, keep face, body, style and voice stable across hundreds of outputs.
When I have a reference movement, transfer it without building a ComfyUI graph by hand.
When I run locally, I pay zero per clip and keep private assets on disk.
When I manage many accounts, show remaining daily API quotas, what is live, and what made money.
5. Information Architecture
HOME is an operator social workspace, not a reporting dashboard. The uploaded Structure Webworks reference video is the design source of truth for the control plane: one engine, seven modules lighting in sequence, pipeline state on screen, revenue visible.
5.1 Primary nav
Area
Contains
HOME
Live pipeline ticker, modules live 0/7, today’s queue, revenue today, internal content feed, winner chips
INTELLIGENCE
Research, trends, opportunities, pinned / excluded items
COMMERCE
Products, affiliate programs, Shop collabs, campaigns
CREATE
AI Studio, UGC Factory, MotionControl, Characters, Motion Library, Assets
DISTRIBUTE
Calendar, publish queue, accounts, quotas, export packs
GROW
Engagement inbox, analytics, revenue, Growth Engine
SYSTEM
Workflows, models, ComfyUI, identity rights, settings, kill switches
5.2 HOME pipeline states
RESEARCHING → WRITING → FILMING → PUBLISHING → ENGAGING → LEARNING → CONVERTING → LIVE. Each state maps to a real job in the orchestrator. Fake animation without a backing job is banned.
5.3 Global objects
Workspace, Product, Affiliate Offer, Character, Voice, Motion, Creative Brief, Hook, Script, Content Asset (master + derivatives), Campaign, Social Account (with subtype), Publication, Generation Job, Workflow, Conversion Event, Creative DNA, Experiment, Consent / Rights Record, Spark Auth Code, Shopping Handoff Payload.
6. End-to-End Operating Loop
Detect opportunity from internal winners, product feeds and operator-supplied research.
Import / score product. Explain the score.
Generate angles, hooks, format SKUs.
Choose creator + voice + motion + workflow.
Generate local draft at 480p/720p.
QA. Upscale winners to 1080p. Optional paid 4K.
Assemble UGC. Emit platform pack + disclosure + audio strategy.
Human approval. Rights preflight. Anti-slop gate. Quota reserve.
Official publish or inbox/export fallback.
Ingest metrics + shop/affiliate/rewards events.
Score organic winner vs revenue winner separately.
Scale Winner: mutate one variable, keep the rest.
6.1 Killer MVP journey
INPUT → OUTPUT
Paste an Amazon or Shopee product URL → select an AI creator → choose TikTok Review + YouTube Short. Output: three 9:16 UGC drafts, a 61–90s Rewards cut if the concept can hold it, a YouTube Short package with containsSyntheticMedia + disclosure footer, a long-form companion script with clickable affiliate URLs, captions, CTA, affiliate link, and an export pack if APIs are blocked.
7. Module A — Intelligence and Research
Answer: what should we create and promote now? Ranked opportunities from legal sources only.
7.1 Allowed sources
Affiliate / Shop product feeds and official marketplace APIs.
Internal historical content performance and conversion data.
Operator-supplied URLs, files, Creative Center screenshots they pasted themselves.
Google Trends and other licensed public trend inputs.
7.2 Forbidden sources
TikTok Research API (academic / non-profit only).
Commercial Content API used as a SaaS trend engine.
Scraping TikTok Creative Center, FYP, or any unofficial HTML.
7.3 Requirements
ID
Requirement
P
INT-01
Store research observations with source, timestamp, market, platform.
P0
INT-02
Rank products/topics with configurable opportunity scoring.
P0
INT-03
Promote winning internal hooks back into research.
P0
INT-04
Trace recommendation → underlying signals.
P0
INT-05
Manual pin / exclude override.
P1
INT-06
Content-gap and format recommendations from the locked format SKU matrix.
P1
8. Module B — Commerce and Affiliate Engine
Provider-agnostic. Amazon is the first implementation. TikTok Shop and Shopee are P0 because this product is social-commerce-first and SEA-relevant. YouTube Shopping tags are P1 because there is no public write API yet.
8.1 Providers
AmazonProvider — URL/ASIN import, media, features, Associates/Influencer link, YT Shopping handoff payload.
TikTokShopProvider — Affiliate Creator API v202405: open-collab search, showcase, general/publisher link generate, shoppable video upload. Separate OAuth from TT4D. Feature-flag OFF for UK/EU.
ShopeeProvider — affiliate link + commission fields + IG/FB/YT Shopping where live.
YouTubeShoppingProvider — eligibility badge + Studio handoff. Merchant API v1alpha for tagged-stats attribution. Not Content API.
CustomFeedProvider — CSV / URL lists.
8.2 Opportunity score default weights
Component
Weight
Trend / internal velocity
20%
Commission rate and cap
15%
Audience / account fit
15%
Content potential (can we show this product on camera)
15%
Competition
10%
Price / conversion fit
10%
Historical CVR
10%
Review quality / claim risk
5%
8.3 Requirements
ID
Requirement
P
COM-01
Import product by marketplace URL or provider ID.
P0
COM-02
Normalize into shared Product schema.
P0
COM-03
Store affiliate destination, disclosure metadata, tracking IDs.
P0
COM-04
Explain opportunity score components.
P0
COM-05
TikTok Shop open-collab search + link generate behind market flag.
P0
COM-06
Shopee affiliate import for ID/MY/TH/VN/PH/SG.
P0
COM-07
YouTube Shopping eligibility + ASIN timestamp handoff payload.
P1
COM-08
Refresh price/availability on a schedule.
P1
COM-09
Ground scripts in product fields/reviews. Flag unverifiable claims.
P0
9. Module C — Content Strategy and Creative DNA
9.1 Locked format SKU matrix
Surface
Default SKU
Notes
TikTok test
9:16 · 15s
Hook ≤1.5s. Premise over polish.
TikTok convert
9:16 · 21–34s
Product identifiable by 3s.
TikTok Rewards
9:16 · 61–90s
Only on personal accounts in eligible geos. Program pays $0 under 60s.
YouTube Short
9:16 · ≤60s if audio-risk else ≤180s
Classification is automatic from file. #Shorts is search insurance.
YouTube companion
16:9 or 9:16 · 3–12 min
Clickable affiliate URLs. Watch-hours machine.
IG Reel
9:16 · 15–90s
Hook ≤1.0s.
IG carousel
4–10 JPEG stills
2× saves vs single image. PNG rejected by TikTok photo API.
Facebook Reel
9:16
Do not drop FB. 3.12B MAU.
Threads
Still or short clip + caption
Text-first. 141.5M DAU.
WhatsApp Status
9:16 · 24h cut
Export pack + click-to-chat. Not a broadcast cannon.
9.2 Locked UGC templates
POV realism · Unpopular opinion + specific number · Problem → solution demo · One-image product-to-video · AI-native comedy / transformation · Faceless storytime + B-roll · Micro-tutorial 15–45s · Before/after · Carousel-from-video · Series part 1/2 · Motion-transfer trend remix · Talking demo (LIVE-ready export, no LIVE ingest API in MVP).
9.3 Creative DNA
creative_dna = { hook_type, hook_archetype, first_1s_visual, opening_visual, creator_id, voice_id, product_id, duration_sku, cta_type, caption_style, audio_source, music_strategy, motion_id, editing_style, platform, post_time, workflow_id, model_id, is_aigc, brand_content_toggle, brand_organic_toggle, shop_product_ids, spark_eligible, series_id, cut_rate, account_id }
9.4 Scale Winner
Generate variants that change exactly one variable: hook, creator/voice, duration SKU, CTA, product angle. Preserve everything else. Identical 20-up clones are blocked by the diversity gate.
10. Module D — AI Studio and Helios-style Workflow Builder
Visual reusable workflows for image/video generation, inspired by HeliosGen’s local node canvas (Tauri + Next + infinite canvas) and integrated with CreatorOS objects. HeliosGen is a reference, not a merge target. Its kie.ai backend is optional cloud, not our default.
10.1 Generation modes
Mode
Behavior
Auto
Router picks local or cloud by capability, VRAM, cost, quality, queue depth.
Local
ComfyUI / local worker only. No per-clip fee.
Cloud
Configured provider adapters (Kling, Seedance, Veo, etc.). Budgeted.
10.2 Resolution doctrine (productized in the generate UI)
Stage
Default
When
Draft
480p or 720p, short frames
Every seed, every hook test.
Winner
1080p 9:16 or 16:9
Passed QA / human pick / early winner signal.
Hero
4K / 8K upscale (LTX spatial ×2, RTX VSR, or paid cloud)
Paid burst or operator override on a proven asset.
The generate button always shows estimated minutes and VRAM fit before the job starts. Batch 4K without a winner flag requires a typed confirmation.
10.3 Requirements
ID
Requirement
P
STD-01
Serialize workflows to versioned JSON.
P0
STD-02
Run sequential and parallel branches.
P0
STD-03
Map CreatorOS objects into workflow inputs.
P0
STD-04
Persist generation history and lineage.
P0
STD-05
Reusable templates and locked production workflows.
P0
STD-06
Resolution stage selector + hardware estimate.
P0
STD-07
Infinite canvas in Developer Mode. Simple form UI is the default for UGC Factory.
P1
11. Module E — MotionControl
USER PROMISE
Upload or select a character + upload or select a reference motion → generate a video that follows the performer. Local mode has no per-generation application charge.
Mode
Purpose
Default engine
Animate Character
Body + expression onto reference character
Wan Animate Move
Replace Actor
Replace performer, keep scene
Wan Animate Mix
Face Motion
Head, blink, expression
LivePortrait
Pose Control
Stylized pose-driven
AnimateDiff + DWPose
Experimental full body
Research pipelines
MimicMotion / approved alts
Compatibility preflight: subject count, body/face visibility, scene cuts, duration, occlusion, quality score, actionable warning. Output writes a local master plus a 9:16 1080p social derivative.
Motion Library P0 commerce set: Holding Product, Pointing, Talking, Unboxing, Beauty Demo, Fashion Turn, Reaction, Excited, Lifestyle, Walking, Sitting, Selfie, Product Showcase, Trend Remix, Dance, Fitness.
12. Module F — Character, Voice and Identity Rights
Persistent identity is the lock-in. Typical AI-influencer income in 2026 sits at $3k–$30k/month, $50–200k at the top. Without reusable face, body, voice and motion, every video is a one-off and the thesis dies.
Character types: AI generated, fictional, brand mascot, user, licensed creator, consenting adult real person, authorized public figure.
Permission preflight runs before a job reaches ComfyUI: rights record exists → adult requirement satisfied if needed → requested usage in scope → record valid and not revoked → ALLOW or BLOCK.
Local deployments may enable consensual adult generation for synthetic adults and documented consenting adults when the recorded scope explicitly permits the use. Non-consensual intimate generation is not a supported product mode. YouTube additionally lets people request removal of AI likeness — rights preflight runs again before upload, not only before generate.
13. Module G — UGC Affiliate Factory
Main flow: Product → Creator → Angle → Format SKUs → Script + shot plan → Produce video → Voice + captions + product media + CTA → Platform packager.
13.1 Production modes
Faceless — product media + voice + captions.
AI Creator — persistent character + product + AI voice.
Motion UGC — character + reference motion + MotionControl + product overlay.
Talking Avatar — character + script + voice + lip sync.
Remix — winning DNA + one mutated variable.
13.2 Acceptance criteria
9:16 derivative available. Hook in opening seconds. Product identifiable. CTA and disclosure configurable. Captions in social safe area. Identity acceptably consistent. Asset linked to product, campaign, DNA, master and derivatives.
Script claims grounded in product fields. Spoken + on-screen disclosure when commercial. is_aigc / containsSyntheticMedia set.
Audio strategy chosen per surface before render. No trending TikTok sound muxed onto a YouTube file.
14. Module H — Distribution and Social Accounts
This module is where v2.0 was too polite. Official APIs are hostile. The product must encode that hostility instead of hiding it in a risk table.
14.1 Publish modes
Mode
When
Direct
Audited official API, user-approved metadata, remaining quota > 0.
Inbox / draft
TikTok Upload-to-Inbox. YouTube private until process/audit.
Export pack
Always available. MP4 + caption + disclosure checklist + Shopping handoff JSON.
14.2 Account model
platform, account_name, niche, country, language, default_character_id, audience_profile, content_frequency, affiliate_program, status, connection_state, audit_status, daily_quota_remaining, token_expiry, account_subtype.
account_subtype is locked because TikTok money stacks conflict: personal_rewards (Creator Rewards, personal account only) · business_shop (Shop / branded / CML) · creator_hybrid_manual. Autopilot must not flip Personal → Business.
14.3 TikTok connector contract
OAuth: Login Kit + video.upload + video.publish + user.info.basic + video.list.
MVP = Inbox Upload /v2/post/publish/inbox/video/init/. Unaudited Direct Post is SELF_ONLY, max 5 active users/24h.
Direct Post /v2/post/publish/video/init/ stays behind feature flag until Content Posting audit clears.
Every Export page calls creator_info. Privacy dropdown has NO default. Comment/Duet/Stitch off by default. Consent copy switches when branded.
post_info persists brand_content_toggle, brand_organic_toggle, is_aigc. Affiliate/Shop posts are Branded Content under policy effective 31 Aug 2026.
No watermark. Editable caption. Preview + explicit consent. ~15 Direct Posts/account/day shared across every API client. Init 6 req/min.
post_id arrives on webhook post.publish.publicly_available after moderation. Do not join analytics on PUBLISH_COMPLETE.
Photo posts: JPEG/WebP, max 1080p, 20MB, no PNG.
Spark Ads: store spark_auth_code + expiry. No public generate-code API.
14.4 YouTube connector contract
Data API v3 resumable videos.insert. No Shorts endpoint. Short = vertical or square AND ≤180s, classified from the file.
Must set selfDeclaredMadeForKids, containsSyntheticMedia on photoreal, paid-promotion when required, disclosure footer.
Quota after 1 Jun 2026: videos.insert is its own 100 calls/day/project bucket. Do not shard GCP projects. File quota-extension audit in M00.
Unverified projects: uploads stay private until compliance audit.
Dual-track default: Short for reach + long-form companion with clickable affiliate URLs.
Shopping tags: eligibility badge + Studio handoff. No public write API. Merchant API v1alpha for attribution.
Default public cap 3–5 / channel / day. Warn at 8. Block at 12 unless override + reason.
14.5 Other connectors
Instagram Professional Graph v26: Reels, feed, carousel ≤10, 100 API posts/24h. JPEG images. Product tags need Facebook Login for Business.
Facebook Reels. Threads caption + still/clip. X official API if token exists else export. Pinterest adapter later.
WhatsApp: Status export + click-to-chat deep link. Cloud API is CRM, not a public feed. Do not build a broadcast spam cannon.
14.6 Calendar / queue
Views: calendar, queue, campaign, account. Fields: approval, scheduled time, publish mode, status, retry, platform error, remaining quota, spark code, shopping handoff state.
15. Module I — Engagement and Lead Intent
Turn accessible comments into structured intent. Official comment ingest is uneven. Do not promise TikTok auto-reply at MVP. YouTube commentThreads.list → draft reply → human approve → comments.insert.
Intent classes: Purchase, Product question, Price, Link request, Positive, Negative, Lead/booking, Spam.
Default: suggested replies with campaign context, human approval required. Never auto-reply in health/legal/finance/politics threads. Capture path for commerce is Shop showcase / product tag / long-form link, not a comment URL on a Short.
16. Module J — Analytics, Revenue and Growth Engine
16.1 Layers
Layer
Metrics we can actually get
Content
Official views/likes/comments/shares. YouTube AVD and watch time via Analytics API when scoped. TikTok Display API does NOT give watch-time, completion, saves or demographics.
Commerce
Affiliate clicks, Shop orders/GMV/commission, YT Shopping tagged stats, Rewards payout import.
Production
Generation cost, render time, workflow, success/fail, GPU seconds.
Profitability
Attributed revenue − generation cost − paid distribution.
16.2 Winner logic
Separate OrganicWinner and RevenueWinner.
Minimum sample and age (YouTube: <1k views or <48h cannot be a winner).
Confidence score when Display API views lag (TikTok can lag ~48h).
Store why an item was declared a winner.
16.3 Growth loop
Published content → performance + conversion → Creative DNA → winner detection → one-variable mutation → new content. One-click Scale Winner on HOME.
17. Autopilot and Agent Architecture
Autopilot is goal-directed orchestration with budgets, permissions, approval rules and stop conditions. It is not unrestricted posting.
Agent
Responsibility
Research
Find and summarize opportunities from allowed sources.
Product
Rank offers.
Strategist
Audience, angle, format SKU, experiment.
Script
Hooks/scripts/captions grounded in product fields.
Creative Director
Character, workflow, model, motion, resolution stage.
Production
Dispatch and monitor generation.
Packager
Per-platform derivatives, audio, disclosure.
Publisher
Queue approved variants. Never silent Direct Post.
Community
Classify engagement, draft replies.
Analyst
Performance + attribution.
Growth
Next controlled experiment.
17.1 Default Autopilot policy
Objective: maximize affiliate contribution profit.
Daily content cap: 5 public YouTube / channel, TikTok limited by remaining official quota and operator override.
AI/GPU budget configurable. Local jobs do not decrement a dollar budget; they decrement a concurrency/VRAM budget.
Approval required before publish. Per-account “allow autopilot publish” flag required in addition to workspace policy.
Stop if 7-day contribution profit < threshold, if rights record revoked, if connector error rate spikes, or if diversity gate fail-rate spikes.
YMYL AI-persona expert pack is blocked by default.
18. ComfyUI Runtime, Model Routing and Resolution
CreatorOS Web/API → Rights + Policy Preflight → Workflow Router → Local Worker / Cloud Adapter → ComfyUI or provider → Result + lineage.
18.1 2026 workflow registry
Workflow
Task
P
flux2_klein_t2i / edit
Fast local images, identity guidance. Apache-2.0 4B. ~8GB.
P0
wan22_ti2v_5b
Draft video 720p on 8–12GB.
P0
wan22_i2v_a14b
Higher-quality 720p on 16GB.
P0
wan27_hero
Longer / higher-res on 24GB. 4K only as hero stage.
P1
ltx25_t2v_audio
Video + native audio. 4K path with spatial upscaler.
P1
wan_animate_move / mix
MotionControl body / replacement.
P0
liveportrait
Face / expression.
P1
rtx_vsr / ltx_upscale_4k
Winner upscale.
P1
product_ugc
Composite UGC assembly.
P0
closed_* adapters
Kling / Seedance / Veo budgeted cloud burst.
P2
LICENSE WATCH
Wan 2.2 and FLUX.2 Klein 4B are Apache-2.0 and commercially shippable locally. FLUX.2 Klein 9B and FLUX.2 [dev] are non-commercial without a license — do not ship them in the default pack. LTX has a revenue-threshold license; confirm before hosting weights in a multi-tenant cloud. Wan 3.0 in ComfyUI as of 25 Aug 2026 is treated as a partner/API node until open weights and license are verified.
18.2 Hardware routing
VRAM
Default local pack
8–12GB
FLUX.2 Klein 4B + Wan 2.2 5B @ 480p/720p draft. No 4K.
16–22GB
Wan 2.2 14B FP8 @ 720p. LTX distilled with offload. 4K = upscale queue, not native.
24GB+
Wan 2.7 / LTX fuller precision. Native 1080p comfortable. 4K hero allowed.
Unknown / weak
Force draft presets. Offer cloud burst. Never hide a 40-minute queue behind a spinner.
18.3 Honest unit economics (print in admin + generate UI)
Owned 4080/4090: ~$0 per clip after electricity.
Rented A40: about $0.03–$0.05 per 5s 720p Wan 2.2.
Runway Gen-4.5: about $1.44 per 5s.
Seedance 2.0 API: about $0.025–$0.05/s if we add a closed adapter.
That gap is the wedge. If we meter local pixels we become a worse Runway.
19. System Architecture and Deployment
WEB / DESKTOP CLIENT → API GATEWAY / BFF → WORKFLOW ORCHESTRATOR → Analytics · Social Connectors · Commerce Providers · AI Gateway → Cloud AI and/or Local Worker → ComfyUI → GPU.
Layer
Recommendation
Web UI
Next.js + React + TypeScript + Tailwind.
Desktop shell
Tauri for local-first distribution.
API / BFF
TypeScript service. Python FastAPI for AI/media.
DB
PostgreSQL hybrid/cloud. SQLite allowed for single-user local.
Queue
Redis + BullMQ MVP. Temporal later for long workflows.
Storage
Local disk in Local mode. R2/S3-compatible in Hybrid/Cloud. Verified domain for TikTok PULL_FROM_URL.
Video
FFmpeg. Platform packager is a first-class service.
Local inference
ComfyUI + pinned custom nodes.
Observability
Job logs, failure reason, GPU util, cost, quota remaining.
Mode
Data / compute
Use
Local
Local DB, media, ComfyUI/GPU
Private power users, offline
Hybrid
Cloud control plane + local worker + optional cloud AI
Target production mode
Cloud
Managed DB, object storage, workers
Hosted SaaS
20. Data Model Highlights
Keep the v2.0 domain map. Additive locks for v3.0:
content_assets.master_id + content_derivatives(platform, spec, audio_strategy, disclosure_pack, file_url).
social_accounts.account_subtype, audit_status, daily_quota_remaining, allow_autopilot_publish.
publications.publish_mode, publish_id, post_id (nullable until publicly_available), spark_auth_code, shopping_handoff_json, contains_synthetic_media, is_aigc, brand_content_toggle.
generation_jobs.resolution_stage (draft|winner|hero), vram_estimate, cost_estimate.
creative_dna expanded fields from §9.3.
Lineage: every published derivative traces to master, product, campaign, hook, script, character, motion, voice, workflow version, model, job, rights record.
21. API Requirements (additive)
Keep v2.0 endpoints. Add:
POST /assets/{id}/derivatives — build platform pack.
GET /social/accounts/{id}/preflight — TikTok creator_info / YT quota / token health.
POST /publications/{id}/inbox — TikTok inbox upload.
POST /publications/{id}/export-pack — always-on fallback.
GET /commerce/youtube/shopping-handoff/{content_id}.
POST /growth/winners/{id}/scale — one-variable mutation.
POST /rights/preflight — generate and again before publish.
22. Workflow and Event Model
Keep v2.0 events. Add: derivative.built, preflight.blocked, quota.reserved, quota.exhausted, publish.inbox_delivered, publish.publicly_available, shopping.handoff.ready, winner.organic.detected, winner.revenue.detected, slop.gate.blocked.
Event-driven so long generation survives HTTP timeouts, agents stay decoupled, and publish retries are idempotent on (workspace_id, content_id, platform, checksum).
23. Security, Privacy, Safety, Rights and Platform Compliance
23.1 Privacy modes
Local Privacy — no cloud inference, local assets, telemetry off, local rights records.
Hybrid Privacy — cloud metadata as configured; generation can be forced local.
Cloud — managed storage/inference under deployment policy.
23.2 Rights
Permission is an explicit data object. Consent may expire or be revoked. Commercial rights tracked separately from face/voice rights. Adult local workflows require adult status plus explicit scope. Non-consensual intimate generation unsupported.
23.3 Platform compliance checklist
TikTok audit pack UI: privacy with no default, commercial disclosure, is_aigc, music confirmation, preview, consent, no watermark.
YouTube: containsSyntheticMedia, MFK accurate, paid-promotion toggle, FTC footer, grounded claims, anti-slop cap, no project sharding.
Music per platform. CML does not travel.
No Research API. No Creative Center scrape. No unofficial bots.
C2PA embed opt-in only. Silent permanent YouTube AI-label lock is forbidden as default.
23.4 Security
Encrypt tokens at rest. Minimal OAuth scopes, incremental. Workspace isolation. Audit rights changes and publishes. Signed URLs. No arbitrary untrusted ComfyUI custom-node install. Pin node commits. Validate uploads.
24. Non-Functional Requirements
Area
Target
Availability
Control plane ≥99.5% MVP. Local gen remains usable if cloud is down in Local mode.
API p95
<800ms excluding generation.
Generation success
≥90% usable completion in Beta for supported workflows.
Honesty
Generate UI shows ETA + VRAM fit. No fake unlimited 4K.
Idempotency
No duplicate publish on retry.
Cost controls
Per-user / workspace / global budgets for cloud. Local concurrency caps.
Observability
Job logs, GPU, cost, quota, connector health.
Accessibility
Keyboard-accessible primary flows. Readable captions.
25. Admin, Operations and Kill Switches
System dashboard: users, jobs, failure rate, generation cost, GPU queue, connector health, remaining YouTube insert quota, TikTok audit status.
Kill switches: disable cloud generation; disable a workflow/model; pause a social connector; pause a commerce provider; stop Autopilot globally or per workspace; block a token; pause Direct Post while leaving Inbox + Export alive.
26. UX and Design System
Feel: a creative production operating system, not enterprise reporting. Visual, fast, high-density where needed, large media previews, real job stages instead of generic spinners. Advanced model parameters live in Developer Mode.
Desktop: left nav · main workspace · right inspector. HOME uses the seven-module live pipeline from the reference video.
MotionControl mobile flow: Character → Motion → Preview/Settings (including resolution stage) → Generate → Result/Share.
Core principles: Auto is default. Every AI recommendation is editable. Every autonomous action has budget, permission and approval state. Cost and ETA before large batches. Winner scaling is one click. Platform packager results are visible as a pack, not a single MP4.
27. MVP Scope and Milestones
Milestone
Scope
Exit criteria
M00 Foundation
Next.js, workspace, DB, storage, queue, audit log, local-worker protocol, GCP project + YT quota-extension request.
Sign in, durable job, quota bucket exists.
M01 AI Studio
Provider abstraction, image/video gen, history, resolution stage.
Prompt/reference → asset in library with stage + lineage.
M02 ComfyUI
Local connection, workflow registry, GPU status, model inventory.
Web request → local ComfyUI → result.
M03 MotionControl
Wan Move/Mix, upload, analysis, 9:16 derivative.
Image + motion → usable master + social MP4.
M04 Character/Rights
Persistent character, voice link, rights registry, preflight.
Saved character reused only after ALLOW.
M05 Commerce
Amazon + Shopee import, TikTok Shop search flagged, opportunity score.
URL becomes campaign-ready Product.
M06 UGC Factory
Hook/script, voice, captions, 3-pack + Rewards cut + YT companion script, platform packager.
One product + creator → platform pack.
M07 YouTube Official
OAuth, resumable upload, disclosure fields, dual-track, shopping handoff, idempotent retry, kill switch.
Approved Short + companion path works or export pack is complete.
M07b TikTok Official
Inbox Upload, audit-pack UI, is_aigc + commercial toggles, webhooks, Display API join, Direct Post flag.
Inbox delivery works unaudited. Direct Post not required to exit.
M08 Analytics
Official metrics + click/Shop/Rewards import + content profit.
Publication maps to performance + commerce.
M09 Growth
Creative DNA, organic vs revenue winners, one-variable Scale Winner.
System proposes controlled variants.
M10 Autopilot
Goal/budget/rules, approval gates, diversity cap, stop rules.
One bounded daily loop with oversight.
STRICT MVP DEFINITION
AI Studio + ComfyUI + MotionControl + Character Library + Amazon/Shopee import + UGC script + AI voice + UGC video + resolution pipeline + platform export pack + YouTube Shorts official path + TikTok Inbox Upload + affiliate link. Direct public TikTok and YouTube Shopping write-API are not MVP gates.
28. Testing and Acceptance
28.1 Functional
Import Amazon or Shopee URL → normalized product.
Persistent character + rights preflight allow/block.
MotionControl image + video → master + 9:16 MP4.
One product/creator → ≥3 UGC variants + platform pack.
YouTube private resumable upload with containsSyntheticMedia + footer. Retry does not duplicate.
TikTok Inbox Upload with required UX. Unaudited Direct Post cannot go public.
Click/revenue event joins to content.
Winner rule fires and Scale Winner changes one variable only.
4K hero path is gated and estimated. Draft default is 720p or below.
28.2 Reliability
Worker disconnect, ComfyUI crash, GPU OOM, provider timeout, duplicate generation, expired token, marketplace API failure, partial upload, rights revoked before queued job, publish retry without duplicate, quota 429 queued to next day.
28.3 Quality gates
Gate
Target
Supported generation success
≥90% Beta
Rights preflight
100% blocked when permission missing/expired
Lineage completeness
100% published derivatives contain required IDs
Publish idempotency
No duplicate in retry test
Disclosure completeness
100% commercial posts carry platform flags + footer
Cost / ETA telemetry
≥95% jobs report estimate
29. Roadmap
Phase
Capabilities
1 Create
Studio, ComfyUI, MotionControl, Characters, Amazon/Shopee UGC, resolution doctrine.
2 Distribute
YouTube official, TikTok Inbox, audit pack, multi-account calendar, export packs.
3 Measure
Official metrics, Shop/affiliate attribution, Creative DNA, profit dashboard.
4 Grow
Scale Winner, experiments, Spark code storage, Shopping tag handoff polish.
5 Operate
Bounded Autopilot, multi-market portfolio, budget optimizer, TikTok Direct Post post-audit.
6 Marketplace
Motion/workflow/creator packs. Optional ActivityPub/PeerTube adapter. Still not a public FYP.
30. Risks and Mitigations
Risk
Impact
Mitigation
“Unlimited 4K” expectation
Churn when 16GB cards take 15–30 min
Resolution doctrine in UX. ETA before generate.
GPU / VRAM
Local failures
Detect hardware, low-VRAM presets, cloud burst.
Custom node breakage
Workflow instability
Pinned registry, versioning, rollback.
TikTok audit reject
Direct Post stays private
Inbox + export first. Audit-pack UI exact.
YT inauthentic-content
Channel-level demonetization
Caps, diversity gate, grounded scripts, human approval.
YT quota 100 inserts/day/project
SaaS multi-tenant ceiling
Quota audit in M00. Per-workspace caps. No sharding.
Shorts links don’t click
Zero affiliate revenue
Dual-track long-form + Shopping handoff.
Music / Content ID
Blocks, muted audio, lost RPM
Per-platform audio policy. ≤60s if claim risk.
Attribution gaps
Wrong optimization
Confidence scores, min sample, separate organic/revenue winners.
Autopilot slop
Bans + wasted GPU
Budgets, approval, stop rules, one-variable mutation.
Identity misuse
Legal / reputational
Rights registry, double preflight, no non-consensual intimate mode.
Cloud cost runaway
Negative unit economics
Local default, budgets, draft-first.
License foot-gun
Cannot commercially ship a model
Default pack = Apache-2.0 only. License watch on LTX / FLUX.2 larger variants / Wan 3.0.
Building a social network
Years of moderation + zero commerce
Explicit Phase 6 adapter only. Internal feed is workspace-private.
31. Sources and Implementation References
Reviewed 2 September 2026. References, not licenses to copy code wholesale.
HeliosGen — github.com/SegFault42/HeliosGen — local visual workflow UX. Tauri + Next + SQLite. Optional kie.ai. Interaction model only.
Amazon Affiliate automation pattern — github.com/profullstack/amazon-affiliate — URL → product → script → voice → video → publish sequence.
ComfyUI Wan 2.2 / Wan Animate docs, Wan 2.7 local GPU guide (runaihome, Jun 2026), LTX-2.5 ComfyUI docs (Aug 2026), FLUX.2 Klein ComfyUI docs.
TikTok for Developers Content Posting API Direct Post + Inbox + Photo, updated Aug 2026. Branded Content Policy 4 Aug 2026 effective 31 Aug 2026. Shop Affiliate Creator API v202405.
YouTube Data API v3. Quota model 1 Jun 2026. containsSyntheticMedia May 2026. Inauthentic content 16 Jul 2026. Amazon × YouTube Shopping 27 Aug 2026. Content API for Shopping sunset 18 Aug 2026.
Gigapay Global Creator Economy Report 2026 — Shop GMV $112.2B, brand spend $32.6B. eMarketer / SFN social commerce 2026.
Internal reference video — Structure Webworks AI Social Media Operating System. HOME control-plane design source.
32. Initial Engineering Backlog (v3.0 additive)
ID
Item
P
RES-001
Resolution stage on generation jobs + UX estimate
P0
PKG-001
Platform packager service (encode + audio + disclosure pack)
P0
SOC-004
TikTok Inbox Upload + creator_info preflight UI
P0
SOC-005
TikTok audit-pack Export page
P0
SOC-006
YouTube resumable upload + synthetic media + footer
P0
SOC-007
YouTube dual-track companion job
P0
SOC-008
Per-account daily cap + diversity gate
P0
COM-005
TikTok Shop provider skeleton + market flag
P0
COM-006
Shopee provider
P0
COM-007
YouTube Shopping handoff payload
P1
ANA-004
Split organic vs revenue winner states
P1
GRO-004
One-variable Scale Winner constraint
P1
AGT-003
Autopilot cannot silent Direct Post
P0
LIC-001
Default model pack license allowlist
P0
33. Final Product Definition
CreatorOS v3.0
A local-first AI Social Media Operating System that generates unlimited images and video on the operator’s hardware at the highest resolution that hardware can finish, packages official platform derivatives, distributes through audited APIs or export packs, measures shop and affiliate money, learns Creative DNA, and scales only what works — inside explicit budgets, rights, quotas and approval rules.
Maturity ladder (unchanged, now with teeth):
AI creates content — locally, draft-first, no per-clip fee.
AI prepares and distributes content — official APIs + export packs, never bots.
AI understands which content performs — using metrics the APIs actually return.
AI understands which content makes money — Shop, affiliate, Rewards, Shopping tags.
AI creates more of what makes money — one variable at a time, inside caps.
P2P Labs  ·  CreatorOS Master PRD v3.0  ·  2 September 2026  ·  Internal