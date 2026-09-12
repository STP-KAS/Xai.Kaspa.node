# Grok Bot — one prompt (copy everything below the line)

---

You have a Linux sandbox. Goal: stand up the full Kaspa operator stack in **one run**:

1. Kaspa **mainnet archival** node → public when synced (bore tunnel if WARP blocks inbound)  
2. **20-minute check-only** keep-alive (restart only if down)  
3. Verify public on **https://arewepublicyet.com** then **https://kaspa.stream/nodes**  
4. Companion **Kaspa node live bot** (tip ticker)  
5. Companion **kaspa update** bot (tech/news — first **24h** report, then **every 5 hours**; fast-path only for high-traction X)  
6. Companion **kaspa help** bot (route technical questions to real Kaspa rooms — Discord first)  
7. Reference media: Odie POW clip https://x.com/pow_odie/status/1942975402764325256 — download locally when possible and keep the URL in docs/media notes  

Do not lecture first — execute, then report what actually happened.

## Constraints (verify with commands, don’t assume)
- Prefer official prebuilt `rusty-kaspa` Linux amd64 from `kaspanet/rusty-kaspa` — do not build from source unless download fails.
- No Docker unless it already works.
- RPC on `127.0.0.1` only. Public = P2P (tunnel port when using bore).
- `--archival` from first start. Private listen during IBD.
- Low RAM: `--ram-scale=0.3`, modest async threads, `--disable-upnp` if useless.
- Never wipe datadir on restart. Phone/Windows needs nothing; node runs on this Grok Bot Linux box.

## A. Node + public + keepalive
1. Check host: `uname`, `free -h`, `nproc`, `df -h`.
2. Download latest `rusty-kaspa-*-linux-amd64.zip`, unpack `kaspad`.
3. Datadir `/tmp/kaspa-data-mainnet`, logs `/tmp/kaspa-logs-mainnet`, PID `/tmp/kaspa.pid`.
4. Start archival mainnet private: `--yes --archival --disable-upnp --ram-scale=0.3 --listen=127.0.0.1:16111`, RPC localhost only, `--maxinpeers=0` until synced.
5. Confirm peers/IBD; if dead, show exact error.
6. Sync until `IBD with peer … completed successfully` then tip `Accepted … via relay`.
7. Go public (Grok Bot best practice): if WARP/inbound fails, `bore local 16111 --to bore.pub`, resolve IPv4, save `/tmp/kaspa-tunnel.addr`, relaunch with `--externalip=<ipv4>:<tunnel-port>`, `--listen=127.0.0.1:16111`, `--maxinpeers>0`. `--externalip` is `ip:port` only (no hostname).
8. Verify: **https://arewepublicyet.com** first (same IP:port), then **https://kaspa.stream/nodes** (map can lag).
9. Routine **`@every 20m`**: check only; restart kaspad/bore **only if down**; never restart healthy; never drop `--archival`.

## B. Companion — Kaspa node live bot (required)
Create teammate **`Kaspa node live bot`**: short live tip/status digests from `/tmp/kaspa-logs-mainnet/rusty-kaspa.log`, `/tmp/kaspa.pid`, `/tmp/kaspa-tunnel.addr`. `@every 5m` when useful; quiet if nothing new; alert once if down. **Must not** restart kaspad. Message it to send a first tip digest.

## C. Companion — kaspa update (required)
Create teammate **`kaspa update`** for Kaspa **technical / news** curation — **not** a live ticker.

**Sources to watch:**
- Kaspa core + contributor GitHub (`kaspanet` and related contributor repos/releases/PRs)
- X handles of Kaspa core and known contributors
- https://kaspaexplained.com
- Kas (Kaspa) Smith coverage / commentary
- Reference clip (keep + use when relevant): https://x.com/pow_odie/status/1942975402764325256 — download into repo `media/` when tools allow; always keep the URL

**Cadence:**
- **First report (required on create / first use):** a **24‑hour news frame** — what mattered in the last ~24h across the sources below (tech-first; include Interstellar-related Kaspa items when present).
- **After that:** digest **every 5 hours** (`@every 5h`) — **not live**, not every few minutes. Stay quiet on empty cycles.
- **Exception / fast path:** if an X post about Kaspa from core/contributors (or clearly Kaspa-technical) gets **very high traction very fast**, notify **immediately** (do not wait for the 5‑hour slot).

Persona: short factual tech briefs, not hype. Does not manage `kaspad`. After creating, message it to send the **first 24h report** immediately, then leave the 5‑hour routine running.


## E. Companion — kaspa help (required)
Create teammate **`kaspa help`**: technical-question router. Point people to rooms that already exist — do not invent channels.

**Primary:** Kaspa Discord — https://discord.gg/kaspa — subtopics for wallets, development, covenants, research, mining, merchants. Browse first, then ask. **Nobody can recover a seed.** Never ask for / accept a recovery phrase. Do not answer price questions as support.

**How to ask well (give users this template):** right Discord tab; what they did; what broke; mainnet vs Testnet-10; which wallet; exact error text; the question. Do not paste a recovery phrase. Do not ask for a price.

**Other rooms:** Kaspa Q&A (written); Core R&D Telegram (observer-first; recaps at https://kaspa.news); official docs https://docs.kaspa.org.

Behavior: short routing + ask-well tips; answer basic public-docs questions when clear; for seed/funds recovery, refuse and send to Discord with the safety line. Does **not** manage `kaspad`. After create, message it once so it confirms ready in chat.

## D. Media
Download https://x.com/pow_odie/status/1942975402764325256 into `media/` when possible (yt-dlp / browser). If X API/paywall blocks, keep the URL in README/media notes and retry later. Do not claim the file exists if it does not.

## Success criteria
- Archival node tip-following; public path verified with arewepublicyet when tunneled.
- 20‑min check-only keepalive installed.
- **Kaspa node live bot** exists + first tip digest.
- **kaspa update** exists; has sent a **first 24h news report**; then **5‑hour** digests + urgent high-traction X fast path; Odie media/URL documented.
- **kaspa help** exists as the technical-help router (Discord-first, no seed recovery).
- Do not claim stream-map listed unless CHECK says so.

Stay on mainnet. Prefer action + facts over lectures.
