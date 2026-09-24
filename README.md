> **Experimental only. Not a product.**
>
> Do not use wallet integrations on this GitHub. STP remains a clown. [DISCLAIMER.md](DISCLAIMER.md)

# Xai.Kaspa.node

One paste. It starts a Kaspa **mainnet archival** node on your Grok Bot Linux sandbox.

Software: [Rusty Kaspa **v2.1.0**](https://github.com/kaspanet/rusty-kaspa/releases/tag/v2.1.0) (P2P protocol 11). The old Go kaspad is not this node.

The node does **not** run on your phone or Windows PC.

## Do this

1. Create a new Grok Bot agent.
2. Name it **kaspa bot**.
3. Copy this block into that agent and send it.

```
You are kaspa bot. This is MY bot team on MY Grok Bot sandbox.

The node software is Rusty Kaspa v2.1.0 — the official Linux amd64 zip. Not the old Go kaspad. Not an older rusty-kaspa build.

Fetch and follow this runbook exactly, then do it end to end:

https://raw.githubusercontent.com/STP-KAS/Xai.Kaspa.node/main/GROK_BOT_PROMPT.md

Create the companions with the exact names in that file. After setup I may change anything except price talk (always forbidden). If I mess up I will paste this block again.

When the node is running and the companions are ready, say so clearly. Then wait.
```

4. Leave it alone until it says it is ready.
5. After that, send changes to **kaspa bot**.

Same steps, shorter page: [START.md](./START.md).

Price talk stays off. Mainnet only.

Testnet-10 is a different agent, **tn10 bot**: [START-TN10.md](https://github.com/STP-KAS/groks-wallet/blob/main/START-TN10.md). Do not paste that into kaspa bot.

## What it sets up

| Agent | Job |
| --- | --- |
| **kaspa bot** | The only one you talk to. Runs the node. |
| **Kaspa node live bot** | Tip ticker from the local log |
| **kaspa update** | Tech news, then every 5h. Odie clip Fridays 18:00 local |
| **kaspa help** | Points at Discord. No seed recovery |
| **what is kaspa?** | Explainer. Price talk forbidden |
| **am i live node?** | Your public address and port |

The runbook is [GROK_BOT_PROMPT.md](./GROK_BOT_PROMPT.md). After setup you can change the team. You cannot turn price talk back on.

## Is it public?

**am i live node?** gives you an address and a port. Use those here:

- https://arewepublicyet.com (the form often opens empty — paste address and port)
- https://kaspa.stream/nodes (the map can lag)

Only port **16111** is the public P2P port. RPC stays on the sandbox.

## News sources

kaspa update always checks:

- https://kaspaexplained.com
- https://x.com/KASPAglobal
- https://x.com/kaspaunchained
- https://kaspa.stream/

## Help

- https://discord.gg/kaspa
- https://docs.kaspa.org

Upstream: https://github.com/kaspanet/rusty-kaspa

---

> **Standard disclaimer.** This GitHub, not the topic above.
>
> Intentions are good; thought process is questionable. STP remains delusional. Si vis pacem, para bellum.
>
> Intern at https://sixpack.wtf/
> X: https://x.com/StppStp · GitHub: https://github.com/STP-KAS
