# atlasnow

#project

## Outcome
**AtlasNow** = Local Demand-to-Action Control Tower untuk HQ multi-cabang.

**Tagline:** Optimize Every Outlet. Capture More Demand.  
**Promise:** Turn existing Google presence into measurable local growth.

SOP discoverability: [[03 Areas/SEO-AEO-GEO]]  
TikTok developer: org **PT Sorak Digital Media** · app **AtlasNow** (Business) App ID `7679020348364392455`. **Not** SWYPE. Keys stay on this app only.

**2026-09-02 19:58:** Developer Portal — **AtlasNow Live** (Production). Confirmed product **Local Service API** only. Scopes Live: `local.shop.manage`, `local.product.manage`, `local.voucher.manage`. This is **TikTok GO Dining till** (query + redeem voucher), not Login Kit, not DMs, not Shop CS. Live kasir still needs dining **merchant_id** + token after Merchant Portal Accept. Spec: `docs/superpowers/specs/2026-08-28-tiktok-local-service-design.md`.

**2026-09-02 GO till demo (built):** public `https://atlasnow.co/demo/go`. In-app: Chat apps → TikTok GO till (merchant ID → they Accept AtlasNow in Merchant Portal → Fetch token → map shops). Loyalty Scan sample QR `TT-DEMO-*` + recap tebus per outlet (not GMV). Live TT- redeem still needs merchant token. Not DMs.  
**Money master (wajib dibaca sebelum develop fitur berbayar / Free / kredit / payment):** [[AtlasNow-Monetization-PRD]]

**Language (locked 2026-09-06):** product surface = **workspace**, never **meja**. Physical table (QR di meja toko) stays meja.

**WhatsApp Commerce (proposed 2026-10-23):** [[AtlasNow-WhatsApp-Commerce-PRD]] — pilot YOLA FUN. Katalog + cart WhatsApp, order, link bayar di gateway merchant, atribusi cabang. Belum live. Uang tetap [[AtlasNow-Monetization-PRD]]. Nomor tetap [[AtlasNow-WhatsApp-Decision]].

### 2026-10-28
- Changed: No deploy. Authenticated production QA was not run. The only active super admin is `hello@atlasnow.co` on `p2p-labs`, and this browser is on the sign-in page. Meta configuration `1401943948578182` still stops at the Business Suite login. Webhook fields were re-read and are complete. `WHATSAPP_COEXISTENCE_ENABLED` stays unset. No monitor account was created.
- Why: Coexistence UAT needs a signed-in module check, a dashboard read of that configuration, an eligible number, and a named alert destination.
- Next: Sign in as `hello@atlasnow.co`, then open Chat apps, inbox, commerce, loyalty, and YOLA. Sign in to Meta and read configuration `1401943948578182` without editing it.

### 2026-10-28
- Changed: No deploy and no flag change. Guest journal shows `srv1756392` logging until 10:09:01 UTC and a new kernel at 10:09:32 UTC, with no in-guest shutdown, OOM, or disk-full event. CPU was idle. B3.1 image `sha256:5759d97016ae58c5044b5bc4d2135359972b16ecae4125a0317e16ea3060ff63` came back healthy. YOLA order `YOLA-20261027-000001` is still present. Phone rows were not moved. A signed empty webhook returned 200 and did not add messages.
- Why: The owner reported the VPS down. The guest was up through 10:09 UTC, then the hypervisor restarted it. Provider power logs are not on the machine. Hostinger guest-agent telemetry was reading memory and process lists, not requesting a shutdown.
- Next: Authenticated walk of chat apps, inbox, commerce, loyalty, and YOLA still needs a signed-in session. Meta configuration `1401943948578182` still needs a dashboard read before Coexistence UAT. Name an external alert destination before adding a monitor.

### 2026-10-28
- Changed: No new deploy. Live app `1551959122621683` already subscribes `messages`, `account_update`, `history`, `smb_message_echoes`, `smb_app_state_sync`, and `message_template_status_update` on `https://atlasnow.co/api/webhooks/whatsapp`. `WHATSAPP_COEXISTENCE_ENABLED` stays unset. Embedded Signup config `1401943948578182` and Pages config `2295500691270291` were left as they are. Real Business App onboarding was not run.
- Why: The webhook fields are ready. Graph cannot show whether configuration `1401943948578182` includes Business App onboarding, and no eligible number was named.
- Next: Sign in to the Meta App Dashboard and read that configuration before creating another one. Name one Business App number before turning the flag on.

### 2026-10-28
- Changed: Deployed coexistence and conversation handoff `e9105a062983d7bce781205d4a2a36e45e92764a` (`release/yola-phone-claim`) as image `sha256:5759d97016ae58c5044b5bc4d2135359972b16ecae4125a0317e16ea3060ff63`, tag `atlasnow-atlas:yola-e9105a0`. Migrations `20261028190000_wa_message_source` and `20261028200000_conversation_handoff` applied. `WHATSAPP_COEXISTENCE_ENABLED` stays unset. Caddy, Postgres, and WAHA were not recreated. YOLA and P2P phone rows stayed put. Automation tables stayed empty. No WhatsApp message was sent. Real Business App onboarding was not run.
- Why: Staff replies need a conversation handoff with its own expiry. The earlier outage was this laptop's Singapore VPN: the VPS captured zero packets from `194.5.82.44`, while `116.206.196.6` got HTTPS 200 and an SSH banner.
- Next: Name one eligible Business App number before turning the flag on. Confirm webhook fields `history`, `smb_app_state_sync`, `smb_message_echoes`, and `account_update` in the Meta dashboard. Callback stays `https://atlasnow.co/api/webhooks/whatsapp`. Rollback tag `atlasnow-atlas:rollback-pre-coexistence-b31` is `sha256:89aacc333206c10e9ea709fde7fd85951d68fb76fb18d41ef831bf2bad872ed7`. Dump `/root/atlasnow-backups/atlasnow-20261028-pre-coexistence-b31.dump` sha256 `a64fb28645819cb9b68d607fcd298fb436160b2bff7a743ad9268278ff45e7dd`.

### 2026-10-28
- Changed: Committed coexistence as a second WhatsApp connection method on `release/yola-phone-claim` at `896225e97d9225591fc552da070e1ffd2186f02e`. Same Cloud connector. Launch stays off unless `WHATSAPP_COEXISTENCE_ENABLED=true`. Migration `20261028190000_wa_message_source` adds `WaMessage.source`. Not deployed. `76.13.198.28` did not accept SSH or HTTPS from this network, so production is still image `sha256:89aacc333206c10e9ea709fde7fd85951d68fb76fb18d41ef831bf2bad872ed7`.
- Why: An eligible WhatsApp Business App number should be able to stay on the phone while AtlasNow uses Cloud API. Existing numbers must not be converted, and a new connection must not turn automation on.
- Next: Deploy `896225e` when the VPS answers. Leave the coexistence flag unset. Subscribe `history`, `smb_app_state_sync`, `smb_message_echoes`, and `account_update` on app `1551959122621683` without changing the callback. Real Business App onboarding is still unverified.

### 2026-10-28
- Changed: Deployed workspace automation `6ce841bfb6b6c3dbfff386a55395c62171aa7d21` (`release/yola-phone-claim`) as image `sha256:89aacc333206c10e9ea709fde7fd85951d68fb76fb18d41ef831bf2bad872ed7`. Migration `20261028180000_workspace_automation_runtime` applied. `WorkspaceAutomation`, allowlist, audit, and outbound tables are empty. YOLA and P2P phone rows were not moved. Flags and the allowlist stayed off and empty. No WhatsApp message was sent.
- Why: Each workspace needs its own inbound, payment, and marketing switches. A missing row stays off, and the YOLA phone stays on the existing flags.
- Next: The two-recipient pilot still needs named, consented, authorized numbers. Rollback image `atlasnow-atlas:rollback-pre-automation-b2` (`sha256:7715202abd5d7a60b4b0a8d65c4038e562e21cfd6b24ab3551cb97b77b89da85`). Dump `/root/atlasnow-backups/atlasnow-20261028-pre-automation-b2.dump` sha256 `f73e236df6bc939545b9d20ff78a4e212b463d09a671cb12f329a75cc9760f29`.

### 2026-10-28
- Changed: Deployed phone-ownership guard `9642967788a16cfdd8936440ca3c116a7abc400b` (`release/yola-phone-claim`) as image `sha256:7715202abd5d7a60b4b0a8d65c4038e562e21cfd6b24ab3551cb97b77b89da85`. Migration `20261028160000_workspace_automation` created an empty table. YOLA and P2P phone rows were not moved. Flags and the allowlist stayed off and empty. No WhatsApp message was sent.
- Why: `ensureWabaPhone` could rewrite `tenantId` and the Cloud connector was saved before that check. A second workspace must not capture an already connected number.
- Next: The two-recipient pilot still needs named, consented, authorized numbers. Rollback image `atlasnow-atlas:rollback-pre-phone-claim` (`sha256:df3adf6094819b670bc0b80dee9ca3a8270313d435c5dd888d66a0846afcbab1`). Dump `/root/atlasnow-backups/atlasnow-20261028-pre-phone-claim.dump` sha256 `0a8d31d500b60f9e7b76cbc7aef4250b8be994d1f36f5809e3fc41c8553a8911`.

### 2026-10-28
- Changed: Deployed YOLA pilot checkout `dc670ec65aa5f50ec87080aa6fdfa7b1cc0e2aaf` (`release/yola-pilot-v2`) as image `sha256:df3adf6094819b670bc0b80dee9ca3a8270313d435c5dd888d66a0846afcbab1`. Public demo checkout is `/pay/yola/{token}`. Migration `20261028120000_yola_order_origin` applied. Synthetic order `YOLA-20261027-000001` stays origin synthetic and `PENDING_PAYMENT`; its sandbox session is `SIMULATED_PAID` and it has no ticket. Its two outbound rows are `quarantine`. Flags and the pilot allowlist stay off and empty. No WhatsApp message was sent.
- Why: A completed Flow needs one sandbox order and a dummy payment link that cannot settle revenue or issue a ticket. The signed-in `/yola` page could not also be the public checkout.
- Next: Name two consented recipients and authorize each send before `YOLA_PILOT_LINK_SEND_ENABLED` can be turned on. Rollback image `atlasnow-atlas:rollback-pre-pilot-v2` (`sha256:5a976374ee0dde936fb182d98b16192ff44f420f6e87ecff0844948398be52ee`). Dump `/root/atlasnow-backups/atlasnow-20261028-pre-pilot-v2.dump` sha256 `c465aa85d7402896a49cf95d8ac897ff473551daf65d9137e35a54424451013e`.

### 2026-10-27
- Changed: Deployed visit-time patch `5a46f4c3a58ac9f4f0bf5e86612923ee0340de1f` as image `sha256:5a976374ee0dde936fb182d98b16192ff44f420f6e87ecff0844948398be52ee`. Workspace `yola-fun-gandaria-city` (`cmvqlxwnt0001khwmqphni4if`) under agency `p2p-labs`. Phone `1324915324031839` linked there. P2P phone unchanged. Flags false. Synthetic order `YOLA-20261027-000001` is TEST SYNTHETIC, not a customer.
- Why: The published Flow submits `SLOT_*` ids. The system-user token already on the P2P Cloud connector can read the YOLA WABA and the approved template. The QA user token was not copied.
- Next: One real Flow send still needs a named allowlisted recipient and an explicit flag change. Rollback image `atlasnow-atlas:rollback-pre-slot-5a46f4c`. Dump `/root/atlasnow-backups/atlasnow-20261027-pre-slot-5a46f4c.dump`.

### 2026-10-27
- Changed: Read-only Meta check on the running `8450d4b` image. No rebuild, no migration, no phone-row write, flags stayed false.
- Why: Graph, using the existing commerce QA token, confirmed WABA `1736564147618215` (PT Sorak Digital Media) and phone `1324915324031839` (`+1 555-436-2839`). Approved template `yolafun_presale_offer` (`1762350784861919`, en, MARKETING) opens Flow `1744309183784887` on screen `OFFER`. The Flow dropdown submits `SLOT_1000` style ids, which the current parser rejects.
- Next: Name the YOLA workspace before inserting a `WabaPhone` row. Do not attach this phone to `p2p-labs-jeyw`. Set `YOLA_WA_ACCESS_TOKEN` in `/opt/atlasnow/.env` and recreate atlas with `--no-build`. Leave the four flags false.

### 2026-10-27
- Changed: Deployed YOLA FUN on atlasnow.co from `release/yola-commerce-production` `8450d4b4f76a543126add98b84e8d08443ca9965`. Image `sha256:d71ae2187234e502f900965a471a935b278fac5fd70dea525711cd548e759bfd` (amd64). Migration `20261027120000_yola_fun_commerce` applied. Sends, bulk, live payments, and live tickets are false. Phone id and Graph token are unset.
- Why: The live database already had the two October inbox migrations and did not have `commerce_orders`. The release image carries the inbox files, omits `commerce_orders`, and adds only the YOLA tables.
- Next: Link the YOLA phone to its workspace `WabaPhone` row and set `YOLA_WA_PHONE_NUMBER_ID`. Put `YOLA_WA_ACCESS_TOKEN` on the VPS, then verify the Marketing template. Leave the four flags false until that read and a named recipient exist. Rollback image `atlasnow-atlas:rollback-pre-yola-8450d4b`. Dump `/root/atlasnow-backups/atlasnow-20261027-pre-yola-8450d4b.dump`.

### 2026-10-27
- Changed: YOLA FUN Postgres module on clean branch `release/yola-commerce-production` at `6b46fc9c4d1bcf278d1d208604e134d0157307ce`, based on last verified production commit `f686143`. Additive migration `20261027120000_yola_fun_commerce`. Existing webhook only. Flags off. Not deployed.
- Why: The demo SQLite app cannot boot on the Biznet stack. SSH to the VPS timed out and TLS to atlasnow.co returned no handshake bytes, so the live image was not re-read and production migrate was not run.
- Next: Restore SSH, confirm the running image digest and `_prisma_migrations`, back up Postgres, then apply only `20261027120000_yola_fun_commerce`. Leave sends, bulk, live payments, and live tickets off. Put `YOLA_WA_ACCESS_TOKEN` on the VPS, not in chat, before a Graph template read.

### 2026-10-27
- Changed: No production deploy. YOLA FUN commerce stays uncommitted on `hackathon/yola-fun-demo` at `8cb8e3867fff126e6541070676a80ee6ee657889`. It is local SQLite under `/demo/yola` and is not on the Biznet production stack.
- Why: Deploying that branch onto atlasnow.co would replace the live app and its Postgres history.
- Next: Do not push or boot this branch on the VPS. Production webhook stays `https://atlasnow.co/api/webhooks/whatsapp`.

### 2026-10-27
- Changed: Marketing template send path on `hackathon/yola-fun-demo`, still uncommitted. Status stays `UNVERIFIED` until `verifyMarketingTemplate()` reads Meta. An env flag of APPROVED does not approve it. One opted-in test send can be queued and stays held. Bulk send stays disabled. No live WhatsApp send. Production webhook untouched.
- Why: Founder reported the Marketing Flow template approved. This machine has no Meta token, so the API check could not run and the status was not flipped.
- Next: Provide `YOLA_WA_ACCESS_TOKEN` outside chat, then one named recipient who has opted in. Do not republish the Flow. Do not deploy.

### 2026-10-27
- Changed: Local YOLA FUN commerce engine on `hackathon/yola-fun-demo`, still uncommitted, on top of `8cb8e3867fff126e6541070676a80ee6ee657889`. Keyword routing queues one held Flow invitation. A matching `flow_token` creates one `PENDING_PAYMENT` order `YOLA-YYYYMMDD-######` at Rp499.000. Mock payment can issue one two-visit ticket. Real WhatsApp send stays off because the published Flow ID is not in the repo. Production webhook untouched.
- Why: M1–M4 need a working local path before Meta or Xendit credentials exist.
- Next: Founder supplies the published Flow ID through environment config, not chat. Do not republish the Flow. Do not deploy. Do not move `https://atlasnow.co/api/webhooks/whatsapp`.

### 2026-10-27
- Changed: Local Flow inbox on `hackathon/yola-fun-demo`, uncommitted, on top of `8cb8e3867fff126e6541070676a80ee6ee657889`. New route `POST /api/demo/yola/flow-webhook` verifies `X-Hub-Signature-256` with `YOLA_FLOW_APP_SECRET`, accepts one sandbox `nfm_reply`, and stores a CREATED order in `data/yola-flow-demo.sqlite`. List at `/demo/yola/submissions`. No ticket. Production webhook untouched. Not connected to Meta.
- Why: Phase 1 of the YOLA FUN Flow presale needs a signed receiver before any phone test. App `1551959122621683` still shares the live callback, so this route stays local.
- Next: Founder approves a separate Meta app and an isolated HTTPS callback before any subscribe or send. Do not publish the Draft Flow. Do not deploy.

### 2026-10-27
- Changed: YOLA FUN demo on `hackathon/yola-fun-demo` at `8cb8e3867fff126e6541070676a80ee6ee657889` is now one product, Kartu Presale 2× Masuk, Rp499.000, Gandaria City. Local ad, WhatsApp simulator, sandbox payment, demo QR, staff check-in at `/demo/yola/check-in`. Sandbox PAID is simulated revenue, not omzet. Business chat identity +1 555-436-2839. No deploy.
- Why: Founder replaced the visit-request story with presale → payment → QR entry for the client demo.
- Next: Restart from `atlasnow-yola-demo` with `npx next dev --turbopack -p 3010`. Clear the session before the live walkthrough. Do not merge or deploy.

### 2026-10-27
- Changed: Local YOLA FUN client demo on branch `hackathon/yola-fun-demo` at `3e75def82a2749a234abe72bc803e851f44e05c0`. Worktree `atlasnow-yola-demo`, base `dc676f9`. Customer `/demo/yola`, workspace `/demo/yola/workspace`, port 3010. In-memory qualified lead only. Fixture insight, not live Muse Spark.
- Why: Morning client demonstration. Synthetic branches. Not a production workspace.
- Next: Leave Draft PRs #1–#8 unmerged. Do not deploy this demo. Restart with `npx next dev --turbopack -p 3010` from the worktree. YOLA FUN production stays NO-GO.

### 2026-10-26
- Changed: M2.4 operator signing on Draft PR https://github.com/joefebrian/atlasnow/pull/8. Commit `5b1dc5e7c5da8e9df02cf9a6b49cdb903c9512cf`. GitHub run https://github.com/joefebrian/atlasnow/actions/runs/40359014239 staged the migration package and refused to persist an attestation for this private repository. The preflight now checks a detached Ed25519 approval. `scripts/release-trust-fingerprint.txt` is `UNPINNED`. No founder key was created. Commerce Actions https://github.com/joefebrian/atlasnow/actions/runs/40363106623 succeeded (unit and db). That run is not a release approval. No production connection.
- Why: GitHub-native attestation cannot be stored for this user-owned private repository.
- Next: Stop. Do not re-run the attestation workflow. Do not merge. Staging and production stay NO-GO. Image binding is NOT VERIFIED. YOLA FUN stays NO-GO.

### 2026-10-26
- Changed: M2.4 attestation gate on Draft PR https://github.com/joefebrian/atlasnow/pull/8. Commit `ef13691369e9b96844e4fd664d819ef2fbffa6c1`. The signer workflow is manual and attests the migration package only. The session token cannot install `.github/workflows/release-provenance.yml` (contents API 404, scopes `gist`, `read:org`, `repo`). No GitHub attestation was issued. Commerce Actions https://github.com/joefebrian/atlasnow/actions/runs/40349945085 succeeded. That run is not a provenance attestation. No production connection.
- Why: A pull-request trigger would attest arbitrary head commits, and this identity cannot write workflow files.
- Next: Stop. The founder installs the workflow from the GitHub website if they choose. Do not merge. Staging and production stay NO-GO. YOLA FUN stays NO-GO.

### 2026-10-26
- Changed: M2.4 provenance correction on Draft PR https://github.com/joefebrian/atlasnow/pull/8. Commit `8ff38f27077042bf0d23a1ee2dd0aede08ab518c`. The operator preflight requires a GitHub artifact attestation and rejects a caller-supplied SHA. The signer workflow is `scripts/release-provenance.workflow.yml` and is not installed. Actions https://github.com/joefebrian/atlasnow/actions/runs/40342510703 succeeded on that SHA. No production connection.
- Why: Comparing `--git-sha` with `approvedGitSha` did not prove the packaged artifact was built from that commit.
- Next: Stop. The signer workflow still needs a credential with workflow scope. Staging and production stay NO-GO. Do not merge PR #1 through #8. Do not deploy. YOLA FUN stays NO-GO.

### 2026-10-26
- Changed: M2.4 release safety on Draft PR https://github.com/joefebrian/atlasnow/pull/8. Commit `8f9b7b3b0aa33a04c01a0237b73123fbc5fb297e`. Base is PR #7 at `9881e352c5536854bd6e5dbb4fe20f4403ffc505`. Restored both inbox SQL files at the observed checksums. Ordinary boot starts the server and does not run Prisma migrate. The offline preflight fails closed because `approvedGitSha` is null. Import and feed stay applied with unknown historical authorization. Orders and both conversational folders stay unapproved. Actions https://github.com/joefebrian/atlasnow/actions/runs/40302639619 succeeded on that SHA.
- Why: The read-only inventory found 39 finished rows. The 37-row note is incorrect. A later image that migrates on boot would apply the three pending folders.
- Next: Stop. A future staging-readiness assessment is NO-GO. Production rollout is NO-GO. Do not merge PR #1 through #8. Do not deploy. YOLA FUN stays NO-GO.

### 2026-10-26
- Changed: M2.3 image checklist correction on Draft PR https://github.com/joefebrian/atlasnow/pull/7. Commit `9881e352c5536854bd6e5dbb4fe20f4403ffc505`. Actions https://github.com/joefebrian/atlasnow/actions/runs/40283685660 was in progress when this note was written. Only `docs/M2_3_MIGRATION_INVENTORY.md`. Expected images are `postgres:16-alpine`, `devlikeapro/waha:latest`, `caddy:2-alpine`, and the locally built `atlas` image (`atlasnow-atlas` or `atlasnow-atlas:latest`). A mismatch is recorded and stops the visit. No production connection.
- Why: The operator table had shortened image names, so a live image could be accepted without matching `compose.yaml`.
- Next: Stop. Staging and production stay NO-GO. Wait for the founder's three metadata texts. Do not merge PR #1 through #7. Do not deploy. YOLA FUN stays NO-GO.

### 2026-10-26
- Changed: M2.3 operator procedure correction on Draft PR https://github.com/joefebrian/atlasnow/pull/7. Commit `243beec28bfa225a73fbd2a5b31d33ea909e0878`. Actions https://github.com/joefebrian/atlasnow/actions/runs/40271678560 was in progress when this note was written. The founder confirms compose project `atlasnow` at `/opt/atlasnow` and stops on a mismatch. The read-only query selects the container role and database. The running image file list is not the next deployment. No production connection.
- Why: The export must name `POSTGRES_USER` and `POSTGRES_DB`, and the current image must not be treated as the next release inventory.
- Next: Stop. Staging and production stay NO-GO. Wait for the founder's three metadata texts. Do not merge PR #1 through #7. Do not deploy. YOLA FUN stays NO-GO.

### 2026-10-26
- Changed: M2.3 production migration inventory procedure on `feature/conversational-commerce-m2-3`. Commit `3bb6d223506e71396aeee2b83cf46fd460fa93a9`. Draft PR https://github.com/joefebrian/atlasnow/pull/7 stacked on PR #6. Actions https://github.com/joefebrian/atlasnow/actions/runs/40268740531 was queued when this note was written. Procedure is `docs/M2_3_MIGRATION_INVENTORY.md`. Clean commit `6efaa659` has 40 migration checksums. The two inbox folders are absent. The five later folders are unapproved. Production was not opened.
- Why: M2.2 is accepted as a review and still NO-GO until an operator supplies `_prisma_migrations` metadata.
- Next: Stop. Wait for the founder's separately authorized CSV and image hash list. Do not merge PR #1 through #7. Do not deploy. Do not pass production credentials to an agent. YOLA FUN stays NO-GO.

### 2026-10-26
- Changed: M2.2 review correction on Draft PR https://github.com/joefebrian/atlasnow/pull/6. Commit `6efaa659a14c2f3712d9b6f2dc0d9dfde235d48e`. Actions https://github.com/joefebrian/atlasnow/actions/runs/40267589141 was in progress when this note was written. The review now records that Prisma 5.22.0 `migrate deploy` applied a pending migration on a disposable loopback database after an applied folder was removed, and that `migrate deploy` and `migrate status` both exited 0 after the local file no longer matched the stored SHA-256. Production `_prisma_migrations` was not opened. No schema, entrypoint, or migration change.
- Why: A missing applied folder cannot be relied on to stop application startup. Unconditional `migrate deploy` on boot stays a release blocker.
- Next: Stop. NO-GO for staging and production until an operator supplies the six `_prisma_migrations` columns and a later change makes startup skip migrate by default. Do not merge PR #1, #2, #3, #4, #5, or #6. Do not deploy. Do not pass production credentials to an agent. YOLA FUN stays NO-GO.

### 2026-10-26
- Changed: Conversational commerce M2.2 release-readiness review on `feature/conversational-commerce-m2-2`. Commit `28ad2362ef767da7708ececa007020741b5ccc79`. Draft PR https://github.com/joefebrian/atlasnow/pull/6 stacked on PR #5. Review is `docs/M2_2_RELEASE_READINESS.md`. No schema change. Production history was not opened.
- Why: QA persistence at `df3e7f2` is accepted, and a production or staging boot would still run `prisma migrate deploy` on every folder in the image.
- Next: Stop. NO-GO for staging implementation until a backup proves the production migration inventory and boot stops migrating by default. Do not merge PR #1, #2, #3, #4, #5, or #6. Do not deploy. YOLA FUN stays NO-GO.

### 2026-10-26
- Changed: Conversational commerce M2.1B atomic rollback on `feature/conversational-commerce-m2-1b`. Head `df3e7f2997fcddad6bc7a499d62db40bff146ac9`. Boundary fix `84b8ff477e45f8a1e601d8777b8e84353afb8593`. Draft PR https://github.com/joefebrian/atlasnow/pull/5. Actions https://github.com/joefebrian/atlasnow/actions/runs/40262845004. A connection inserted inside `runAtomic` rolls back when the callback returns a failure or throws. No schema change.
- Why: Prisma commits a transaction callback that returns. Skipping the diff flush left the direct connection insert committed.
- Next: Stop. Do not merge PR #1, #2, #3, #4, or #5. Do not deploy. Do not migrate production. YOLA FUN stays NO-GO.

### 2026-10-26
- Changed: Conversational commerce M2.1B row-level payment, webhook, attribution, policy, and credential persistence on `feature/conversational-commerce-m2-1b`. Implementation `1c19dfe900bb663e01012996db9a0ceff451fd41`. CI workflow `e99cb2aa7b7c4b427ed314fc299bb1e3a3559065`. Draft PR https://github.com/joefebrian/atlasnow/pull/5 stacked on PR #4. Actions https://github.com/joefebrian/atlasnow/actions/runs/40260873495. Disposable `atlasnow_cc_qa_*` only. Not applied to production.
- Why: The remaining QA snapshot rewrite and one global advisory lock could still overwrite a concurrent booking when a payment, webhook, attribution, policy, or credential write ran.
- Next: Stop. Production migration, a webhook route, a gateway, and a live provider need a separate approval. Do not merge PR #1, #2, #3, #4, or #5. Do not deploy. YOLA FUN stays NO-GO.

### 2026-10-26
- Changed: Conversational commerce M2.1A row-level booking persistence on `feature/conversational-commerce-m2-1a`. Booking commit `b0447e1c7fc7ed8510c8a52e5ae641d7d4b244de`. CI workflow `e2ea6dad766dad5e70fe53bd12f258d03fd8ec1c`. Draft PR https://github.com/joefebrian/atlasnow/pull/4 stacked on PR #3. Actions https://github.com/joefebrian/atlasnow/actions/runs/40254829247. Disposable `atlasnow_cc_qa_*` only. Not applied to production.
- Why: The QA snapshot rewrite and one global advisory lock serialized unrelated merchants and rewrote every Cc row on a booking write.
- Next: Stop. M2.1B replaces payment, webhook, attribution, credential, and policy snapshot writes before the adapter is production-grade. Do not merge PR #1, #2, #3, or #4. Do not deploy. YOLA FUN stays NO-GO.

### 2026-10-26
- Changed: Conversational commerce M2 QA PostgreSQL adapter on `feature/conversational-commerce-m2`. Implementation `0cdeb608d32b2b661c7d89fddc69dd0282fc1c2c`. CI workflow `280900fd2c7b6c10ed196fc13b0213df27f369d6`. Draft PR https://github.com/joefebrian/atlasnow/pull/3. Actions https://github.com/joefebrian/atlasnow/actions/runs/40251614342. Disposable `atlasnow_cc_qa_*` only. Not applied to production.
- Why: The schema review was conditionally accepted. The adapter needed a nullable idempotency foreign key, location consistency, BIGINT amounts, provider-scoped live slots, and a fail-closed QA database.
- Next: Stop. Production migration and deployment need a separate approval. Do not merge PR #1, #2, or #3. YOLA FUN stays NO-GO.

### 2026-10-26
- Changed: Conversational commerce M2 schema and QA review on `feature/conversational-commerce-m2`, commit `d5bd07e47bfff1471908b4c978ce1932271944dc`. Draft PR https://github.com/joefebrian/atlasnow/pull/3 stacked on PR #2. Actions https://github.com/joefebrian/atlasnow/actions/runs/40247773374. Documentation only. `prisma/schema.prisma` unchanged. No migration folder.
- Why: PostgreSQL persistence needs a reviewed schema, claim transaction, and disposable QA database before any adapter is written.
- Next: Stop. Wait for approval before editing the Prisma schema, creating a migration, or writing the SQL adapter. Do not merge PR #1, #2, or #3. Do not deploy. YOLA FUN stays NO-GO.

### 2026-10-26
- Changed: Conversational commerce M1C.2 pre-persistence gate on `feature/conversational-commerce-m1a`, commit `18a965c71c5a26f7a595b8245720aa0f1fd2cf3c`. Draft PR https://github.com/joefebrian/atlasnow/pull/2. Actions https://github.com/joefebrian/atlasnow/actions/runs/40246864273. In-memory only. No migration, route, gateway, or Flow.
- Why: A transient provider error could close the idempotency key after a booking was already committed, and a shared booking or transaction reference could resolve to another tenant.
- Next: Stop. Do not start a SQL adapter, a webhook route, a gateway, or YOLA FUN onboarding until a separate review.

### 2026-10-26
- Changed: Conversational commerce M1C.1 orchestration boundary hardening on `feature/conversational-commerce-m1a`, commit `f57506298781d549a2232c41843ed67266b39831`. Draft PR https://github.com/joefebrian/atlasnow/pull/2. Actions https://github.com/joefebrian/atlasnow/actions/runs/40245579152. In-memory only. No migration, route, gateway, or Flow.
- Why: A losing idempotency claim could still call the provider, a Commerce writer could submit a forged paid event, and a crash after the claim left no envelope for recovery.
- Next: Stop. Do not start a SQL adapter, a webhook route, a gateway, or YOLA FUN onboarding until a separate review.

### 2026-10-26
- Changed: Conversational commerce M1C port-backed orchestrator on `feature/conversational-commerce-m1a`, commit `0ee2aacec34f63d1ca7e619aab5651b822f09373`. Draft PR https://github.com/joefebrian/atlasnow/pull/2. Actions https://github.com/joefebrian/atlasnow/actions/runs/40221202475. In-memory ports only. No migration, route, gateway, or Flow.
- Why: The orchestrator kept a second copy of bookings, payments, and idempotency beside the repository. M1C makes the ports the source of truth and keeps provider calls outside the atomic write.
- Next: Stop. Do not start a SQL adapter, a webhook route, a gateway, or YOLA FUN onboarding until a separate review.

### 2026-10-26
- Changed: Conversational commerce M1B.1 persistence contract correction on `feature/conversational-commerce-m1a`, commit `66cd7c6ba100740342981fda4ea9e28217c0ec42`. Draft PR https://github.com/joefebrian/atlasnow/pull/2. Actions https://github.com/joefebrian/atlasnow/actions/runs/40218702460. No migration, route, gateway, or Flow.
- Why: Repository results could be mutated in place, a reservation could disagree with its connection, and policy and webhook identity were wider than one merchant surface or one connection.
- Next: Stop. Do not start M1C. Do not merge PR #1 or PR #2. YOLA FUN stays NO-GO.

### 2026-10-26
- Changed: Conversational commerce M1B persistence ports on `feature/conversational-commerce-m1a`. Code `05d82d0faab0d28de23cc8a89b44d960f0bd6143`. CI `903aa40050097b0c28267e9a22f554930abdb283`. Schema sketch only. Draft PR https://github.com/joefebrian/atlasnow/pull/2. No migration, route, gateway, or Flow.
- Why: The orchestrator needs durable boundaries for bookings, payments, webhooks, and attribution before any table is created.
- Next: Stop. Do not start M1C. Do not merge PR #1 or PR #2. YOLA FUN stays NO-GO.

### 2026-10-26
- Changed: Conversational commerce M1A.2 on `feature/conversational-commerce-m1a`, commit `d6aefd64c05d096f3ac4c0777c42ca2532596468`. Timeout reconciliation uses the original provider and request. Each payment attempt has its own ledger. Draft PR https://github.com/joefebrian/atlasnow/pull/2. No migration, route, gateway, or Flow.
- Why: A lookup against a different provider could treat a committed timeout as absence, and one transaction ledger mixed independent payment attempts.
- Next: Stop. Do not start M1B. Do not merge PR #1 or PR #2. YOLA FUN stays NO-GO.

### 2026-10-25
- Changed: Conversational commerce M1A.1 contract hardening on `feature/conversational-commerce-m1a`. Contract commit `8b9bba557b932993f07ec34283ec5b2cb254aabf`. CI commit `0adef948fa5e3f81ece04f28f6fd2df1847675b9`. Draft PR https://github.com/joefebrian/atlasnow/pull/2. A timeout stays pending until lookup or a documented idempotency guarantee. Payment proof must match the stored attempt. No migration, route, gateway, or Flow.
- Why: A timeout or an evidence label could otherwise authorize a second booking or a paid status.
- Next: Stop. Do not start M1B, persistence, webhooks, or payments. Do not merge PR #1 or PR #2. YOLA FUN stays NO-GO.

### 2026-10-25
- Changed: Conversational commerce M0 contracts and M1A in-memory orchestrator on `feature/conversational-commerce-m1a`, commit `53989bb21600a1d647aa869f2fc1ee2c3083870d`. Draft PR https://github.com/joefebrian/atlasnow/pull/2 targets `feature/commerce-meta-catalog`. No migration, no route, no gateway, no Flow, no catalog write.
- Why: Booking, payment, and attribution need a provider-neutral contract before any table or live adapter. Catalog commerce stays the product master.
- Next: Stop. Persistence, webhooks, and provider clients need a separate review. Do not merge PR #1 or PR #2. Do not onboard a pilot from this slice.

### 2026-10-25
- Changed: Read-only YOLA FUN onboarding audit. Production has no tenant, location, commerce connection, or WABA row for YOLA FUN. The public site still has no SKU or price. Verdict is NO-GO for live catalog onboarding. QA catalog and the test line were not reused. No product, flag, OAuth, or payment change.
- Why: Admission tickets and party or event services are restricted or prohibited on Meta commerce surfaces that AtlasNow can use. Approved-seller status is unknown.
- Next: Merchant confirms legal entity, Meta Business admin, their own WABA and catalog, and exact offers. Do not create a workspace or list a ticket.

### 2026-10-25
- Changed: Imported one QA product, `ATLASNOW-QA-SHAPE-001`, from catalog `1649727826536046` into tenant `commerceqa20261023tenant`. Price `28780`, Meta id `28730199909979244`, review `UNKNOWN`, eligibility `UNKNOWN`. A second import did not create or overwrite a row. Import flags were then removed. Discovery stays on for that tenant. Image stayed `sha256:027689fb313384f8511a6c5ce85681010692cb4ca31cc09b57411ee840d88bef`. Backup `/root/atlasnow-backups/atlasnow-20261025T150250Z-pre-qa-import.dump` sha256 `d73398502aef87a1fb56efb2874fdd9865b1c4db836a3d3bd4e2859811ab797f`.
- Why: Founder approved one QA import. The write is local. Meta was not updated.
- Next: Do not enable sync, polling, order capture, or payments. Do not import another SKU without approval.

### 2026-10-25
- Changed: Deployed the price parser hotfix. Running image `sha256:027689fb313384f8511a6c5ce85681010692cb4ca31cc09b57411ee840d88bef` (`atlasnow-atlas:price-f686143`, commit `f68614367c40e7f921519f4700c00e0f7728cfd8`). QA discovery still on for `commerceqa20261023tenant`. Import stays off. Live read of catalog `1649727826536046` parsed `IDR28,780` as `28780`. Product master stayed empty. PR #1 was not merged.
- Why: Founder approved this image. The previous parser left the QA price null.
- Next: Do not import `ATLASNOW-QA-SHAPE-001` until a separate approval. Rollback image is `atlasnow-atlas:rollback-pre-price-f686143` (`sha256:0beb661d88142a2fd1b00a379bb38c94db036c035b56de8c6a0e497b2e1d7f68`). Leave the additive columns in place.

### 2026-10-25
- Changed: Price parser accepts `IDR28,780`. Commit `f68614367c40e7f921519f4700c00e0f7728cfd8` on draft PR #1. Actions run https://github.com/joefebrian/atlasnow/actions/runs/40188477743 passed. Staged image `atlasnow-atlas:price-f686143` digest `sha256:027689fb313384f8511a6c5ce85681010692cb4ca31cc09b57411ee840d88bef` is not running. Production stays on `sha256:0beb661d88142a2fd1b00a379bb38c94db036c035b56de8c6a0e497b2e1d7f68` with QA discovery still on.
- Why: The live QA catalog price was `IDR28,780`, which the parser did not read as 28780.
- Next: Do not boot the staged image until a separate approval. Do not enable import.

### 2026-10-25
- Changed: Enabled read-only Meta catalog discovery for `commerceqa20261023tenant` only. Same image `sha256:0beb661d88142a2fd1b00a379bb38c94db036c035b56de8c6a0e497b2e1d7f68`. Import, sync, polling, order capture, and payments stay unset. QA catalog `1649727826536046` lists SKU `ATLASNOW-QA-SHAPE-001` as Meta-only. Price label is `IDR28,780`. Parsed `unitPriceIdr` is null. Product master was not written.
- Why: Founder authorized discovery for that tenant. Compose injects only keys listed on the atlas service, so the two variables were added there and in `.env`.
- Next: Do not import, sync, or enable payments. A price parser change needs its own approval before any import of this SKU.

### 2026-10-25
- Changed: Deployed Slice 2.5 to production. Running image `sha256:0beb661d88142a2fd1b00a379bb38c94db036c035b56de8c6a0e497b2e1d7f68` (`atlasnow-atlas:slice25-465904984325`, commit `465904984325a62c92b3008e9b04787e235af4b1`). Migrate applied only `20261024200000_commerce_catalog_import` and `20261024220000_commerce_catalog_feed`. `20261024180000_commerce_orders` was not applied. History is 39 finished. Commerce switches stay unset. PR #1 was not merged.
- Why: Founder authorized this commit and this image. The entrypoint migrates on boot.
- Next: Do not enable discovery, import, sync, order capture, or payments. The read-only Meta catalog QA pilot needs its own authorization. Do not `docker compose up --build` from `/opt/atlasnow`; that tree is not this commit. Code rollback after this migrate is `atlasnow-atlas:rollback-app-pre-slice25-4659049` (`sha256:61817fc4acd8cf1121c76c9be68934ddd3737f2a3479fb58c47d0612c0e7e001`), the previous app plus the two new folders. The pre-migrate image `sha256:c57dd5418ebdf1e40649a66ec536dc2be2ad2bdc29ff9a09bf69fcd7643ede9c` cannot boot against the new history.

### 2026-10-25
- Changed: Slice 2.5 preflight only. Approved commit `465904984325a62c92b3008e9b04787e235af4b1`. Live image remains `sha256:c57dd5418ebdf1e40649a66ec536dc2be2ad2bdc29ff9a09bf69fcd7643ede9c`, also tagged `atlasnow-atlas:rollback-pre-slice25-4659049`. New dump `/root/atlasnow-backups/atlasnow-20261025-pre-slice25-4659049.dump` sha256 `d3d5164037317dc3985f0e02d11575860304364d1e6d3c530ac0fa345e1b3dd6`. Staged image `atlasnow-atlas:slice25-465904984325` digest `sha256:0beb661d88142a2fd1b00a379bb38c94db036c035b56de8c6a0e497b2e1d7f68` is not running. It has 39 migration folders and omits `20261024180000_commerce_orders`. Not booted.
- Why: Release preparation needed a backup and a checked image before any migrate-on-boot.
- Next: Wait for Founder authorization that names this commit. Do not start the staged image. Do not set a commerce switch.

### 2026-10-25
- Changed: Commerce page no longer queries CommerceOrder while order capture is off. Tip `4659049` on `feature/commerce-meta-catalog` (fix `391615e`). Catalog discovery and import are separate tenant gates. A discovery grant does not enable the import POST. The Slice 2.5 image still omits `20261024180000_commerce_orders`. Push run https://github.com/joefebrian/atlasnow/actions/runs/40151615323 passed, including the release database test. Not deployed. Not merged.
- Why: A Slice 2.5 database has no CommerceOrder table. The page was querying it on every load. A read-only QA pilot must not open import for every merchant.
- Next: Leave the draft pull request unmerged. Do not rebuild production. Do not set a commerce switch.

### 2026-10-25
- Changed: Slice 2.5 release gates on `feature/commerce-meta-catalog`, commit `c1abf1a`. Import opens only when the switch is true and the tenant id is listed. Local catalog export stays blocked because radius and unit are not stored. Manifest: `docs/COMMERCE_SLICE_2_5_RELEASE.md`. Push run https://github.com/joefebrian/atlasnow/actions/runs/40150001034 and pull request run https://github.com/joefebrian/atlasnow/actions/runs/40150005334 both passed on that commit. Not deployed. Not merged.
- Why: A production image would migrate on boot. Order capture stays out of a Slice 2.5 image until Milestone C is approved on its own. The QA import must not open for every merchant.
- Next: Leave the draft pull request unmerged. Do not rebuild production. Do not set a commerce switch. A live QA import of SKU ATLASNOW-QA-SHAPE-001 still needs a separate approval and starts read-only.

### 2026-10-25
- Changed: Commerce GitHub Actions now runs the catalog import, feed, and publish tests. Commit `f64502b` on `feature/commerce-meta-catalog`. Push run https://github.com/joefebrian/atlasnow/actions/runs/40149503443 passed. The `gh` login still cannot edit workflow files. The update went through the GitHub connection that can. Not deployed. Not merged.
- Why: The review required a new green run that actually lists the five catalog tests. The earlier run on `089bb76` only ran the old list.
- Next: Leave the draft pull request unmerged. Do not rebuild production.

### 2026-10-25
- Changed: Catalog file review on `feature/commerce-meta-catalog`, commit `089bb76`. Commerce files match the successful QA feed. Local files need city, country, region, a circle origin, a radius, and unit KM or MI. An empty catalog type is unverified. Preview separates product-data blockers from execution blockers and still does not send. Not deployed. Not merged.
- Why: Address plus coordinates matched the Meta upload error for SKU ATLASNOW-QA-SHAPE-001. Radius is not stored, so the export route still cannot emit a local file. The three pending migrations stay off production. Order capture remains a separate migration.
- Next: Leave the draft pull request unmerged. The catalog tests are already in GitHub Actions as of `f64502b`. Do not rebuild production. Do not turn catalog sync on. A live QA import still needs a separate approval and starts read-only.

### 2026-10-24 (Catalog file and publish preview)
- Changed: Commerce can preview a Meta CREATE or UPDATE and download a catalog file. Commit `28a34c3` on `feature/commerce-meta-catalog`. Live sync stays off. The live sync route still does not send. Migration `20261024220000_commerce_catalog_feed` was applied on localhost only. Proposal: `docs/COMMERCE_CATALOG_BIDIRECTIONAL.md`. Not deployed.
- Why: After import, the merchant needs to see differences, keep the Meta ids, and produce a file for a manual upload. A missing required field stops the file. A local catalog needs one outlet address and coordinates.
- Next: Review the draft pull request. Do not rebuild production and do not turn `COMMERCE_CATALOG_SYNC_ENABLED` on.

### 2026-10-24 (Meta catalog import)
- Changed: Commerce can list the connected Meta catalog and import selected products into the product master. Commit `34f07c7` on `feature/commerce-meta-catalog`. Switch `COMMERCE_CATALOG_IMPORT_ENABLED` stays unset. Migration `20261024200000_commerce_catalog_import` was applied on localhost only. Proposal: `docs/COMMERCE_CATALOG_IMPORT.md`. Not deployed.
- Why: Linking a catalog stored the catalog id and left the product master empty. Import copies the chosen Meta item, including SKU `ATLASNOW-QA-SHAPE-001`, without pushing back to Meta and without overwriting an existing SKU.
- Next: Review the draft pull request. Do not rebuild production and do not turn the import switch on until that proposal is accepted.

### 2026-10-24 (WhatsApp order capture)
- Changed: Inbound WhatsApp catalog orders can be stored as `PENDING_PAYMENT` with payment `NOT_INITIATED`. Commit `022e477` on `feature/commerce-meta-catalog`. Capture switch `COMMERCE_ORDER_CAPTURE_ENABLED` stays unset. Migration `20261024180000_commerce_orders` was applied on localhost only. Proposal: `docs/COMMERCE_ORDER_CAPTURE.md`. Not deployed.
- Why: The test number ending 2839 already produced a native catalog order. AtlasNow needs to keep that order, check the SKU against the product master, and ignore webhook retries, without taking payment.
- Next: Review the draft pull request. Do not rebuild production and do not turn the capture switch on until that proposal is accepted. Do not start payment automation.

### 2026-10-24 (Commerce payments decision)
- Changed: Wrote `docs/COMMERCE_PAYMENTS_PRD.md` and pushed it as `37577fb` on `feature/commerce-meta-catalog`. Shopper checkout is the merchant's own Xendit or Midtrans. AtlasNow fees stay on the Monetization PRD rails. No commission rate. Nothing deployed.
- Why: Two later models, one shopper path. A payment link visit must not mark an order paid. Merchant production callbacks are not replaced.
- Next: Review the PRD on the pull request. Do not build the payments slice until that review accepts it. Live processing stays off.

### 2026-10-23 (Commerce production deploy)
- Changed: Commerce Slice 2 from `b7ba45e` is on https://atlasnow.co. Commerce URL: https://atlasnow.co/commerce. OAuth callback: https://atlasnow.co/api/commerce/meta/callback. Five commerce migrations applied after a verified dump. Internal brand AtlasNow Commerce QA (`atlasnow-commerce-qa`) is under P2P Labs. Catalog sync, poll, checkout, and payment stay off. Draft PR #1 is not merged.
- Why: Founder-controlled Meta connection testing on the production domain, without a staging subdomain and without YOLA FUN.
- Next: Joe adds the commerce callback in the Meta app and enters credentials himself. Do not start OAuth, do not add `catalog_management`, do not start Slice 3.

### 2026-10-23 (Commerce worker race)
- Changed: A poll worker rechecks the product before it marks a batch synced. The internal poll route stays off. Commit `b7ba45e` on draft PR https://github.com/joefebrian/atlasnow/pull/1. Not merged. Live sync stays off.
- Why: A merchant can edit the price while Meta is still answering.
- Next: Do not start Slice 3. Do not turn on live catalog sync or the poll switch.

### 2026-10-23 (Commerce final hardening)
- Changed: A late catalog batch is not applied when the price or catalog changed. Historical Meta ids stay in the database and are hidden after a catalog switch. Submitted batches can be polled without the browser. Draft PR https://github.com/joefebrian/atlasnow/pull/1 is at `b14497d`, with the Actions workflow in `6a7df29`. Not merged. Live sync stays off.
- Why: The review asked for those checks before merge.
- Next: Finish the push after the workflow scope is granted. Do not start Slice 3. Do not turn on live catalog sync. Do not apply the loyalty or broadcast schema diff.

### 2026-10-23 (Commerce review fixes)
- Changed: Catalog batch success waits for Meta processing. A new Meta login clears the old catalog until it is checked again. Commit `f23ef18` on draft PR https://github.com/joefebrian/atlasnow/pull/1. Not merged. Live sync stays off.
- Why: The review asked for those checks before merge.
- Next: Wait for another review. Do not start Slice 3. Do not turn on live catalog sync.

### 2026-10-23 (Commerce draft PR)
- Changed: Targeted commerce tests re-run, 28 passed. Docs note the draft review rule. Pull request https://github.com/joefebrian/atlasnow/pull/1 stays unmerged.
- Why: The reviewer will read the draft. Live Meta sync stays off.
- Next: Wait for review. Do not start Slice 3.

### 2026-10-23 (Commerce handoff docs)
- Changed: Added `docs/AI_DEV_STATUS.md`, `docs/COMMERCE_ARCHITECTURE.md`, and `docs/DECISION_LOG.md`. Commerce is on branch `feature/commerce-meta-catalog` (`c045788`). PR https://github.com/joefebrian/atlasnow/pull/1. Not merged.
- Why: Joe wants a reviewer to read status from the repo instead of a fresh explanation each time.
- Next: Review the PR. Do not start Slice 3. Do not turn on live catalog sync.

### 2026-10-23 (Commerce slice 2 catalog connection)
- Changed: Commerce can start an official Meta login, store the token encrypted, and link a discovered catalog and WhatsApp number to one merchant. Sync preview, idempotent jobs, and permission errors are in. Live catalog push, checkout, and payment stay off.
- Why: Joe accepted slice 1 and asked for the connection manager before any checkout.
- Next: Founder adds `catalog_management` and the callback URL on the Meta app, then puts the App ID and secret in Settings → API. Do not turn on `COMMERCE_CATALOG_SYNC_ENABLED` until a catalog permission check passes. Apply the three commerce migrations on the server only when this ships.

### 2026-10-23 (Commerce slice 1 hardening)
- Changed: Product list is searchable and filterable. Photo upload, outlet search with Select all, and View / Edit / Archive. Archived products stay archived. SKU unique per merchant, case-insensitive. IDR stays a whole number. Readiness cards stay Not connected even if a saved flag says otherwise. Detail shows each outlet as available or unavailable here.
- Why: Joe asked to harden the product master before any Meta sync or WhatsApp checkout.
- Next: Apply `20261023120000_commerce_products` and `20261023180000_commerce_image_sku` on the server only when this ships. Do not connect WhatsApp checkout, Meta Catalog, or a payment gateway.

### 2026-10-23 (WhatsApp Commerce product master)
- Changed: Workspace page Commerce. Brand admin can create, edit, and archive products with variants, IDR price, and outlet availability. WhatsApp, Meta Catalog, and payment stay Not connected. No checkout and no live catalog sync.
- Why: First slice of [[AtlasNow-WhatsApp-Commerce-PRD]]. AtlasNow is the product source of truth. Cart is not a sale.
- Next: Apply migration `20261023120000_commerce_products` on the server when this ships. Do not connect a gateway or `catalog_management` until Joe locks the rail and publishes the scope.

### 2026-10-23 (WhatsApp Commerce PRD)
- Changed: Filed v0.1 PRD “Boost Sales with WhatsApp Catalog” into the vault. Working name WhatsApp Commerce. Pilot merchant YOLA FUN. Cart is not payment. AtlasNow is not merchant of record.
- Why: Joe asked for this as a new module and for the feature to live in Obsidian before build.
- Next: Pick the first slice. Do not wire a payment gateway or new Meta catalog permission until founder locks the rail and publishes the extra scope.

### 2026-10-05 (coming soon last)
- Changed: Google Business Profile and Google Ads Local Campaign are the last two system cards, so they sit on the bottom row.
- Why: Joe wanted Coming soon at the end, below the live systems.
- Next: Hard refresh atlasnow.co.

### 2026-10-05 (plain problem slides)
- Changed: Problem heading is “Owners already feel the complexity. AtlasNow gives them one desk to run every outlet.” All 10 slides rewritten in plainer EN and ID. ID QR card still says QR meja / QR di meja. Product surface stays workspace.
- Why: Joe asked for language that is very easy to understand, and for that new heading.
- Next: Hard refresh atlasnow.co.

### 2026-10-05 (systems row of four and three)
- Changed: Removed the systems lede. Seven cards sit four on the first row and three on the second.
- Why: Joe did not want that sentence, and did not want Revenue attribution alone.
- Next: Hard refresh atlasnow.co.

### 2026-10-05 (seven homepage systems)
- Changed: What AtlasNow is is seven cards: conversations, loyalty, Google Business Profile, Google Ads Local Campaign, WhatsApp Broadcast, TikTok GO voucher redemption, revenue attribution. GBP and Ads carry Coming soon / Segera hadir.
- Why: Joe asked the block to detail those seven, with the two Google items marked coming soon.
- Next: Hard refresh atlasnow.co.

### 2026-10-05 (homepage systems section)
- Changed: “What AtlasNow is” title is “Five systems. One desk for every location.” Lede names the five systems without the crawler sentence. Bottom two cards sit centered. ID uses workspace.
- Why: Joe asked to polish that block.
- Next: Hard refresh atlasnow.co.

### 2026-10-05 (homepage lede features)
- Changed: Hero lede lists customer conversations, loyalty customer, Google Business Profile, Ads local campaigns, WhatsApp Broadcast and TikTok GO voucher redemption. ID keeps workspace.
- Why: Joe revised that operating-system sentence.
- Next: Hard refresh atlasnow.co.

### 2026-10-05 (homepage proof line)
- Changed: Hero proof is “Every outlet connected. Every customer managed. Every opportunity visible from HQ.” ID: Setiap outlet tersambung. Setiap pelanggan dikelola. Setiap peluang terlihat dari HQ.
- Why: Joe replaced the loyalty-for-one-brand line.
- Next: Hard refresh atlasnow.co.

### 2026-10-05 (hero eyebrow and Demand highlight)
- Changed: Eyebrow is “Multi-location system operations” (ID: Operasi sistem multi-lokasi). Demand highlight has a little more gap after More and padding inside the mint box.
- Why: Joe asked to rename the eyebrow and give the Demand mark some space.
- Next: Hard refresh atlasnow.co.

### 2026-10-05 (homepage Book Demo)
- Changed: Hero line is “Connect WhatsApp, Instagram, Facebook Messenger, & TikTok Message into one INBOX” (ID: Sambungkan … ke satu INBOX). Hero button is Book Demo → Google appointment schedule. Header Sign up / Open AtlasNow unchanged.
- Why: Joe asked for that inbox line and to replace the hero Open AtlasNow button with Book Demo.
- Next: Hard refresh atlasnow.co.

### 2026-10-04 (homepage hero two lines)
- Changed: EN and ID lede break after “Google” from lg up, so that paragraph is two lines. Narrow screens stay one flowing paragraph.
- Why: Joe asked for that operating-system sentence to sit on two lines.
- Next: Hard refresh.

### 2026-10-04 (homepage hero)
- Changed: EN hero is the revenue-ops lockup: eyebrow, Optimize Every Outlet / Capture More Demand, operating-system lede, channel line. Centered. ID uses the same meaning with workspace.
- Why: Joe sent the hero to put on the homepage.
- Next: Hard refresh atlasnow.co. ID locale shows the Indonesian lede.

### 2026-10-04 (inbox image retention)
- Changed: Workspace setting on Chat apps: keep inbox photos 30 days (default), 14 days, or 7 days. A scheduler deletes the file; chat text stays; purged rows are not downloaded again. Privacy and Terms state the same periods.
- Why: Joe wants image files removed after a month, with 14-day and 7-day choices, written into the legal pages.
- Next: Settings → Chat apps. Public /privacy and /terms.

### 2026-10-04 (inbox Messenger and Instagram images)
- Changed: Messenger and Instagram image attachments download from the Meta CDN at webhook time (Page token for Instagram) and show in the same thread photo slot as WhatsApp HQ. Non-CDN urls are ignored.
- Why: Joe asked for the WhatsApp photo fix on Messenger and Instagram too.
- Next: Reload Inbox. Photos already stored only load if the CDN url in the webhook has not expired.

### 2026-10-04 (inbox WhatsApp image)
- Changed: WhatsApp HQ image messages store jpeg/png/webp on the message row and the thread shows the photo. Older `[image]` rows fetch once from the Cloud media id.
- Why: Joe sent a test photo; the bubble only showed the text `[image]`.
- Next: Reload Inbox and open the chat. `[unsupported]` is still a Meta type with no file.


- Changed: Public footer one row on lg: copyright left; social + legal right (divider, smaller 24px marks). Mobile stacks credit → icons → links. Live.
- Why: Joe: penempatan logo sosial di footer ga enak.
- Next: Uncommitted. Hard refresh.

### 2026-10-03 (social icons hover color)
- Changed: Default public social marks = one black plate / white glyph (`*-mono.png` for IG, FB, TikTok; Threads + X already that). Hover/focus shows brand color (IG gradient, FB blue, TikTok cyan/magenta). X + Threads stay. HQ custom upload still grayscale → color on hover. Live footer + login.
- Why: Joe: default samain biar rapi; warna sesuai icon cuma di hover.
- Next: Uncommitted. Hard refresh.

### 2026-10-03 (social icons)
- Changed: Public social marks = Joe’s PNGs in `public/brand/social/` (Instagram, Facebook, Threads, TikTok, X). `PublicSocialLinks` uses them when HQ hasn’t uploaded a custom icon. Live footer + login.
- Why: Joe: ganti icon sosial dengan 5 file itu.
- Next: Uncommitted. Hard refresh.

### 2026-10-03 (privacy justify)
- Changed: Legal article body (`/privacy`, also `/terms` `/cookies` `/data-deletion`) `text-justify`.
- Why: Joe: rata kanan kiri di atlasnow.co/privacy.
- Next: Uncommitted.

### 2026-10-03 (PT only in footer)
- Changed: Visible UI: `PT Sorak Digital Media` only in footer `© YEAR AtlasNow · A P2P Labs (PT Sorak Digital Media) product`. Login under-logo `A P2P Lab product`. About `Made by P2P Labs` + `P2P Labs · hello@…`. Invoices / JSON-LD `legalName` still the PT (not on-page copy).
- Why: Joe: PT di footer aja; sisanya jangan ada.
- Next: Uncommitted. Hard refresh `/login`.

### 2026-10-03 (public product credit short)
- Changed: Login under-logo + public footer (home/login/signup/AppShell) → `A P2P Lab product` / `© YEAR AtlasNow · A P2P Lab product`. About still `Made by P2P Labs (PT Sorak Digital Media)`. Legal operator + invoices + JSON-LD still P2P Labs / PT Sorak Digital Media.
- Why: Joe screenshot `/login` — drop PT from this credit line; Lab singular.
- Next: Uncommitted. Refresh `/login` if the old string is cached.

### 2026-10-03 (homepage design restored)
- Changed: Live homepage layout back to original: problem **carousel**, body as `<p>`, no FactTable, no numbered lists. Copy back to marketing length. ID product-surface **meja** → **workspace**; physical QR di meja kept. Skip link / llms.txt / logo WebP / meta still on.
- Why: Joe: design berantakan after GEO stuffing (ol + tables + 10-card grid + “October 2026”).
- Next: GEO CIT-02/03 will drop on next audit. Design wins. Uncommitted.

### 2026-10-03 (SEO/AEO/GEO homepage)
- Changed: Homepage GEO sixth-pass live (FactTable + 40-word named-subject ledes, numbered `<ol>`). geo.new `aud_314326b647b7475e30046cdc071f93f3` (rules v22, 08:08Z). Original 13: ACC-20, CIT-02, CIT-03, IMG-04, CORE-02, CORE-04, ENT-02, IMG-06, IMG-07, CIT-05, PERF-14, A11Y-05, CIT-08 **pass**. CIT-02 avg 63 (best 71: “Do owners already feel this at the brand?”). CONT-03 recovered. GEO technical 100, Basic SEO 100.
- Why: geo.new audit 2026-10-03 started 76/100 with 13 open actions. Fifth-pass CIT-03 stuck at 68; problem H2 named-subject + answer variant raised structure to 85 / total 71.
- Next: ENT-08 fail is Moz DA 1 — earn links over weeks. Leave PERF-12 (lab TTFB 805 ms) and PERF-15 (14 scripts). Do not add FAQPage (SCH-17 out of original 13). Uncommitted.

### 2026-09-19 (Meta App Review approved)
- Changed: Submission **19 Sep 2026 23:41 GMT+7** approved. New Advanced Access: `pages_manage_metadata`, `pages_messaging`, `instagram_manage_messages`. Renewed: `whatsapp_business_messaging`, `pages_show_list`, `business_management`, `public_profile`, `whatsapp_business_management`, `instagram_basic`. **Did not** request `pages_read_engagement`. App **AtlasNow** `1551959122621683` still **Unpublished**.
- Why: Joe screenshot App Review. Last Policy 1.6 resubmit landed.
- Next: Joe clicks **Publish → Live** when ready (testers-only until then). Then smoke Connect Page/IG as a non-tester. Drop in-app “In development” captions. No Pixel, no MBA on live HQ, no extra perms.

### 2026-09-13 (Review Capture P0 live)
- Changed: `/r/{token}` 302 to Google writereview; intent events + UTM; QR on Reviews + Outlets 360 Reputation. Tiles: intents, new reviews, **Estimated** rate. Capture all outlet plans. GBP reply still Gold. Migration `20260911180000_review_capture` applied.
- Why: Joe gassed P0.
- Next: Map Place ID (ChIJ) on outlets, print QR. P1 AI later.

### 2026-09-16 (GitHub)
- Changed: First remote. Private [joefebrian/atlasnow](https://github.com/joefebrian/atlasnow) `main` = local product snapshot (607 files). `.env` not in git.
- Why: Joe: push atlasnow juga.
- Next: Railway/deploy still separate.

### 2026-09-11 (Meta Business Agent = later roadmap)
- Changed: Joe parked **Meta Business Agent** as future Atlas development, not Wave A. Inbox stays **human reply**. Do not Enable agent on live HQ Cloud numbers (thread control → Atlas standby). Test only on a spare WABA/number if ever. Not a live SKU; monetization PRD still “we do not sell MBA.”
- Why: Meta email “test agent at no charge”; Joe: menarik, roadmap.
- Next: App Review Messenger/IG + iPaymu KYC. Don’t build MBA.

### 2026-09-11 (footer legal name)
- Changed: Public copyright (home/legal/login/signup/AppShell) → `© YEAR AtlasNow · A P2P Labs (PT Sorak Digital Media) product`. Login left credit same. About “Made by …” already had PT (2026-09-10).
- Why: Joe: last convo was PT in the footer, not only About.
- Next: Live check atlasnow.co footer.

### 2026-09-10 (About credit)
- Changed: `/about` Developer block → **Made by P2P Labs (PT Sorak Digital Media)** (ID: Dibuat …). Same line under the body + email.
- Why: Joe screenshot lock.
- Next: Footer copyright now includes PT (2026-09-11).

### 2026-09-10 (signup = one brand)
- Changed: `/signup` always **CLIENT / one brand**. Dropped One vs Several toggle (that created AGENCY). Optional checkbox “I run more than one brand” → tenant notes for Activate. Logo first, then name, WA, email, password, terms, Continue; Google/Facebook at the bottom. `kind=agency` ignored.
- Why: Joe: page felt weird; daftar 1 dulu; group activation di backend.
- Next: Deploy. Follow-up baca notes “Asked for several brands”.

### 2026-09-09 (GA4 Ads-ready)
- Changed: Consent Mode v2 on public pages (denied until OK, then analytics + ads granted). Cookie notice **v3** (re-consent). Events: `generate_lead`, `sign_up`, `click_to_whatsapp`, `select_item`. Enhanced conversions = hashed email on signup/contact. `url_passthrough` + `_gcl_au`. AW- tag env `NEXT_PUBLIC_GOOGLE_ADS_ID` empty until Joe pastes. Legal/cookies updated. Still no Meta Pixel. Still no GA in workspace.
- Why: Joe will connect Google Ads; maximize GA4 now.
- Next: Joe — Admin GA4: key events, link Ads, Google signals ON, ignore query `brand`, internal IP, GSC. Paste AW- ID when Ads account exists, then rebuild.

### 2026-09-09 (GA4 G-HY5V8HH3Z1)
- Changed: Public-only GA4 after cookie OK (`G-HY5V8HH3Z1`). Not inbox/loyalty/cards. Ads denied. `generate_lead` on contact + `/signup/pending`. Cookie notice key bumped to v2. Privacy/cookies/FAQ/help copy updated (no longer “we don’t run Analytics”).
- Why: Joe pasted gtag snippet; picked Generate leads + traffic.
- Next: Deploy + OK the banner on atlasnow.co; Realtime in GA. FAQ row in DB may still be old until reset in Settings.

### 2026-09-09 (payment: Indonesia first, Creem parked)
- Changed: Locked [[AtlasNow-Monetization-PRD]] §12.11 + §15.3 sequence. **Rail A IDR dulu** (invoice/BCA now; iPaymu KYC in progress, not locked vs Xendit/Midtrans). SG/US merchant later = **USD on Creem** (Creem’s FX if any). **No Atlas FX API.** No third rail. `/pricing` stays IDR. Wallet stays IDR. Do not wire Creem or debit credits until ID actually collects.
- Why: Joe: foreign merchants standard USD / follow PG FX, but finalize Indonesia payment gateway first.
- Next: Finish iPaymu KYC (product/jasa email). Do not integrate iPaymu or Creem until Joe says gas.

### 2026-09-09 (ES v4 config + Chat apps Connect)
- Changed: Facebook Login config **WhatsApp ES v4** `1401943948578182` (Cloud API, system-user, never, WABA MANAGE). Stored `META_WHATSAPP_ES_CONFIG_ID` — not Pages+IG `2295500691270291`. Chat apps primary button **Connect WhatsApp Business** (coexistence extras). Token paste = P2P fallback. Skip `/register` on `FINISH_WHATSAPP_BUSINESS_APP_ONBOARDING`. Ingest `smb_message_echoes`.
- Why: Joe created the v4 configuration; gas connect flow.
- Next: Joe — Facebook Login **Allowed domains** + JS SDK + WhatsApp webhook fields `history` / `smb_message_echoes` / `smb_app_state_sync` / `account_update`. App still In development (testers only). Then try Connect on Chat apps.

### 2026-09-09 (signup HP field)
- Changed: `/signup` wajib nomor WhatsApp (08 / +62 / 62) → `Tenant.contactPhone`. Google/Facebook signup bawa HP di OAuth state. Login OAuth existing user tetap tanpa HP. Follow-up tables show the number. [[AtlasNow-Free-Activation-PRD]] §3.
- Why: Joe: field HP masukin aja. ES v4 tetap belum — itu Embedded Signup Meta (coexistence), bukan HP.
- Next: Deploy signup. Jangan ES v4 sampai Joe minta.

### 2026-09-09 (click-to-WA pending + WA pribadi wording)
- Changed: `/signup/pending` tombol **Chat HQ AtlasNow** (`wa.me/6285863666290?text=Halo AtlasNow, saya baru daftar [merek]`). Mereka harus Send — buka jendela 24 jam, Activate = session reply, bukan template. Brand query dari signup + OAuth. **Dua nomor:** chat HQ boleh HP pribadi; nomor **toko** Cloud **tidak bisa** WA pribadi — harus ganti ke WhatsApp Business App dulu. Bukan “WA pribadi = no, tercatat.” Patched [[AtlasNow-Free-Activation-PRD]] §6a, [[AtlasNow-WhatsApp-Decision]] rule 7, [[AtlasNow-PRD]] §6.0.
- Why: Joe: setup #2 saja; #3 wording sebelumnya ambigu.
- Next: Deploy pending page. Jangan ES v4 / HP-on-signup / payment gateway sampai Joe minta.

### 2026-09-09 (Free activation PRD + coexistence)
- Changed: Locked [[AtlasNow-Free-Activation-PRD]]. Signup HP wajib; Activate manusia; click-to-WA ke HQ AtlasNow (bukan template dari customer); kontak masuk P2P Labs. Free boleh 1 HQ Cloud + coexistence (app hijau). TP = PT Sorak + app AtlasNow `1551959122621683`. Trust line kecil di `/pricing` Free card. Silver parked. Payment gateway / kredit Meta = follow-up Monetization. Patched [[AtlasNow-PRD]] §6.0, [[AtlasNow-Monetization-PRD]] #8, [[AtlasNow-WhatsApp-Decision]], [[AtlasNow-Loyalty-Decision]].
- Why: Narik owner yang sudah WA Business di HP; filter ngasal tetap manusia.
- Next: Jangan build dulu kecuali Joe minta. Lalu: signup HP + pending wa.me; ES v4 + webhook coexistence; training modul setelah Connect bisa di-demo. App masih In development — Live + App Review sebelum ES ke merek luar.

### 2026-09-09 (Free training + 2-outlet cap)
- Changed: Dropped “Use the desk first / Pakai mejanya dulu” from `/pricing` Free card (hook is now QR/stamps/receipt photos). Same phrase off landing + pitch. `/deck_train` now starts Free: what’s on/not (from the pricing bullets), onboarding (signup → brand mark → 2 outlets → P2P adds users → menus), then existing loyalty slides kept. `Tenant.plan` + Locations hard-stop at 2 store doors on Free (create, unarchive, CSV, Google-map create). P2P can change plan on the client page.
- Why: Joe: that line belongs in deck_train first, not the pricing card; 2-outlet cap was copy-only.
- Next: Open `/deck_train` (login) and walk Free slides. Brand Admin still cannot self-serve invite. Birthday WA H-2 stays off Free (needs HQ Cloud / Silver). Do not rewrite Silver/Gold training yet.

### 2026-09-09 (IG inbox @username)
- Changed: Inbox title for IG/Messenger uses Graph profile → `waContact.displayName`. IG = `@joefebrian.h`. Messenger PSID `GET /{id}?fields=name` failed (unsupported); fallback `first_name,last_name` + Page `/conversations?user_id=` participants. UI never titles with IGSID/PSID.
- Why: Joe: IG inbound showed IGSID; Messenger showed PSID `28143730531949661` not the Facebook name.
- Next: Hard-refresh Inbox after deploy. Messenger shows Facebook **name** (no public @handle). Record live Send + native cut. Do not resubmit `pages_read_engagement`. Do not Publish Meta app.

### 2026-09-07 (Meta App Review UI)
- Changed: Chat apps + Conversations captions for Meta review — asset (Page / IG) visible, Facebook Login + webhook subscribe panel, live Send helper, inbound “Received via webhook”, 4s poll on Messenger/IG threads. Drop `pages_read_engagement` still.
- Why: Reviewer Policy 1.6: screencast must show asset selection, live send from app, native delivery, and a webhook event on the same Page.
- Next: Switch UI to EN, re-record 3 perms (`pages_messaging`, `instagram_manage_messages`, `pages_manage_metadata`). Do not Publish Meta app yet. Do not resubmit `pages_read_engagement`.

### 2026-09-07
- Changed: Public cancel/refund — no cash refund of paid invoices; workspace until paid period ends; 30-day notice. On `/pricing#cancel` + `/terms#fees-cancellation-refunds`.
- Why: Joe locked A (SaaS, like finishing a paid month — not an instant refund).
- Next: Deploy pricing + terms. Do not invent prorata.

### 2026-09-06
- Changed: Language lock — say **workspace**, not meja/desk, for the AtlasNow product surface.
- Why: Joe: meja ambiguous in ID.
- Next: Coexistence still discussion; HQ default remains dedicated Cloud (not WhatsApp Business App on phone) until Joe locks otherwise.

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
