# Policy Engine

A spend policy is what a parent account writes to govern an agent it controls. It is the thing that makes handing real spending power to software defensible: the agent gets genuine authority, and you give up none of your own.

---

## What a policy can say

| Rule | Effect |
|---|---|
| Daily limit | Ceiling on total USDG across a rolling 24 hours |
| Per-transaction limit | Ceiling on any individual payment |
| Allowed recipients | Allowlist of addresses, handles, or domains (for x402) the agent may pay |
| Asset restrictions | Which assets it may spend — USDG alone by default; bridged USDC and ETH can be added |
| Time windows | The hours or days in which it may transact at all |
| Approval threshold | A figure above which a human must explicitly authorize before execution |

---

## Writing one

Policies are configured from the parent dashboard under **Agents → [agent name] → Spend Policy**, or through the API. See [API: Agents](../api/agents.md).

They can be rewritten whenever you like. Changes bind transactions from that point forward and never reach back into anything already settled.

---

## How enforcement works

This is where MansaFi parts company with conventional spend controls. The check runs before signing, not as an after-the-fact review. The agent's signing flow evaluates the proposed payment against the current policy; failing any test, the transaction is never built and never submitted. There is no scenario where an agent attempts something out of policy and has it quietly rejected downstream. It never gets signed at all.

---

## The approval path

Above the configured threshold, the agent builds the transaction and holds it, then notifies the parent account. The human sees the figure, the payee, and whatever context came with it, then authorizes or declines.

- Authorized: signed and submitted immediately
- Declined: discarded, with nothing submitted and nothing moved
- Ignored: expires after a configurable window, 24 hours by default, and is treated as declined

The threshold is a dial between autonomy and oversight. Set it to zero for an agent whose every payment you want to see; set it high for one you trust to handle routine, low-value work unattended.

---

## A policy in practice

```json
{
  "daily_limit_usdg": 500.00,
  "per_transaction_limit_usdg": 50.00,
  "allowed_recipients": ["api.market", "*.anthropic.com", "@yourname"],
  "assets": ["USDG"],
  "active_hours": "00:00-23:59",
  "hitl_threshold_usdg": 25.00
}
```

Under these rules the agent buys from `api.market` and `anthropic.com` domains at will up to $25 a payment. Beyond $25, or toward any payee off the list, it either waits for a human or is refused outright.

---

## Continue

- [x402](x402.md)
- [Event Stream](event-stream.md)
