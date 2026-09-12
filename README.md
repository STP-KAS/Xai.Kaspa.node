# Xai.Kaspa.node

**One Grok Bot prompt** → this four-agent Kaspa stack:

| Agent | Role |
|-------|------|
| **kaspa bot** | Main operator — archival node, bore/public, 20‑min keep-alive |
| **Kaspa node live bot** | Tip ticker |
| **kaspa update** | Tech/news (24h first → every 5h) + Odie clip Fridays 18:00 |
| **kaspa help** | Discord-first tech help router |

> **TL;DR:** Paste [`GROK_BOT_PROMPT.md`](./GROK_BOT_PROMPT.md). Your phone/Windows needs nothing; work runs on Grok Bot’s Linux sandbox.

| | |
|---|---|
| Network | Kaspa **mainnet** archival |
| Public checks | [arewepublicyet.com](https://arewepublicyet.com) (primary), [kaspa.stream/nodes](https://kaspa.stream/nodes) |
| Discord help | [discord.gg/kaspa](https://discord.gg/kaspa) |
| Docs | [docs.kaspa.org](https://docs.kaspa.org) |

## Quick start

1. Open Grok Bot.  
2. Copy everything under the line in [`GROK_BOT_PROMPT.md`](./GROK_BOT_PROMPT.md).  
3. Send it. Expect the four agents above plus node sync/public checks.  
4. Leave keep-alive, tip-digest, 5h update, and Friday Odie routines enabled.

## Who runs it

**kaspa bot** runs `kaspad` on the **bot’s Linux sandbox** — not on your Windows/phone. Outbound may show a Cloudflare WARP IP; for public P2P use a **bore** tunnel and advertise `ipv4:tunnel-port`. See the prompt for details.

## Am I public?

1. **https://arewepublicyet.com** — use advertised `--externalip` (often bore IPv4 + tunnel port).  
2. **https://kaspa.stream/nodes** — crawler/map; can lag even when arewepublicyet already succeeds.

## Reference media

- Odie POW: https://x.com/pow_odie/status/1942975402764325256  
- File: [`media/odie-pow-weekly.mp4`](./media/odie-pow-weekly.mp4) — shown by **kaspa update** every Friday 18:00 local.

## Limits

Archival needs lots of disk. Keep-alive restarts processes only if down; it cannot recreate data after a full disk wipe. WARP alone usually cannot list on the stream map without a tunnel or real public IP. This repo is an operator prompt + notes, not a hosted node service.

Upstream: [kaspanet/rusty-kaspa](https://github.com/kaspanet/rusty-kaspa).
