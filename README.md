# Xai.Kaspa.node

Your own Kaspa Grok Bot team — started from GitHub, not a long copy-paste.

## Your team

Anyone who follows [`START.md`](./START.md) gets **their own** agents on **their** Grok Bot sandbox. Change things whenever you want. If you break something, return to START.md for a **fresh start**:

https://github.com/STP-KAS/Xai.Kaspa.node/blob/main/START.md

## Step 1

1. Create a **new Grok Bot agent** named **`kaspa bot`**
2. Paste the short block in [`START.md`](./START.md) and send

**kaspa bot = only input.** Companions are day-to-day read-only (still yours to customize via Grok).

### Paste this into kaspa bot

```
You are kaspa bot. This is MY bot team on MY Grok Bot sandbox. Fetch and follow this GitHub runbook exactly, then execute it end-to-end for me:

https://raw.githubusercontent.com/STP-KAS/Xai.Kaspa.node/main/GROK_BOT_PROMPT.md

Create the companion agents as read-only day-to-day helpers (Kaspa node live bot, kaspa update, kaspa help, what is kaspa?, am i live node?). I may customize anything later with Grok; if I mess up I will re-paste from START.md for a fresh start. Report when the stack is up.
```

## Agents

| Agent | Role |
|-------|------|
| **kaspa bot** | Input / operator — your node |
| **Kaspa node live bot** | Tip ticker |
| **kaspa update** | News + Friday Odie |
| **kaspa help** | Discord-first help |
| **what is kaspa?** | Explainer (no price predictions) |
| **am i live node?** | Public check card — per-user IP from that sandbox’s tunnel (updates when IP/port changes) |

## Am I live? (per user)

**am i live node?** is custom per user: it reads **that** sandbox’s `/tmp/kaspa-tunnel.addr` and rebuilds the card when IP/port changes (new bore tunnel, etc.).

The site form often opens **empty** — use the card values:

1. Open https://arewepublicyet.com/
2. **Address** / **Port** from the bot card (or first `ip:port` in `/tmp/kaspa-tunnel.addr`)
3. **Network** = mainnet
4. Click **Test Node Connectivity**

Also: https://kaspa.stream/nodes (map can lag even when the check passes).

## Sources (kaspa update)

- https://kaspaexplained.com  
- https://x.com/KASPAglobal  
- https://x.com/kaspaunchained  
- https://kaspa.stream/  

## Help / docs

- https://discord.gg/kaspa  
- https://docs.kaspa.org  

Upstream: [kaspanet/rusty-kaspa](https://github.com/kaspanet/rusty-kaspa).
