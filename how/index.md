# Basics

Tributary is a protocol for automated recurring payments on Solana. You approve once, payments execute on schedule, your funds never leave your wallet.

______________________________________________________________________

## Pick Your Path

What do you want to do?

**I want to accept payments on my site** → [React Button](https://docs.tributary.so/react-button/index.md) for a drop-in component, or [Checkout Links](https://docs.tributary.so/checkout/index.md) for no-code hosted payment pages.

**I want full control over the payment flow** → [Integration Options](https://docs.tributary.so/integration/index.md) to compare approaches, then [SDK Reference](https://docs.tributary.so/sdk/index.md) for the complete TypeScript API.

**I want to bill for API usage** → [x402 Payments](https://docs.tributary.so/x402/index.md) — HTTP 402 middleware that gates access behind pay-as-you-go or subscription payments.

**I want to monitor and verify payments server-side** → [Payment Tokens (JWT)](https://docs.tributary.so/jwt-auth/index.md) to verify active subscriptions, [REST API](https://docs.tributary.so/api/rest-api/index.md) to query payment data, or [WebSocket API](https://docs.tributary.so/api/websocket/index.md) for real-time notifications.

**I want to build a payment service on top of Tributary** → [Providers](https://docs.tributary.so/providers/index.md) for the gateway model, [Architecture](https://docs.tributary.so/architecture/index.md) for the full technical picture.

**I want to use the CLI** → [CLI Tools](https://docs.tributary.so/tools/index.md) for protocol management from the command line.

______________________________________________________________________

## Quick Start

The fastest path to a working payment:

```bash
pnpm install @tributary-so/payments @tributary-so/sdk @solana/web3.js
```

```typescript
import { PaymentsClient } from "@tributary-so/payments";
import { Connection } from "@solana/web3.js";
import { Tributary } from "@tributary-so/sdk";

const connection = new Connection("https://api.mainnet-beta.solana.com");
const tributary = new Tributary(connection, wallet);
const payments = new PaymentsClient(connection, tributary);

const session = await payments.checkout.sessions.create({
  mode: "subscription",
  line_items: [{ description: "Pro Plan", unitPrice: 10, quantity: 1 }],
  paymentFrequency: "monthly",
  tributaryConfig: {
    gateway: "CwNybLVQ3sVmcZ3Q1veS6x99gUZcAF2duNDe3qbcEMGr",
    recipient: "YOUR_WALLET",
    trackingId: "user-pro-plan",
  },
});

console.log(session.url); // Share this link with your customer
```

Verify the subscription is active:

```typescript
const status = await payments.subscriptions.checkStatus({
  trackingId: "user-pro-plan",
  userPublicKey: "USER_WALLET",
});

if (status.status === "active") {
  // Grant access
}
```

Full details in [Checkout Links](https://docs.tributary.so/checkout/index.md) and [Payment Tokens](https://docs.tributary.so/jwt-auth/index.md).

______________________________________________________________________

## Reference

|                     |                                                |
| ------------------- | ---------------------------------------------- |
| **Program ID**      | `TRibg8W8zmPHQqWtyAD1RxBRXEdyU13Mu6qX1Sg42tJ`  |
| **USDC Mint**       | `EPjFWdd5AufqSSqeM2qN1xzybapC8G4wEGGkZwyTDt1v` |
| **Default Gateway** | `CwNybLVQ3sVmcZ3Q1veS6x99gUZcAF2duNDe3qbcEMGr` |

| Network       | URL                                   |
| ------------- | ------------------------------------- |
| Mainnet RPC   | `https://api.mainnet-beta.solana.com` |
| Devnet RPC    | `https://api.devnet.solana.com`       |
| Tributary API | `https://api.tributary.so`            |
| Checkout      | `https://checkout.tributary.so`       |

______________________________________________________________________

## Payment Types

| Type          | Best For                   | Docs                                                                              |
| ------------- | -------------------------- | --------------------------------------------------------------------------------- |
| Subscription  | Fixed recurring billing    | [Subscription Payments](https://docs.tributary.so/policies/subscription/index.md) |
| Milestone     | Project-based deliverables | [Milestone Payments](https://docs.tributary.so/policies/milestone/index.md)       |
| Pay-as-you-go | Metered / usage-based      | [Pay-as-you-go Payments](https://docs.tributary.so/policies/payasyougo/index.md)  |

______________________________________________________________________

## Full Guide Index

| Page                                                                  | What You'll Find                                |
| --------------------------------------------------------------------- | ----------------------------------------------- |
| [Integration Options](https://docs.tributary.so/integration/index.md) | Compare all integration methods                 |
| [SDK Reference](https://docs.tributary.so/sdk/index.md)               | TypeScript, React, Payments, x402, CLI packages |
| [React Button](https://docs.tributary.so/react-button/index.md)       | Drop-in `<SubscriptionButton>` component        |
| [Checkout Links](https://docs.tributary.so/checkout/index.md)         | Hosted payment pages, no frontend required      |
| [Payment Tokens](https://docs.tributary.so/jwt-auth/index.md)         | Server-side JWT verification                    |
| [x402 Payments](https://docs.tributary.so/x402/index.md)              | HTTP 402 middleware for API monetization        |
| [REST API](https://docs.tributary.so/api/rest-api/index.md)           | Query subscriptions, events, webhooks           |
| [WebSocket API](https://docs.tributary.so/api/websocket/index.md)     | Real-time payment notifications                 |
| [Architecture](https://docs.tributary.so/architecture/index.md)       | Protocol design and account structure           |
| [Smart Contract](https://docs.tributary.so/smart-contract/index.md)   | On-chain program details                        |
| [Fees](https://docs.tributary.so/fees/index.md)                       | Protocol and gateway fee breakdown              |
| [Security](https://docs.tributary.so/security/index.md)               | Non-custodial model and audit status            |
| [Providers](https://docs.tributary.so/providers/index.md)             | Build a payment gateway                         |
| [Use Cases](https://docs.tributary.so/use-cases/index.md)             | Business applications and examples              |
| [FAQ](https://docs.tributary.so/faq/index.md)                         | Common questions                                |
