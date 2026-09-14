# Agent Wallets

Software gets a real account here, not a delegated one. An agent is not a human account wearing an API key and a callback URL — it has a wallet of its own, an identity of its own, and a history of its own, operating inside rules its owner wrote. That is what a financial account looks like when machines were assumed from the start.

---

## What an agent is issued

Every agent account comes with genuine infrastructure:

- An ERC-4337 smart account on Robinhood Chain, with a signing key separate from its parent's
- An Agent ID namespaced under that parent (`@yourname/agent-name`)
- Its own encrypted balance in MansaFi's confidential token contracts
- A payment history that rolls into the parent's feed as it happens

It can hold USDG, be funded by its parent, and transact on its own judgment inside whatever limits it was given. Real economic agency, fenced.

---

## From task to settlement

```
Owner creates the agent account
        ↓
Owner writes a spend policy (ceilings, permitted payees, hours)
        ↓
Owner funds the agent's vault
        ↓
Agent decides a task warrants a payment
        ↓
Policy is evaluated before anything is signed
        ↓
Inside the limits: agent signs and submits directly
        ↓
Above the approval threshold: owner is notified, approves or declines
        ↓
Settles on Robinhood Chain → webhook fires → parent feed updates
```

The consequential detail sits in the middle. Policy enforcement lives in the smart account's validation contract and runs before the chain will accept the transaction, not as a review afterward. An agent is not merely discouraged from exceeding its limits — it has no path to landing a valid transaction that does. [Policy Engine](policy-engine.md) has the mechanics.

---

## What people use this for

- Coding agents paying for model calls as they run, rather than drawing down prepaid credit
- Trading systems executing inside a stated risk budget
- Agentic platforms billing per sub-task, close to real time
- Developer tools metering consumption straight to the agent consuming it, with no billing intermediary

---

## Why agent payments need encryption

Agent activity is confidential by default, exactly as human activity is, and the reason carries further than it first appears. A public spend pattern is a live feed of a business's usage volume, cost base, and competitive tempo. MansaFi keeps those figures encrypted while leaving the agent's address and its transaction record fully visible on-chain, like any other account. Provable activity, private numbers.

---

## Continue

- [Policy Engine](policy-engine.md)
- [x402](x402.md)
- [Event Stream](event-stream.md)
