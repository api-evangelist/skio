# Skio (skio)

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Skio is a subscription-management platform for Shopify DTC brands (acquired by Recharge in 2026), powering recurring orders, passwordless subscriber portals, and one-click Shop Pay checkout. Its public developer API is **GraphQL-first**, served from a single endpoint at `https://graphql.skio.com/v1/graphql` and documented at [code.skio.com](https://code.skio.com/). Skio's data model mirrors Shopify's GraphQL objects — most entities carry a `platformId` field holding the corresponding Shopify GID (e.g. `gid://shopify/SubscriptionContract/12346616394`), which lets you cross-query Shopify.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/skio/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/skio/refs/heads/main/apis.yml)

## Access Model

Access is **gated to paying Skio merchants**. API tokens are generated from the Skio dashboard (API section) and scope to a single shop; they are passed as `authorization: API <token>`. Because Skio does not publish a complete GraphQL SDL, the schema in this repo is **honestly modeled** (`endpointsModeled`) from Skio's documented queries, mutations, and examples at [code.skio.com](https://code.skio.com/). Skio has also announced a newer **public REST API** ([changelog](https://skio.com/changelog/public-rest-api)); its endpoint paths are not yet fully documented publicly, so only the GraphQL surface is modeled in detail here.

Documented API limits: max query depth of 4 nested levels, max 100 nodes per request, and 2,000 requests per minute per API token.

## Tags

- Subscriptions
- Shopify
- Ecommerce
- DTC
- Recurring Billing
- GraphQL

## Timestamps

- **Created:** 2026-07-10
- **Modified:** 2026-07-10

## APIs

### Skio Subscriptions API

Query and manage recurring subscriptions — list and fetch subscriptions and their lines, then create, cancel, pause, unpause, reactivate, skip, ship now, swap product variants, edit interval, apply discount codes, and update the next billing date. Mirrors Shopify's `SubscriptionContract` via `platformId`.

- **Human URL:** [https://code.skio.com/](https://code.skio.com/)
- **Base URL:** `https://graphql.skio.com/v1/graphql`

#### Tags

- Subscriptions
- Recurring Billing
- GraphQL

#### Properties

- [Documentation](https://code.skio.com/)
- [API Reference](https://code.skio.com/)
- [GraphQL Schema](graphql/skio-schema.graphql)
- [GraphQL Overview](graphql/skio-graphql.md)

### Skio Subscribers API

Look up storefront users (subscribers) and their addresses and payment methods, filter by email, and generate passwordless magic links and quick-action tokens for self-service subscriber portals. `StorefrontUser` mirrors Shopify's `Customer` object.

- **Human URL:** [https://code.skio.com/](https://code.skio.com/)
- **Base URL:** `https://graphql.skio.com/v1/graphql`

#### Tags

- Subscribers
- Customers
- GraphQL

#### Properties

- [Documentation](https://code.skio.com/)
- [API Reference](https://code.skio.com/)
- [GraphQL Schema](graphql/skio-schema.graphql)

### Skio Orders API

List and fetch orders generated by subscriptions and their line items, filter by subscriber or creation time, and read aggregated daily revenue metrics. `Order` and `OrderLineItem` mirror Shopify's `Order` objects via `platformId`.

- **Human URL:** [https://code.skio.com/](https://code.skio.com/)
- **Base URL:** `https://graphql.skio.com/v1/graphql`

#### Tags

- Orders
- Ecommerce
- GraphQL

#### Properties

- [Documentation](https://code.skio.com/)
- [API Reference](https://code.skio.com/)
- [GraphQL Schema](graphql/skio-schema.graphql)

### Skio Products & Selling Plans API

Read products and product variants, manage pricing policies and billing and delivery policies, and add or remove product variants from selling plan groups that define which products can be sold as subscriptions.

- **Human URL:** [https://code.skio.com/](https://code.skio.com/)
- **Base URL:** `https://graphql.skio.com/v1/graphql`

#### Tags

- Products
- Selling Plans
- Catalog
- GraphQL

#### Properties

- [Documentation](https://code.skio.com/)
- [API Reference](https://code.skio.com/)
- [GraphQL Schema](graphql/skio-schema.graphql)

## Common Properties

- [LinkedIn](https://www.linkedin.com/company/skio)
- [Website](https://skio.com)
- [Documentation](https://code.skio.com/)
- [Plans](plans/skio-plans-pricing.yml)
- [Rate Limits](rate-limits/skio-rate-limits.yml)
- [Fin Ops](finops/skio-finops.yml)

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
