MASTER PRODUCT REQUIREMENTS DOCUMENT
AI Creator CommerceOperating System
Local-first AI Social Media + UGC Affiliate + Motion Control Platform
Field
Value
Document Version
2.1
Status
Master PRD - Product + Engineering
Date
2 September 2026
Deployment
Local-first, Hybrid, optional Cloud
Working Product Name
CreatorOS (replaceable codename)
Primary Outcome
Autonomous social-commerce content operation optimized for attributable revenue
Source Inputs
MotionControl concept, ComfyUI/Wan workflows, HeliosGen architecture, Amazon Affiliate automation reference, AI Social Media OS reference video, NVIDIA RTX local creator stack (NVIDIA App, Broadcast, NVENC, Studio Driver, G-Assist, ChatRTX, ComfyUI NVFP4/FP8, RTX Video node).
North StarResearch -> Create -> Animate -> Publish -> Engage -> Measure -> Monetize -> Learn -> Repeat.
Document Control
Version
Date
Summary
1.0
31 Aug 2026
Initial free Motion Control product concept.
1.5
2 Sep 2026
Added local ComfyUI orchestration, character rights registry and consent-aware adult workflows.
2.0
2 Sep 2026
Unified MotionControl, Helios-style generation studio, UGC Affiliate, social distribution, analytics and autonomous growth loop into one AI Creator Commerce OS.
2.1
2 Sep 2026
Added NVIDIA RTX Local Creator Stack as a first-class runtime layer; locked NVIDIA-owned free software vs open-source generation; added Grok terminal operating instructions for engineering agents.
Locked Product Decisions
The root product is an AI Creator Commerce Operating System, not a standalone Motion Control utility.
MotionControl is a production module inside the Create layer.
ComfyUI is the preferred local inference/orchestration runtime for open-source workflows.
HeliosGen is a reference architecture for local visual workflow UX and multi-model generation; its concepts are adapted rather than merged blindly.
Affiliate product automation is provider-agnostic. Amazon is the first implementation, followed by TikTok Shop, Shopee, YouTube Shopping and custom feeds.
Analytics must feed winning creative patterns back into Research and Production; without the feedback loop the product is only a generator.
The system supports Local, Hybrid and Cloud deployment modes. Hybrid is the target production architecture.
Real-person and public-figure generation is permission-based. Consensual adult use may be enabled locally when rights and scope are recorded. Non-consensual intimate generation is not a supported product mode.
NVIDIA-owned software is a free capability layer for RTX operators, not a replacement generation model. CreatorOS must detect, recommend and optionally orchestrate NVIDIA App, Studio Driver, Broadcast, NVENC, RTX Video (export-capable nodes only), G-Assist and ChatRTX without claiming NVIDIA provides unlimited image/video generation.
Local generation remains ComfyUI + approved open-weight models (Flux/Qwen/Wan/LTX/Hunyuan). NVIDIA contributions are drivers, encoder, AI filters, precision formats (NVFP4/FP8) and official ComfyUI/LTX/FLUX templates.
Default local production stack on NVIDIA hardware: Studio Driver + ComfyUI (FP8 on RTX 40, NVFP4 on RTX 50) + OBS/FFmpeg via NVENC + Broadcast as optional capture/mic preprocessor. Game Ready Driver is allowed only when the workstation is dual-use gaming.
Table of Contents
#
Section
1
Executive Summary
2
Problem, Vision and Product Thesis
3
Goals, Non-Goals and Success Metrics
4
Users and Jobs-to-be-Done
5
Product Information Architecture
6
End-to-End Operating Loop
7
Module A - Intelligence and Research
8
Module B - Commerce and Affiliate Engine
9
Module C - Content Strategy and Creative DNA
10
Module D - AI Studio and Helios-style Workflow Builder
11
Module E - MotionControl
12
Module F - Character, Voice and Identity Rights
13
Module G - UGC Affiliate Factory
14
Module H - Distribution and Social Accounts
15
Module I - Engagement and Lead Intent
16
Module J - Analytics, Revenue and Growth Engine
17
Autopilot and Agent Architecture
18
ComfyUI Local Runtime and Model Routing
19
System Architecture and Deployment
20
Data Model
21
API Requirements
22
Workflow and Event Model
23
Security, Privacy, Safety and Rights
24
Non-Functional Requirements
25
Admin and Operations
26
UX and Design System
27
MVP Scope and Milestones
28
Testing and Acceptance Criteria
29
Roadmap
30
Risks and Mitigations
31
Source and Implementation References
32
Appendix - Initial Backlog
33
NVIDIA RTX Local Creator Stack
34
Grok Terminal Operating Instructions
1. Executive Summary
CreatorOS is a local-first AI Creator Commerce Operating System that converts market opportunity into attributable social-commerce revenue. It combines trend and product intelligence, affiliate product ingestion, AI strategy and scripting, reusable AI characters, image/video generation, motion transfer, social publishing, engagement intelligence, revenue attribution and a closed-loop optimization engine.
Product PromiseGive the system products, characters, social accounts and business objectives. It continuously creates, distributes and improves revenue-generating social content.
1.1 Core Operating Loop
Market Intelligence   -> Product Opportunity   -> Content Strategy   -> AI / UGC Production   -> MotionControl / Edit   -> Distribution   -> Engagement   -> Affiliate Click / Lead   -> Conversion / Revenue   -> Analytics   -> Winning Pattern Extraction   -> Next Content Batch
1.2 Why This Is Not Another AI Generator
Generation is only one stage. Every asset is connected to product, creator, hook, workflow, account, campaign and revenue data.
The system measures creative profitability, not just views.
Winning hooks, creators, motions, formats, CTAs and posting conditions are converted into reusable Creative DNA.
The next content batch is generated using learned performance patterns.
Local inference lowers marginal generation cost and increases privacy; cloud providers remain available for quality or speed.
2. Problem, Vision and Product Thesis
2.1 Problems
Social-commerce teams use disconnected tools for research, scripting, generation, editing, publishing and analytics.
Most AI video products optimize for generation quality but do not know whether the content sells.
Affiliate operators manually choose products, write scripts, produce variants and update links across many accounts.
Creative learnings are lost in spreadsheets or human memory instead of becoming machine-readable reusable signals.
Cloud-only generation makes high-volume UGC expensive and creates vendor lock-in.
Local AI workflows are powerful but difficult for non-technical operators to run consistently.
2.2 Vision
Create an operating system in which AI can observe market signals, plan content, produce creative, distribute approved content, measure outcomes and continuously optimize toward business objectives such as affiliate profit, GMV, leads or booked calls.
2.3 Product Thesis
ThesisThe moat is not the underlying generation model. The moat is the accumulated relationship between Product Data + Creator Identity + Creative DNA + Distribution Context + Performance Data + Revenue Attribution.
3. Goals, Non-Goals and Success Metrics
3.1 Product Goals
Generate platform-native UGC affiliate videos from a product URL and creator profile with minimal manual work.
Support local open-source video workflows through ComfyUI and optional cloud generation through provider adapters.
Create persistent AI creator identities, voices and motion styles for repeatable content production.
Publish or prepare channel-specific content packages for major social platforms through official APIs where available.
Measure content performance and affiliate revenue down to creative components.
Detect winners and generate controlled creative mutations.
Provide an Autopilot mode only after enough attribution and quality data exists.
3.2 Non-Goals for MVP
Building a new foundation video model.
Supporting every affiliate network at launch.
Fully autonomous public posting on every social platform before approval, permissions and API reliability are validated.
High-end NLE replacement comparable to Premiere Pro or CapCut desktop.
Perfect product placement in every generated frame.
Unlimited free cloud GPU generation.
3.3 North Star and KPI Hierarchy
Metric
Definition
Why It Matters
North Star
Affiliate contribution profit per 1,000 AI-generated content views
Connects reach, conversion and generation cost.
Content Profit
Attributed commission/revenue - generation cost - paid distribution
Primary creative economics metric.
EPC
Affiliate earnings / affiliate clicks
Measures commerce efficiency.
Winner Rate
% of published content above chosen performance threshold
Measures system learning quality.
Generation Success
Completed usable generations / submitted jobs
Measures production reliability.
Scale Uplift
Performance of winner variants vs baseline
Measures Growth Engine value.
Cost per Successful Video
AI + GPU + processing cost / usable outputs
Controls unit economics.
4. Users and Jobs-to-be-Done
Persona
Primary Job
Key Needs
Affiliate Operator
Turn product opportunities into large volumes of profitable content.
Product import, scripts, UGC, links, publishing, revenue attribution.
AI Creator Network Operator
Run multiple persistent AI creators across niches and countries.
Character consistency, voice, motion library, account portfolio, batch workflows.
Social Media Manager
Plan and distribute platform-native content.
Calendar, approval, variants, analytics, engagement.
Performance Marketer
Find creative combinations that drive revenue.
Creative DNA, attribution, scale winner, experiment design.
Local AI Power User
Run advanced generation privately.
ComfyUI, workflow import, model manager, GPU controls, offline mode.
Agency / Brand Team
Operate multiple workspaces and clients.
Workspace isolation, roles, reports, approval, cost/revenue visibility.
4.1 Core Jobs-to-be-Done
When I find a product worth promoting, generate several native UGC concepts so I can test demand quickly.
When a social post becomes a winner, identify what caused the win and create controlled variants.
When I create an AI creator, keep face, body, style and voice reusable across hundreds of outputs.
When I have a reference movement, transfer it to a character without manually building a ComfyUI graph.
When I run locally, keep private assets on my device and avoid per-generation vendor charges.
When I manage many accounts, tell me what is publishing, what is performing and what is making money.
5. Product Information Architecture
HOMEINTELLIGENCE  Research  Trends  OpportunitiesCOMMERCE  Products  Affiliate Programs  CampaignsCREATE  AI Studio  UGC Factory  MotionControl  Characters  Motion Library  AssetsDISTRIBUTE  Calendar  Publish Queue  AccountsGROW  Engagement  Analytics  Revenue  Growth EngineSYSTEM  Workflows  Models  ComfyUI  Identity Rights  Settings
5.1 Global Objects
Workspace
Product
Affiliate Offer
Character
Voice
Motion
Creative Brief
Hook
Script
Content Asset
Campaign
Social Account
Publication
Generation Job
Workflow
Conversion Event
Creative DNA
Experiment
Consent / Rights Record
6. End-to-End Operating Loop
1. Detect opportunity2. Select/import product3. Score offer and audience fit4. Generate content angles and hooks5. Choose creator + voice + motion/format6. Generate image/video assets7. Assemble UGC output8. Review/approve9. Publish/schedule10. Capture performance + commerce events11. Score content and creative components12. Detect winner / loser patterns13. Generate next controlled variants
6.1 Killer MVP Journey
InputPaste an Amazon product URL -> select an AI creator -> choose TikTok Review.
OutputThree 9:16 UGC videos with hook, script, voice, captions, product media, CTA, affiliate link and platform-ready metadata.
7. Module A - Intelligence and Research
7.1 Objective
Answer: What should we create and promote now? The module turns external and internal signals into ranked opportunities.
7.2 Sources
Social trend inputs (where legally/API-accessible)
Google Trends / search trend signals
Affiliate product feeds and marketplace APIs
Competitor/account observations
Internal historical content performance
Internal affiliate conversion and revenue data
User-supplied research files/URLs
7.3 Opportunity Object
{  "topic": "portable blender",  "market": "US",  "platform": "tiktok",  "trend_velocity": 2.4,  "competition_score": 0.61,  "affiliate_score": 0.88,  "recommended_formats": ["POV", "review", "problem_solution"]}
7.4 Functional Requirements
ID
Requirement
Priority
INT-01
Create and store research observations with source, timestamp, market and platform.
P0
INT-02
Rank products/topics using configurable opportunity scoring.
P0
INT-03
Generate content-gap and suggested-format recommendations.
P1
INT-04
Promote winning internal hooks back into research results.
P0
INT-05
Support manual pinning and exclusion so operators can override AI ranking.
P1
INT-06
Maintain traceability from recommendation to underlying signals.
P0
8. Module B - Commerce and Affiliate Engine
8.1 Provider Abstraction
AffiliateProvider  -> AmazonProvider  -> TikTokShopProvider  -> ShopeeProvider  -> YouTubeShoppingProvider  -> CustomFeedProvider
8.2 Amazon MVP
The first provider should reproduce the useful primitives demonstrated by the referenced Amazon Affiliate automation project: product URL/ID ingestion, reliable product data, product media, AI review script generation, voiceover, video creation, affiliate-link insertion and YouTube/social publishing. The CreatorOS implementation must expose these capabilities through its own provider interfaces rather than depending on the reference CLI.
8.3 Product Fields
provider_product_id, title, brand, category, price, discount, rating, review_countfeatures, images, videos, availability, marketaffiliate_url, commission_rate, commission_amount, last_synced_at
8.4 Affiliate Opportunity Score
Component
Default Weight
Trend Velocity
20%
Commission
15%
Audience Fit
15%
Content Potential
15%
Competition
10%
Price/Conversion Fit
10%
Historical CVR
10%
Review Quality
5%
8.5 Requirements
ID
Requirement
Priority
COM-01
Import product by marketplace URL or provider ID.
P0
COM-02
Normalize provider-specific data into a shared Product schema.
P0
COM-03
Store affiliate destination, disclosure metadata and tracking identifiers.
P0
COM-04
Refresh price/availability on a configurable schedule.
P1
COM-05
Calculate opportunity score and explain score components.
P0
COM-06
Support product lists, tags and campaign assignment.
P0
COM-07
Support non-Amazon providers without schema redesign.
P0
9. Module C - Content Strategy and Creative DNA
9.1 Strategy Outputs
Audience insight
Content angle
Hook variants
Script
Shot list
Visual opening
CTA
Caption
Hashtags/keywords
Affiliate placement
Platform adaptation
Compliance/disclosure notes
9.2 Hook Factory
Score
Meaning
Scroll Stop
Likelihood of interrupting feed behavior.
Curiosity
Open loop strength.
Clarity
How quickly value/product context is understood.
Commercial Intent
Potential to drive commerce action.
Platform Fit
Native fit for the selected social platform.
9.3 Creative DNA Schema
creative_dna = {  hook_type, opening_visual, creator_id, voice_id, product_id,  duration, cta_type, caption_style, music_type, motion_id,  editing_style, platform, post_time, workflow_id, model_id}
9.4 Scale Winner
Generate 3 hook variants
Generate alternate creator/voice variant
Generate shorter and longer duration variants
Generate CTA variant
Generate alternate product angle
Preserve all unchanged creative components for controlled experimentation
10. Module D - AI Studio and Helios-style Workflow Builder
10.1 Objective
Provide a visual, reusable workflow system for image/video generation and content automation, inspired by HeliosGen's local node-based approach while integrated with CreatorOS data objects and orchestration.
10.2 Canvas Node Families
Family
Nodes
Intelligence
Trend Search; Product Research; Viral Hook Finder; Competitor Analyzer
LLM
Prompt; Script; Hook; Caption; CTA; Review
Image
Text-to-Image; Image-to-Image; Character; Product Image; Background; Thumbnail
Video
Text-to-Video; Image-to-Video; Motion Control; Lip Sync; Remix
Audio
TTS; Voice; Music; SFX
Commerce
Product; Affiliate Link; Commission; Offer
Social
Publish; Schedule; Platform Variant
Logic
Condition; Router; Delay; Iterator; A/B Variant; Webhook
10.3 Generation Modes
Mode
Behavior
Auto
Router selects local or cloud workflow by capability/cost/quality.
Local
Use local ComfyUI/other local worker only.
Cloud
Use configured cloud AI provider.
10.4 Workflow Requirements
ID
Requirement
Priority
STD-01
Infinite or large canvas with drag/connect nodes.
P1
STD-02
Serialize workflows to versioned JSON.
P0
STD-03
Run sequential and parallel branches.
P0
STD-04
Map CreatorOS objects into workflow inputs.
P0
STD-05
Persist generation history and lineage.
P0
STD-06
Support reusable templates and locked production workflows.
P0
STD-07
Allow custom workflow import in Developer Mode.
P1
11. Module E - MotionControl
11.1 User Promise
MotionControlUpload/select a character + upload/select a reference motion -> generate a video following the performer movement.
11.2 Product Modes
Mode
Purpose
Default Engine
Animate Character
Apply body and expression motion to reference character.
Wan2.2 Animate Move
Replace Actor
Replace performer while preserving scene/environment.
Wan2.2 Animate Mix
Face Motion
Head, blink, expression and portrait motion.
LivePortrait workflow
Pose Control
Stylized pose-driven generation.
AnimateDiff + DWPose/OpenPose
Experimental Full Body
Alternative research pipelines.
MimicMotion/approved alternatives
11.3 Inputs
Character image or saved Character
Reference video or saved Motion
Start/end trim
Prompt (optional)
Identity Strength
Motion Strength
Face Preservation
Background mode
Output aspect ratio
Resolution/FPS preset
11.4 Character and Motion Compatibility
Detect number of subjects
Estimate body/face visibility
Detect major scene cuts
Check duration and dimensions
Warn about occlusion and extreme motion
Return quality score and actionable recommendation
11.5 Free/Local Runtime Principle
Local mode has no per-generation application charge, but compute cost is borne by the operator hardware/electricity. Cloud free tiers must use quotas, queue priority and resolution/duration caps.
11.6 Motion Library
Commerce motions: Holding Product; Pointing; Talking; Unboxing; Beauty Demo; Fashion; Reaction; Excited; Lifestyle; Walking; Sitting; Selfie; Product Showcase; TikTok Trend; Dance; Fitness.
12. Module F - Character, Voice and Identity Rights
12.1 Character Object
character_idnametypereference_images[]face_embedding / local identity representationbody_referencevoice_idstylepersonalitydefault_languagecontent_permissionscommercial_rightsconsent_record_id
12.2 Character Types
AI Generated
Fictional
Brand Mascot
User
Licensed Creator
Consenting Adult Real Person
Authorized Public Figure
12.3 Identity Rights Registry
Field
Purpose
identity_id
Stable identity reference.
adult_verified
Adult status where adult content is enabled.
consent_document_path
Local or secure document reference.
consent_status
Pending / Verified / Expired / Revoked.
permitted_usage
Allowed generation scopes.
adult_content_permission
Explicit scope for adult generation.
commercial_permission
Commercial/affiliate usage rights.
voice_permission
Voice cloning/use rights.
face_permission
Face/likeness use rights.
valid_from / valid_until
Consent validity window.
12.4 Permission Preflight
Real identity detected/selected  -> Rights record exists?  -> Identity/adult requirement satisfied?  -> Requested usage is in permitted scope?  -> Record is valid and not revoked?  -> ALLOW or BLOCK
12.5 Adult Local Mode
A local deployment may enable consensual adult generation for fictional/synthetic adults and documented consenting adults, including authorized public figures when the recorded scope explicitly permits the requested use. The application must not offer a workflow for non-consensual intimate generation. Rights status is evaluated before the job reaches the inference runtime.
13. Module G - UGC Affiliate Factory
13.1 Main Flow
Select Product  -> Select Creator  -> Select/Generate Content Angle  -> Select Format  -> Generate Script + Shot Plan  -> Produce Video  -> Add Voice + Captions + Product Media + CTA  -> Render Platform Variants
13.2 UGC Formats
Product Review
Problem -> Solution
POV
Tutorial
Comparison
Unboxing
Demo
Storytime
Listicle
Reaction
Before/After
Trend Remix
13.3 Production Modes
Mode
Composition
Faceless
Product imagery/B-roll + voice + captions.
AI Creator
Persistent character + product + AI voice.
Motion UGC
AI character + reference motion + MotionControl + product overlay/placement.
Talking Avatar
Character + script + voice + lip sync/face motion.
Remix
Winning creative DNA + new hook/product/creator while preserving selected variables.
13.4 UGC Acceptance Criteria
9:16 export available
Hook appears in opening seconds
Product is clearly identifiable
CTA and affiliate disclosure are configurable
Captions are legible in social safe area
Creator identity remains acceptably consistent
Rendered asset is linked to product, campaign and creative DNA
14. Module H - Distribution and Social Accounts
14.1 Supported Account Model
TikTok
Instagram
YouTube
Facebook
X
Threads
Pinterest
Other provider adapters
Publishing must use official or authorized APIs where available. Where direct publishing is unavailable or restricted, the system exports platform-ready assets and metadata rather than bypassing platform controls.
14.2 Account Fields
platform
account_name
niche
country
language
default_character_id
audience_profile
content_frequency
affiliate_program
status
connection_state
14.3 Calendar and Queue
Calendar view
Queue view
Campaign view
Account view
Approval state
Scheduled time
Publish status
Retry state
Platform response/error
14.4 Platform Variants
Platform
Default Adaptation
TikTok
9:16; concise caption; trend-first hook.
Instagram Reels
9:16; caption/hashtags; safe-area optimized.
YouTube Shorts
9:16; searchable title; description; affiliate links/disclosure.
Facebook
Platform-specific copy and CTA.
15. Module I - Engagement and Lead Intent
15.1 Purpose
Turn engagement signals into structured intent and measurable next actions. The design follows the reference Social Media OS idea that engagement, capture and monetization are part of one funnel rather than isolated tools.
15.2 Intent Classification
Purchase Intent
Product Question
Price Question
Link Request
Positive
Negative
Lead/Booking Intent
Spam/Irrelevant
15.3 Requirements
ID
Requirement
Priority
ENG-01
Ingest accessible comments/messages via authorized APIs.
P1
ENG-02
Classify intent and confidence.
P1
ENG-03
Generate suggested replies with campaign/product context.
P1
ENG-04
Require human approval by default for outbound replies.
P1
ENG-05
Link engagement to content and downstream click/lead events where possible.
P1
16. Module J - Analytics, Revenue and Growth Engine
16.1 Analytics Layers
Layer
Metrics
Content
Views; watch time; completion; shares; saves; comments; follower delta; CTR.
Commerce
Affiliate clicks; orders; GMV; commission; revenue; EPC; CVR.
Production
Generation cost; render time; model/workflow; success/failure; GPU seconds.
Profitability
Attributed revenue - generation cost - paid distribution.
16.2 Revenue Dashboard
Views                 1,240,000Affiliate Clicks          31,420Orders                     2,041GMV                      $84,390Commission                $9,420AI / GPU Cost               $816Net Contribution          $8,604
16.3 Growth Loop
Published Content  -> Performance + Conversion Data  -> Feature Extraction / Creative DNA  -> Winner Detection  -> Recommendation  -> Controlled Variants  -> New Published Content
16.4 Winner Logic
Configurable threshold by views, watch-time, EPC, conversion, profit or composite score.
Minimum sample-size guard before declaring a winner.
Separate organic winner and revenue winner states.
Prevent false winner classification from low-volume outliers.
Store why an item was declared a winner.
17. Autopilot and Agent Architecture
17.1 Autopilot Objective
Autopilot is a goal-directed orchestration mode, not unrestricted autonomous posting. It uses explicit budgets, account permissions, content policies, approval rules and stop conditions.
17.2 Agent Roles
Agent
Responsibility
Research Agent
Find and summarize content/product opportunities.
Product Agent
Rank affiliate products/offers.
Strategist Agent
Select audience, angle, format and experiment.
Script Agent
Generate hooks/scripts/captions.
Creative Director
Select character, workflow, model, motion and style.
Production Agent
Dispatch and monitor generation/rendering.
Publisher Agent
Prepare/schedule approved platform variants.
Community Agent
Classify engagement and draft responses.
Analyst Agent
Evaluate performance and attribution.
Growth Agent
Recommend and create next controlled experiment.
17.3 Autopilot Configuration
Objective: Maximize Affiliate Contribution ProfitDaily Content Cap: 20AI/GPU Budget: $50/dayPlatforms: TikTok, Instagram, YouTubeApproval: Required before publishStop Rule: Pause if 7-day contribution profit < configured threshold
18. ComfyUI Local Runtime and Model Routing
18.1 Role
ComfyUI is a local inference orchestration layer. CreatorOS owns product objects, auth, rights checks, job scheduling and result lineage; ComfyUI owns model graph execution and generation workflow details.
CreatorOS Web/API   -> Rights + Policy Preflight   -> Workflow Router      -> ComfyUI API         -> Local GPU         -> Workflow Result
18.2 Initial Workflow Registry
Workflow
Task
Status
wan_animate_move
Full-body character animation
P0
wan_animate_mix
Character replacement
P0
liveportrait
Face/head/expression transfer
P1
animatediff_dwpose
Stylized pose generation
P1
mimicmotion
Experimental full-body
P2
product_ugc
Composite UGC generation
P1
video_upscale
Post-processing/upscale
P1
18.3 Workflow Versioning
workflow_id, workflow_version, model_version/checkpoint, custom node versions/commitssampler, scheduler, steps, CFG, seed, resolution, frames, FPSLoRAs/adapters, input asset IDs
18.4 Developer Mode
Developer Mode exposes: active engine/workflow; raw/imported workflow JSON; input/output node mapping; advanced generation parameters; missing model/custom-node diagnostics; workflow version pinning.
18.5 Model Manager
Model Manager detects GPU/VRAM, recommends compatible workflows, installs/disables/deletes approved models, tracks disk footprint, applies low-VRAM presets, and reports offline-ready model packages.
19. System Architecture and Deployment
19.1 High-Level Architecture
WEB / DESKTOP CLIENT        |API GATEWAY / BFF        |WORKFLOW ORCHESTRATOR  |        |        |        |  |        |        |        +--> Analytics / Attribution  |        |        +-----------> Social Connectors  |        +--------------------> Commerce Providers  +-----------------------------> AI Gateway                                     |                           +---------+---------+                           |                   |                       Cloud AI            Local Worker                                               |                                            ComfyUI                                               |                                           Local GPU
19.2 Recommended Stack
Layer
Recommendation
Web UI
Next.js + React + TypeScript + Tailwind.
Desktop shell (optional)
Tauri for local-first desktop distribution.
API/BFF
TypeScript service and/or FastAPI depending on workload.
AI/Media Service
Python + FastAPI.
Database
PostgreSQL for cloud/hybrid; SQLite allowed for single-user local desktop.
Queue
Redis + BullMQ for MVP; Temporal for complex long-running production workflows at scale.
Storage
Cloudflare R2/S3-compatible; local disk in Local mode.
Video processing
FFmpeg.
Local inference
ComfyUI.
Observability
Structured logs, traces, generation metrics, GPU metrics.
19.3 Deployment Modes
Mode
Data/Compute
Use Case
Local
Local DB, local media, local ComfyUI/GPU.
Private power users and offline operation.
Hybrid
Cloud dashboard/DB + local worker/ComfyUI + optional cloud AI.
Recommended multi-user production mode.
Cloud
Cloud DB, object storage and AI workers/providers.
Managed SaaS deployment.
19.4 Local Worker
Cloud Dashboard <-> Authenticated Secure Channel <-> CreatorOS Local Worker <-> ComfyUI <-> GPU
20. Data Model
20.1 Core Tables / Collections
Domain
Entities
Identity
users, workspaces, memberships, roles
Commerce
products, product_media, affiliate_offers, affiliate_clicks, orders, commissions
Creative
characters, voices, motions, hooks, scripts, briefs, creative_dna, assets
Generation
ai_providers, ai_models, workflows, workflow_versions, generation_jobs, generation_inputs, generation_outputs
Campaign
campaigns, campaign_products, campaign_characters, experiments
Social
social_accounts, publications, publication_metrics, comments, engagement_events
Analytics
content_metrics, attribution_events, revenue_events, winner_scores, recommendations
Rights
identity_records, consent_records, permission_scopes, rights_audit_log
System
settings, feature_flags, budgets, rate_limits, audit_logs
20.2 Generation Job State
QUEUED -> PREFLIGHT -> PREPROCESSING -> WAITING_FOR_WORKER -> GENERATING -> POSTPROCESSING -> READY                                                  |                                               FAILED / CANCELED
20.3 Content Lineage Requirement
Every published content asset must be traceable back to product, campaign, hook, script, character, motion, voice, workflow version, model/provider, generation job and source assets. This lineage is required for reproducibility and Creative DNA analysis.
21. API Requirements
Area
Representative Endpoints
Products
POST /products/import; GET /products; POST /products/{id}/refresh
Characters
POST /characters; GET /characters; POST /characters/{id}/references
Motions
POST /motions; GET /motions; POST /motions/analyze
Generation
POST /generations; GET /generations/{id}; POST /generations/{id}/cancel
UGC
POST /ugc/brief; POST /ugc/generate; POST /ugc/{id}/variants
Workflows
GET /workflows; POST /workflows/import; POST /workflows/{id}/run
Social
POST /social/accounts/connect; POST /publications; GET /publish-queue
Analytics
GET /analytics/content; GET /analytics/revenue; GET /analytics/creative-dna
Growth
POST /winners/{content_id}/scale; GET /recommendations
Rights
POST /rights/identities; POST /rights/consents; POST /rights/preflight
21.1 Generation Request
{  "task": "motion_ugc",  "mode": "auto",  "character_id": "char_123",  "product_id": "prod_123",  "motion_id": "mot_123",  "workflow_id": "wan_animate_move",  "aspect_ratio": "9:16",  "resolution": "720p"}
22. Workflow and Event Model
22.1 Core Events
product.discovered
product.imported
opportunity.scored
brief.created
hook.created
script.created
generation.requested
generation.completed
generation.failed
content.approved
content.published
metrics.updated
affiliate.clicked
conversion.received
winner.detected
variant.requested
22.2 Why Event-Driven
Agents remain decoupled.
Long-running generation survives web request timeouts.
Every stage can be retried independently.
Auditability is improved.
New social or commerce connectors can subscribe without rewriting the generation pipeline.
23. Security, Privacy, Safety and Rights
23.1 Privacy Modes
Mode
Behavior
Local Privacy
No cloud inference; local assets; telemetry off; local rights records.
Hybrid Privacy
Cloud metadata as configured; sensitive generation can be forced local.
Cloud
Managed storage/inference subject to deployment policy and provider requirements.
23.2 Rights and Consent
Permission is an explicit data object, not a UI disclaimer.
Consent may be time-limited or revoked.
Requested use must match allowed scope before inference.
Commercial/affiliate rights are tracked independently from appearance/voice rights.
Adult local workflows require adult status and the relevant explicit permission scope for real people.
Non-consensual intimate generation is not supported.
23.3 Security Requirements
Encrypt secrets/API tokens at rest.
OAuth tokens scoped minimally and refresh securely.
Workspace data isolation.
Audit all rights changes and publishing actions.
Signed URLs for cloud object access.
No arbitrary ComfyUI custom-node installation from untrusted sources by default.
Pin approved node versions / commit hashes.
Validate uploaded files and enforce size/type limits.
24. Non-Functional Requirements
Area
Target / Requirement
Availability
Web/control plane target >=99.5% for MVP; local generation remains usable if cloud control plane is unavailable where local mode permits.
Performance
Non-generation API p95 < 800 ms under normal load.
Job Reliability
Infrastructure failures retry safely; duplicate publish/generation side effects prevented via idempotency.
Generation Success
Target >=90% usable completion in Beta for supported workflows.
Storage
Configurable retention; clean orphaned temp assets.
Cost Controls
Per-user, per-workspace and global generation budgets.
Scalability
Queue workers horizontally scalable; provider adapters stateless where possible.
Observability
Job-level logs, failure reason, provider latency, GPU utilization, cost telemetry.
Accessibility
Keyboard-accessible primary product flows; contrast and readable caption controls.
Localization
UI/content metadata ready for multi-language and market-specific templates.
25. Admin and Operations
System dashboard: active users, jobs, failure rate, generation cost, GPU queue.
User/workspace management: quota, suspend, usage, costs.
Workflow registry: enable/disable/version/rollback.
Model registry: capability, VRAM, disk footprint, status.
Affiliate provider health: API status, sync errors, quota.
Social connector health: token expiry, publish errors, API limits.
Rights audit: consent status, expiries, blocked requests.
Feature flags: Autopilot, Adult Local Mode, direct publishing, cloud provider availability.
25.1 Kill Switches
Disable cloud free generation globally
Disable a failing workflow/model
Pause all direct publishing
Pause a social connector
Pause a commerce provider
Stop Autopilot globally or per workspace
Block a compromised API token/provider
26. UX and Design System
26.1 Product Feel
The UX should feel like a creative production operating system rather than enterprise reporting software: visual, fast, high-density where needed, with large media previews, strong status visibility and minimal jargon for non-technical users. Advanced model parameters live behind Developer Mode.
26.2 Desktop Layout
LEFT NAV           MAIN WORKSPACE                    RIGHT INSPECTORProducts            media/canvas/calendar/table       context settingsCreate              previews/workflows/results        selected objectDistribute                                            AI/model controlsGrow
26.3 MotionControl Mobile Flow
1 Choose Character -> 2 Choose Motion -> 3 Preview/Settings -> 4 Generate -> 5 Result/Share
26.4 Core UX Principles
Show actual job stage, not a generic spinner.
Keep Auto as default; expose model/workflow details only when needed.
Every AI recommendation is editable.
Every autonomous action has budget/permission/approval state.
Surface cost and expected impact before large batch generation.
Make winner scaling a first-class one-click action.
27. MVP Scope and Milestones
Milestone
Scope
Exit Criteria
M00 Foundation
Next.js app; workspace; DB; storage; Redis/queue; audit basics; local-worker protocol.
User can sign in/create workspace and submit a durable background job.
M01 AI Studio
Provider abstraction; image/video generation; history; reference assets; simple workflow templates.
Prompt/reference -> generated asset -> library.
M02 ComfyUI
Local connection; workflow registry; GPU status; queue; model inventory.
Web request -> local ComfyUI -> result with lineage.
M03 MotionControl
Wan Move/Mix; motion upload; character upload; analysis; 9:16 output.
Image + reference video -> usable MP4.
M04 Character/Rights
Persistent character; voice reference; identity strength; consent/rights registry.
Saved character can be reused with successful preflight.
M05 Amazon Commerce
Amazon URL import; normalized product; affiliate URL; images/features; opportunity score.
Product URL becomes campaign-ready Product object.
M06 UGC Factory
Hook/script; voice; captions; product media; creator video; render.
Amazon URL + Creator -> 3 UGC variants.
M07 Distribution
YouTube first; publish/export metadata; queue/calendar; approval.
Approved Short can be published through authorized connection.
M08 Analytics
Content metrics; clicks; revenue import; content profit.
Published content maps to performance + commerce metrics.
M09 Growth Engine
Creative DNA; winner detection; Scale Winner variants.
System generates controlled variants from measured winner.
M10 Autopilot
Goal/budget/rules; agent orchestration; approval gates.
System can run one bounded daily campaign loop with operator oversight.
27.1 Strict MVP
MVP DefinitionAI Studio + ComfyUI + MotionControl + Character Library + Amazon Product Import + UGC Script + AI Voice + UGC Video + YouTube Shorts Export/Publish + Affiliate Link.
28. Testing and Acceptance Criteria
28.1 Functional Acceptance
Import supported Amazon product URL and create normalized product record.
Create persistent character and attach reference assets.
Run permission preflight for real-person character.
Submit MotionControl generation and receive MP4.
Generate at least three UGC variants from one product/creator combination.
Create platform-ready 9:16 output with captions and CTA.
Publish or export YouTube Shorts package.
Record click/revenue event and connect it to content.
Identify winner using configured rule and create a controlled variant batch.
28.2 Reliability Tests
Worker disconnect during generation
ComfyUI crash
GPU OOM
Provider timeout
Duplicate generation request
Expired social token
Marketplace API failure
Partial media upload
Rights record revoked before queued job starts
Publish retry without duplicate post
28.3 Quality Gates
Gate
Target
Supported generation success
>=90% Beta
Critical API contract tests
100% passing
Publish idempotency
No duplicate publication in retry test
Rights preflight
100% blocked when required permission missing/expired
Lineage completeness
100% published assets contain required lineage IDs
Cost telemetry
>=95% generation jobs report compute/provider cost estimate
29. Roadmap
Phase
Capabilities
Phase 1 - Create
AI Studio; ComfyUI; MotionControl; Characters; Amazon UGC.
Phase 2 - Distribute
Multi-account calendar; YouTube; more official social connectors; approval workflows.
Phase 3 - Measure
Commerce attribution; Creative DNA; profitability dashboard.
Phase 4 - Grow
Scale Winner; experiments; recommendation engine; automated content mutation.
Phase 5 - Operate
Autopilot agents; multi-market account portfolio; budget optimizer.
Phase 6 - Marketplace
Motion templates; workflow marketplace; creator packs; reusable production recipes.
30. Risks and Mitigations
Risk
Impact
Mitigation
Generation quality variance
Unusable outputs / user frustration
Compatibility scoring, workflow presets, fallback routing, QA sampling.
GPU/VRAM constraints
Local failures
Hardware detection, low-VRAM presets, frame/resolution caps, cloud fallback.
Custom node breakage
Workflow instability
Approved registry, pinned commits, workflow versioning, rollback.
Affiliate/API changes
Product ingestion breaks
Provider abstraction, sync health, graceful degradation.
Social API restrictions
Cannot auto-publish everywhere
Official connectors; export-ready fallback; never rely on prohibited bypasses.
Attribution gaps
Wrong optimization decisions
Confidence scores, last-click + configurable attribution, minimum sample thresholds.
Autopilot quality drift
High-volume low-quality content
Budgets, approval gates, daily caps, winner thresholds, stop rules.
Identity/right misuse
Legal and reputational risk
Structured rights registry, scope preflight, audit log, non-consensual intimate use unsupported.
Cloud cost runaway
Negative unit economics
Budget limits, quotas, model routing, local compute.
Product hallucination
Misleading claims
Ground scripts in product source fields/reviews; fact-check constraints; editable claims.
Operators confuse NVIDIA free apps with unlimited official video generation
False expectations / churn
PRD-locked messaging; UI copy states NVIDIA accelerates, open models generate.
Broadcast + ComfyUI concurrent VRAM contention
OOM / failed jobs
Preflight free-VRAM check; pause Broadcast effects during heavy generate.
RTX Video browser upscale marketed as export
Broken client deliverables
Capability flag export_capable=false for browser VSR.
Game Ready driver instability in long Comfy queues
Failed overnight batches
Recommend Studio Driver; log driver branch on every job.
Windows 10 driver feature freeze after Oct 2026
Missing NVFP4/new nodes
Detect OS; warn Win10 operators; hybrid cloud fallback.
31. Source and Implementation References
The following public references were reviewed on 2 September 2026 and inform implementation direction. They are references, not requirements to copy code wholesale.
Reference
Relevant Takeaways
HeliosGen - https://github.com/segfault42/heliosgen
Open-source local visual AI workflow builder; infinite node canvas; multi-model image/video pipelines; local database/media; Tauri + Next.js/React/TypeScript; Kie.ai backend.
Amazon Affiliate - https://github.com/profullstack/amazon-affiliate
Amazon URL/ID -> product data -> AI script -> ElevenLabs voice -> FFmpeg video -> YouTube publish -> affiliate link/social promotion pattern.
ComfyUI Wan2.2 Animate workflow - https://docs.comfy.org/tutorials/video/wan/wan2-2-animate
Wan Animate supports character animation and replacement. Workflow guidance includes DWPose/face preprocessing and Move/Mix operation.
Wan2.2 / Wan-Animate - https://github.com/Wan-Video/Wan2.2
Primary open model family reference for character animation/replacement capability.
Internal reference video uploaded by product owner
AI Social Media Operating System concept: content/production/distribution/engagement/monetization/analytics with winning hooks feeding back into research and a compounding growth loop.
NVIDIA App / Studio Driver / ShadowPlay
Workstation control plane, driver branch, capture overlay. Not a generation runtime.
NVIDIA Broadcast 2.2
Free AI mic/cam preprocessing on RTX 2060+; Studio Voice on 3060 desktop+.
NVIDIA ComfyUI + LTX/FLUX RTX guides (2026)
Official local visual gen path; NVFP4/FP8; RTX Video node for export upscale.
Project G-Assist / ChatRTX
Optional local assistants. G-Assist = system tuner. ChatRTX = file RAG demo. Neither is the Creative Director agent.
31.1 Architectural Interpretation
HeliosGen contributes the interaction model and local workflow philosophy, not the root product definition.
Amazon Affiliate contributes a proven automation sequence and provider integration reference, not the final data architecture.
ComfyUI is an execution runtime beneath a stable CreatorOS workflow abstraction.
The internal Social Media OS reference contributes the feedback-loop principle: analytics and monetization must drive the next research and content cycle.
32. Appendix - Initial Engineering Backlog
ID
Backlog Item
Priority
PLAT-001
Workspace + RBAC
P0
PLAT-002
Asset storage abstraction local/R2
P0
PLAT-003
Redis job queue + idempotency
P0
PLAT-004
Local Worker registration/heartbeat
P0
AI-001
AI provider interface
P0
AI-002
ComfyUI client + queue bridge
P0
AI-003
Workflow registry/versioning
P0
AI-004
Model/GPU capability detection
P1
MOT-001
Character image upload/analyze
P0
MOT-002
Motion video upload/trim/analyze
P0
MOT-003
Wan Move workflow integration
P0
MOT-004
Wan Mix workflow integration
P0
MOT-005
Result page + library
P0
CHR-001
Persistent Character CRUD
P0
CHR-002
Voice profile linkage
P1
RGT-001
Identity rights registry
P0
RGT-002
Permission preflight service
P0
COM-001
AffiliateProvider interface
P0
COM-002
Amazon provider product import
P0
COM-003
Affiliate offer/tracking fields
P0
COM-004
Opportunity score
P0
UGC-001
Hook/script generation
P0
UGC-002
TTS/voice integration
P0
UGC-003
UGC render composition
P0
UGC-004
Three-variant campaign generation
P0
SOC-001
SocialAccount model
P0
SOC-002
YouTube OAuth + publishing
P0
SOC-003
Calendar/publish queue
P0
ANA-001
Content metrics ingestion
P1
ANA-002
Affiliate click/conversion ingestion
P1
ANA-003
Content profit computation
P1
GRO-001
Creative DNA extraction
P1
GRO-002
Winner detection
P1
GRO-003
Scale Winner variant service
P1
AGT-001
Agent event bus
P2
AGT-002
Bounded Autopilot policy engine
P2
NV-001
Detect NVIDIA GPU, VRAM, driver branch (Studio vs Game Ready), NVENC generation, Tensor Core presence
P0
NV-002
NVIDIA capability card in Settings/System: recommended apps, missing installs, VRAM tier routing
P0
NV-003
Prefer Studio Driver recommendation for production workstations; expose one-click deep-link to NVIDIA App
P1
NV-004
NVENC encode path in UGC render/FFmpeg/OBS export presets (HEVC/AV1 by GPU generation)
P0
NV-005
ComfyUI precision routing: NVFP4 for RTX 50, FP8 for RTX 40, GGUF/offload for <=16GB
P0
NV-006
Optional Broadcast virtual device detection for talking-head capture pipelines
P2
NV-007
RTX Video Super Resolution as Comfy/export node only; never market browser VSR as export upscaler
P1
NV-008
Cost model: local GPU seconds + electricity estimate; no NVIDIA per-generation fee
P0
NV-009
Grok terminal instruction pack version-pinned with PRD; agent must load before implementation work
P0
NV-010
Kill-switch: disable NVIDIA-specific optimizations if driver/API probe fails; fall back to generic CUDA/CPU encode
P1
Final Product Definition
CreatorOSAn AI Creator Commerce Operating System that identifies opportunities, creates social-native affiliate content, runs local or cloud AI production, distributes approved content, measures revenue, learns Creative DNA and scales what works.
The product should progress in maturity as follows:
AI creates content.
AI prepares and distributes content.
AI understands which content performs.
AI understands which content makes money.
AI creates more of what makes money - within explicit budget, rights and approval rules.
33. NVIDIA RTX Local Creator Stack
This section is additive to v2.0 and is locked for v2.1. It defines what an NVIDIA GPU actually gives CreatorOS for free, what it does not give, and how the product must use that stack.
33.1 Product Decision
Owning an NVIDIA RTX card does not unlock an official unlimited NVIDIA image/video generator. It unlocks a free capability layer: drivers, encoder, realtime AI filters, local assistants, and accelerated open-source inference. CreatorOS generation remains ComfyUI + approved open-weight models, optionally routed to cloud providers.
33.2 Capability Map
Capability
NVIDIA component
CreatorOS use
Not this
Workstation control
NVIDIA App
Detect GPU/driver, deep-link install, overlay capture for reference takes
Not the CreatorOS UI
Production stability
Studio Driver
Default recommendation for generate/edit machines
Not required for inference to start
Capture / replay
ShadowPlay overlay
Optional reference-motion capture; Instant Replay for failed takes
Not a multi-scene NLE
Mic / camera AI
Broadcast 2.2
Optional talking-head preprocess; virtual mic/cam into OBS
Not TTS; not character voice
Watch-time upscale
RTX Video Super Resolution + HDR
Playback of references in browser/VLC
Not an export upscaler
Export upscale
RTX Video node in ComfyUI
Postprocess generated UGC to 1080p/4K when export-capable node is present
Not the Chrome filter
Encode
NVENC H.264 / HEVC / AV1
Default FFmpeg/OBS/UGC render encoder so inference VRAM stays free
Not a substitute for generation
Precision / VRAM
NVFP4 (RTX 50), FP8 (RTX 40)
Router picks quantized Comfy checkpoints by GPU family
Not a quality guarantee
System assistant
Project G-Assist (Alt+G)
Optional operator helper for thermals/settings; plugin surface watched
Not Autopilot / Growth Agent
Local file chat
ChatRTX
Optional private RAG over workspace docs
Not Script Agent source of truth
Dev containers
AI Workbench
Optional engineer path
Not in creator MVP
Cloud playground
build.nvidia.com
Research sandbox only
Not production inference; rate-limited
33.3 Hardware Tiers for Router
Tier
Typical GPU
CreatorOS local policy
T0 Entry
RTX 8–12GB
Image yes (SDXL / Flux GGUF). Video only LTX/Wan 5B quantized, short clips, heavy offload. Broadcast during generate = off.
T1 Production
RTX 16GB
Image comfortable. LTX-2.3 FP8 + Wan 5B/14B GGUF. UGC Factory default 720p 5–8s. NVENC encode required.
T2 Studio
RTX 24GB (4090 class)
Wan 14B / Hunyuan 1.5 / overnight batch. MotionControl P0 workflows. Broadcast allowed if free VRAM >= 4GB after load.
T3 High
RTX 32GB+ (5090 class)
NVFP4 preferred. Higher-res / longer chain / concurrent queue workers. Still not a Veo replacement.
TCloud
No NVIDIA / insufficient VRAM
Hybrid/cloud adapters. Local worker optional for encode only.
33.4 Runtime Principles
No per-generation NVIDIA license fee. Cost telemetry records GPU-seconds and estimated kWh only.
ComfyUI stays the inference orchestrator. NVIDIA App is never a workflow engine.
Prefer Studio Driver on machines whose primary job is generation. Log driver branch + version on every Generation Job.
NVENC is the default final-render encoder when available. Do not encode H.264 on the same CUDA context that is denoising video if NVENC exists.
Browser RTX Video is playback-only. Only Comfy/Resolve/SDK export paths may be labeled Upscale for Publish.
Broadcast, G-Assist plugins, and overlay must yield VRAM before a generation job starts if free VRAM is below the workflow minimum + 2GB headroom.
Dead or deprecated NVIDIA apps (example: NVIDIA Canvas) must not appear in product copy or install checklists.
Windows 10: warn that Game Ready/Studio feature drops after October 2026. Do not block local mode.
License of the open model (Flux Dev vs Schnell/Klein, LTX community cap, Wan Apache 2.0) is still enforced by the Rights + Policy Preflight. NVIDIA stack does not change model license.
33.5 Functional Requirements
ID
Requirement
Priority
NVS-01
On worker start, probe nvidia-smi / NVML: name, VRAM total/free, driver version, driver branch if detectable, NVENC support, GPU architecture family (20/30/40/50).
P0
NVS-02
Surface a System > NVIDIA panel listing installed vs missing recommended apps and one-action deep links.
P1
NVS-03
Workflow router must accept gpu_tier and precision_policy (auto|fp4|fp8|gguf|offload).
P0
NVS-04
UGC render pipeline must select NVENC when present; fall back to libx264/libsvtav1 with explicit log.
P0
NVS-05
Generation preflight fails closed if required VRAM exceeds free VRAM after optional Broadcast pause.
P0
NVS-06
Do not ship or recommend ChatRTX/G-Assist as content generators. If exposed, label Operator Tools.
P0
NVS-07
Job lineage stores gpu_name, vram_mb, driver_version, precision, encoder.
P0
NVS-08
Settings copy must state local mode has no NVIDIA token cost; electricity/hardware is operator-borne.
P0
33.6 Install Checklist for RTX Operators
Shipped in-product and in Grok terminal instructions. Order is mandatory for support.
1. Install NVIDIA App from NVIDIA official site. Skip GeForce Experience.
2. Clean-install Studio Driver on production machines.
3. Confirm nvidia-smi works and VRAM matches the physical card.
4. Install Broadcast only if talking-head capture is in scope.
5. Install ComfyUI via Stability Matrix or ComfyUI Desktop. Do not invent a second Python stack.
6. Download approved checkpoints through Model Manager. Flux Schnell/Klein or Qwen for commercial image. LTX FP8 + Wan GGUF for video.
7. Verify one still image, then one 5s video, then NVENC encode of that file.
8. Only then connect the CreatorOS Local Worker.
33.7 Messaging Rules
Allowed: Unlimited generations on your GPU after setup. Cost is electricity and time.
Allowed: NVIDIA gives you the engine room. Open models do the painting.
Forbidden: NVIDIA unlimited official Sora. Forbidden: RTX Video exports 4K from Chrome. Forbidden: G-Assist writes viral scripts.
34. Grok Terminal Operating Instructions
This section is the in-PRD copy of the terminal instruction pack. The canonical operator file lives beside this PRD as GROK.md / GROK_TERMINAL_INSTRUCTIONS_CreatorOS.md. Engineering agents running in terminal MUST load that file before writing code, schemas, or workflows for CreatorOS.
34.1 When to load
Any implementation, review, architecture, or GTM task for CreatorOS / MotionControl / UGC Factory / ComfyUI worker.
Any local image/video / NVIDIA / affiliate / social publishing question tied to this product.
34.2 Hard rules for Grok in this repo
Treat this PRD v2.1 as source of truth. Do not shrink the product back into a Motion Control toy.
Do not invent a new foundation model. Route through ComfyUI + provider adapters.
Do not bypass official social APIs. Export-ready fallback only.
Do not implement non-consensual intimate generation. Rights preflight before inference.
Do not promise cloud unlimited GPU. Local unlimited = no per-job app fee.
Do not install untrusted Comfy custom nodes by default. Pin approved commits.
NVIDIA stack is acceleration + capture + encode. Open weights generate.
Every published asset needs lineage: product, character, hook, workflow version, model, job, GPU, encoder.
Autopilot stays gated: budget, approval, stop rules.
Prefer Hybrid architecture: cloud control plane + local worker.
34.3 Terminal bootstrap
From repo root, an operator starts a Grok/CLI agent with: load GROK.md, then the relevant role skill (project-manager, system-analyst, database-engineer, system-security, ui-ux, web-developer). Work the swarm order only in product/strategy answers. In implementation mode, execute against the current milestone in Section 27 and the backlog IDs including NV-001..NV-010.
34.4 Definition of done for NVIDIA-related tickets
Worker reports GPU inventory.
Router selects a legal workflow for that VRAM tier.
Job records precision + encoder.
Render uses NVENC when present.
UI does not call NVIDIA apps a generator.
Failure path is explicit: OOM, driver missing, Broadcast VRAM steal, encode fallback.