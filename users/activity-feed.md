# Activity Feed

Your feed narrates your money in sentences rather than hex. Everything you have paid or been paid, scannable in a glance.

---

## How entries read

Each row is written to be read, not parsed:

```
Sent $50.00 to @maria, Confidential
Received $1,200.00 from @acmepayroll, Confidential
Agent payment to api.market, $0.004, via @yourname/research-bot
```

Payments made by agents carry a visual tag, so it is never ambiguous whether a charge came from software or from your own hands, even though both belong to your account. Where machines spend, that clarity is not optional.

---

## Status

| Status | What it means |
|---|---|
| `Confirmed` | On-chain and final |
| `Pending` | Submitted, awaiting a block. Usually resolves inside a second. |
| `Failed` | Never settled. Nothing moved. Retry is one tap. |

---

## Narrowing it down

Filters available on the feed:

- Date range
- Asset (USDG, ETH)
- Direction (sent, received)
- Kind (human, agent, or DeFi once it ships)

---

## Your view versus everyone else's

You read decrypted figures because you hold the decryption key for your own account. Anyone examining the same transactions from outside — a block explorer included — sees two addresses and a ciphertext they have no way to open. Complete for you, silent for them. [Encrypted Amounts](../privacy/encrypted-amounts.md) explains the mechanism.

---

## Getting the records out

For accounting or filing, export the full decrypted history from **Settings → Export → Transaction History**. It runs on your device and decrypts with your key, so the plaintext export is never something MansaFi could observe. Your records leave your hardware only when you send them somewhere. Detail in [Proving a Payment](../privacy/proving-a-payment.md).

---

## Checking the chain yourself

Every entry links out to the Robinhood Chain transaction behind it. Nothing here requires taking our word: confirm independently on the block explorer that the payment occurred between those two addresses, even though the explorer will never be able to show you the figure.
