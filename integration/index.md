# Integration Options

Tributary offers multiple ways to integrate automated payments. Choose the method that fits your use case.

## Integration Methods

### 1. Payments SDK 🛒

*Best for: Quick checkout links with zero API keys*

- Use `@tributary-so/payments` for Stripe-compatible checkout
- Generate shareable payment URLs
- Track subscription and one-time payment status
- Zero configuration required

```typescript
import { PaymentsClient } from "@tributary-so/payments";

const stripe = new PaymentsClient(connection, tributary);
const session = await stripe.checkout.sessions.create({
  mode: "subscription",
  line_items: [{ description: "Pro Plan", unitPrice: 10, quantity: 1 }],
  paymentFrequency: "monthly",
  tributaryConfig: { gateway, recipient, trackingId },
});
```

👉 **Get Started:** [Checkout Quickstart](https://docs.tributary.so/quickstart/checkout/index.md)

______________________________________________________________________

### 2. Direct SDK Integration 💻

*Best for: Full programmatic control and custom flows*

- Use `@tributary-so/sdk` for complete protocol interaction
- Build custom payment UI and logic
- Full control over transaction construction
- Support for all payment types (subscriptions, milestones, pay-as-you-go)

```typescript
import { Tributary } from "@tributary-so/sdk";

const tributary = new Tributary(connection, wallet);
const instructions = await tributary.createSubscriptionInstruction(/*...*/);
```

👉 **Get Started:** [SDK Quickstart](https://docs.tributary.so/quickstart/integration/index.md) | [SDK Reference](https://docs.tributary.so/sdks/index.md)

______________________________________________________________________

### 3. React Button 🚀

*Best for: Fast integration in React applications*

- Use `@tributary-so/sdk-react` for pre-built components
- Drop-in subscription buttons with minimal code
- Built-in wallet integration and error handling
- Ideal for web apps and dashboards

```tsx
import { SubscriptionButton } from "@tributary-so/sdk-react";

<SubscriptionButton
  amount={new BN(10000000)}
  recipient={recipient}
  interval={PaymentInterval.Monthly}
  label="Subscribe $10/month"
/>;
```

👉 **Get Started:** [Button Quickstart](https://docs.tributary.so/quickstart/button/index.md)

______________________________________________________________________

### 4. REST API 📡

*Best for: Backend integration and real-time notifications*

- Query subscription status and payment events
- WebSocket notifications for payment events
- Webhook management for external notifications
- No SDK required - pure HTTP

```bash
# Get subscription status
curl "https://api.tributary.so/v1/subscriptions?trackingId=my-sub"

# WebSocket for real-time updates
socket.emit("subscribe", { trackingId: "my-sub" });
```

👉 **Get Started:** [API Overview](https://docs.tributary.so/api/overview/index.md)

______________________________________________________________________

### 5. x402 HTTP Payments 🌐

*Best for: API monetization and micropayments*

- Express.js middleware for HTTP 402 payments
- Subscription or pay-as-you-go billing
- JWT-based authenticated access
- Standards-compliant HTTP payment protocol

```typescript
import { createX402Middleware } from "@tributary-so/x402";

app.use(
  "/api/premium",
  createX402Middleware({
    scheme: "deferred",
    amount: 100,
    recipient: process.env.RECIPIENT!,
  })
);
```

👉 **Get Started:** [x402 Overview](https://docs.tributary.so/x402/index.md)

______________________________________________________________________

## Choosing the Right Integration

| Use Case                 | Method               |
| ------------------------ | -------------------- |
| Share payment links      | Payments SDK         |
| AI agent monetization    | Payments SDK         |
| Custom payment UI        | Direct SDK           |
| Complex payment logic    | Direct SDK           |
| React web app            | React Button         |
| Backend-only integration | REST API             |
| API monetization         | x402                 |
| Real-time notifications  | REST API + WebSocket |

## SDK Packages

| Package                   | Purpose                    |
| ------------------------- | -------------------------- |
| `@tributary-so/sdk`       | Core protocol interaction  |
| `@tributary-so/payments`  | Stripe-compatible checkout |
| `@tributary-so/sdk-react` | React components           |
| `@tributary-so/x402`      | HTTP 402 middleware        |
| `@tributary-so/cli`       | Command-line tools         |

## Next Steps

1. **Learn the Protocol:** [What is Tributary?](https://docs.tributary.so/what/index.md)
1. **Choose Your Integration:** Review quickstart guides above
1. **Explore Payment Types:** [Subscriptions](https://docs.tributary.so/subscription-payments/index.md), [Milestones](https://docs.tributary.so/milestone-payments/index.md), [Pay-as-you-go](https://docs.tributary.so/pay-as-you-go/index.md)
1. **Build:** Check [use cases](https://docs.tributary.so/use-cases/index.md) for inspiration

## Need Help?

- 📖 [SDK Reference](https://docs.tributary.so/sdks/index.md)
- 📖 [API Reference](https://docs.tributary.so/api/overview/index.md)
- ❓ [FAQ](https://docs.tributary.so/faq/index.md)
- 💬 [Discord](https://discord.gg/tributary)
