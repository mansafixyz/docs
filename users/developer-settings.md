# Developer Settings

The API Keys screen issues credentials and attaches webhook endpoints without anyone hand-rolling a request. It is the dashboard face of the [API Reference](../api/auth-and-keys.md).

---

## Issuing a key

Press **+ New key**, name it — `Production`, say — and pick an environment:

| Environment | Prefix | What it touches |
|---|---|---|
| Live | `hc_live_` | Real USDG, real transfers |
| Test | `hc_test_` | Robinhood Chain testnet; nothing real moves |

The complete key appears exactly once, right after creation. Copy it before the panel closes. Only a hash is retained, so nobody can retrieve it later — us included. Lose it and the answer is to revoke and reissue, which is not an inconvenience so much as the definition of key security working.

---

## Revoking

**Revoke** beside any live key kills it on the spot, permanently: the very next request authenticating with it fails. Revoked keys remain listed and labeled **Revoked**, leaving the audit trail whole.

---

## Attaching a webhook

**+ Add endpoint** under Webhooks asks for:

- The HTTPS URL to deliver to
- The events it should receive: `transfer.settled`, `transfer.failed`, `payment.received`, `policy.limit_reached`

An endpoint hears only the types you check. Register as many as you need for different consumers — a Slack relay here, a billing system there — each with its own selection.

---

## Running endpoints

Any endpoint can be flipped **Active**/**Inactive** or deleted. Deactivating suspends delivery while preserving the configuration, which is what you want while debugging the receiver; deleting removes it for good.

---

## Payload documentation

Key and endpoint management is all this screen covers. Event catalog, payload shapes, and signature checking live in [Event Stream](../agents/event-stream.md) and the [Webhooks API](../api/webhooks.md).

---

## Continue

- [Auth & Keys](../api/auth-and-keys.md)
- [Event Stream](../agents/event-stream.md)
