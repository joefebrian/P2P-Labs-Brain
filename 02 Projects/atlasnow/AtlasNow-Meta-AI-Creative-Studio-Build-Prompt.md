# Copy/paste prompt for Grok — AtlasNow Meta AI Creative Studio

You are working inside the **existing AtlasNow.co codebase**. Your task is to implement the attached **AtlasNow — Meta AI Creative Studio PRD v1.0** as a native merchant workflow, not as a detached demo app.

## Non-negotiables

1. **First perform a read-only codebase audit.** Identify actual framework, sidebar/nav, route conventions, tenant/location permissions, media storage, product catalog, WhatsApp/YOLA FUN, existing Meta Model API client, background jobs, tests and deployment setup. Report verified file paths and proposed changes. Do not assume the PRD's suggested route names already exist.
2. **Reuse the existing AtlasNow patterns** for auth, RBAC, multi-tenant scoping, location selection, storage, analytics, UI components and navigation. Preserve existing features. Avoid generic AI-generated design motifs; match the product's design system.
3. **Validate Meta Model API with real calls**, not mocked success: `muse-spark-1.3` for structured creative brief and `muse-image-1.0` for actual image editing/generation using merchant photos as references. Add `sam-3.1` for segmentation only when a real response and mask pipeline work. Meta docs: https://dev.meta.ai/docs/overview . Do not silently fall back to unrelated image providers while labeling the feature Meta-powered.
4. The merchant path is: **choose location / product → upload photo → select preset → generate → review / approve → export**. Start with Product Hero, Promo Offer and Best Seller. Source facts like prices, discounts and logos must be drawn in a deterministic overlay/compositor, not guessed by AI.
5. Add a working asset library with persistence, meaningful states, error recovery, quota / request caps, server-only secrets, usage logs and tenant isolation.
6. Do **not** implement autonomous Meta Ads publication or claim ROI/revenue attribution without verified integration. Exports and actual tracked clicks may be shown separately from orders.
7. **YOLA FUN voice-to-order is a stretch feature**, not a prerequisite to shipping a working Creative Studio. If time allows, implement using `muse-voice-transcribe-1.0` + real menu validation + explicit order confirmation, following existing WhatsApp paths.
8. Write tests including a second-tenant isolation test, lint/build, and capture the real model request evidence needed for a hackathon demo. Never expose keys or customer PII.
9. **Stop before production deployment and request explicit founder approval.** Do not change live payments, login, booking, unrelated YOLA FUN behavior, or production data without approval.

## Execution order

- **Step 0:** Return a concise repo audit, integration status for each model, actual routes/components involved, risk list and exact file plan.
- **Step 1:** Implement only the P0 Studio workflow and Meta model integrations, using project conventions.
- **Step 2:** Test API calls, upload → creative → approval → export, library persistence, error paths and multi-tenant isolation.
- **Step 3:** Deliver: changed files, screenshots, test results, verified model IDs/request logs (redacted), known limitations, and production deployment checklist. **Do not deploy until approval.**

**Read the PRD before coding and treat it as the requirements source. When the current code conflicts with PRD assumptions, preserve the existing architecture and report the deviation.**
