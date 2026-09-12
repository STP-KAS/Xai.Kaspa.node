# Grok Bot — one prompt (copy everything below the line)

---

You have a Linux sandbox. Goal: run a Kaspa **mainnet archival** full node, make it **public** when fully synced, keep it alive with a **20-minute** health check (restart / resume sync if needed), and help me see it on https://kaspa.stream/nodes. Do not lecture first — execute, then report what actually happened.

## Constraints (verify with commands, don’t assume)
- Prefer the official prebuilt `rusty-kaspa` Linux amd64 release from `kaspanet/rusty-kaspa` on GitHub — do **not** build from source unless the binary download fails.
- No Docker unless it already works on this machine.
- Keep **RPC on 127.0.0.1 only**. Public means **P2P** (`16111`), not open RPC.
- Not a public peer until IBD/sync has finished successfully (listen private during IBD).
- Use `--archival` from the first start (keeps historical block data; heavy disk).
- Use low-RAM-friendly flags if memory is tight: `--ram-scale=0.3`, modest `--async-threads`, `--disable-upnp` if UPnP is useless here.
- Ephemeral disks lose data on full machine reset — mitigate by (1) never wiping the datadir on restart, (2) a standing **every 20 minutes** keep-alive routine that restarts `kaspad` and **resumes** IBD from the existing datadir if the process died.

## Procedure
1. Check: `uname -a`, `free -h`, `nproc`, `df -h`, `which docker`, disk for data under `/tmp` or a durable path you create.
2. Fetch latest official Linux x86_64 zip (`rusty-kaspa-*-linux-amd64.zip`), unpack `kaspad`.
3. Data dir e.g. `/tmp/kaspa-data-mainnet` (reuse forever; do not delete between restarts). Logs alongside. Save PID to a known file (e.g. `/tmp/kaspa.pid`).
4. Start **mainnet archival** in background, private at first:
   - `--yes --archival --disable-upnp --ram-scale=0.3`
   - `--listen=127.0.0.1:16111`
   - `--rpclisten=127.0.0.1:16110` (borsh/json RPC localhost only)
   - `--maxinpeers=0` until synced; keep outbound peers for IBD
5. After start: PID, first ~80 log lines, RSS, alive after 20–30s. Must show peer connect and/or IBD progress or call it a failed experiment.
6. Watch until fully synced (Finished IBD / IBD 100% / steady tip). If it dies: paste exact OOM/panic/error; restart with the **same datadir** (resync/resume — do not `--reset-db` unless corruption is proven).
7. **When fully synced**, go public:
   - Relaunch same datadir with `--archival`, `--listen=0.0.0.0:16111`, `--maxinpeers` > 0, `--externalip=<public-ip>:16111`
   - If behind Cloudflare WARP / CGNAT / no UPnP: try bind + externalip + any workable TCP tunnel; report honestly if inbound is impossible.
8. Verify public: `ss` shows `0.0.0.0:16111`, then look up the IP on **https://kaspa.stream/nodes** (and/or https://arewepublicyet.com).
9. **Keep-alive (required):** create a standing routine on a **`@every 20m`** schedule (24/7 — node uptime is time-critical). Each run: if `kaspad` is healthy and still `--archival`, stay quiet; if dead/missing, restart with the same flags/mode (private vs public) and **same datadir**, tell me once that you restarted/resumed sync. Never drop `--archival`.

## Success criteria
- Process stays up with peer/IBD activity during sync.
- After sync: archival + public P2P, real attempt to appear on https://kaspa.stream/nodes.
- 20-minute keep-alive routine is installed and will restart/resume without wiping data.

Stay on mainnet. Prefer action + facts over lectures.
