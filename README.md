# MansaFi

**Confidential money for people and the software that works for them. Self-custodied, settled on Robinhood Chain, with amounts that stay between the two parties involved.**

---

Two models dominate how value moves today, and neither one is comfortable. A bank keeps your ledger secret from the world and wide open to itself, its processors, and whoever it sells the pattern to. A public blockchain does the reverse: perfect auditability, zero discretion, your payroll legible to any stranger with an RPC endpoint.

MansaFi refuses the choice. Payments land on Robinhood Chain where the network can confirm they happened, while the figures involved stay encrypted end to end. Counterparties are legible. Sums are not. And the key that unlocks your own numbers never leaves the device in your hand.

The same account holds a freelancer collecting USDG on a Tuesday afternoon and a research agent paying eleven cents for an inference call at 4am. Software gets a real wallet here, bounded by limits its owner writes, reporting into the same activity feed as everything else.

---

## The chain underneath

MansaFi deploys its own confidential token contracts to Robinhood Chain, the AI-native Ethereum Layer 2 Robinhood operates. Those contracts hold balances as ciphertext and accept transfers accompanied by zero-knowledge proofs, leaving the participating addresses in plain view. With 100ms blocks and rollup economics beneath it, the combination clears a bar no previous chain quite reached: private, instant, self-custodied payments that a normal person can afford to make.

Balances are denominated in USDG, Paxos' Global Dollar issued natively on the chain, with bridged USDC accepted alongside it. A sliver of ETH is kept topped up in the background to pay gas, which is the last you will hear about gas.
