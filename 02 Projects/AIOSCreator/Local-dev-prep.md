# AIOSCreator — local-dev prep

#resource #sop

Tidak build. Tidak `npm install`. Tidak tarik model. Ini checklist mesin + layout repo.

## Hardware fit

RTX **3060 12GB** → PRD pack **8–12GB**:
- Draft default **480p / 720p**
- FLUX.2 Klein **4B** (Apache-2.0, ~8GB)
- Wan 2.2 **5B**
- 4K = **upscale queue later**, bukan native
- Jangan janji Wan 2.7 4K di mesin ini (15–30+ min / clip, impractical)

ffmpeg sudah ada: `C:\ffmpeg\bin\ffmpeg.exe` (8.1.2).

## Tools

| Tool | Kenapa | Status |
|---|---|---|
| Git | repo [AIOSCreator](https://github.com/joefebrian/AIOSCreator) | **OK** portable 2.55.0 · `%LOCALAPPDATA%\Programs\Git` |
| Node.js | Next.js control plane | **OK** 22.19.0 + npm 10.9.3 · `%LOCALAPPDATA%\Programs\nodejs` |
| pnpm | package manager | **OK** 11.25.0 via corepack |
| Python 3.12 | FastAPI worker + ComfyUI later | **OK** 3.12.10 |
| uv | Python package runner | **OK** 0.12.9 |
| ffmpeg | platform packager | **OK** 8.1.2 essentials |
| NVIDIA driver | CUDA 12.6 runtime | **OK** 560.94 · RTX 3060 12GB |
| SQLite | bundled in Python | **OK** 3.49.1 |
| ComfyUI | local inference | **OK** native `%LOCALAPPDATA%\Programs\ComfyUI` · `:8188` · torch 2.6.0+cu124 · **autostart** `scripts/start-comfyui.cmd` (Startup + `focus-dev.ps1`) |
| Stability Matrix | optional model GUI | **skip** — CreatorOS talks to ComfyUI API, not SM |
| Docker Desktop | Postgres/Redis Hybrid | **jangan** di Phase 0 |
| VS Build Tools | native addons (better-sqlite3 fallback) | **belum** — optional, `scripts/admin-once.ps1` as Admin |
| Windows long paths | node_modules deep trees | **belum** — same admin script |

Restart terminal setelah winget selesai supaya PATH ke-load.

H3 motion **lanes** (draft / identity / quality) = [[H3-Motion-Profiles]]. Jangan tarik FastVideo VSA atau Acc LoRA sebelum INT8 I2V lolos 1 clip di 3060.

**TaoMate-H3** = streaming H3 for Hopper nodes only ([[TaoMate-H3]]). **Jangan clone / pip / flash-attn hopper di PC ini.**

## PC focus (Grok Build + CreatorOS)

Dual Xeon E5-2696 v4 parks cores on **Balanced**. Script tiap session (user-level, UltraViewer **tidak** di-kill):

```
apps/AIOSCreator/scripts/focus-dev.cmd
```

Sudah di-copy ke Startup folder. Efek: High Performance, Game DVR off, Copilot/Search extras stop, `grok` + `node` + `python` = High priority.

Sekali sebagai Admin (UAC):

```
apps/AIOSCreator/scripts/admin-once.ps1
```

Itu yang nulis Defender exclude (`Grok`, ComfyUI, nodejs), stop SysMain, long paths, VS Build Tools. **Jangan** auto-elevate dari remote UltraViewer — UAC secure desktop bisa lock session.

## Docker decision

**Skip.** Local mode PRD = local DB + local media + local GPU.

Pasang Docker **hanya jika** Joe minta Hybrid (hosted control plane + local worker). Saat itu: Postgres + Redis container, **bukan** ComfyUI di Docker.

## Repo layout (siap, kosong)

```
apps/AIOSCreator/          ← product code (bukan note Obsidian)
  README.md
  .gitignore
  .env.example
  apps/web/                ← Next.js (M00)
  apps/worker/             ← Python FastAPI → ComfyUI (M01–M02)
  data/media/              ← local masters + derivatives (gitignored)
  data/db/                 ← SQLite (gitignored)
```

Vault notes tetap di `02 Projects/AIOSCreator/`. Jangan campur `node_modules` ke root vault.

## Env (no secrets in vault)

Salin `.env.example` → `.env` di `apps/AIOSCreator`. Jangan commit.

- `XAI_API_KEY` — SpaceXAI / xAI, server-side only
- Social OAuth tokens — encrypt at rest later
- Tidak ada per-clip billing key untuk gen lokal

## Milestone gate (PRD §27)

Kerja berikutnya **setelah** Git/Node/Python ready, urut:

1. **M00** Foundation — Next.js, SQLite, job log, local-worker protocol
2. **M01** AI Studio — provider abstraction, lineage
3. **M02** ComfyUI — web request → local GPU → asset
4. M03–M10 sesuai PRD. Autopilot terakhir.

## Anti-slop (MVP, bukan Phase 5)

Default 3–5 public YouTube posts / channel / day. Diversity gate. Human approval ON. Unlimited **generation** OK. Unlimited **identical publish** = channel death (YT 16 Jul 2026).

## Links
- [[02 Projects/AIOSCreator]]
- [[Home]]
