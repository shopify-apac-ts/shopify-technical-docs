# Shopify Collective Architecture

This document summarizes the main Shopify Collective flows: connection and onboarding, product sharing and synchronization, order routing, automatic payments, fulfillment, and returns.

## 1. End-to-End Flow

The end-to-end architecture starts when both merchants install Shopify Collective and pass recurring eligibility checks. The supplier then shares products through a catalog, the retailer imports those products, Collective keeps product data synchronized, and customer orders are routed to the supplier for fulfillment. Automatic payments move supplier revenue from the retailer's Shopify Payments balance to the supplier's Shopify Payments balance while the retailer keeps the commission.

```mermaid
flowchart TD
    subgraph ONB["1. Connection and Onboarding"]
      INS["Both merchants install Collective"] --> ELG{"Eligibility check<br/>Shopify Payments / active plan<br/>supported currency / supported country"}
      ELG -. "Revalidated hourly" .-> ELG
      ELG --> INV["Invitation<br/>Free Flow / Discovery"]
      INV --> BCA["BrandCuratorAssignment<br/>status: pending -> approved<br/>commission % / payments_enabled"]
    end
    BCA --> CAT["2. Supplier creates catalog<br/>open / closed access"]
    CAT --> IMP["Retailer imports products<br/>ProductImport"]
    IMP --> SYNC["3. Product and image synchronization<br/>continuous sync through ProductSet"]
    SYNC --> ORD["4. Customer purchases in retailer store"]
    ORD --> PAY["5. Automatic payment<br/>Retailer balance -> Supplier balance<br/>Retailer keeps commission"]
    ORD --> FUL["Supplier fulfills the order"]
    FUL --> RET["6. Return<br/>retailer opens request -> supplier approves/rejects<br/>label attached -> received and closed -> refunded"]
```

## 2. Order, Fulfillment, and Automatic Payment Flow

When a customer purchases a Collective product from the retailer, Collective receives the order event, creates the supplier-side order and fulfillment order, and creates the payment intent and debit operation. Supplier payout is credited after fulfillment, so payment settlement follows the fulfilled quantity rather than only the original order.

```mermaid
sequenceDiagram
    participant C as Customer
    participant R as Retailer Store
    participant COL as Collective
    participant SUP as Supplier Store
    participant SP as Shopify Payments

    C->>R: Checkout with any gateway
    R-->>COL: Order webhook
    COL->>SUP: Create supplier order / fulfillment order
    COL->>COL: Create OrderPaymentIntent + Debit Operation
    COL->>SP: shopifyPaymentsBalanceDebit<br/>Debit retailer balance
    SUP->>SUP: Fulfill product
    SUP-->>COL: Fulfillment webhook
    COL->>COL: Create Credit Operation for fulfilled items only
    COL->>SP: shopifyPaymentsBalanceCredit<br/>Credit supplier balance
    Note over R,SUP: Example: retail price $100 / supplier cost $60 -> retailer keeps $40 as commission
    Note over COL,SP: Cancellations and refunds are reversed with DebitReverse and CreditReverse operations
```

## 3. Returns State Flow

Returns are initiated by the retailer and reviewed by the supplier. If approved, the supplier attaches return label or tracking details, receives the item, closes the return, and restocks or refunds as needed. The retailer can cancel the return at any time, and the supplier can also cancel after approval.

```mermaid
flowchart LR
    A["Retailer opens return request"] --> B{"Supplier decision"}
    B -->|"Approve"| C["Attach label / tracking details"]
    B -->|"Reject"| X["Return rejected"]
    C --> D["Item received -> close return"]
    D --> E["Restock + refund if needed"]
    A -. "Retailer can cancel at any time" .-> F["Return canceled"]
    C -. "Supplier can also cancel after approval" .-> F
```

## Key Integration Concepts

- **Supplier:** The merchant that owns the source products, shares them through Collective, and fulfills routed orders.
- **Retailer:** The merchant that imports supplier products, sells them on its storefront, and keeps the configured commission.
- **Catalog / price list:** The supplier-controlled product sharing surface that determines which products a retailer can import and sell.
- **Product import and sync:** The retailer-side product record is created from the supplier's shared product data and kept synchronized for product, image, and inventory changes.
- **Automatic payments:** Collective coordinates debit and credit operations through Shopify Payments so the supplier receives the supplier cost and the retailer keeps the margin.
- **Returns:** The retailer initiates the return request, while the supplier decides whether to approve it and handles receiving and closure.

## References

- [About Shopify Collective](https://shopify.dev/docs/apps/build/collective)
- [Share and import products](https://shopify.dev/docs/apps/build/collective/products)
- [Request and accept fulfillment orders](https://shopify.dev/docs/apps/build/collective/orders)
