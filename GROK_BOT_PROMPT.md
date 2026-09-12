# Grok Bot — one prompt (copy everything below the line)

---

You have a Linux sandbox. Goal: run a Kaspa **mainnet archival** full node, make it **public** when fully synced (Grok Bot + bore tunnel best practice when WARP blocks inbound), keep it alive with a **20-minute check-only** routine, verify on **https://arewepublicyet.com** and **https://kaspa.stream/nodes**, and create a companion **Kaspa node live bot** as a live tip ticker. Do not lecture first — execute, then report what actually happened.

## Constraints (verify with commands, don’t assume)
- Prefer the official prebuilt `rusty-kaspa` Linux amd64 release from `kaspanet/rusty-kaspa` on GitHub — do **not** build from source unless the binary download fails.
- No Docker unless it already works on this machine.
- Keep **RPC on 127.0.0.1 only**. Public means **P2P**, not open RPC.
- Not a public peer until IBD/sync has finished successfully (listen private during IBD).
- Use `--archival` from the first start (keeps historical block data; heavy disk).
- Use low-RAM-friendly flags if memory is tight: `--ram-scale=0.3`, modest `--async-threads`, `--disable-upnp` if UPnP is useless here.
- Ephemeral disks lose data on full machine reset — mitigate by (1) never wiping the datadir on restart, (2) a standing **every 20 minutes** keep-alive that **checks** `kaspad` (and the tunnel if used) and restarts **only if down**.
- Your phone/Windows needs nothing installed; the node runs on this Grok Bot Linux box.

## Procedure
1. Check: `uname -a`, `free -h`, `nproc`, `df -h`, `which docker`, disk for data under `/tmp` or a durable path you create.
2. Fetch latest official Linux x86_64 zip (`rusty-kaspa-*-linux-amd64.zip`), unpack `kaspad`.
3. Data dir e.g. `/tmp/kaspa-data-mainnet` (reuse forever; do not delete between restarts). Logs alongside. Save PID to `/tmp/kaspa.pid`.
4. Start **mainnet archival** in background, private at first:
   - `--yes --archival --disable-upnp --ram-scale=0.3`
   - `--listen=127.0.0.1:16111`
   - `--rpclisten=127.0.0.1:16110` (borsh/json RPC localhost only)
   - `--maxinpeers=0` until synced; keep outbound peers for IBD
5. After start: PID, first ~80 log lines, RSS, alive after 20–30s. Must show peer connect and/or IBD progress or call it a failed experiment.
6. Watch until fully synced. Real rusty-kaspa log cues include `IBD with peer … completed successfully` and then steady `Accepted … blocks … via relay` / tip-following (no more IBD %). If it dies: paste exact OOM/panic/error; restart with the **same datadir** (resume — do not `--reset-db` unless corruption is proven).
7. **When fully synced**, go public (Grok Bot best practice):
   - If the box public IP is Cloudflare WARP / inbound fails: run a TCP tunnel to local P2P, e.g. `bore local 16111 --to bore.pub`, note `bore.pub:<port>`, resolve IPv4 of `bore.pub`. Save addr to `/tmp/kaspa-tunnel.addr`.
   - Relaunch same datadir with `--archival`, `--listen=127.0.0.1:16111` (or `0.0.0.0` if truly bare-metal public), `--maxinpeers` > 0, `--externalip=<reachable-ipv4>:<port>` (tunnel port when using bore — **not** always 16111).
   - `--externalip` must be `ip:port` (no hostname).
8. Verify public: tunnel + kaspad both alive. First probe **https://arewepublicyet.com** with that **same IP and port** (active P2P-gRPC). Then CHECK **https://kaspa.stream/nodes** (map can lag even when arewepublicyet already succeeds). Report both results honestly.
9. **Keep-alive (required):** create a standing routine on a **`@every 20m`** schedule (24/7 — node uptime is time-critical). Each run: **check only**. If `kaspad` (and bore, if public-via-tunnel) is healthy and still `--archival`, do **nothing**. If **down**, restart with the same flags/mode and **same datadir**, tell me once. Never restart a healthy node. Never drop `--archival`.
10. **Companion live tip ticker (required):** create a teammate agent named **`Kaspa node live bot`** whose job is short live tip/status digests from this node — not a second node. Give it a persona that:
    - Reads `/tmp/kaspa-logs-mainnet/rusty-kaspa.log`, `/tmp/kaspa.pid`, `/tmp/kaspa-tunnel.addr`
    - Leads with latest tip/relay/header lines; brief ticker tone
    - Installs an **`@every 5m`** routine: post when useful new tip activity; quiet if nothing new; alert once if node down
    - **Must not** restart `kaspad` (keepalive stays with this main agent)
    - Knows am-I-public URL https://arewepublicyet.com with the advertised IP:port
    - Then message that bot to send me an immediate first tip digest
11. Report final: PID, archival, public addr, arewepublicyet + stream results, keepalive + live-bot created. Never claim “listed on the map” unless the CHECK says so; never claim public without arewepublicyet (or equivalent active P2P) success when using a tunnel.

## Success criteria
- Process stays up with peer/IBD activity during sync.
- After sync: archival + publicly reachable P2P (arewepublicyet success when tunneled).
- 20-minute keep-alive: check only; restart only if down.
- **Kaspa node live bot** exists with a tip-digest routine and has sent a first digest.
- Optional map listing on https://kaspa.stream/nodes may lag.

Stay on mainnet. Prefer action + facts over lectures.
