# FAQ

---

## General

**What is MansaFi?**

A privacy-first crypto neobank on Robinhood Chain, Robinhood's AI-native Ethereum Layer 2. It is a self-custodied account for USDG and ETH in which transfer amounts are encrypted by default, settlement lands in the next ~100ms block, and people and AI agents hold accounts side by side.

**Do I need to understand blockchains to use it?**

No. Registration is an email address and a passkey, much like setting up Face ID for anything else. Keys, encryption, and settlement are all handled beneath the surface.

**What currency does it hold?**

USDG — Paxos' Global Dollar, issued natively on Robinhood Chain — with bridged USDC supported as well. A little ETH is kept on hand automatically for gas so network fees never require your attention.

**Is it anonymous?**

No, and deliberately so. Identity is verified when the account opens and your address is public on-chain. What stays private is the figure moving through the account: confidentiality, not anonymity. [Regulatory Posture](../compliance/regulatory-posture.md) explains why that distinction carries weight.

---

## For individuals

**How are my amounts kept private?**

Transfers run through confidential token contracts — an encrypted-balance ERC-20 holding amounts as ElGamal ciphertexts, with zero-knowledge proofs built on your device and checked by an on-chain verifier. Only you and the counterparty can open them. See [Encrypted Amounts](../privacy/encrypted-amounts.md).

**Can anyone see what I hold?**

No. Your balance sits on-chain as ciphertext that only your key opens. An observer sees that your address exists and holds some balance, never the figure.

**What if I need to prove a payment to a landlord or an auditor?**

Issue a disclosure proof for that one payment. It reveals what you choose, to whom you choose, and stops there. See [Proving a Payment](../privacy/proving-a-payment.md).

**My phone is gone — now what?**

A passkey synced through iCloud Keychain or Google Password Manager restores access on another device immediately. An exported key does the same. See [Keys & Recovery](../privacy/keys-and-recovery.md).

**Is my history stored in plaintext anywhere?**

Not by MansaFi. Your decrypted history is rendered locally with your own key; the servers handle ciphertext and public metadata only. There is nothing there to leak.

---

## For builders

**How do agent accounts work?**

Each agent receives an ERC-4337 smart account on Robinhood Chain and an Agent ID namespaced under a parent. It transacts under a policy the parent writes — daily ceilings, permitted payees, hours, and an optional approval threshold. See [Agent Wallets](../agents/agent-wallets.md).

**Can an agent outspend what I authorized?**

No. Policy checks happen before signing rather than as a review afterward, so a violating transaction is never constructed and there is nothing left to catch. See [Policy Engine](../agents/policy-engine.md).

**Is x402 supported?**

Yes, natively, on every agent account. See [x402](../agents/x402.md).

**How do I hear about an agent's payments?**

Subscribe to webhook events. See [Event Stream](../agents/event-stream.md) and the [Webhooks API](../api/webhooks.md).

**Can I read an agent's amounts through the API?**

Only by decrypting them client-side with your key. The API never returns a plaintext figure, because the servers hold no decryption key either. The guarantee runs all the way through.

---

## Compliance

**Why require KYC for a privacy product?**

Because confidentiality and anonymity are different things. Amounts are hidden; identities are not. Every account is tied to a verified person or entity, which is exactly what allows the product to operate under the GENIUS Act framework and to answer lawful process when it comes.

**What happens with large or cross-border payments?**

Above regulatory thresholds they fall under Travel Rule requirements, counterparty screening included. See [Identity Verification](../compliance/identity-verification.md).

**Is any of this open source?**

The confidential transfer logic — the token contracts and their on-chain verifier — is open source and auditable on Robinhood Chain. The application layer (app, backend, indexer) is not open source during beta.

---

## Fees

**What do transfers cost?**

Nothing during beta. You pay Robinhood Chain gas, typically a fraction of a cent, drawn automatically from your ETH float.

**Does the API cost anything?**

Not during beta. A metered tier for high-volume agent traffic is planned as part of the post-beta revenue model.
