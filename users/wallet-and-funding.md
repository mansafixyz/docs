# Wallet & Funding

The Wallet screen is the short answer to three questions: what you hold, where it is linked, and how it gets in and out.

---

## Spendable balance

The figure at the top is what your primary account can spend right now in USDG. Directly beneath it sits the Robinhood Chain address your account is linked to. With nothing linked yet you will instead see a prompt to add one from [Settings](settings.md), which external payouts require.

---

## Adding funds

**Top up** puts USDG into your primary account:

1. Take a preset — $10, $25, $50, $100 — or type your own figure
2. Continue to receive a single-use Robinhood Chain deposit address
3. Send USDG there from any EVM wallet or exchange; bridged USDC works too and generally fills in around two seconds
4. Press **Transferred** once it is on its way

MansaFi watches the chain for the deposit, which usually resolves within seconds. Your balance updates and the panel closes itself. Nothing to refresh, nothing to sit and wonder about.

---

## The numbers alongside

| Figure | Meaning |
|---|---|
| Spent this month | Settled outbound volume since the 1st of the current month |
| Total topped up | Everything this account has received from outside MansaFi |
| Avg settlement time | Mean time to finality across your settled payments |

---

## Recent activity

Wallet lists the latest payments on the primary account with counterparty, memo, and time. Incoming carries a down arrow, outgoing an up arrow. For the complete picture across every account, with filters and receipts, go to the [Activity Feed](activity-feed.md).

No network fee is levied by MansaFi on a transfer. What you send is what lands, down to the cent.

---

## Continue

- [Settings](settings.md)
- [Insights](insights.md)
