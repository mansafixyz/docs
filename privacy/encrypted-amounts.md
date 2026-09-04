# Encrypted Amounts

One distinction carries the entire design: MansaFi is confidential, not anonymous. Addresses sit in the open on Robinhood Chain. Figures do not. The network can check your payments; nobody can read them.

Here is how that is actually accomplished.

---

## The primitive

MansaFi ships its own confidential token contracts — an encrypted-balance ERC-20 descended from the Zether line of work. Nothing in the EVM provides a confidential transfer natively, so this layer had to be written and deployed rather than imported. Two techniques carry the weight:

- **ElGamal encryption** stores balances and transfer amounts as ciphertext with homomorphic structure, which lets the contract add and subtract values it cannot read.
- **Zero-knowledge range proofs**, validated by an on-chain verifier, establish that a transfer is well-formed — funds available, quantity non-negative — while disclosing nothing about the quantity itself.

Put together, the chain confirms a payment is legitimate and updates two encrypted balances correctly, having learned nothing about the number in question.

---

## An ordinary ERC-20 transfer

```
Sender Address [PUBLIC] → Amount [PUBLIC] → Receiver Address [PUBLIC]
```

Anyone holding an RPC URL reads every figure you have ever moved, indefinitely. That default is the thing MansaFi was built to retire.

---

## A MansaFi transfer

```
Sender Address [PUBLIC] → Amount [ENCRYPTED] → Receiver Address [PUBLIC]

Proof: zero-knowledge attestation that the ciphertext is a valid transfer,
       carrying no information about its value
```

---

## The sequence

1. You compose a transfer in the MansaFi app.
2. The Privacy Engine on your device constructs a ZK proof using your decryption key. The cleartext figure stays local throughout.
3. Ciphertext and proof go to Robinhood Chain as a call into the confidential token contract, proof supplied as calldata.
4. Inside that same transaction, the verifier contract checks the proof and the token contract rewrites both encrypted balances — ultimately secured by Ethereum through the rollup's settlement. Addresses stay public; the figure stays opaque and remains so.
5. Sender and recipient, each holding a private decryption key, read the value. Nobody else can.
6. When someone legitimately needs to see one specific payment, you mint a disclosure proof for that payment alone. See [Proving a Payment](proving-a-payment.md).

---

## Why bother

Public ledgers bought verifiability by making everything visible, which serves analysts well and account holders poorly. It means a stranger can watch your salary arrive, your rent leave, and your company's runway shrink, in real time, forever. MansaFi keeps the part worth keeping — the network still validates and permanently records each transfer — and discards the surveillance that came bundled with it. For an economy where software transacts continuously, that was never a viable default.

---

## Cost of the guarantee

Proofs are generated client-side in WASM, in the browser or the mobile app. On current hardware that is a sub-second pause before submission — imperceptible in practice. Devices too constrained for that fall back to a server-assisted path that consumes only client-derived proof inputs; the plaintext figure is never transmitted under any configuration.

---

## Continue

- [Proving a Payment](proving-a-payment.md)
- [Keys & Recovery](keys-and-recovery.md)
