# Settings

Settings holds the levers: your profile, the wallet you are linked to, the ceilings you have set for yourself, and your data.

---

## Profile

- **Handle** is fixed once claimed and cannot be edited. See [Handles](handles.md).
- **Display name** appears on your public profile and changes whenever you want.
- **Email** is whatever you registered with, and is where receipts and alerts are sent.

---

## Linked wallet

Set or replace the Robinhood Chain address MansaFi uses for payouts and on-chain activity. The format is validated before anything is saved, so a malformed address is refused immediately rather than quietly stored and discovered later.

---

## Your own limits

| Control | Effect |
|---|---|
| Daily limit | Stops outbound payments once the day's total reaches it. `0` disables. |
| Monthly limit | A hard ceiling for the calendar month. `0` disables. |
| Require confirmation | Interposes a confirmation step on anything above $0.50. |
| Auto top-up | Refills the primary account when it runs low. |

These bind your own account. Limits on what an *agent* may spend are a different mechanism entirely — see [Policy Engine](../agents/policy-engine.md) — and they are enforced on-chain rather than held as a preference. Worth keeping straight: agent limits are not settings, they are constraints.

---

## Execution preferences

| Control | Effect |
|---|---|
| Stream results | Shows a payment progressing rather than waiting for the end state |
| Save execution history | Keeps run outputs and receipts on the account for later |
| Share anonymised usage data | Optional product telemetry. Content is never included. |

---

## Taking your data out

**Export all data** produces one JSON file carrying accounts, payments, alerts, API keys, and webhooks — your whole footprint, portable. This is wider than the payments-only export described in [Proving a Payment](../privacy/proving-a-payment.md). Use this one for a complete snapshot, and that one when a decrypted payment history is specifically what bookkeeping or a regulator wants.

---

## Closing the account

Requesting deletion signs you out at once and queues the account and its data for permanent erasure inside 30 days. Support can reverse it while that window is open. Once it closes, it is done, and gone means gone.

---

## Continue

- [Wallet & Funding](wallet-and-funding.md)
- [Proving a Payment](../privacy/proving-a-payment.md)
