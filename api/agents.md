# Agents & Spend Policies

Creating agent accounts and managing their policies from code. A handful of calls gives an agent its own wallet with enforceable limits around it. [Policy Engine](../agents/policy-engine.md) covers the concepts.

---

## Create an agent

```
POST /v1/accounts/me/agents
```

### Body

```json
{
  "name": "research-bot",
  "spend_policy": {
    "daily_limit_usdg": 500.00,
    "per_transaction_limit_usdg": 50.00,
    "allowed_recipients": ["api.market", "*.anthropic.com"],
    "assets": ["USDG"],
    "active_hours": "00:00-23:59",
    "hitl_threshold_usdg": 25.00
  }
}
```

### Response

```json
{
  "account_id": "acct_9d3a2f",
  "handle": "@yourname/research-bot",
  "public_key": "9d3a2fXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX",
  "status": "active",
  "spend_policy_id": "policy_4471"
}
```

---

## Amend a policy

```
PATCH /v1/agents/{account_id}/spend-policy
```

Partial updates are accepted: the fields you send change, everything else stands.

```json
{
  "per_transaction_limit_usdg": 75.00,
  "hitl_threshold_usdg": 40.00
}
```

Changes bind anything the agent tries to sign after the call and leave settled payments alone. Tighten or loosen in flight, without stopping the agent.

---

## Read a policy

```
GET /v1/agents/{account_id}/spend-policy
```

### Response

```json
{
  "policy_id": "policy_4471",
  "daily_limit_usdg": 500.00,
  "per_transaction_limit_usdg": 75.00,
  "allowed_recipients": ["api.market", "*.anthropic.com"],
  "assets": ["USDG"],
  "active_hours": "00:00-23:59",
  "hitl_threshold_usdg": 40.00,
  "updated_at": "2026-07-02T10:11:00Z"
}
```

---

## Decide a held payment

Anything above `hitl_threshold_usdg` waits rather than signing itself. You remain the final word on every payment that matters.

```
POST /v1/agents/transactions/{transaction_id}/approve
POST /v1/agents/transactions/{transaction_id}/reject
```

Both return the updated state. An approval signs and submits immediately; a rejection discards the request and moves nothing.

---

## List what's waiting

```
GET /v1/agents/transactions/pending
```

### Response

```json
{
  "pending": [
    {
      "transaction_id": "tx_5c1e2a",
      "agent": "@yourname/research-bot",
      "to": "compute-provider.io",
      "requested_at": "2026-07-02T14:00:00Z",
      "expires_at": "2026-07-03T14:00:00Z"
    }
  ]
}
```

Figures are absent here for the same reason they are absent everywhere else in the API: they are encrypted, and only client-side decryption with your key reveals them. The dashboard decrypts locally when you open a pending approval.

---

## Errors

| Status | Code | Meaning |
|---|---|---|
| `400` | `invalid_policy` | A policy field failed validation — a negative limit, for instance |
| `403` | `not_agent_owner` | The authenticated account does not own that agent |
| `404` | `transaction_not_found` | No pending transaction under that ID |
| `409` | `transaction_expired` | The approval window has already closed |
