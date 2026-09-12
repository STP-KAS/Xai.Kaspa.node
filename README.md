# Xai.Kaspa.node

**One prompt → one main agent (`kaspa bot`) → it creates the rest.**

Paste [`GROK_BOT_PROMPT.md`](./GROK_BOT_PROMPT.md) into Grok Bot. Easiest path: you only talk to **kaspa bot**; it builds the companions.

## Agents

| Agent | Role |
|-------|------|
| **kaspa bot** | Archival mainnet node, bore/public, 20‑min keep-alive |
| **Kaspa node live bot** | Tip ticker |
| **kaspa update** | News/tech (24h first → every 5h) + Odie Fridays 18:00 |
| **kaspa help** | Discord-first tech help |
| **what is kaspa?** | Explain Kaspa (no price predictions) |

## kaspa update — always check

- https://kaspaexplained.com  
- https://x.com/KASPAglobal  
- https://x.com/kaspaunchained  
- https://kaspa.stream/  

Plus GitHub core/contributors, Kas Smith, Odie clip.

## Am I public?

- https://arewepublicyet.com (primary active probe)  
- https://kaspa.stream/nodes (map; can lag)

## what is kaspa? — price rule

No price predictions. On price asks it uses the fixed “Price talk is not a source…” reply, then steers to real skills/docs.

## Help

- Discord: https://discord.gg/kaspa  
- Docs: https://docs.kaspa.org  

## Media

- Odie: https://x.com/pow_odie/status/1942975402764325256 → `media/odie-pow-weekly.mp4` (Friday 18:00 via **kaspa update**)

## Limits

Runs on Grok Bot’s Linux sandbox (not your phone/Windows). WARP often needs a bore tunnel for public P2P. Keep-alive restarts only if down. Not a hosted node service.

Upstream: [kaspanet/rusty-kaspa](https://github.com/kaspanet/rusty-kaspa).
