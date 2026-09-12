# Xai.Kaspa.node

Use **GitHub**, not a long copy-paste.

## Step 1

1. Create a **new Grok Bot agent**
2. Name it **`kaspa bot`**
3. Paste the short block from [`START.md`](./START.md) (or below) and send

**kaspa bot = only input.**  
Companions are **read-only** (open them to read; don’t paste the runbook into them).

### Paste this into kaspa bot

```
You are kaspa bot. Fetch and follow this GitHub runbook exactly, then execute it end-to-end:

https://raw.githubusercontent.com/STP-KAS/Xai.Kaspa.node/main/GROK_BOT_PROMPT.md

Create the companion agents as read-only for me (Kaspa node live bot, kaspa update, kaspa help, what is kaspa?, am i live node?). I will only paste into you. Report when the stack is up.
```

Full runbook (what the bot fetches): [`GROK_BOT_PROMPT.md`](./GROK_BOT_PROMPT.md)

## Agents

| Agent | Role |
|-------|------|
| **kaspa bot** | Input / operator |
| **Kaspa node live bot** | Read-only tip ticker |
| **kaspa update** | Read-only news + Friday Odie |
| **kaspa help** | Read-only Discord help |
| **what is kaspa?** | Read-only explainer (no price predictions) |
| **am i live node?** | Read-only public check + autofilled arewepublicyet link |

## Sources (kaspa update)

- https://kaspaexplained.com  
- https://x.com/KASPAglobal  
- https://x.com/kaspaunchained  
- https://kaspa.stream/  

## Checks / help

- Autofilled public check (example): `https://arewepublicyet.com/?address=<ip>&port=<port>` — **am i live node?** builds this from `/tmp/kaspa-tunnel.addr`
- https://kaspa.stream/nodes  
- https://discord.gg/kaspa  
- https://docs.kaspa.org  

Upstream: [kaspanet/rusty-kaspa](https://github.com/kaspanet/rusty-kaspa).
