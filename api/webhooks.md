# Webhooks

Managing subscriptions from code, so your systems learn about a settlement as it happens. [Event Stream](../agents/event-stream.md) holds the event catalog and payload format.

---

## Subscribe

```
POST /v1/webhooks
```

### Body

```json
{
  "url": "https://yourapp.com/hooks/mansafi",
  "events": ["transfer.confirmed", "agent.transaction.pending_approval"]
}
```

### Response

```json
{
  "webhook_id": "wh_2c9f1a",
  "url": "https://yourapp.com/hooks/mansafi",
  "events": ["transfer.confirmed", "agent.transaction.pending_approval"],
  "secret": "whsec_xxxxxxxxxxxxxxxxxxxx",
  "created_at": "2026-07-02T09:00:00Z"
}
```

The `secret` appears once. It is what verifies the `X-MansaFi-Signature` header on deliveries.

---

## List

```
GET /v1/webhooks
```

---

## Remove

```
DELETE /v1/webhooks/{webhook_id}
```

Effective at once; nothing further is delivered to that subscription.

---

## Verifying a delivery

Deliveries carry `X-MansaFi-Signature`, an HMAC-SHA256 over the raw body keyed by your secret. Checking it takes a few lines:

```python
import hmac
import hashlib

def verify_signature(payload_bytes, signature_header, secret):
    expected = hmac.new(
        secret.encode(),
        payload_bytes,
        hashlib.sha256
    ).hexdigest()
    return hmac.compare_digest(expected, signature_header)
```

Anything failing that check should be dropped before it is processed.

---

## Replay

```
POST /v1/webhooks/{webhook_id}/replay/{event_id}
```

For when your endpoint was briefly down and you would rather pull one specific event back than wait out the retry schedule.

---

## Delivery history

```
GET /v1/webhooks/{webhook_id}/deliveries
```

Recent deliveries for a subscription with response codes and retry counts, so debugging starts from the full record rather than a guess.
