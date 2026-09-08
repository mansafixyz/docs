# Handles

A handle is the readable name — `@yourname` — that stands in for your account. It is how money finds you without anyone reading, retyping, or fumbling a raw EVM address.

---

## Claiming one

Handles are claimed at signup and can be changed afterward from **Settings → Handle**, availability permitting.

- Between 3 and 20 characters
- Letters, digits, and underscores
- Lookup ignores case; the casing you chose is what gets displayed

---

## What happens on send

A handle is an off-chain mapping MansaFi maintains between `@yourname` and your public Robinhood Chain address. Paying one works like this:

1. The app resolves `@yourname` into an address.
2. The transfer is constructed and signed as usual, directed at your actual Robinhood Chain account.
3. The handle itself never reaches the chain. What settles is a plain address-to-address transfer.

So a handle buys convenience and introduces no new party to trust. The payment underneath carries exactly the guarantees described in [Encrypted Amounts](../privacy/encrypted-amounts.md) — readable for humans, cryptographic where it counts.

---

## Agent handles

Agent accounts receive a namespaced handle beneath their parent: `@yourname/agent-name`. When software spends money, knowing that it was software matters, and the namespace makes it obvious in the payer's interface and in your own feed that an autonomous system was involved rather than a person. See [Agent Wallets](../agents/agent-wallets.md).

---

## Changing yours

Change a handle and the old one is released for others after a short hold. Request links built on the previous handle stop resolving at that point. Your Robinhood Chain address is untouched by any of this, so direct address-based history stays valid regardless. The name is mutable; the chain record is not.

---

## Continue

- [Moving Money](moving-money.md)
- [Activity Feed](activity-feed.md)
