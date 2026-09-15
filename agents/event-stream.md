# Event Stream

Every payment touching your account, or any agent beneath it, is pushed out in real time. Dashboards, parent applications, and monitoring systems stay current the moment money moves — nothing to poll, nothing lagging behind.

---

## Subscribing

From **Dashboard → Developer → Webhooks**, or through the API:

1. Supply an HTTPS endpoint that accepts `POST`
2. Choose the event types it should receive
3. MansaFi signs each payload with an HMAC built on a secret shown once at creation

Check the `X-MansaFi-Signature` header against that secret on every request before you trust the body.

---

## The catalog

| Event | Emitted when |
|---|---|
| `transfer.initiated` | A payment has been submitted and awaits confirmation |
| `transfer.confirmed` | A payment settled on-chain |
| `transfer.failed` | A payment did not settle |
| `agent.transaction.pending_approval` | An agent payment crossed its approval threshold |
| `agent.transaction.approved` | A human authorized a queued agent payment |
| `agent.transaction.rejected` | A human declined one |
| `agent.policy.updated` | A spend policy changed on one of your agents |

---

## A payload

```json
{
  "event": "transfer.confirmed",
  "account": "@yourname/research-bot",
  "direction": "sent",
  "counterparty": "api.market",
  "asset": "USDG",
  "confidential": true,
  "tx_hash": "0x8f3ad41c9be2...7c1a",
  "timestamp": "2026-07-02T14:23:09Z"
}
```

Note the absent field. The amount is missing by construction, not by oversight: confidential transfers carry encrypted figures on-chain and MansaFi's backend holds no decryption key of yours, so it cannot report a number it cannot read. Integrations that need the figure decrypt it client-side with their own key — the identical mechanism the app uses to render your feed.

---

## When delivery fails

Any delivery that does not come back `2xx` is retried on exponential backoff for up to 24 hours. Missed events can also be replayed by hand from the webhook log in the dashboard, so a short outage never costs you a record.

---

## Continue

- [Agent Wallets](agent-wallets.md)
- [Webhooks API](../api/webhooks.md)
