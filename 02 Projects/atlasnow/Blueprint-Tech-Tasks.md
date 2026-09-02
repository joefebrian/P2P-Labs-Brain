---
title: AtlasNow — Blueprint → Tech Tasks
related:
  - "[[AtlasNow-Blueprint]]"
  - "[[AtlasNow-PRD]]"
  - "[[atlasnow]]"
date: 2026-08-04
status: ready-for-build
---

# AtlasNow — Blueprint → Tech Tasks

> Repo: `/Users/joefebrian/Downloads/Working Desk/Atlas Technology/atlasnow`  
> Stack target: Next.js App Router + TS + Tailwind + Postgres + jobs + Google OAuth

## Locked decisions (founder)

| Decision | Status |
|---|---|
| WAHA | **Prototype / temporary bridge only** — jalan dulu sambil Meta WhatsApp Business API registration di-approve |
| WA Cloud API | Target jangka panjang; model data connector-neutral dari awal |
| MVP promise | Local Demand-to-Action Control Tower (bukan full Revenue OS) |
| Canonical entity | `atlas_location_id` |

---

## Epic map (Blueprint phases → engineering epics)

```text
BP Phase 0 Foundation  →  E0 Tenancy + Locations + Connectors shell + Data Health
BP Phase 1 Control     →  E1 Metrics + Control Tower + Signals + Actions + Proof
BP Phase 1.5 Convert   →  E2 Vouchers + Offers registry + Redemption CSV
BP Phase 2 Conversation→  E3 WAHA prototype (temp) → swap to Meta Cloud API
BP Phase 3 Revenue     →  E4 POS/CRM bridge (later)
BP Phase 4 Intelligence→  E5 NBA / experiments (later)
```

---

## E0 — Foundation (tech tasks)

### E0.1 App shell & tenancy
| ID | Task | Deliverable / acceptance | Est. files |
|---|---|---|---|
| T-001 | Init product layout + 10 nav stubs | Sidebar: Control Tower … Reports | `src/app/(app)/layout.tsx`, `src/components/nav/*` |
| T-002 | Postgres + Prisma schema base | migrate works local | `prisma/schema.prisma` |
| T-003 | Auth for P2P staff | login → session | `src/lib/auth/*`, `(auth)/login` |
| T-004 | Tenant + membership + role enum | roles: SUPER_ADMIN, ANALYST, HQ_*, REGION, BRANCH, VIEWER | `Tenant`, `Membership` models |
| T-005 | Tenant context middleware | every query scoped `tenant_id` | `src/lib/tenant/*` |
| T-006 | AuditEvent writer | writes/approvals/PII access loggable | `AuditEvent` + helper |

### E0.2 Location Master
| ID | Task | Acceptance | Files |
|---|---|---|---|
| T-010 | `Location` model + immutable `atlas_location_id` | cannot reuse after archive | prisma + API |
| T-011 | CSV import dry-run + commit | create/update/conflict report downloadable | `api/locations/import` |
| T-012 | `SourceMapping` CRUD + confidence | GBP/GSC/Ads/WA/social/redemption IDs | mapping UI |
| T-013 | Duplicate external ID guard | one external → one active location | service rule |
| T-014 | Readiness engine | READY / PARTIAL / BLOCKED + reason per source | `readiness.ts` |
| T-015 | Locations portfolio table | filter city/region/status | `(app)/locations` |
| T-016 | Location 360 shell (tabs empty/live) | Overview + Data contract first | `(app)/locations/[id]` |
| T-017 | Store Event Log (P1) | renovation/closure/campaign periods | optional after MVP loop |

### E0.3 Connectors shell + Google OAuth
| ID | Task | Acceptance | Files |
|---|---|---|---|
| T-020 | Connector registry model | Google / GSC / Ads / WAHA / MANUAL | `Connector`, `SyncRun` |
| T-021 | Google OAuth connect flow | store tokens encrypted/env-safe | `lib/google/oauth.ts` |
| T-022 | List authorized GBP accounts/locations | pagination, readMask | `lib/google/gbp/business-info.ts` |
| T-023 | Map GBP location → atlas_location_id | conflict UI | Data Health |
| T-024 | GSC property connect | property + last sync visible | `lib/google/gsc.ts` |
| T-025 | GSC page pattern mapping | exact URL or regex; collision blocks store-level | mapping rules |
| T-026 | Honest GSC portfolio-only mode | shared `/outlets` → no store ranking | UI state |
| T-027 | Social Account Registry | handle/URL/scope/owner/status; NOT_PRESENT ok | SOC models + UI |
| T-028 | Sync job runner | scheduled + on-demand; status/errors | Inngest/BullMQ |
| T-029 | Data Health dashboard | freshness, coverage, conflicts, disconnected | `(app)/data-health` |

### E0.4 Metric infrastructure (shared)
| ID | Task | Acceptance | Files |
|---|---|---|---|
| T-030 | `MetricObservation` store | grain location_day + source_run_id | prisma |
| T-031 | Metric Data Contract component | 8 fields on every card (PRD §14.1) | `MetricCard.tsx` |
| T-032 | Metric dictionary GBP enums | labels + forbidden interpretations | `lib/metrics/gbp-dictionary.ts` |
| T-033 | Missing vs zero vs threshold vs error | distinct UI states | design system states |
| T-034 | Timezone default Asia/Jakarta | storage UTC, display TZ | util |

**E0 done when:** Demo tenant + CSV locations + Google connect (or fixture mode) + Data Health + empty Control Tower with real readiness counts.

---

## E1 — Control (tech tasks)

### E1.1 GBP Performance + Reviews + Posts (read-first)
| ID | Task | Acceptance | Files |
|---|---|---|---|
| T-040 | Sync GBP multi daily metrics | enums PRD §8.2 stored correctly | performance job |
| T-041 | Performance cards on Location 360 | contract complete; no visit claim on directions | UI |
| T-042 | Monthly search keywords (P1) | threshold ≠ invented count | optional |
| T-043 | Reviews sync + inbox | filter rating/location/reply state | `(app)/reputation` |
| T-044 | Review taxonomy stub | multi-label + confidence; QA sample later | classifier interface |
| T-045 | Posts inventory list | lifecycle visible; no fake active | `(app)/posts` |
| T-046 | Pub/Sub notifications (P1) | new review queues targeted sync | later |

### E1.2 Leakage engine + actions
| ID | Task | Acceptance | Files |
|---|---|---|---|
| T-050 | `Signal` model + create API | evidence refs, severity, confidence, freshness | prisma + API |
| T-051 | Rule: Data health block | always priority; blocks optimization | rules/ |
| T-052 | Rule: Profile visibility drop | 28d vs prior + peers guardrails | rules/ |
| T-053 | Rule: Weak intent rate | impressions up, actions down | rules/ |
| T-054 | Rule: Review response leak | negative unreplied > SLA | rules/ |
| T-055 | Priority score 0–100 | weights PRD §10.1 | `priority.ts` |
| T-056 | Suppress invalid recommendations | BLOCKED/stale/low confidence | guard |
| T-057 | Leakage Queue triage UI | accept/edit/FP/snooze + audit | `(app)/leakage-queue` |
| T-058 | `Action` create (owner, deadline, proof req) | mandatory fields | Action Center |
| T-059 | Approval workflow flag | public-write / budget actions need approver | state machine |
| T-060 | Proof submit + validate | API preferred; manual + reviewer | proof upload |
| T-061 | Measurement window + outcome enum | IMPROVED…NOT_MEASURABLE | jobs |
| T-062 | Audit timeline view | signal→decision→proof→outcome | Location Timeline tab |
| T-063 | Control Tower widgets | stores needing action, overdue, health blockers | `(app)/control-tower` |
| T-064 | Branch mobile task view | tasks only, no chart dump | responsive / branch role |

### E1.3 Reporting lite
| ID | Task | Acceptance | Files |
|---|---|---|---|
| T-070 | Weekly action report | signals, tasks, proof, blockers | `(app)/reports` |
| T-071 | Monthly portfolio skeleton | sections + evidence language | report template |
| T-072 | Metric drill-down to contract | any number → source run | UI |

**E1 done when:** full loop on ≥5 demo/real locations: signal → assign → proof → outcome pending + Control Tower usable.

---

## E2 — Convert Lite (tech tasks)

| ID | Task | Acceptance |
|---|---|---|
| T-080 | Voucher registry + code generator | `SOURCE-LOC-CAMPAIGN-PERIOD` unique |
| T-081 | Separate ADS vs GBP codes | cannot collide same loc/campaign/period |
| T-082 | Offer post draft + exact preview | no publish without approval |
| T-083 | Publish GBP offer (approved only) | audit + idempotency |
| T-084 | Ads location asset mapping registry | map to atlas_location_id |
| T-085 | Redemption CSV dry-run + import | duplicate/void handling |
| T-086 | Evidence ladder labels | EXPOSED→…→ATTRIBUTED_SALE distinct |
| T-087 | Verified redemption dashboard | 1 campaign E2E |

---

## E3 — Conversation (WAHA temporary → Meta Cloud API)

> [!warning] WAHA = prototype / temporary
> Dipakai **sementara** agar observability WhatsApp bisa jalan sambil **Meta WhatsApp Business API** registration di-approve.  
> Data model **connector-neutral** (`provider: WAHA | META_CLOUD`).  
> Kill switch + private network + retention wajib.

### E3.1 Now (prototype)
| ID | Task | Acceptance |
|---|---|---|
| T-090 | `MessagingProvider` abstraction | session, message, contact interfaces |
| T-091 | WAHA adapter | webhook auth, dedupe message id |
| T-092 | Map session → HQ \| one location | ambiguous disabled |
| T-093 | Ingest inbound/outbound | direction + timestamps |
| T-094 | Identity confidence enum | never invent phone from `@lid` |
| T-095 | Conversation boundary 24h | configurable |
| T-096 | SLA first human response | exclude bot if tagged |
| T-097 | Taxonomy + confidence | intent/topic/sentiment/urgency |
| T-098 | Conversations UI (restricted raw content) | policy + audit |
| T-099 | Session health + kill switch | disconnect → incident |
| T-100 | Retention jobs | raw 30d default (or shorter) |

### E3.2 Later (Meta approved)
| ID | Task | Acceptance |
|---|---|---|
| T-110 | Meta Cloud API adapter | same domain models |
| T-111 | Migrate session mapping | no data rewrite of atlas_location_id |
| T-112 | Deprecate WAHA path | feature flag off; docs updated |
| T-113 | Official templates / agent identity (if needed) | named agent only via platform |

---

## E4 — Revenue (later)

| ID | Task |
|---|---|
| T-120 | POS/booking/CRM connector |
| T-121 | Voucher ↔ transaction match |
| T-122 | Contribution margin fields |
| T-123 | Verified attributed sale reports |

---

## E5 — Intelligence (later)

| ID | Task |
|---|---|
| T-130 | Peer-group benchmark |
| T-131 | Next-best action |
| T-132 | Test/control stores |
| T-133 | Incrementality labels only with method |

---

## Cross-cutting tech tasks (all phases)

| ID | Task |
|---|---|
| X-01 | Tenant isolation automated tests |
| X-02 | Secrets never in logs/vault |
| X-03 | Idempotent sync upserts |
| X-04 | Rate-limit queue for Google writes |
| X-05 | 29-day GBP raw cache expiry job |
| X-06 | i18n ID primary labels |
| X-07 | Observability: sync dashboard + alerts |
| X-08 | Fixture/demo mode (build UI without Google approval) |
| X-09 | Feature flags: `waha_enabled`, `google_write_enabled` |

---

## Suggested build order (engineering sprints)

| Sprint | Focus | Task IDs |
|---|---|---|
| **S1** | Shell + auth + tenant + nav | T-001…T-006 |
| **S2** | Location master + CSV + readiness | T-010…T-016 |
| **S3** | Google OAuth + GBP list + map + Data Health | T-020…T-029, X-08 |
| **S4** | Metric store + dictionary + GSC honest mode | T-024…T-026, T-030…T-034 |
| **S5** | GBP Performance sync + Control Tower | T-040…T-041, T-063 |
| **S6** | Signals + Actions + Proof loop | T-050…T-062 |
| **S7** | Reviews + Posts read | T-043…T-045 |
| **S8** | Convert Lite vouchers | T-080…T-087 |
| **S9** | WAHA prototype (temp) | T-090…T-100 |
| **S10** | Reports + hardening | T-070…T-072, X-01…X-07 |
| **S11+** | Meta Cloud API swap | T-110…T-113 |

---

## Stack → folder convention (repo)

```text
src/
  app/
    (auth)/
    (app)/
      control-tower/
      leakage-queue/
      locations/
      reputation/
      posts/
      ads/
      conversations/   # feature-flagged
      action-center/
      data-health/
      reports/
    api/
  components/
    metrics/MetricCard.tsx
    nav/
  lib/
    auth/
    db/
    tenant/
    google/
    metrics/
    signals/rules/
    messaging/          # WAHA + future Meta
      providers/
      types.ts
  jobs/
prisma/
docs/                   # optional mirror of PRD snippets
```

---

## Definition of “Blueprint covered” for MVP ship

Sesuai Blueprint §18 + PRD DoD:

1. Map branches + data health gaps  
2. View signals with source definitions  
3. Identify high-priority leakage  
4. Assign action + PIC + deadline  
5. Verify proof  
6. Measure post-action signal or redemption  
7. Report without overclaim  

WAHA prototype **tidak** memblok MVP ship Control; Conversation = add-on / parallel track sampai Meta approve.
