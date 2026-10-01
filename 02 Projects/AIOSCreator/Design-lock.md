# AIOSCreator — Design lock

#decision

Locked 2026-09-02. **IA SoT = PRD v2.0** (left nav groups, main workspace, right inspector). The Structure Webworks 7-module graphic is a *feedback-loop* reference, not the nav tree. P2P Labs colour: [[p2plabs/P2P-Labs-Design-System]].

## Stack (ship this)

| Layer | Choice | Why |
|---|---|---|
| Primitives | **shadcn/ui** + Tailwind v4 + `cva` + `clsx` + lucide | HeliosGen already uses this (`components.json` style `base-nova`, MIT). Matches Next.js. Own the CSS. |
| Interaction | **HeliosGen** (look, don’t merge) | Infinite canvas, job history, prompt assistant, workflow nodes (`@xyflow/react`). PRD already named it UX reference. |
| Motion | `motion` (Framer) for module-light sequence | HOME seven modules must bind to real jobs — no fake loop. |
| State | zustand (HeliosGen) | Light enough for local-first. |
| Desktop later | Tauri 2 + SQLite (`node:sqlite`) | HeliosGen DESKTOP.md. Not M00. |
| Colour | P2P Labs tokens, **not** HeliosGen default, **not** Ant blue | Navy `#0B0F2B` · purple `#652DFF` · lime `#A6FF1A` · canvas `#F3F4F8` |

## Ant Design — take patterns, do **not** install `antd`

PRD: creative production OS, **not** enterprise reporting. `antd` is CSS-in-JS, different visual language, fights Tailwind/shadcn.

Steal only:

- Dense table + filter + pagination for Analytics / Publications
- Form validate + i18n for Settings / rights
- Calendar / timeline for DISTRIBUTE
- ConfigProvider-style token sheet (we already have Labs tokens)

Do not: Ant Layout sider, Ant Button as primary CTA, mix two component libraries.

## HeliosGen — take / leave

**Take**
- Guest / local mode: no account required for Phase 0
- Job poller (HTTP timeout ≠ generation timeout)
- ffmpeg/ffprobe from PATH, degrade if missing
- Workflow canvas for **CREATE → AI Studio** (nodes = CreatorOS workflow, not raw ComfyUI). Visual SoT: [[Helios-canvas-ref]]
- History + folders + local media dir
- Prompt rewrite panel (maps to Hunyuan “prompt rewrite” *idea*, run on SpaceXAI)

**Leave**
- kie.ai as default backend (credits = opposite of unlimited local wedge)
- Cloud models (Veo, Kling, Seedance) as P0 — those are **closed_* P2** in PRD
- Supabase / R2
- Copying Helios as the whole product (no kie.ai, no replacing OS nav)
- HOME is PRD v2 IA, not a canvas. Canvas = AI Studio only.

## Layout chrome

Desktop: left nav · main workspace · right inspector (PRD §26).  
HOME = seven-module pipeline, not a blank canvas. Canvas lives under **CREATE**.

## Links
- https://github.com/SegFault42/HeliosGen
- https://github.com/shadcn-ui/ui
- https://github.com/ant-design/ant-design
- [[02 Projects/AIOSCreator]]
