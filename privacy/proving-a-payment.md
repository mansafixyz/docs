# Proving a Payment

Keeping a figure private is not the same as being unable to evidence it. MansaFi makes disclosure a scalpel: prove one payment to one party, on your initiative, leaving every other row in your history untouched.

---

## Disclosure proofs

A disclosure proof reveals a single transaction's amount to a recipient you nominate, signed with your account key so they can rely on it not being invented. Scope is yours to set, and it stops exactly where you set it.

Common reasons to issue one:

- Showing a landlord, employer, or supplier that a specific payment cleared
- Answering a tax authority or auditor asking about one transaction
- Meeting a Travel Rule screening obligation with a counterparty institution (see [Identity Verification](../compliance/identity-verification.md))

### Issuing one

1. Open the payment in your feed and choose **Generate disclosure**.
2. Decide what travels with it: the figure alone, or the figure plus its memo.
3. MansaFi produces a proof, signed by your key, attesting to that transaction's contents.
4. Hand the resulting link or export file to whoever asked.

Nothing adjacent is exposed in the process. The proof is bound to the single transaction you picked, and to nothing else in your account.

---

## Full history export

For bookkeeping or filing, your decrypted history exports in one action.

- Found at **Settings → Export → Transaction History**
- Emits CSV or JSON carrying decrypted figures, timestamps, counterparties, and memos
- Ingests cleanly into the usual crypto tax tooling (Koinly, TokenTax, CoinTracker)

The whole operation runs on your device: your key decrypts your records and the file is written locally. The decrypted export never reaches MansaFi's infrastructure, which has no mechanism to receive it.

---

## Things MansaFi will not do

- It will not decrypt your transactions for a third party. Every disclosure originates with you and carries your signature.
- It will not retain a cleartext mirror of your history on its servers.
- It will not forge a valid disclosure proof without your private key — an impossibility of construction rather than a promise of restraint, and therefore one that survives being pressured.

---

## The regulatory fit

This mechanism is precisely what lets MansaFi hold the confidentiality-not-anonymity line described in [Regulatory Posture](../compliance/regulatory-posture.md). Identity is verified when the account opens. Addresses are public. Figures stay sealed until you unseal one, or until lawful process directed at you as the account holder compels it.

---

## Continue

- [Identity Verification](../compliance/identity-verification.md)
- [Keys & Recovery](keys-and-recovery.md)
