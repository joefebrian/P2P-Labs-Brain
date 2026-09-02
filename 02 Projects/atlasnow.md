# atlasnow

#project

## Outcome
**AtlasNow** = Local Demand-to-Action Control Tower untuk HQ multi-cabang.

**Tagline:** Optimize Every Outlet. Capture More Demand.  
**Promise:** Turn existing Google presence into measurable local growth.

SOP discoverability: [[03 Areas/SEO-AEO-GEO]]  
TikTok developer (2026-08-31): org **PT Sorak Digital Media** · app **AtlasNow** (Business) App ID `7679020348364392455`. **Not** SWYPE. Keys stay on this app only.

**Parked (Joe 2026-08-31):** native TikTok inbox waits for **Business Messaging** (partner / TikTok review). Do not wire Login Kit OAuth as if it were DMs. Wave A path stays TikTok ads/bio → WhatsApp. GO till is a separate product if we pick it later.  
**Money master (wajib dibaca sebelum develop fitur berbayar / Free / kredit / payment):** [[AtlasNow-Monetization-PRD]]

### 2026-09-01 (broadcast Meta report PRD — not built)
- Changed: PRD + spec for Broadcast **History**: Meta `sent` / `delivered` / `read` / `failed` / **Action** (inbound or quick-reply). Read receipts incomplete by design. No URL-click, no visits, no revenue. Lives on Broadcast, not loyalty Reports. H-2 batches included. Webhook `statuses[]` still skipped in code until gas. Joe locked Action = reply/button, not store visit.
- Why: Joe on Broadcast Session note: asked if sent / read / action report is covered here. Asked to write Meta-only PRD first.
- Next: Built (Joe: gas 2026-09-02). Tab History on Broadcast. Store wamid + Meta statuses + Action. Deploy migrate `20260902120000_broadcast_meta_history`. Broadcast Who two-blocks still separate.

### 2026-09-01 (support Radit PRD — not built)
- Changed: PRD + spec for **Help desk** — human agent **Radit**, queue of one, widget on public atlasnow.co **and** inside the desk. 10 min silence **after Radit replies** auto-closes and points at hello@atlasnow.co. Client bubbles **Not seen yet** until Radit opens. Super Admin menu stores threads. Not mixed with brand WhatsApp inbox. Not AI. Desk hours default **09:00–17:00 Jakarta**, widget **off** outside hours (shows the **contact form** to hello@, not the queue), hours editable in Super Admin.
- Why: Joe: support P2P for people who use AtlasNow or will; C both surfaces; approach A queue; 10 min belongs to the customer; seen receipt like Intercom. Then: chat open 09–17, box dead after hours, preferably settings.
- Next: Built (Joe: gas). Widget on public + desk + login. Super Admin Help desk `/support`. Hours 09:00–17:00 Jakarta (settings). Off-hours = contact form. 10 min visitor silence close. Not seen until Radit opens. Screenshot attach still later. Deploy migrate `20260901200000_support_helpdesk` on VPS. Broadcast Who two-blocks still waiting separately.

### 2026-08-31 (Google OAuth consent)
- Changed: Google Auth Platform (project AtlasNowBusiness Profile) — branding atlasnow.co privacy/terms; scopes `business.manage` + openid/email/profile; Audience **Testing** External; test users hello@atlasnow.co, raditya@p2plabs.asia, yusuf@p2plabs.asia. **Do not Publish.** 4 redirect URIs on the Web client.
- Why: Joe finished Console setup after API access case 7-1225000041380.
- Next: Confirm Client ID/secret in Settings → API. Smoke-test Connect with a test-user Google account. Reviews v4 still waits allowlist.

### 2026-09-01 (birthday code at till + report)
- Changed: HQ sets birthday **code style** (prefix / include year / random length) in Settings → Loyalty → Birthday. Kasir must type the WhatsApp code to Redeem. Code stored on LoyaltyRedemption and listed on the monthly loyalty report. Till does not display the issued code.
- Why: Joe: kasir wajib ketik kode WA; redeem tercatat di report; penentuan code di-setup.
- Next: Already-sent codes keep their old format. New sends use the style.

### 2026-09-01 (birthday template named vars)
- Changed: `birthday_greeting` fills Meta **named** vars: `customer_name` = join name, `voucher_number` = Loyalty → Birthday Reward, `code_voucher` = Atlas unique `BDY26-XXXX` per member/year (kasir sees it). Same body every brand; each WABA still submits to Meta. Broadcast has a Fill birthday_greeting preset.
- Why: Joe’s Meta form uses `{{customer_name}}` / `{{voucher_number}}` / `{{code_voucher}}`, not `{{1}}`. Asked if one template can be universal.
- Next: Submit that exact body on each brand WABA (or use the preset). Fill Reward or H-2 skips (`no_reward`).

### 2026-09-01 (birthday H-2 auto)
- Changed: Daily 00:20 Asia/Jakarta (+ boot catch-up) sends **birthday_greeting** once per year to **aktif** members who ticked birthday WA, whose birthday is H-2 / H-1 / today. Needs HQ Cloud + APPROVED template. IMAGE header = brand logo. Manual send of the same template counts as the once. STOP / BERHENTI opts out; MULAI / START resumes. Super Admin: Settings → Loyalty → Birthday → Send H-2 notes now.
- Why: Joe: bangun member aktif + opt-in + ultah H-2, kirim birthday_greeting sekali.
- Next: Don’t debit WA credits (Meta bills the WABA). Don’t send to calon. Don’t treat the birthday tick as a promo CSV.

### 2026-09-01 (broadcast flow)
- Changed: Broadcast Templates tab is now 1 what (APPROVED only) → 2 who (birthday opt-in list) → 3 send. Submit-to-Meta moved under a fold. Copy: birthday opt-in is a list, **not** automatic H-2. Send button says why it’s blocked (no template / no people / needs header / confirm).
- Why: Joe: flow should be pick what, pick how many numbers, send. Asked if `birthday_greeting` auto-sends to Birthday opt-in — it does not.
- Next: H-2 auto still not built. If Joe wants it: cron Jakarta, aktif + opt-in + birthday in 2 days + approved template, once. Don’t invent CSV blast.

### 2026-09-01 (landing brand hairline)
- Changed: Homepage section dividers (What you get + sibling sections) and public footer — 2px AtlasNow swirl bar (cyan/sky/aqua/mint/lime/peach/blush/lavender) instead of gray `border-t`. Not a thick Google-style stripe.
- Why: Joe: garis batas `#product` pakai kombinasi warna logo, kayak color bar, jangan terlalu tebal.
- Next: Tweak thickness/order if it still feels faint or too candy.

### 2026-09-01 (Google Sign-in works)
- Changed: Joe confirmed **Sign in with Google** works for `hello@atlasnow.co` (OAuth test user). Signup pending page still correct for new accounts (`loginEnabled` off).
- Why: Console branding + 4 scopes + 4 redirects + Testing audience.
- Next: Do not Publish the Google OAuth app. GBP Account Management quota still 0 until case **7-1225000041380**. Connect listings after allowlist. Free desk-on-signup still parked.

### 2026-08-31 (GBP API access submitted)
- Changed: Joe submitted **Google Business Profile API access**. Case **7-1225000041380**. GCP project number **386272165216** (AtlasNowBusiness Profile / P2P Lab — not Sorak). Website `https://atlasnow.co`. Google: ~7–10 working days.
- Why: Reviews v4 (`Google My Business API`) is gated; Account Management + Business Information are the public APIs. Form: listings + human review replies for brands we operate — no invented visits.
- Next: Follow up **~2026-09-10 / 10 working days**. If no email, reply on that case. Do not enable Q&A / Lodging / Performance while waiting.

### 2026-08-29 (Home date range + compare)
- Changed: Control Tower / Home is a real desk: From–To picker (7d / 28d / this month / custom), compare vs previous equal period. Period cards = stamps, new members, people who wrote, new Google reviews (not Maps visits). Live queues stay “right now.”
- Why: Joe: dashboard by date with comparison.
- Next: Deploy with the rest of this pass.

### 2026-08-29 (login polish + InfoTip)
- Changed: `/login` — logo clipped to a black circle with mint ring (PNG square no longer sits on cyan blur). Removed fake GBP 4.9 card. Copy = locked tagline + merchant desk (no Agency, no “on the map”). InfoTip on flow steps, Google/Facebook, signup, follow-up. Stale branding in DB self-heals to the new story. **Live on atlasnow.co.**
- Why: Joe: review pages one-by-one starting at login; system context ngaco; logo looks bad on that background.
- Next: Same pass on signup, then Control Tower after login.

### 2026-08-29 (Monetization PRD = master)
- Changed: [[AtlasNow-Monetization-PRD]] declared **master for money** on *any* development. Pointers: product PRD, Direction, Blueprint, SEO SOP, Product Engineering, repo + vault AGENTS. Product PRD = what exists; Monetization = what we charge. Conflict → Monetization wins until founder edits it.
- Why: Joe: “Monetization PRD ini jadi master kita kalau develop apapun juga.”
- Next: Keep editing that file when packaging changes — don’t scatter prices in tickets. Do **not** wire Creem or debit credits until pack IDR locks.

### 2026-08-29 (payment scheme ID vs luar)
- Changed: [[AtlasNow-Monetization-PRD]] §15.3 — paying entity in Indonesia → IDR invoice/transfer (later Xendit/Midtrans for packs). Paying entity luar → USD via Creem. Wallet always IDR. One tenant one rail. PayPal still not primary.
- Why: Joe asked how Indonesia vs overseas payment should work.
- Next: Don’t send local HQ to Creem USD. Wire nothing until pack prices lock.

### 2026-08-29 (SEO/AEO/GEO)
- Changed: Homepage SSR section names Google Business Profile, Google Maps, WhatsApp CRM, outlet operations, revenue attribution (receipts, not Maps). Meta title/description, canonical, OG, robots/sitemap, JSON-LD. FAQ answers stay in HTML. SOP in [[03 Areas/SEO-AEO-GEO]].
- Why: Joe: crawlable copy, not only animation; AEO/SEO/GEO as a first-class area.
- Next: Real OG image 1200×630. Optional `?lang=` URLs if we want ID indexed separately.

### 2026-08-26 (white-label mobile, direction)
- Changed: PRD direction — future branded mobile app per agency/brand/client. Skin = merk, engine = AtlasNow. Staff/members must not feel they use “our” system. Wave I, not Wave A. [[AtlasNow-Direction-PRD]] §6.
- Why: Brands want a standalone app with their name on the icon.
- Next: Do not build App Store binaries until members + loyalty APIs are stable. Staff shell first when we start.

### 2026-08-26 (white-label: icon + name)
- Changed: Locked the split — mobile **icon and app name = merk**; **data = AtlasNow** (no second CRM).
- Why: Joe confirmed the storefront vs engine split.
- Next: Still Wave I. Branding pack per tenant when we start.

### 2026-08-26 (white-label journey)
- Changed: Wrote [[AtlasNow-White-Label-Mobile-Journey]] — J0 pondasi web → J5 agency skin. Gates, not dates. Staff app before member app.
- Why: Far away, but web work must not create a second CRM.
- Next: Keep APIs tenant-scoped; complete branding pack (name + logo) per merk on web.

### 2026-08-26 (QR stamp logic, not shipped)
- Changed: Simulated competitor digital-stamp pitch against live AtlasNow. JOIN QR ≠ stamp QR. Proposed: kasir scans member QR (or one-time trx QR) instead of typing HP; Approve + Redeem stay. [[AtlasNow-Loyalty-QR-Stamp-Logic]]
- Why: Counter QR auto-stamp would farm stamps and break form-first.
- Next: Joe locks path B vs C. Do not deploy.

### 2026-08-26 (QR stamp: member first)
- Changed: Locked — collect customer (JOIN) first; only then a **member stamp QR** kasir scans. Combination of live AtlasNow + digital card. Path C parked. Not shipped.
- Why: Data customer dulu; stiker toko jangan nge-stamp.
- Next: Build only when Joe says. Meanwhile JOIN + ketik HP stays.

### 2026-08-26 (Reports loyalty month + stamp card v1)
- Changed: Reports menu is the monthly loyalty recap (Cirqle-style 4 cards, named **AtlasNow**). Metrics = members returned, stamps/receipts, gifts redeemed, top regular/spender — from real stamp/redemption rows, not visits. v1 stamp card: customer chats HQ `Status Stamp` (24h service window) + kasir ketik HP. Path B member QR still later.
- Why: Joe asked to put the monthly recap in Reports, adapt to our programs, and keep stamp display cheap.
- Next: Weekly ops reports still later. Connect HQ Cloud so Status Stamp replies send. Do not ship member QR until asked.

### 2026-08-26 (training deck)
- Changed: In-app tutorial at `/deck_train` (partnership + merchant). 15 slides: who does what, live vs later, 5-step flow, kasir 15-second script, stamp card v1, pocket sheet. PPTX at `/docs/AtlasNow-pelatihan.pptx`. Agency and brand can open it (not pitch-only).
- Why: Joe asked for training slides for partnership employees and partner merchants.
- Next: Present from the app; send PPTX to stores.

### 2026-08-26 (deck_train stamp knowledge)
- Changed: `/deck_train` is now the stamp loyalty presentation. Header **Knowledge** panel (two doors, two QRs, Approve/Redeem, menus). Slides: knowledge, doors, two QRs, click-play starting with “punya member?”.
- Why: Joe asked for knowledge panel + presentation on deck_train for stamp management.
- Next: Present from atlasnow.co/deck_train after login.

### 2026-08-26 (stamp QR after DB check)
- Changed: Locked till flow — not Cirqle auto-stamp. Belum member → JOIN QR. Sudah → Cek HP dulu, baru QR stamp `/card/{token}` (kasir scan). Scan of JOIN QR is rejected as daftar. Loyalty desk: two-door copy, scan/paste, struk after member found. WA Status Stamp includes card link.
- Why: Joe: kasir tanya membership, cek database, baru scan stamp QR. Loyalty management should be solid with this.
- Next: Train kasir on Cek member. Deploy with the scan routes.

### 2026-08-26 (training: simple + click demo)
- Changed: Training deck now plain-language Indonesian. Slide 3 is a click-through HTML mock (scan QR → daftar → kasir ketik HP → Approve → chat Status Stamp → Redeem). Extra click toys on daftar / kasir / kantor / kartu slides. Live on atlasnow.co/deck_train.
- Why: Joe: bahasa mudah, sampling flow klik HTML, bukan teks saja.
- Next: Kasir coba klik slide “Coba klik”. PPTX still text-only takeaway.

### 2026-08-26 (deploy training)
- Changed: Shipped `/deck_train` and `https://atlasnow.co/docs/AtlasNow-pelatihan.pptx` to production. PPTX is public so stores can download without a login.
- Why: Joe: dorong di atlasnow.co.
- Next: Open Pelatihan after login; kirim PPTX ke kasir.

### 2026-08-26 (deploy reports)
- Changed: Built and shipped to atlasnow.co. `/reports` and `/api/loyalty/report` live. No new migration. WAHA/Postgres left running.
- Why: Logic was already in; Joe asked to build.
- Next: Open Reports after login. Status Stamp still needs HQ Cloud connected.

### 2026-08-26 (activate + merchant reward)
- Changed: Clarified — “donut” is a sample; gift = merchant setup. Membership + first stamp **activate on the first valid trx**.
- Why: Joe: collect customer first; activate from first real receipt.
- Next: QR stamp (member QR) still not shipped.

## Status
🟢 **S2 + S3 shipped** — Location Master + Google Business Profile connector (OAuth / mock) + map  
Agency admin + clients + branding/i18n

### 2026-08-25
- Changed: HQ WhatsApp Cloud API (WABA) per brand — webhook `/api/webhooks/whatsapp`, Chat apps connect, inbox reply on META_CLOUD only. Branch WAHA remains monitor-only. Location `kind=HQ`.
- Why: Official HQ number for blast/loyalty/inbox; Chromium WAHA must not send.
- Next: Brand pastes Phone number ID + token; Meta webhook subscribe `messages`. Loyalty stamp/redeem after this lands.

### 2026-08-25 (later)
- Changed: Loyalty web desk — Settings → Loyalty (stamp/spender rules), menu Loyalty (submit struk, antrian Approve, Redeem). Outlet confirmed WA field. Notify HQ skipped until Cloud API is connected.
- Why: Cloud API setup is slow; stamp/redeem/fraud rules can run without Meta.
- Next: Connect WABA; then WA Status Stamp / notify on Approve goes live automatically.

### 2026-08-25 (multi-reward)
- Changed: Settings → Loyalty now has add/remove reward rows. Stamp: 5 stamp → X, 10 stamp → Y (claim each once; card resets only after the highest gift). Top spender: juara 1 / 2 / 3 each get their own gift (not cumulative).
- Why: One reward field was not enough for merchant programs.
- Next: Still waiting on Meta Cloud API for HQ WhatsApp notify.

### 2026-08-25 (customers membership, open)
- Changed: Diskusi menu Customers — master HP + ajakan member. Usul QR form (HP, nama, DOB, email) + reward ultah H-2. **Belum dikunci, belum di-build.** Catatan: [[02 Projects/atlasnow/AtlasNow-Customer-Membership-Discussion]].
- Why: Customers sekarang cuma buku chat WA; kasir tidak realistis ngetik DOB.
- Next: Lanjut diskusi QR (di kasir vs meja) lalu lock sebelum coding.

### 2026-08-25 (customers membership)
- Changed: Master member — QR join (HP, nama, DOB, email, centang “Boleh kirim ucapan ulang tahun via WhatsApp”), status calon→aktif setelah struk Approve tembus min merek. Settings QR satu merek vs per cabang. Menu Customers calon/aktif. Stamp ditolak tanpa daftar dulu. Ultah redeem kasir (H-2 WA nanti, HQ Cloud).
- Why: Joe locked form-first, min per brand, QR dual placement, checkbox sempit.
- Next: H-2 birthday send when Cloud API is connected; blast promo umum still not this checkbox.

### 2026-08-25 (pitch deck)
- Changed: Pitch deck rebuilt around the live loop — Maps, reviews, brand WhatsApp, members (scan ≠ member), loyalty (stamp / top spender / birthday). Honest now-vs-later and pain points.
- Why: Deck still sold WAHA handset + Messenger as live.
- Next: Present at /deck_pitch (agency).

### 2026-08-25 (brand guidelines)
- Changed: UI + pitch + landing restyled to AtlasNow kit — watercolor mark, warm white, charcoal primary, sky/mint/lavender washes, Inter as Swiss grotesque stand-in.
- Why: Pitch and app still looked like generic indigo SaaS.
- Next: Swap Inter for licensed Neue Haas Grotesk if they buy the font.

## Domain
- **Production:** https://atlasnow.co
- **Local:** http://localhost:3000
- Google OAuth redirects: `https://atlasnow.co/api/google/oauth/callback` + localhost callback
- Model: **1 GBP Agency** OAuth → map locations to many client tenants

## Repo
```
/Users/joefebrian/Downloads/Working Desk/Atlas Technology/atlasnow
```

```bash
cd "/Users/joefebrian/Downloads/Working Desk/Atlas Technology/atlasnow"
npm run db:seed   # once / after schema change
npm run dev       # → http://localhost:3000
```

### Demo login (agency)
- Workspace: **P2P Labs** (`p2p-labs`, type AGENCY)
- `admin@p2plabs.local` / `AtlasNow@2026` (SUPER_ADMIN)
- `analyst@p2plabs.local` / `AtlasNow@2026` (ANALYST)

### Client database
- Menu **Admin → Clients** (`/clients`) — agency staff only
- Create client (name, industry, contact, notes…)
- **Activate login** → creates Client Admin user + enables `loginEnabled`
- Sample client: `demo-brand` (login inactive until activated)
- Client users cannot sign in until activation

### Brand messaging
**Primary language = English.** Bahasa Indonesia = UI localization.

| Layer | English | Bahasa Indonesia |
|---|---|---|
| Tagline | Optimize Every Location. Capture More Demand. | Optimalkan Setiap Lokasi. Tangkap Lebih Banyak Demand. |
| Hero | Your outlets are already on the map. Now make every one perform. | Outlet Anda sudah di peta. Sekarang buat setiap cabang berkinerja. |
| Promise | Turn existing Google presence into measurable local growth. | Ubah kehadiran Google yang sudah ada menjadi pertumbuhan lokal yang terukur. |
| Flow | Optimize location assets → … → Generate measurable outcomes | Optimalkan aset lokasi → … → Hasilkan outcome yang terukur |

- Language switcher: **EN | ID** (header, login, Settings) — cookie `atlasnow_locale`, default `en`
- Edit branding: **Settings** (`/settings`) — logo + EN primary copy + ID localization

## Docs
- [[02 Projects/atlasnow/AtlasNow-PRD|PRD]]
- [[02 Projects/atlasnow/AtlasNow-Blueprint|Blueprint]]
- [[02 Projects/atlasnow/AtlasNow-Monetization-PRD|Monetization PRD]]
- [[02 Projects/atlasnow/Blueprint-Tech-Tasks|Tech Tasks]]

## Stack
- Next.js + TS + Tailwind
- Prisma 5 + SQLite (local)
- Session JWT (jose) + bcrypt
- `BrandingConfig` singleton for frontend brand data

## WAHA
Temporary prototype until Meta WhatsApp Business API approved. Nav stub only in F1.

## Next actions
- [x] **Fase 2 / S2** — Location Master + CSV + readiness + Location 360
- [x] **S3** — Google OAuth / mock + list + map + Data Health + auto-map by code
- [x] **Settings hub** — Branding + **API Configuration** (central credentials registry)
- [x] **S4 (core)** — MetricObservation + dictionary UI + MetricCard + Visibility + GSC honest stub
- [x] **S1–S4 readiness page** — Settings → Sprint readiness (honest checklist)
- [ ] S4 tail — live GSC connect/mapping (T-024…T-026 full)
- [x] **Reviews inbox (S7 start)** — sync Google reviews + draft/publish reply on one page
- [ ] S5 — live GBP Performance API sync (replace seed with OAuth pull)
- [ ] Lock remaining: voucher, public content approver

## Pipeline (2026-08-19)

Public `/pricing` = Free + quote only. Do **not** print pack IDR, wire Creem, or debit credits until founder locks [[AtlasNow-Monetization-PRD]] §7 or §16. That PRD is **master for money**.

| When | Item | Type |
|---|---|---|
| **Now — ops** | Sewa VPS Singapore + DNS `atlasnow.co` | Joe |
| **Now — ops** | Meta app **Live** + webhook `https://atlasnow.co/api/webhooks/meta` | Joe + legal URLs already shipped |
| **Now — dev** | Deploy kit: Docker Compose (Caddy + Next + Postgres + WAHA) + Prisma Postgres migrate | Engineering — see `deploy/README.md` |
| **Next — product** | Conversations **reply** (WAHA send + Messenger send) — inbox still monitor-only | Engineering |
| **Parked** | Monetization execution: lock IDR → invoice process → billing UI later | Founder then ops |
| **Parked** | Instagram scopes, WhatsApp Cloud, GSC live, GBP Performance live, voucher | After inbox is live on domain |

### 2026-08-19
- Changed: Monetization PRD written (`AtlasNow-Monetization-PRD.md`). Execution parked.
- Why: Rumus/kemasan perlu ada; angka + invoice belum boleh dikode.
- Next: deploy kit so Meta Live has a stable URL.

## Founder decisions (Google / pilot) — 2026-08-05

| Decision | Choice | Rationale |
|---|---|---|
| **GCP project** | **1× P2P Labs project (MVP)** | Not per-client GCP. Cost/quota di-meter di AtlasNow per client, bukan pecah project Google |
| **Who OAuth** | **Agency (P2P)** | Managed service + GBP Agency Dashboard model; Client Admin OAuth = later self-serve |
| **Pilot size** | **20 cabang** first | Fits Location Master + map UX before scale |
| **API path** | **OAuth + Business Information first** → Performance API later | Avoid Performance approval bottleneck |

### Cost visibility (why not 1 GCP per client)
- Google Cloud project per brand = OAuth consent, API enablement, verification, secret sprawl × N
- GBP API read cost rarely is the bill driver for pilot 20 locs
- **Simulate cost in AtlasNow:** locations_count, oauth_connected, sync_runs, API call counters, last_error — billed conceptually per client tenant

### Agency ops note
- Google: [GBP Agency Dashboard](https://support.google.com/business/community-guide/350148688/how-to-sign-up-for-and-use-the-google-business-profile-agency-dashboard?hl=en) / org manages many profiles
- AtlasNow: maps those profiles → `atlas_location_id` per client tenant after agency OAuth

## Decisions log
### 2026-08-15
- Changed: Spec Conversations slice 1 — WAHA live monitor-only inbox
- Why: HQ lihat chat nomor cabang (siapa ↔ cabang mana), bukan helpdesk
- Next: review spec, lalu implementation plan

### 2026-08-15
- Changed: Conversations slice 1 shipped on `feat/conversations-waha-monitor`
- Why: WAHA webhook → inbox monitor-only (cabang ↔ kontak)
- Next: map session WAHA di Location 360, set API key, webhook URL `/api/webhooks/waha`
- Path: `docs/superpowers/specs/2026-08-15-conversations-waha-monitor-design.md`

### 2026-08-15
- Changed: Hydration mismatch on Settings → API (`toLocaleString()` without locale)
- Why: Node (ID/GB → `15/08/2026, 1:23:36 am`) vs browser (en-US → `8/15/2026, 1:23:36 AM`)
- Fix: `formatDateTime()` — explicit EN/ID + timezone `Asia/Jakarta`; used on API config, reviews, data health
- Next: keep using `formatDateTime` for any SSR date text

### 2026-08-15
- Changed: Task 1 pure helpers — identity, parseWahaEvent, 24h window (`src/lib/conversations/*`); npm test script; commit `feb230f`
- Why: Slice 1 foundation for WAHA monitor-only Conversations; no invent phones from @lid
- Next: Task 2+ import helpers for ingestion / open conversation

### 2026-08-15
- Changed: Prisma `WaContact` / `WaConversation` / `WaMessage` + Tenant/Location relations; migration `20260815095027_waha_conversations`; commit `70d5ba4`
- Why: Conversations slice 1 persistence for WAHA monitor-only inbox
- Next: Task 3 webhook ingest into these tables

### 2026-08-15
- Changed: Task 3 ingest — mapping gate, externalId dedupe, 24h split, lid→phone upgrade, kill switch (`src/lib/conversations/ingest.ts`, `waha-config.ts`)
- Why: Persist mapped WAHA `message` / `message.any` into WaContact / WaConversation / WaMessage; never invent phone from @lid
- Next: Task 4 public webhook route + API key auth

### 2026-08-05
- Locked brand messaging (tagline, hero, narrative, promise, growth flow) into PRD §0.0
- **English-first** product language + **EN | ID** language switcher
- **Settings menu** + bilingual branding panel (logo, EN + ID copy) → DB + login/sidebar/Control Tower
- UI demo shows BrandStory on Performance surface
- **No GBP abbreviation** in UI — always “Google Business Profile”
- **Agency admin model:** tenant type AGENCY | CLIENT; Clients menu + activate login
- **Google decisions:** 1 GCP project; agency OAuth; pilot 20 locations; BI API before Performance API
- Cost simulation = product metering per client, not per-GCP-project
- **S2 Location Master:** `Location` + immutable `atlas_location_id`, `SourceMapping`, readiness engine, portfolio UI, CSV dry-run/commit, Location 360 tabs, seed 20 demo-brand stores
- **S3 Google connector:** `Connector` + `SyncRun` + `GoogleRemoteLocation`; agency OAuth or mock; BI list; map / create+map / auto-map by store code; Data Health UI
- **GBP write (profile push):** Location 360 → Push to Google (title, phone, website, address, store code) via Business Information API; Pull from Google; mock updates local cache only

### 2026-08-13
- **Settings hub:** Overview + Branding + **API Configuration** (agency-only)
- `IntegrationConfig` model — secrets AES-GCM; env vars remain fallback
- Catalog: Google Business Profile, Maps, Nominatim, GSC, Ads, WAHA, Meta WhatsApp, App base URL
- OAuth / Maps resolvers read Settings DB first, then env
- Domain **atlasnow.co** documented for OAuth redirects
- Maps fetch: Places phone when API key enabled
- Industry autosuggest on Clients
- Data Health: live OAuth only (mock disabled)
- **S4 start:** `MetricObservation`, GBP dictionary (PRD §8.2), MetricCard contract UI, Location 360 Visibility, Control Tower portfolio live counters

### 2026-08-04
- Scaffold Next.js di Atlas Technology path
- PRD + Blueprint → tech tasks
- WAHA = temp bridge
- **Fase 1 implemented:** login, tenant membership, app shell, 10 modules
- **UI redesign:** light SaaS shell + demo GBP Performance / Reviews / Posts (mock data, honest labels)
- **Feature map from reference UIs:** Performance → Control Tower; Reviews → Reputation; Posts → Posts & Offers (live Google = later sprints)

## Links
- [[02 Projects/P2P Labs|P2P Labs]]
- [[Home]]

### 2026-08-15
- Changed: Task 5 review fix — unreplied SQL superset + q AND; inbound-after-outbound test
- Why: lastOutboundAt==null AND dropped replied-then-inbound; unreplied OR overwrote search
- Next: Task 6 authenticated GET /api/conversations routes

### 2026-08-15
- Changed: Task 5 list/get conversation service + thread-open audit, commit d1a8b1d
- Why: Agency inbox queries over OPEN WaConversation + AuditEvent on thread open (no HTTP/UI)
- Next: Task 6 authenticated GET /api/conversations routes

### 2026-08-15
- Changed: Task 4 WAHA webhook route + apiKeyMatches (timing-safe X-Api-Key), commit 75c5d18
- Why: Public ingest entrypoint for WAHA monitor; fail closed on empty key
- Next: Task 5+ (conversations list/thread service/UI per plan)

### 2026-08-15
- Changed: Task 6 — GET /api/conversations and GET /api/conversations/[id] (agency staff only)
- Why: Authenticated list + thread APIs for WAHA conversations monitor
- Next: UI / remaining tasks consuming these routes

### 2026-08-15
- Changed: Task 7 — agency ConversationsInbox + i18n EN/ID + `stats.mappings`; client still ModulePlaceholder
- Why: Monitor-only WAHA inbox (no composer); emptyNoMap vs emptyWait from ACTIVE WAHA mapping count
- Next: Manual check on :3000 (admin@p2plabs.local → /conversations → webhook row)

### 2026-08-18
- Changed: E3.2 Channels + Meta OAuth (client Connect) + webhook ingest Messenger/IG + map to location
- Why: Client Admin authorize Page themselves; agency sits along
- Next: Agency create Meta App, register redirect + webhook, App Review for prod

### 2026-08-18
- Changed: E3.1 unified inbox — source column/filter, PLATFORM_ID (IGSID/PSID not phone), Customers phone-only
- Why: Pondasi CRM omnichannel sebelum Connect Meta (E3.2)
- Next: E3.2 Client Channels + Facebook Login for Business

### 2026-08-18
- Changed: Auto WAHA session on location save (name=atlas_location_id); QR + pairing on 360 and branch table
- Why: Client must not log into WAHA; staff scan QR on store phone
- Next: User connect Vilo numbers via Location 360

### 2026-08-18
- Changed: Agency Conversations = client cards then inbox `?client=` + branch filter; API scopes tenant
- Why: Same admin UX as Locations — pick brand before seeing chats
- Next: Same pattern on Customers if asked

### 2026-08-18
- Changed: Agency Locations = client cards → `?client=` branch table; client login skips cards
- Why: Admin table mixed brands and defaulted to P2P Labs; user asked cards then table
- Next: Map Vilo branches to GBP

### 2026-08-18
- Changed: Maps pin coords (!3d!4d) over camera @; URL store name over neighbor; Delete on location list
- Why: maps.app.goo.gl/2H9x… is Vilo Gelato Menteng; fetch used viewport and picked Bakpo next door
- Next: User re-fetch Menteng URL + delete junk Gg. Jambu / Bakpo rows

### 2026-08-18
- Changed: Maps fetch prefers Places business name over street slug; Nearby Search fallback; Location 360 re-fetch
- Why: Share links slug Jl./Gg. as /place/; geocode Place Details overwrote Vilo name; 360 had no re-fetch
- Next: User re-fetch Vilo Tomang + archive duplicate street-named rows

### 2026-08-15
- Changed: Conversations final-fix wave — P2002 never 5xx (message + identifier); identity only @c.us / @s.whatsapp.net / bare digits; strip :device; @g.us/@newsletter UNKNOWN
- Why: Review: unique race 500s; group/newsletter JIDs invented as PHONE_VERIFIED
- Next: Parked T1/T2/T7 stay parked
