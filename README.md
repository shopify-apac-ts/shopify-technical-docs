# Shopify Technical Docs

This repository is a documentation library for detailed specifications and process flows across Shopify products.

The goal is to collect product-specific architecture notes, integration behavior, state transitions, and Mermaid-based flow diagrams in one place so they can be reused for technical discussions, partner enablement, and implementation planning.

## Documents

| Document | Shopify product | Coverage |
| --- | --- | --- |
| [Shopify Collective Architecture](./products/shopify-collective/architecture.md) | Shopify Collective | Retailer and supplier flows for product import, price and inventory sync, shipping, orders, automatic payments, fulfillment, cancellations, returns, and pricing-related changes. |

## GitHub Pages

The HTML site entry point is [`index.html`](./index.html). Product pages live in product-specific directories, and each HTML page links back to the Markdown source used to build the visualization.

## Document Style

- Use English for document text, headings, diagrams, and technical labels unless a Japanese version is explicitly requested.
- Keep each document focused on one Shopify product or product area.
- Prefer Mermaid diagrams for architecture, sequence, and state-flow explanations.
- Include links to relevant Shopify documentation when they help readers validate the behavior.
