# Shopify Technical Docs

This repository is a documentation library for detailed specifications and process flows across Shopify products.

The goal is to collect product-specific architecture notes, integration behavior, state transitions, and Mermaid-based flow diagrams in one place so they can be reused for technical discussions, partner enablement, and implementation planning.

## Documents

| Document | Shopify product | Coverage |
| --- | --- | --- |
| [Shopify Collective Architecture](./products/shopify-collective/architecture.md) | Shopify Collective | Retailer and supplier flows for product import, price and inventory sync, shipping, orders, automatic payments, fulfillment, cancellations, returns, and pricing-related changes. |

## GitHub Pages

The HTML site entry point is [`index.html`](./index.html). Product pages live in product-specific directories, and each HTML page links back to the Markdown source used to build the visualization.

Rendered entry points:

- [English site](./index.html)
- [Shopify Collective English HTML](./products/shopify-collective/index.html)
- [Shopify Collective Japanese HTML](./products/shopify-collective/ja/index.html)
- [Shopify Collective English PPTX](./products/shopify-collective/shopify-collective-architecture.pptx)
- [Shopify Collective Japanese PPTX](./products/shopify-collective/ja/shopify-collective-architecture-ja.pptx)

## Disclaimer

This repository is not official Shopify documentation. The maintainers do not accept responsibility for the accuracy, completeness, or consequences of using this content. Use it at your own discretion as supplemental material for understanding Shopify concepts and workflows. Content may change without notice.
