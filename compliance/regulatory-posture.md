# Regulatory Posture

One distinction organizes everything in this section: MansaFi is confidential, not anonymous. Your address is visible, and so is the verified identity behind it. Your figures stay sealed until you unseal one, or until lawful process requires it. Every mechanism below follows from that.

---

## The framework

MansaFi operates under the GENIUS Act of July 2025, which governs regulated stablecoins in the United States. USDG — Paxos' Global Dollar, issued natively on Robinhood Chain — qualifies under that framework, as does the bridged USDC MansaFi accepts, and stablecoin operations here are structured accordingly.

---

## Identity

Verification is mandatory at account creation for every account, Personal and Business alike, including the parent behind any Agent. It comes in tiers:

| Tier | What it takes | What it opens |
|---|---|---|
| Basic | Government ID, liveness check | Standard limits |
| Enhanced | Further documentation, proof of address | Raised limits, Business features |

Anonymous and pseudonymous accounts are not supported. Every account resolves to a verified identity, even though the figures passing through it are encrypted.

---

## Travel Rule

Cross-border and above-threshold payments fall under Travel Rule obligations. MansaFi meets them through:

- Disclosure proofs supplied to a counterparty's compliance system where required (see [Identity Verification](identity-verification.md))
- Counterparty address screening through Chainalysis or TRM Labs
- Conventional identity exchange between regulated originating and beneficiary institutions where that applies

---

## Where MansaFi operates

The beta runs in the United States and selected EU jurisdictions. Anywhere crypto payment services are explicitly prohibited is excluded from beta access.

---

## Where data lives

Account profiles and KYC records are held in a region appropriate to where the account was opened. On-chain data is inherently global, since it lives on Robinhood Chain and settles to Ethereum rather than sitting in MansaFi's infrastructure — a point made plainly during onboarding.

---

## Why these two goals don't collide

The confidential token layer conceals figures. It conceals no identities. Addresses stay public and permanently attached to a verified holder, and lawful process directed at a specific account can be answered through the disclosure mechanism in [Proving a Payment](../privacy/proving-a-payment.md). Confidentiality-not-anonymity is where regulated privacy-preserving payment systems have broadly landed, and the entire contract layer here is built around it: accountability where the law asks for it, confidentiality everywhere else.

---

## Continue

- [Identity Verification](identity-verification.md)
- [Proving a Payment](../privacy/proving-a-payment.md)
