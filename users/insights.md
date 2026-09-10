# Insights

Insights turns raw payment records into a picture of how money actually moves through your accounts — yours and your agents' alike. Private data, genuine signal.

---

## The range selector

One control governs the entire page: **7d**, **30d**, or **90d**. Change it and every figure and chart recalculates, comparison against the matching earlier period included.

---

## Headline figures

| Figure | How it's derived |
|---|---|
| Total transfers | Payments counted within the range |
| Total volume | Sum of those payments |
| Avg transfer amount | Volume divided by count |
| Settled rate | Proportion that reached `Settled` |

Each carries a delta against the immediately preceding window of equal length, so a 7-day view holds this week against last. Where there is no prior activity to compare, the delta is omitted rather than invented. A blank beats a misleading percentage.

---

## Transfers per day

Payment count per day, as bars, across whatever range is selected. Ninety-day views thin their axis labels to stay readable; hovering a bar gives you its exact count and volume.

---

## Volume by account

Splits volume across every account you control, human and agent together. When the question is whether one particular agent is responsible for a spike in spend, this answers it without leaving the page.

---

## Volume by privacy layer

How much volume settled at each layer: **Confidential** (the default), **Shielded**, and **Public**. [Encrypted Amounts](../privacy/encrypted-amounts.md) covers what each does on-chain.

---

## Activity heatmap

Day of week against hour of day, shaded by activity. Agent behavior is what this exposes best: a bot restricted to certain hours lights up its lane, and a scheduled job that is genuinely running on schedule demonstrates it here.

---

## Scope

Everything on this page derives from your own accounts' payments. It never reaches another user's activity, and it changes nothing about what the chain exposes. A lens over records you already hold — no more than that.

---

## Continue

- [Activity Feed](activity-feed.md)
- [Agent Wallets](../agents/agent-wallets.md)
