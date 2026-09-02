# Anatomy of a Transfer

A MansaFi account is two things welded together: a self-custodied Robinhood Chain smart account, and a set of confidential token contracts that treat the number attached to a payment as a secret. Keys stay with you. Finality arrives in well under a second. The figure involved is encrypted before it ever leaves your device.

Who paid whom is never concealed. How much is never revealed.

---

## What happens when you tap send

```
Transfer composed in the app
        ↓
Privacy Engine builds a ZK proof locally, on your hardware
        ↓
Ciphertext + proof submitted to Robinhood Chain
  as a confidential token transfer
        ↓
Verifier contract validates the proof, then rewrites both encrypted balances
        ↓
Both addresses land in the public record.
  The figure is opaque to every observer.
        ↓
Sender and recipient decrypt it with keys only they hold
        ↓
Roughly 100ms later, it is sitting in both activity feeds
```

That proof — asserting the encrypted figure is well-formed, non-negative, and covered by the sender's balance — is assembled entirely on the client. Your cleartext balance and the amounts you move are never handed to a MansaFi server. Not while you type them, not in flight, not in storage.

---

## The public record

Each transfer writes a Robinhood Chain transaction carrying:

- The sending address
- The receiving address
- An ElGamal ciphertext standing in for the amount
- A zero-knowledge proof that the transfer is valid
- Block number and timestamp

Every field of that is queryable by anyone on the block explorer. The world can confirm the payment occurred. The world cannot read the figure. Auditable by everyone, legible to two.

---

## Drawing the line

**Public:** both addresses, the token involved, and the bare fact that a transfer took place.

**Encrypted:** the amount moved and the balances that result from it.

**Outside MansaFi's reach entirely:** your cleartext balance, your cleartext amounts, your decrypted history. The single exception is a disclosure you deliberately generate for a counterparty or regulator.

MansaFi's infrastructure routes calls, paints UI, and watches chain events. It has no key of yours and no readable copy of your balance. This is a property of the architecture, not a clause in a policy document.

---

## Keeping the feed live

A MansaFi indexer follows contract events and feeds the application a current view without anyone polling the chain. State changes — submitted becoming settled — arrive over a WebSocket the moment the block lands.

---

## Continue

- [Choosing an Account](choosing-an-account.md): which account type fits what you're doing
- [Encrypted Amounts](../privacy/encrypted-amounts.md): the cryptography in full
