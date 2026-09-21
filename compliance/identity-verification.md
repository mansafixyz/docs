# Identity Verification

The mechanics of verifying who holds an account, and of meeting cross-border obligations when payments cross a threshold.

---

## How verification runs

Identity is checked once, at account creation, through MansaFi's verification provider — Persona or an equivalent regulated vendor.

1. Submit a photograph of a government-issued ID
2. Complete a liveness capture — a short selfie video matched against that photo
3. Most cases clear within minutes; some route to a human reviewer

Enhanced verification, needed for raised limits or a Business account, adds:

- Proof of address, such as a recent utility bill or bank statement
- For Business accounts, ordinary KYB material: incorporation records and beneficial ownership

---

## Tiers and ceilings

| Tier | Daily ceiling | What it requires |
|---|---|---|
| Basic | Up to $2,500 | Government ID, liveness check |
| Enhanced | Up to $25,000 | Basic, plus proof of address |
| Business | Negotiated | KYB documentation, beneficial ownership disclosure |

Anything beyond the Business tier is handled individually and generally involves direct compliance review.

---

## Meeting the Travel Rule

The Travel Rule obliges financial institutions to pass originator and beneficiary details alongside transfers above a jurisdictional threshold — $3,000 in the United States. Three mechanisms cover it:

1. **Screening.** Before an above-threshold payment settles, the recipient address is checked against sanctions and risk lists via Chainalysis or TRM Labs.
2. **Institution-to-institution exchange.** Where the receiving institution is itself regulated and needs Travel Rule data, that information passes directly between compliance systems — never onto the public chain.
3. **Encrypted figure, disclosed identity.** The amount stays encrypted on-chain throughout. Travel Rule obligations concern identity rather than sums, and the two are treated as separable: compliance data moves through compliance channels, and the ledger never carries a plaintext figure.

---

## What draws a second look

- Payments above your tier's ceiling
- Payments involving an address flagged by sanctions or risk screening
- Patterns resembling structuring — several payments landing just under a reporting threshold

Flagged payments may be held for manual review. If that happens to something you sent, you will be told in-app.

---

## Continue

- [Regulatory Posture](regulatory-posture.md)
- [Proving a Payment](../privacy/proving-a-payment.md)
