# Threat Model

MansaFi is built so that custody, validity, and confidentiality never rest on trusting MansaFi the company. The layers are separate, each answers a distinct threat, and the guarantees are written to survive the company itself appearing in the threat model.

---

## Layer by layer

| Layer | Threat | Answer |
|---|---|---|
| Custody | MansaFi compromised or coerced into moving funds | Keys are non-custodial, born and kept on the device. No private key is ever held. |
| Confidentiality | MansaFi or an outsider reads amounts | Proving and decrypting are client-side. The backend sees ciphertext only. |
| Transfer validity | A malformed or overdrawing transfer is submitted | The on-chain verifier checks range and validity proofs before balances change, and because Robinhood Chain settles to Ethereum through the Arbitrum stack's fraud proofs, that check is ultimately Ethereum-secured. |
| Agent overspend | An agent transacts past its authority | Policies live on-chain in the agent's ERC-4337 validation contract; a violating transaction fails validation. Client-side checks stop it earlier, before signing. |
| Key loss | Device and passkey both gone | Multi-device passkey sync, exportable keys, social recovery after beta. See [Keys & Recovery](../privacy/keys-and-recovery.md). |
| Replay or forgery | A signed transaction is reused or faked | Standard EVM signing and account-nonce semantics, identical to any Robinhood Chain transaction. |
| Censorship | The sequencer stalls or refuses a transaction | Robinhood runs a single sequencer in this phase, but the Arbitrum stack's delayed inbox on Ethereum forces inclusion of anything it ignores. |
| Availability | MansaFi's backend goes down | Funds sit in user-owned smart accounts on Robinhood Chain, not MansaFi-controlled contracts. Any EVM wallet can reach them directly with an exported key. |

---

## The two lists

**Within MansaFi's power:**
- Routing requests, rendering the app, indexing chain events into a live feed
- Generating and delivering webhooks
- Evaluating spend policy at the point an agent's client tries to sign
- Running the KYC and disclosure workflows you initiate

**Beyond it:**
- Moving your funds without your signature. It holds no private key of yours.
- Reading your amounts. It holds no decryption key of yours.
- Altering a signed transaction. The chain rejects anything that fails signature checks, and the verifier rejects anything lacking a valid proof.
- Overriding an agent's policy. Limits are enforced on-chain by the validation contract and checked client-side before signing, not reviewed at a backend's discretion.

The second list matters more. Those are properties of cryptography and consensus, not commitments in a policy document.

---

## Proofs stay on the client

Zero-knowledge proof generation for confidential transfers runs on your device in WASM, never on MansaFi's servers. Structural, not promised: your cleartext balance and amounts never exist in a form MansaFi's infrastructure could intercept, willing or not. The sequencer, for its part, orders ciphertext. It never handles a balance or a figure.

---

## Dedicated RPC

MansaFi runs its own RPC infrastructure rather than leaning on public Robinhood Chain endpoints, for reliability under load. That is a performance decision with no bearing on trust. Any transaction MansaFi submits could equally be submitted through any other provider — it is a standard signed Robinhood Chain transaction — and in the limit, forced through Ethereum's delayed inbox. No privileged path exists, and no gatekeeper.

---

## Submission is idempotent

Each submission is pinned to a specific account nonce, so a transaction retried under poor network conditions can only ever be included once. Idempotent submission over standard EVM nonce semantics makes a double-send structurally unavailable.

---

## Risks, and what answers them

| Risk | Answer |
|---|---|
| Device lost with no synced passkey | Export your key in advance and store it safely; social recovery lands after beta |
| Device too slow to prove quickly | Server-assisted proving from client-derived inputs, never plaintext figures |
| Parent account compromised | Policy limits bound the damage even with a hijacked session; revoke the agent's key from the dashboard immediately |
| Regulatory action against the company | Funds sit in user-owned smart accounts, not MansaFi-custodied ones. On-chain access survives whatever happens to the company. |
| Sequencer or network outage | Redundant RPC providers and a status page; forced inclusion through Ethereum's delayed inbox remains open. Availability suffers; funds do not. |
