# Choosing an Account

Three account types share one set of rails. Same wallet infrastructure, same confidential transfer engine, same guarantees — what changes is who holds the keys, who authorizes what, and how much oversight sits on top.

---

## Personal

For one human being and their money.

**What it does:**
- Holds USDG and ETH; sends and receives confidential transfers
- Carries a `@handle` so nobody has to copy an address
- Produces request links and QR codes on demand
- Exports a decrypted history when tax season arrives

**Privacy posture:**
- Encryption is the default state, not a toggle you remember
- Disclosure happens only when you build a proof for it; silence otherwise

---

## Business

For organizations that need several people to see the same balance without any of them sharing a key.

**What it does:**
- Everything Personal does
- Several authorized signers, each with a defined role
- Raised default ceilings once enhanced verification clears
- Batch disbursement for payroll and vendor runs

**Privacy posture:**
- Identical confidentiality to a Personal account
- Exports shaped to drop straight into bookkeeping and tax software

---

## Agent

A wallet built on the assumption that its holder is software, not a person.

**What it does:**
- Runs its own Robinhood Chain smart account and Agent ID, namespaced beneath a parent (`@username/agent-name`)
- Transacts inside a spend policy the parent writes: daily ceilings, permitted counterparties, asset restrictions, hours of operation
- Speaks x402 without any adapter
- Mirrors every payment into the parent's feed as it happens

**Privacy posture:**
- Encrypted by default, exactly as a human account is
- An optional approval gate above whatever figure the parent chooses

[Agent Wallets](../agents/agent-wallets.md) covers provisioning and governance in depth.

---

## Quick reference

| What you're doing | Use |
|---|---|
| Getting paid and paying people in USDG | Personal |
| Running a shared balance across a team | Business |
| Letting software transact within limits you set | Agent |

An Agent account is never freestanding. It hangs off a Personal or Business parent, it cannot be created without one, and its policy remains the parent's to rewrite at any moment. The agent gets room to act; you keep the authority.
