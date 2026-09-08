# Moving Money

Paying someone on MansaFi has the texture of sending a message rather than filing paperwork. Underneath, each payment is a zero-knowledge proof clearing on Robinhood Chain. From where you sit, it simply works.

---

## Paying

### 1. Pick who

Destinations you can use:

- A `@handle`, which is how most payments go out
- A QR code, scanned in person or from a saved image
- A request link somebody sent you
- A raw EVM address (`0x...`), for advanced cases or wallets outside MansaFi

### 2. Set an amount, optionally a note

The memo field is encrypted and readable only by the two of you. It is never written to the chain in the clear.

### 3. Approve it

Check the figure and the destination, then authorize with your device's biometric prompt — the same passkey from signup. Your device builds the zero-knowledge proof and submits it to Robinhood Chain. Your key, your proof, your hardware.

### 4. That's it

Finality is near-immediate: the payment surfaces in both feeds inside roughly 100 milliseconds. Quicker than a card terminal, and private without being asked. Sending to a raw EVM address still settles on-chain, though confidentiality requires that wallet to support MansaFi's confidential token contracts.

---

## Getting paid

Receiving asks nothing of you. Anything sent to your `@handle`, your address, or a request you generated arrives on its own and appears in your feed.

### Asking for a specific figure

Build a request from **Send/Receive → Request**:

- Attach an amount, or leave it blank and let the payer decide
- Attach a memo explaining what it covers
- Pass along the link or QR code

Request links open in any browser, including for people who have never heard of MansaFi. A new payer is walked through account creation before they pay, so the request doubles as an invitation.

---

## Paying a wallet outside MansaFi

Send USDG to a raw address that is not configured for confidential transfers and MansaFi stops to tell you the payment will clear as an ordinary public ERC-20 transfer instead. That trade-off is always shown before you confirm. Confidentiality is never dropped quietly.

---

## What it costs

MansaFi charges nothing for transfers during beta. You pay only Robinhood Chain gas — typically a fraction of a cent — drawn automatically from your ETH float.

---

## Continue

- [Handles](handles.md)
- [Activity Feed](activity-feed.md)
