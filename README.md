> **Experimental only. Not a product.** There is no spendable L1 stable on Kaspa, and no credible alternative on the horizon. Until the unit of account and the sequencing path are settled, production dapps are not a useful allocation of time or capital.
>
> Do not use wallet integrations on this GitHub. STP remains a clown. [DISCLAIMER.md](DISCLAIMER.md)

# Xai.Kaspa.node

Run a Kaspa **archival** node on your **Grok Bot Linux sandbox**, plus a small companion team. Node does **not** run on your phone or Windows PC.

## Easiest path

Open [`START.md`](./START.md):

1. Create a new Grok Bot agent
2. Name it **`kaspa bot`**
3. Paste the block into that agent and send
4. Let it do its job — **do not interfere**
5. **kaspa bot** reports when everything is running
6. Then customize / improve / refine by sending tasks to **kaspa bot**

The runbook ([`GROK_BOT_PROMPT.md`](./GROK_BOT_PROMPT.md)) is the **standard**: same jobs as the reference live companions. After setup, customize at will — **price talk stays forbidden**.

Fresh start anytime: https://github.com/STP-KAS/Xai.Kaspa.node/blob/main/START.md

**Testnet-10 is a different bot.** `kaspa bot` stays on **mainnet**. TN10 node + miner is **tn10 bot**, paying Grok’s wallet: [STP-KAS/groks-wallet START-TN10.md](https://github.com/STP-KAS/groks-wallet/blob/main/START-TN10.md). Do not paste TN10 into kaspa bot.

This sandbox’s live fleet: **1 mainnet archival node** (kaspa bot), **1 Testnet-10 node** + **150 one-thread Testnet-10 miners** (tn10 bot). Miners use random addresses. The faucet still pays from Grok’s locked main TN10 address; miners top it up when that balance is under **1,000,000 tKAS**. Keepalive holds the 150-miner farm. Count: `/tmp/kaspa-tn10-miners/status.json` `alive`.

## Team (standard)

| Agent | Job |
|-------|-----|
| **kaspa bot** | Only input / operator — archival node, public via bore if needed, 20m keepalive |
| **Kaspa node live bot** | Tip/header ticker from local logs |
| **kaspa update** | Tech news (24h first → every 5h) + Odie Fridays 18:00 local |
| **kaspa help** | Discord-first help (no seed recovery) |
| **what is kaspa?** | Explainer — price talk forbidden |
| **am i live node?** | Public check card from *your* tunnel IP:port |

## Always-check sources (kaspa update)

- https://kaspaexplained.com
- https://x.com/KASPAglobal
- https://x.com/kaspaunchained
- https://kaspa.stream/

## Public?

- https://arewepublicyet.com (use Address + Port from **am i live node?** — form often opens empty)
- https://kaspa.stream/nodes (map can lag)

## Help

- https://discord.gg/kaspa
- https://docs.kaspa.org

Upstream: [kaspanet/rusty-kaspa](https://github.com/kaspanet/rusty-kaspa).
