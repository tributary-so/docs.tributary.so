# Payment Policy

Direct pull payments — the protocol's original, non-programmable policy family.

## Overview

A PaymentPolicy is a non-custodial recurring payment where the gateway pulls tokens **directly** from the user's token account to the recipient. No intermediate accounts, no swaps, no validation hooks — a single `transfer` plus fee split. This page orients the reader to the five PaymentPolicy variants (Subscription, Milestone, Pay-as-you-go, OneTime, UpTo), the shared `PolicyType` envelope, and the referral program, before drilling into each variant's dedicated page.

## Variants at a Glance

| Variant                                                                                           | Amount           | Fires         | Recipient trigger | Best For                     |
| ------------------------------------------------------------------------------------------------- | ---------------- | ------------- | ----------------- | ---------------------------- |
| [Subscription](https://docs.tributary.so/protocol-reference/payment-policy/subscription/index.md) | Fixed per period | Recurring     | No                | Recurring services, SaaS     |
| [Milestone](https://docs.tributary.so/protocol-reference/payment-policy/milestone/index.md)       | Per-phase        | Up to 4×      | Per release_cond. | Project deliverables, escrow |
| [Pay-as-you-go](https://docs.tributary.so/protocol-reference/payment-policy/payasyougo/index.md)  | Variable/claim   | Many (capped) | Yes               | Usage billing (AI/LLM, API)  |
| [OneTime](https://docs.tributary.so/protocol-reference/payment-policy/onetime/index.md)           | Fixed            | Exactly once  | No                | Invoices, one-shot payouts   |
| [UpTo](https://docs.tributary.so/protocol-reference/payment-policy/upto/index.md)                 | ≤ max (caller)   | Exactly once  | Yes               | Usage-based one-shot (x402)  |

All five variants share the same 128-byte fixed layout (ADR-0002), the same `PaymentPolicy` envelope (PDA, lifecycle, fees, referrals, composable hooks), and the same `UserPayment`-as-delegate model. They differ only in scheduling semantics and amount resolution.
