# AtlasNow — Meta AI Creative Studio
## Product Requirements Document (PRD) — Hackathon MVP

**Status:** Proposed / not yet verified against the current AtlasNow repository  
**Version:** 1.0  
**Prepared:** 2026-11-03  
**Product:** AtlasNow.co  
**Strategic goal:** Turn a merchant's basic product photo into accurate, campaign-ready creative assets and connect the output to measurable customer actions.  
**Primary dependency:** Meta Model API credentials reportedly connected; live model inference still must be verified.

---

## 1. Executive summary

Build **AI Creative Studio** as a native AtlasNow merchant workflow. Merchants choose a business location and catalog product, upload a basic photo, select a campaign preset, and generate variations using Meta models. Merchants preview, approve, optionally edit, export, and attach a traceable conversion CTA.

**Product loop:** Photo → Product understanding → Object segmentation → Image generation/editing → Brand-accurate compositing → Approval → Export with CTA → Conversion tracking where technically supported.

**MVP in scope:** working Meta Model API calls; image creative generation; 3 presets; a brand-safe composer; an asset library; export; request/error logging; a small, defensible tracking mechanism.  
**Phase 1 stretch:** SAM 3.1 masks, 3 additional presets, WhatsApp voice-to-order using Muse Voice Transcribe.  
**Not MVP:** autonomous Meta Ads publication, campaign budget changes, video generation by Muse Image, promises of offline revenue attribution without an order/POS connection, or a new standalone chatbot.

## 2. Goals and non-goals

### Goals
1. Demonstrate **genuine, verifiable** Meta Model API use and complete a live demo with real returned artifacts.
2. Give non-designer merchants a sub-five-step creative workflow (location/product → upload → preset → generate → approve/export).
3. Preserve actual product identity and exact merchant-supplied facts (price, offer, logo, branch name).
4. Reuse AtlasNow's tenant, location, permissions, brand, catalog, media, and commerce systems when present.
5. Log enough operational evidence for hackathon validation without exposing secrets or customer PII.

### Non-goals
- Replace the existing AtlasNow navigation, auth, billing, deployment, analytics, or YOLA FUN workflows.
- Claim Meta Ads integration unless the repository contains a functioning, authorized Meta Marketing API integration.
- Auto-send customer messages or auto-create orders without user confirmation.
- Build on local open-weight Muse models during hackathon MVP.

## 3. Information architecture / navigation

**Audit existing sidebar and routes before adding anything.** Names/paths below are proposals, not assertions about the live dashboard.

Recommended location in the navigation:

```
Marketing (existing if present)
  ├── AI Creative Studio   /marketing/creative-studio
  └── Creative Library    /marketing/creative-library   [optional; prefer in-page Library tab if sidebar is crowded]

YOLA FUN (existing)
  └── Voice-to-Order      [inside existing conversations/order workflow, not new root nav]

Analytics (existing)
  └── AI Creative performance / trackable CTA events [when events are instrumented]

Settings / Integrations (existing)
  └── Meta Model API status, quota, error history [admin-only]
```

Do not create a duplicate `Marketing` section if the existing taxonomy already has Growth/Campaigns or equivalent. Reuse an existing relevant parent. Menu items are permission-aware and mobile responsive.

### AI Creative Studio page
- Tabs: **Create**, **Library**, **Usage** (Usage can be admin-only).
- Main CTA: **Create Creative**.
- Empty state: photo-based walkthrough and one safe demo sample (label sample clearly).
- Mobile: simple stepper; desktop: split editor + live preview.
- Visual design: match existing AtlasNow design tokens; no generic AI-dashboard gradients or visually disconnected components.

## 4. Merchant personas

- **Single-location restaurant manager:** promote a lunch meal using a phone photo, existing menu price, local pickup CTA.
- **Multi-location marketing manager:** generate assets with a location-specific phone, address, offer, and brand rules.
- **Retail merchant:** create product visuals for Instagram/Meta placement without changing SKU attributes.

## 5. End-user workflows

### 5.1 Create creative
1. Choose **location**. If only one authorized location exists, preselect.
2. Choose **catalog product** if available; otherwise enter product name, category, price, currency, optional promo and CTA. Do not create a duplicate canonical catalog product just for generation.
3. Upload a product image (JPG/PNG/WebP; validate server-side; suggest <=10 MB for MVP, subject to actual infrastructure limits). Show source image and optional crop.
4. Choose preset (MVP: `Product Hero`, `Promo Offer`, `Best Seller`; additional: `Bundle Deal`, `New Arrival`, `Seasonal`). Pick output dimensions: 4:5 (1080×1350) or 9:16 (1080×1920) as final composited export sizes.
5. Click **Generate**; show queued/running/succeeded/failed state and meaningful progress. Backend uses Muse Spark to structure the brief, SAM 3.1 (when enabled and tested) for segmentation, and Muse Image for generation/editing. If SAM is unavailable, a transparent fallback uses direct reference-image editing; never claim SAM ran when it did not.
6. Show **three variants** (MVP target), each with clear `Regenerate`, `Edit Prompt`, `Approve`, and `Download` actions. Allow merchant to approve before external distribution.
7. Render price, discount, logo, business identity, branch address and CTA via deterministic compositor, not only generative image text. Validate source-of-truth fields.
8. Export PNG/JPG image and copy shareable marketing text. Optionally generate a location-specific WhatsApp CTA link with a campaign tracking identifier if AtlasNow already has a verified messaging integration.

### 5.2 Library
- View current merchant's creations, grouped by location/product/campaign.
- Status: Draft, Processing, Ready for Review, Approved, Failed, Archived.
- Filter by location, preset, date, status.
- Reuse an asset for the same merchant; revalidate offer/price on re-export.

### 5.3 Voice-to-Order (stretch, inside YOLA FUN)
- For inbound WhatsApp voice notes only, retrieve the media using the existing authorized channel integration.
- Convert to supported audio format (only when required), transcribe with `muse-voice-transcribe-1.0`, and optionally supply merchant menu vocabulary.
- Muse Spark extracts structured intent and item/modifier/quantity/pickup time.
- Validate against real merchant catalog, opening hours and current availability.
- Send a **confirmation request** and create/update an order only after the customer approves, using the application's existing order pipeline.
- Keep confidence/error handling, human handoff, and idempotency; never infer availability or fabricate prices.

## 6. Model responsibilities and integration

| Role | Model | Minimum implementation |
|---|---|---|
| Structured creative brief, product facts, captions | `muse-spark-1.3` | Real server-side inference, JSON schema validation, hallucination-resistant field mapping |
| Generate/edit merchant product image | `muse-image-1.0` | Real image edit/generation call, with uploaded source image as reference |
| Foreground segmentation (after validation) | `sam-3.1` | Real segmentation request, mask processing; feature-flagged if unreliable |
| Inbound voice note transcription (stretch) | `muse-voice-transcribe-1.0` | File transcription and transcript-to-order handoff |

Meta official base URL: `https://api.meta.ai/v1` (server-side only).  
Relevant published endpoints:
- Muse Spark: Chat Completions or Responses API with `muse-spark-1.3`.
- Muse Image: `/v1/images/generations`, `/v1/images/edits`, or Responses API for multi-turn editing.
- SAM 3.1: `/v1/responses` with `sam-3.1` and the documented multimodal input schema.
- Muse Voice Transcribe: `POST /v1/asr/transcribe` for files; realtime WebSocket exists but not needed for voice notes.

**Implementation caution:** Do not invent model arguments, response fields, mask encoding, or file transport. Use the official documentation and perform a real request in the project's environment before finalizing adapters. Model access and scopes are not proven merely by storing an API key.

### Mandatory provider design
- A single `MetaModelApiClient` adapter with separate method-level integrations, server-only key and model settings.
- Reuse existing secrets management and env conventions; never embed key in frontend or CI artifacts.
- Timeout, explicit retry for transient 429/5xx (bounded exponential backoff), request IDs and idempotency where applicable.
- Trace each real call by `provider=meta`, actual `model_id`, timestamp, status, duration, merchant/tenant ID (internal), and request ID if returned.
- Persist no raw PII in debug logs. Store source and output images in the existing secured object store, not third-party signed URLs as permanent storage.
- Show real generation state; do not fake progress or API success.
- Optional cost estimate based on actual returned usage/provider pricing, with a clear `estimate` label.

## 7. Preset definitions

1. **Product Hero** — product centered, professional styling, clean background, no unsupported claims.
2. **Promo Offer** — product foreground with deliberate negative space for exact offer/price/CTA overlays.
3. **Best Seller** — premium product emphasis; do not claim bestseller status unless merchant explicitly selects/affirms it.
4. **Bundle Deal** [stretch] — only use actual verified products and bundle data.
5. **New Arrival** [stretch] — feature product and placement, only if merchant declares it new.
6. **Seasonal** [stretch] — adaptable campaign style, no fabricated event claims.

All presets include `style_prompt`, `negative_constraints`, `required_safe_area`, `source_image_reference_required`, `compositor_layout`, and `output_aspect_ratio`.

## 8. Brand / product fidelity policy

- Protect physical product facts (packaging, portion, ingredients, colors, product markings). Merchant must approve visual variations.
- Do not alter names, real prices, discount percentages, stock, product claims or business location using generative guesses.
- For regulated verticals (e.g., clinics), do not fabricate testimonials, patient outcomes or medical before/after images.
- Source merchant brand/logo only from approved tenant assets; draw it via deterministic compositor.
- Ensure final text readable at mobile size and not clipped by platform UI safe areas.
- Preserve source and final artifacts separately, and show an AI-generated/edit disclosure inside product UI where appropriate.

## 9. Multitenancy, security, and permissions

- Every query and storage key must be scoped to merchant/organization; location limited by authorized user access.
- Use existing RBAC and row-level security (if configured). No cross-merchant image sharing by default.
- Signed upload/download URLs with expiration, malware/file-type and size validation, MIME sniffing.
- No public unauthenticated generation endpoint. Per-tenant rate limits, concurrency and credits.
- No access token or personal customer data in prompt/debug logs. No autopublishing or changing ad spend without explicit merchant permission.
- Avoid breaking existing YOLA FUN orders, reviews, auth, billing, or marketing routes.

## 10. Proposed data model (adapt to repo; do not duplicate existing tables)

- `ai_creative_projects`: id, tenant_id, location_id, catalog_product_id?, created_by, preset_id, campaign_name?, status, source_facts_snapshot, created_at/updated_at.
- `ai_creative_assets`: id, project_id, tenant_id, type (`source|mask|generated|composed`), storage_key, width, height, mime, selected, approval_status, created_at.
- `ai_creative_jobs`: id, project_id, task_type, provider, model_id, status, attempts, started_at, ended_at, error_code?, external_request_id?, usage?, estimated_cost?.
- `ai_creative_presets`: id, slug, display_name, parameters, enabled, version.
- `ai_creative_events`: id, tenant_id, location_id, project_id, asset_id?, event_type, occurred_at, campaign_id?, anonymous_session_id? (privacy-reviewed).

Follow existing naming / ORM / migration / tenancy conventions in repository, rather than rigidly copying these names.

## 11. API / backend proposal (internal routes, adapt to current framework)

```
POST   /api/marketing/creatives/projects
GET    /api/marketing/creatives/projects
GET    /api/marketing/creatives/projects/:id
POST   /api/marketing/creatives/projects/:id/source-upload
POST   /api/marketing/creatives/projects/:id/generate
GET    /api/marketing/creatives/jobs/:jobId
POST   /api/marketing/creatives/assets/:assetId/approve
POST   /api/marketing/creatives/assets/:assetId/export
GET    /api/marketing/creatives/presets
GET    /api/marketing/creatives/usage
```

Follow existing backend routing conventions; prefer background job execution for potentially slow model requests. All endpoints require auth + tenant authorization. Validate request schema and handle expired media URLs.

## 12. Outcome tracking / business KPIs

### Product instrumentation
- `creative_project_created`
- `creative_generation_started`
- `creative_generation_succeeded`
- `creative_generation_failed`
- `creative_asset_approved`
- `creative_asset_exported`
- `creative_cta_clicked` (only if AtlasNow link redirects actually observe a click)
- `creative_inbound_lead_matched` (only when existing channel/order IDs can verify the association)
- `creative_order_attributed` (only when an actual tracked order/customer action supports it)

### Operational metrics
- Successful generation rate, completed projects per merchant, median generation latency, model cost per approved asset, approval/download rate.

### Revenue claims safeguards
- Creative export is **not** an ad impression; CTA click is **not** an order; a conversation is **not** a sale.
- If Meta Marketing API / POS attribution is not connected, show `Not connected` instead of fabricated reach, ROAS, conversions or revenue.

## 13. UX details and error states

- Show empty, loading, processing, partial failure, retryable error, quota reached, and no-permission states.
- Support source-image preview and variant comparison at target aspect ratios.
- No silent replacement of uploaded product photo; keep editable source and history.
- Mobile touch targets and accessible labels; adhere to AtlasNow design system.
- Ensure price/coupon/logo overlays stay in safe area; do not rely on AI to render fine print.
- If provider is unavailable, preserve the draft, show a recoverable error, and do not deduct completed-output credits.

## 14. Acceptance criteria / definition of done

**Must pass before marking AI Creative Studio completed:**
1. Authorized merchant can open the module and is restricted to their own tenant/locations.
2. Merchant can upload a valid photo, select a product/preset and generate at least one actual image from Muse Image via Meta Model API.
3. At least one *real* Muse Spark call structures or transforms the brief. Returned model IDs are recorded truthfully.
4. SAM 3.1 is marked integrated **only** if a real segmentation response and useful mask are processed; otherwise show the direct-edit fallback and mark SAM pending.
5. Three variants requested when supported, with per-asset preview; failures are explained and retriable.
6. Final exported creative includes the **exact** merchant-provided price, location-specific CTA, correctly placed logo, and the approved variant.
7. Asset library persists across refresh and authorized navigation.
8. A second merchant cannot read, modify or download the first merchant's files/data.
9. No client bundle or logs expose Meta credentials.
10. At least one complete demo recording can show upload → model request → generated creative → approval → export, plus actual backend logs with secrets redacted.
11. Existing AtlasNow / YOLA FUN workflows remain unchanged and pass smoke tests.
12. No production deployment before founder approval.

### Stretch feature acceptance criteria — Voice-to-Order
1. A real inbound voice note transcribes through Muse Voice Transcribe and logs correct model ID.
2. Order extraction uses real menu prices and resolves ambiguity before creating a confirmed order.
3. Duplicate webhook delivery cannot create duplicate orders.
4. No outbound message sent without the existing channel permissions and conversation policy.

## 15. Build / release sequence for Grok

### Stage 0 — Read-only repository audit (must happen first)
- Inspect framework, deployment setup, menu/sidebar, existing Growth/Marketing/Catalog/Media/YOLA FUN/Analytics routes, auth/RBAC, tenant/location model, storage, queues, design tokens, and Meta Model API integration.
- Report actual file paths/components, existing patterns and potential conflicts.
- Confirm whether `MODEL_API_KEY` can call `muse-spark-1.3`, `muse-image-1.0`, and `sam-3.1` with small real tests, without modifying production data.
- Flag missing access or quotas honestly. No model keys in report.

### Stage 1 — Merchant Creative MVP (P0)
- Add route/menu entry according to existing nav conventions.
- Build wizard, brief builder, image source/reference handling, actual Muse Image call, 3 initial presets, background job statuses, library and export composer.
- Reuse existing media store and catalog/locations. Add tests, instrumentation and cost guardrails.

### Stage 2 — SAM fidelity enhancement (P0 if verified)
- Use SAM mask for product foreground isolation and image generation workflow when output quality improves; keep a functioning Muse Image direct-edit path.
- Compare source vs output for product identity. Feature-flag SAM if unavailable.

### Stage 3 — YOLA FUN voice-to-order (P1/stretch)
- Only begin once Studio E2E flow works and existing WhatsApp orders/voice infrastructure is understood.
- Add voice transcription + validated intent extraction + confirmation.

### Stage 4 — Demo evidence and controlled release
- Record proof of real API usage per integrated model, test case IDs, sample model request IDs (redacted), screenshots/video and results.
- Run lint/build/tests and multi-tenant regression checks.
- Present change summary and deployment plan to founder; **stop for approval before production deployment**.

## 16. Risks / decision log

| Risk | Mitigation |
|---|---|
| API key stored but model access not functional | Real smoke tests before implementation claims |
| Generative output changes the product | SAM masking, image reference, merchant approval and human review |
| Price/logo inaccurate | Render deterministic overlays from catalog fields |
| Many API requests create unbounded bills | per-tenant quota, request caps, bounded retries, max concurrency |
| Existing sidebar/framework differs from assumptions | repository discovery stage, adapt routes, no duplicate nav |
| Meta Ads integration missing | export files and manually usable campaign creatives; don't mislabel as auto-publish |
| Revenue attribution claims unsupported | differentiate exports, clicks, leads, actual orders |
| Hackathon date pressure | ship functioning creative loop before stretch features |

## 17. Official technical references (read before coding)

- Meta Model API overview: https://dev.meta.ai/docs/overview
- Muse Spark quickstart: https://dev.meta.ai/docs/cookbook/quickstart-chat-completions
- Muse Image: https://dev.meta.ai/docs/image-generation
- Muse Image cookbook: https://dev.meta.ai/docs/cookbook/image-generation-basics
- SAM segmentation: https://dev.meta.ai/docs/sam/overview
- Muse Voice Transcribe: https://dev.meta.ai/models/muse-voice-transcribe

**Important:** This PRD specifies the intended build; it does not establish that existing AtlasNow routes, tables, permissions or integrations are already implemented. Grok must verify the live codebase before modifying it.
