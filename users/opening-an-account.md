# Opening an Account

Setting up takes a few minutes and assumes nothing. No phrase to transcribe, no hardware wallet to buy, no prior exposure to crypto. Self-custody, arranged so that ordinary people can actually use it.

---

## Before you start

- A device that supports passkeys: Face ID, Touch ID, Windows Hello, or a hardware security key
- An email address
- Government-issued identification

---

## The flow

### 1. Register

Give an email address and create a passkey on the device in front of you. That passkey is the root your MansaFi keypair is derived from — cryptographic self-custody with nothing to write down and nothing to memorize.

### 2. Clear identity checks

Verification is required when the account opens, consistent with the GENIUS Act framework MansaFi operates under. Private from the public; accountable where the law demands it. Through our verification provider you will supply:

- A photograph of your government ID
- A liveness capture — a brief selfie video

Basic verification releases standard limits. Enhanced verification takes additional documentation and raises those ceilings for Personal and Business accounts alike.

### 3. Take a handle

Pick a `@handle`. It is how the network addresses you, and it spares anyone from ever typing your raw EVM address. See [Handles](handles.md).

### 4. Put money in

Send USDG from an exchange or another wallet, or use a linked bank transfer where your jurisdiction supports it. A small ETH float is maintained automatically for gas, so holding or thinking about ETH is never your problem.

---

## What signup writes to the chain

Those few minutes provision real infrastructure:

- A Robinhood Chain smart account address derived from your passkey
- A confidential token account for USDG inside MansaFi's contracts, which is the piece that makes encrypted transfers possible
- An off-chain profile row tying your `@handle` to your public key, used for lookup and display only

At this point no balance or transaction data exists. Your very first transfer is encrypted like every one after it — privacy is not a setting switched on later.

---

## Which type you get

New registrations default to Personal. Companies should select Business during signup for shared access and higher ceilings. [Choosing an Account](../overview/choosing-an-account.md) compares all three, Agent included.

---

## Continue

- [Moving Money](moving-money.md)
- [Handles](handles.md)
