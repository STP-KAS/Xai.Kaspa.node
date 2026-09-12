# Grok Bot — one prompt (copy everything below the line)

---

You have a Linux sandbox. Goal: run a Kaspa **mainnet archival** full node, make it **public** when fully synced, and help me see it on https://kaspa.stream/nodes. Do not lecture first — execute, then report what actually happened.

## Constraints (verify with commands, don’t assume)
- Prefer the official prebuilt `rusty-kaspa` Linux amd64 release from `kaspanet/rusty-kaspa` on GitHub — do **not** build from source unless the binary download fails.
- No Docker unless it already works on this machine.
- Keep **RPC on 127.0.0.1 only**. Public means **P2P** (`16111`), not open RPC.
- Not a public peer until IBD/sync has finished successfully.
- Use `--archival` from the first start (keeps historical block data; heavy disk).
- Use low-RAM-friendly flags if memory is tight: `--ram-scale=0.3`, modest `--async-threads`, `--disable-upnp` if UPnP is useless here.

## Procedure
1. Check: `uname -a`, `free -h`, `nproc`, `df -h`, `rustc --version` (optional), `which docker`, disk for data under `/tmp` or a durable path you create.
2. Fetch latest official Linux x86_64 zip (`rusty-kaspa-*-linux-amd64.zip`), unpack `kaspad`.
3. Data dir e.g. `/tmp/kaspa-data-mainnet` (or `/home/.../kaspa-data-mainnet` if more durable). Logs alongside.
4. Start **mainnet archival** in background, private at first:
   - `--yes --archival --disable-upnp --ram-scale=0.3`
   - `--listen=127.0.0.1:16111`
   - `--rpclisten=127.0.0.1:16110` (and borsh/json RPC on localhost only)
   - `--maxinpeers=0` until synced; keep outbound peers for IBD
5. After start: PID, first ~80 log lines, RSS, alive after 20–30s. Must show peer connect and/or IBD progress or call it a failed experiment.
6. Watch until fully synced (log phrases like Finished IBD / IBD 100% / steady tip with no IBD). If it dies: paste exact OOM/panic/error; don’t blindly retry nonsense.
7. **When fully synced**, go public:
   - Relaunch same datadir with `--archival`, `--listen=0.0.0.0:16111`, `--maxinpeers` > 0, `--externalip=<public-ip>:16111`
   - If behind Cloudflare WARP / CGNAT / no UPnP: try everything reasonable (bind public, externalip, TCP tunnel only if it can advertise a reachable P2P host:port). Report honestly if inbound is impossible on this host.
8. Verify public: `ss` shows `0.0.0.0:16111`, optional inbound peers, then look up the IP on **https://kaspa.stream/nodes** (and/or https://arewepublicyet.com). Screenshots help.
9. Report: PID, archival yes/no, public address, map lookup result, disk/RSS. Never claim “node is running/public” unless process is alive and evidence matches.

## Success criteria
- Process stays up with peer/IBD activity during sync.
- After sync: archival + public P2P, and a real attempt to appear on https://kaspa.stream/nodes.

Stay on mainnet. Prefer action + facts over lectures.
