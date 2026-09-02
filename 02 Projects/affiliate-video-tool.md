# affiliate-video-tool

#project

## Outcome
Tool internal: scan creator video, deteksi produk/brand affiliate, multiupload, multi-AI failover — **hemat storage**.

## Status
🟡 Active · **session focus (switched from AtlasNexus)**

## Repo
`/Users/joefebrian/affiliate-video-tool`  
Run: `./run-web.sh` → http://localhost:8080  
Login: `admin` + password di `.env` (`AUTH_PASSWORD`)

## Stack (ringkas)
- FastAPI + SQLite + yt-dlp + ffmpeg + tesseract
- AI: multi Gemini/OpenAI key, auto-switch saat 429
- Brand scan YouTube + analisa video downloaded (OCR + Vision)
- Storage: **PC download default**; analisa = temp file → hapus; hasil di `affiliate_products_json`

## Next actions
- [ ] Verify analisa produk end-to-end dengan Gemini `gemini-flash-latest`
- [ ] Bulk import key GSuite company (yang masih ada free-tier)
- [ ] (Optional) auto-cleanup file permanen > N hari

## Decisions log
### 2026-08-11
- Context switch: AtlasNexus → **affiliate-video-tool** (focus session)
- Local: `./run-web.sh` on :8080

### 2026-08-04
- **Storage priority 1**: temp analyse → auto-delete; simpan hanya JSON hasil produk (bukan full video di server).
- **Gemini model**: `gemini-2.0-flash` free tier sering `limit: 0` → default + fallback `gemini-flash-latest`.
- **Multi-AI**: banyak key Gemini GSuite + priority failover otomatis.

### Earlier (2026-07)
- YouTube brand scan + visual items (pakaian/aksesoris).
- Videos Downloaded: tombol Analisa Produk.
- Filter noun / product intent untuk kurangi noise subtitle.

## Links
- [[02 Projects/Projects MOC|Projects MOC]]
- [[03 Areas/Affiliate & Monetization|Affiliate]]
- [[03 Areas/AI Systems|AI Systems]]
- [[Home]]
