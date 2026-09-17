# Auth & Keys

The REST API puts accounts, transfers, and agent wallets behind a single bearer token. Every call requires an API key belonging to a MansaFi account.

---

## Minting a key

Keys come from the **Developer** area of your dashboard:

1. Sign in to your MansaFi account
2. Go to **Dashboard → Developer → API Keys**
3. Press **Generate New Key**
4. Name it — `production`, `dev`, `internal-tool`
5. Copy it somewhere safe; it is displayed once

A key is scoped to the account that minted it. Transfers you initiate over the API carry precisely the confidentiality guarantees of transfers made in the app. The privacy layer does not thin out because the caller is code.

---

## Sending it

Put the key in the `Authorization` header on every request:

```
Authorization: Bearer <your_api_key>
```

For example:

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

---

## Two kinds of key

| Prefix | Network | Purpose |
|---|---|---|
| `hc_live_` | Mainnet | Production; produces real on-chain transactions |
| `hc_test_` | Testnet | Development; no real USDG required |

Integrate against test keys. Testnet calls run on the Robinhood Chain testnet (chain ID 46630) and never touch mainnet (chain ID 4663) or real funds.

---

## Managing keys

The dashboard lets you:

- **List** every key with its last-used timestamp
- **Revoke** any key, effective immediately
- **Inspect usage** per key: request count and total USDG moved

---

## Handling them safely

- Keep keys in environment variables or a secrets manager, never in source control.
- Rotate the moment you suspect exposure.
- Use a distinct key per environment.
- Revoke anything you have stopped using.

A live key can move funds out of your account. Treat it as you would a private key.

---

## The limit of what a key can do

No API key will ever decrypt a transaction amount server-side on your behalf. That boundary is structural rather than procedural. An integration that needs a confidential figure must decrypt it on the client with your account's decryption key, exactly as the MansaFi app does.
