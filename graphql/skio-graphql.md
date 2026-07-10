# Skio GraphQL API

Skio is a subscription-management platform for Shopify DTC brands. Its public developer API is **GraphQL-first**, served from a single endpoint, and its data model mirrors Shopify's GraphQL objects — most entities carry a `platformId` field holding the corresponding Shopify GID (e.g. `gid://shopify/SubscriptionContract/12346616394`), which lets you cross-query Shopify.

The API is Hasura-style: read queries accept `where`, `order_by`, `limit`, and `offset` arguments; writes are exposed as purpose-built mutations (`createSubscription`, `cancelSubscription`, `pauseSubscription`, `applyDiscountCode`, etc.).

**Endpoint:** `https://graphql.skio.com/v1/graphql`
**Documentation:** https://code.skio.com/

## Authentication

API token, generated from the Skio dashboard (API section), passed in the request header:

```
Content-Type: application/graphql
authorization: API <token>
```

Access is gated to Skio merchants (a paid Scale or Enterprise plan). A token scopes to a single shop.

## Limits (documented)

- **Depth limit:** maximum 4 nested levels per query
- **Node limit:** maximum 100 nodes per request
- **Rate limit:** 2,000 requests per minute per API token

## Example query

```graphql
query getSubscriptions {
  Subscriptions(
    where: { StorefrontUser: { email: { _eq: "test@test.com" } } }
    order_by: { createdAt: desc }
  ) {
    id
    platformId
    createdAt
    StorefrontUser {
      email
      platformId
    }
    SubscriptionLines(where: { removedAt: { _is_null: true } }) {
      priceWithoutDiscount
      ProductVariant {
        title
        Product { title }
      }
    }
  }
}
```

## Example mutation

```graphql
mutation cancelSubscription($input: CancelSubscriptionInput!) {
  cancelSubscription(input: $input) {
    ok
  }
}
```

## Notes on this schema

- Schema: [skio-schema.graphql](skio-schema.graphql)
- This is an **honestly-modeled** schema (`endpointsModeled: true`). Object/field names, queries, and mutations reflect Skio's documented API reference at https://code.skio.com/, but exhaustive field lists and the full Hasura-generated filter input types are approximated where Skio does not publish a complete SDL.
- Skio also announced a newer **public REST API** (see https://skio.com/changelog/public-rest-api); its endpoint paths and resources are not yet fully documented publicly, so only the GraphQL surface is modeled in detail here.
