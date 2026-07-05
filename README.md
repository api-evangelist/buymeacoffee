# Buy Me a Coffee (buymeacoffee)

Buy Me a Coffee is a creator-support platform that lets fans tip creators ("buy a coffee"), subscribe to recurring memberships, and buy extras from a creator's shop. Its developer API is a **read-only REST interface** (base `https://developers.buymeacoffee.com/api/v1`) that gives a creator programmatic access to their own account data: one-time supporters, memberships/subscriptions, and Extras purchases.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/buymeacoffee/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/buymeacoffee/refs/heads/main/apis.yml)

## Access Model & Authentication

- **Public and self-serve.** Any Buy Me a Coffee account holder can create a personal access token in the **Developer Dashboard** (log in with your regular Buy Me a Coffee account, then **Create New Token**; a read-only option is available). There is no partner/approval gate.
- **Bearer token.** Add `Authorization: Bearer <token>` to every request.
- **Read-only.** The documented API is GET-only and scoped to the creator's own account data.
- **Note on documentation.** The full API reference sits behind the Developer Dashboard login, and Buy Me a Coffee does not publish a machine-readable OpenAPI document publicly. The collection endpoints and query params here (`/supporters`, `/subscriptions` with `status`, `/extras`, all paginated) are confirmed from the developer docs, community wrappers, and the Microsoft Power Platform connector. The single-resource **by-ID** paths (`/supporters/{id}`, `/subscriptions/{id}`, `/extras/{id}`) are honestly **modeled** from the documented "get by ID" operations — the exact URL templates are inferred, not quoted verbatim.

## Tags

- Creator Economy
- Memberships
- Subscriptions
- Tips
- Payments
- Donations

## Timestamps

- **Created:** 2026-07-05
- **Modified:** 2026-07-05

## APIs

### Buy Me a Coffee Supporters API

Read-only access to a creator's one-time supporters (tips / "coffees") and the messages they leave. List all supporters with pagination, or retrieve a single supporter by its unique ID.

- **Base URL:** `https://developers.buymeacoffee.com/api/v1`
- `GET /supporters` — list one-time supporters (paginated)
- `GET /supporters/{id}` — get a supporter by ID *(modeled)*

### Buy Me a Coffee Subscriptions API

Read-only access to a creator's recurring memberships / subscriptions. List members filtered by status (`all`, `active`, `inactive`) with pagination, or retrieve a single member's subscription details by ID.

- **Base URL:** `https://developers.buymeacoffee.com/api/v1`
- `GET /subscriptions?status=active` — list members / subscriptions (paginated)
- `GET /subscriptions/{id}` — get a member by ID *(modeled)*

### Buy Me a Coffee Extras API (BETA)

Read-only access to a creator's Extras purchases — the shop items and rewards fans buy. List all extra purchases with pagination, or retrieve a single extra purchase by its unique Purchase ID.

- **Base URL:** `https://developers.buymeacoffee.com/api/v1`
- `GET /extras` — list Extras purchases (paginated)
- `GET /extras/{id}` — get an Extras purchase by ID *(modeled)*

### Buy Me a Coffee Webhooks

Server-push HTTP webhooks configured in the dashboard (**Integrations → New webhook**). Buy Me a Coffee POSTs a JSON event envelope to your subscriber URL for donation, membership / recurring-donation, extra purchase, commission, and wishlist events. Each request is signed with an **HMAC-SHA256** signature in the `x-signature-sha256` header. This is server-to-endpoint HTTP, **not** a WebSocket.

Event types include: `donation.created`, `donation.refunded`, `membership.started`, `membership.updated`, `membership.cancelled`, `membership.paused`, `recurring_donation.started`, `recurring_donation.updated`, `recurring_donation.cancelled`, `extra_purchase.created`, `extra_purchase.updated`, `extra_purchase.refunded`, `commission_order.created`, `commission_order.refunded`, `wishlist_payment.created`, `wishlist_payment.refunded`.

## Pricing

No monthly fee. Buy Me a Coffee retains a **flat 5% platform fee** per transaction (tips, memberships, and shop sales); creators keep 95% before payment processing. Standard Stripe processing (~2.9% + $0.30 per transaction, plus a small payout fee) is charged separately. The developer API is free to use. See [`plans/buymeacoffee-plans-pricing.yml`](plans/buymeacoffee-plans-pricing.yml).

## WebSocket Review

Buy Me a Coffee does **not** expose a documented public WebSocket API. Its own API is request/response REST, and its only server-push mechanism is outbound HTTP webhooks. See [`review.yml`](review.yml).

## Common Properties

- [LinkedIn](https://www.linkedin.com/company/buymeacoffee)
- [Website](https://www.buymeacoffee.com)
- [Documentation](https://developers.buymeacoffee.com/)
- [Plans](plans/buymeacoffee-plans-pricing.yml)
- [Rate Limits](rate-limits/buymeacoffee-rate-limits.yml)
- [Fin Ops](finops/buymeacoffee-finops.yml)

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
