# Transfers

Creating and inspecting transfers from code. Anything created here is confidential by default, exactly as it would be from the app — privacy is the baseline, not a flag you must remember.

---

## Create

```
POST /v1/transfers
```

### Body

```json
{
  "to": "string",
  "amount": "string",
  "asset": "USDG",
  "confidential": true,
  "memo": "string"
}
```

| Field | Type | Required | Meaning |
|---|---|---|---|
| `to` | `string` | Yes | Recipient `@handle` or raw 0x address |
| `amount` | `string` | Yes | Decimal string |
| `asset` | `string` | No | `USDG` unless stated |
| `confidential` | `boolean` | No | `true` unless stated. Set `false` only for wallets without confidential token support. |
| `memo` | `string` | No | Encrypted; readable by sender and recipient alone |

### Response

```json
{
  "transfer_id": "tr_7f3a1c2d",
  "status": "confirmed",
  "to": "@vendor",
  "confidential": true,
  "tx_hash": "0x8f3ad41c9be2...7c1a",
  "created_at": "2026-07-02T14:23:09Z"
}
```

The figure is absent from the response even though you just supplied it in the request. That is the confidentiality guarantee applied without exception: the API confirms settlement, and reading the amount back requires client-side decryption like any other confidential read.

---

## Retrieve

```
GET /v1/transfers/{transfer_id}
```

### Response

```json
{
  "transfer_id": "tr_7f3a1c2d",
  "status": "confirmed",
  "from": "@yourname",
  "to": "@vendor",
  "confidential": true,
  "tx_hash": "0x8f3ad41c9be2...7c1a",
  "created_at": "2026-07-02T14:23:09Z",
  "confirmed_at": "2026-07-02T14:23:09Z"
}
```

### Statuses

| Status | Meaning |
|---|---|
| `pending` | Submitted, awaiting confirmation |
| `confirmed` | Settled on-chain |
| `failed` | Never settled. Nothing moved. |

---

## List

```
GET /v1/transfers
```

### Query parameters

| Parameter | Type | Default | Meaning |
|---|---|---|---|
| `limit` | `integer` | `20` | Page size, `100` maximum |
| `offset` | `integer` | `0` | Pagination offset |
| `status` | `string` | (none) | Restrict to one status |
| `from` | `string` | (none) | ISO 8601; transfers after this point |
| `to` | `string` | (none) | ISO 8601; transfers before this point |

---

## Errors

| Status | Code | Meaning |
|---|---|---|
| `400` | `invalid_request` | Malformed body or a missing required field |
| `402` | `insufficient_balance` | The account does not hold enough of the asset |
| `404` | `recipient_not_found` | No account behind that handle |
| `422` | `recipient_not_confidential_ready` | Recipient wallet lacks confidential token support; resend with `"confidential": false` to proceed publicly |

---

## Worked example

```bash
curl -X POST https://api.mansafi.xyz/v1/transfers \
  -H "Authorization: Bearer hc_live_xxxxxxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{
    "to": "@vendor",
    "amount": "125.00",
    "asset": "USDG",
    "confidential": true,
    "memo": "Invoice #4471"
  }'
```
