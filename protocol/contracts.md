# Contracts

MansaFi accounts rest directly on its confidential token contracts, deployed to Robinhood Chain — an encrypted-balance ERC-20 in the Zether lineage. Nothing in the EVM supplies a confidential transfer natively, so this layer is MansaFi's own work, open source and verified on-chain. There is no parallel MansaFi ledger and no private database of record. Understand the token contract and you understand how balances and transfers actually behave.

---

## Account state

Each holder keeps a balance in the confidential token contract for USDG, with bridged USDC supported alongside it. The contract stores encrypted state next to the ordinary public ERC-20 fields.

```solidity
struct ConfidentialAccount {
    bool approved;                       // Whether confidential transfers are enabled
    ElGamalPubkey elGamalPubkey;         // Public key this account's balance encrypts under
    ElGamalCiphertext pendingBalanceLo;  // Encrypted incoming balance, low bits
    ElGamalCiphertext pendingBalanceHi;  // Encrypted incoming balance, high bits
    ElGamalCiphertext availableBalance;  // Encrypted spendable balance
    AeCiphertext decryptableAvailableBalance; // Encrypted for the owner's fast local read
    bool allowConfidentialCredits;
    bool allowNonConfidentialCredits;
    uint64 pendingBalanceCreditCounter;
    uint64 maximumPendingBalanceCreditCounter;
    uint64 expectedPendingBalanceCreditCounter;
    uint64 actualPendingBalanceCreditCounter;
}
```

`availableBalance` and the pending fields are ciphertexts. Only the holder of the matching ElGamal private key — derived from your account key — can open them. To anyone else, MansaFi included, they are noise.

---

## What a transfer carries

A confidential transfer call supplies proof data next to the encrypted figure, all produced on the sender's client and passed as calldata:

```solidity
struct TransferProofData {
    ElGamalCiphertext newSourceCiphertext;        // Sender's updated encrypted balance
    ElGamalCiphertext transferAmountCiphertextLo; // Encrypted amount, low bits
    ElGamalCiphertext transferAmountCiphertextHi; // Encrypted amount, high bits
    Proof equalityProof;   // Ciphertexts are consistent with each other
    Proof validityProof;   // The amount is well-formed
    Proof rangeProof;      // The amount is non-negative and in range
}
```

MansaFi's on-chain verifier — Solidity, with Arbitrum Stylus (Rust/WASM) carrying the verification hot path — checks these inside the same transaction, before either encrypted balance is touched. Since the rollup's fraud-proof settlement anchors Robinhood Chain to Ethereum, whatever the verifier concludes is backed by Ethereum's own security. The proofs disclose nothing but validity.

---

## The off-chain index

A PostgreSQL index, fed from contract event streams, exists purely to make the interface fast and searchable. It holds:

- Address-to-`@handle` mappings
- Transaction metadata already public on-chain: both addresses, timestamp, hash
- Webhook subscriptions and the state of their deliveries

It holds no decrypted balance and no decrypted amount. Anything sensitive lives in exactly two places: encrypted on-chain, and decrypted on your device.

---

## How an agent account differs

On-chain, an agent account is an ERC-4337 smart account holding a confidential token balance under its own signing key. What makes it an agent account is the validation contract: MansaFi's Agent Engine binds it to a parent and writes the spend policy into the account's on-chain validation logic, so a transaction beyond policy fails validation at the chain. Client-side checks reject it earlier still, but the on-chain constraint is what keeps the limit binding if the client is ever compromised. That combination is how autonomous software gets real spending power without unbounded exposure. See [Threat Model](threat-model.md).

---

## Further reading

- [System Design](system-design.md)
- [Threat Model](threat-model.md)
