# System Design

MansaFi is a confidential payment layer for people and the software they run, built on Robinhood Chain with its own confidential token contracts — an encrypted-balance ERC-20 descended from Zether — providing the privacy primitive. The EVM offers no such primitive natively, so that contract layer was written here and verified on-chain. And unlike most fintech, MansaFi keeps no settlement ledger of its own. Robinhood Chain is the ledger, with Ethereum underneath it.

---

## What this layer is responsible for

1. **Custody and signing.** Each account is an ERC-4337 smart account governed by a keypair generated on the client. No keys reach MansaFi.
2. **Confidential transfers.** Amounts are encrypted by the token contracts; proofs are produced on the client.
3. **Gas abstraction.** A small per-account ETH float is maintained automatically, refilled by an internal swap when it dips, so users reason only in USDG. Gas becomes a detail of the implementation.
4. **Agent policy.** Spend policies are checked client-side during the agent's signing flow and enforced on-chain by the agent account's validation contract.
5. **Indexing.** Chain events are indexed off-chain from contract event streams, powering the live feed and the webhook system without anyone polling.

Everything demanding trust — who holds funds, whether a transfer is valid — is settled by Robinhood Chain and MansaFi's on-chain contracts, with correctness ultimately backed by Ethereum through the rollup's fraud-proof settlement. Everything else — rendering, notifications, indexing — is convenience layered above. That separation is the whole design.

---

## The stack

```
+-------------------------------------------------+
|                 Applications                    |
|      Web . Mobile (iOS/Android) . SDK           |
+---------------------+---------------------------+
                      |
+---------------------v---------------------------+
|                  API surface                    |
|   REST + WebSocket . Agent API . Webhooks       |
+---------------------+---------------------------+
                      |
+---------------------v---------------------------+
|                 Core services                   |
|                                                 |
|  Wallet Engine   Privacy Engine   Agent Engine  |
|  (keys,          (ZK proofs,      (policies,    |
|   tx building)    client-side)     x402)        |
|                                                 |
|  Indexer (contract event streams + PostgreSQL)  |
+---------------------+---------------------------+
                      |
+---------------------v---------------------------+
|            Robinhood Chain Mainnet              |
|  Confidential Tokens . ZK Verifier . x402       |
+-------------------------------------------------+
```

---

## Who has to trust whom

- **With funds:** nobody trusts MansaFi. Keys are born and kept on the device; the servers observe signed transactions and never a private key.
- **With figures:** nobody trusts MansaFi. Proving and decrypting happen on the client, and the backend handles ciphertext exclusively.
- **With agents:** limits are enforced at the signing layer and in the account's on-chain validation contract, never at MansaFi's discretion after the fact. A transaction violating policy is not produced in the first place.

---

## Further reading

- [Contracts](contracts.md): the on-chain state layout
- [Threat Model](threat-model.md): layer-by-layer security
