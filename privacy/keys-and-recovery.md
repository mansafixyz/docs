# Keys & Recovery

Self-custody here is structural rather than aspirational. Key material is created on your device and stays there. MansaFi's servers hold no copy and see nothing in the clear. Ownership sits where it should.

---

## You hold two keypairs

| Keypair | Job |
|---|---|
| **Signing key** | An ordinary EVM (secp256k1) key controlling your smart account and signing its transactions, identical in kind to any Ethereum wallet's |
| **Decryption key** | Unwraps your confidential token balance so you can read your own figures and history |

Both descend from a single secret generated on your hardware during onboarding, and neither is ever transmitted to MansaFi unencrypted.

---

## Keys from a passkey

Onboarding leans on WebAuthn rather than a phrase you copy onto paper. Self-custody, nothing to misplace in a drawer.

1. You register with an email address and a device passkey — Face ID, Touch ID, Windows Hello, or a hardware key.
2. Your device runs a key derivation function over the passkey to produce your MansaFi keypair, locally.
3. The resulting private material is encrypted into the secure enclave or its platform equivalent.
4. MansaFi observes a public key and signed transactions, and nothing further.

This closes off the most common way self-custody fails in practice — a seed phrase written down and then lost — while surrendering nothing, because the key remains exportable at your discretion.

---

## Taking your key with you

Export is available whenever you want it, at **Settings → Security → Export Key**. The exported key imports into any standard EVM wallet — MetaMask, Rabby, Rainbow — because what governs your MansaFi smart account is a plain Ethereum-style key and Robinhood Chain is fully EVM-compatible. Nothing here is a walled garden.

Securing the exported copy is on you. Whoever holds it holds the account.

---

## If you lose the device

- **Synced passkeys:** registered on a second device, or held by a syncing provider such as iCloud Keychain or Google Password Manager, access is restored the moment you sign in elsewhere.
- **Social recovery (after beta):** nominate trusted contacts who can jointly authorize a recovery.
- **Exported backup:** an export you made and stored safely restores the account on any device.

No recovery route goes around your key material, and that is deliberate. MansaFi cannot reset anything or let you back in, having never held what would be required to do so.

---

## The privacy connection

Your decryption key is also what makes disclosure and export possible without trusting an intermediary. Because you alone hold it, you alone can read your history or evidence a payment's contents to someone else. Control and confidentiality come from the same object sitting in the same enclave. See [Proving a Payment](proving-a-payment.md).
