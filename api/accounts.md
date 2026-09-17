# Accounts & Balances

Reading account details and balances for the authenticated account. The privacy architecture holds even at the read layer: the servers cannot see your balances, so decryption stays on your side.

---

## The authenticated account

```
GET /v1/accounts/me
```

### Response

```json
{
  "account_id": "acct_8f2b1c",
  "handle": "@yourname",
  "type": "personal",
  "public_key": "0x8F2b1CxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxA9e",
  "kyc_status": "verified",
  "created_at": "2026-01-14T09:00:00Z"
}
```

| Field | Type | Meaning |
|---|---|---|
| `account_id` | `string` | Internal account identifier |
| `handle` | `string` | The account's `@handle` |
| `type` | `string` | `personal`, `business`, or `agent` |
| `public_key` | `string` | Robinhood Chain address, 0x-prefixed |
| `kyc_status` | `string` | `unverified`, `pending`, `verified`, or `enhanced` |
| `created_at` | `string` | ISO 8601 timestamp |

---

## Balances

```
GET /v1/accounts/me/balances
```

Returns a decrypted balance per asset held. The request must carry a decryption proof built on the client, because the servers have no way to decrypt the balance themselves — a cryptographic property of the system rather than a policy you are asked to trust.

### Request

```json
{
  "decryption_proof": "base64-encoded proof generated client-side"
}
```

### Response

```json
{
  "balances": [
    { "asset": "USDG", "amount": "1245.30" },
    { "asset": "ETH", "amount": "0.0042" }
  ]
}
```

Omit `decryption_proof` and the endpoint reports only whether each asset's balance is non-zero, with no figure attached, since the encrypted value is unreadable to it.

---

## Agent accounts

```
GET /v1/accounts/me/agents
```

Lists every agent namespaced beneath the authenticated account — the whole fleet in one call.

### Response

```json
{
  "agents": [
    {
      "account_id": "acct_9d3a2f",
      "handle": "@yourname/research-bot",
      "public_key": "0x9D3a2FxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxC4b",
      "status": "active",
      "spend_policy_id": "policy_4471"
    }
  ]
}
```

[Agents](agents.md) covers creating agents and working with their policies.

---

## Errors

| Status | Code | Meaning |
|---|---|---|
| `401` | `unauthorized` | Key missing or invalid |
| `403` | `kyc_required` | Required identity verification is incomplete |
| `422` | `decryption_proof_invalid` | Proof does not correspond to the account's balance ciphertext |
