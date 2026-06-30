# Repository Instructions

This repository is a source-first documentation library for Shopify product architecture notes, detailed specifications, and process-flow visualizations.

## Change Workflow

- After any repository change, always commit and push without waiting for an additional user request.
- Push committed changes to both remotes on `main`:
  - `origin`: `https://benzookapi@github.com/benzookapi/shopify-technical-docs.git`
  - `ts`: `https://junichiokamuraSP@github.com/shopify-apac-ts/shopify-technical-docs.git`
- Use `/usr/bin/git` if the bundled runtime `git` fails or exits unexpectedly.
- This repository does not require tests. Do not add or run a test workflow unless the user explicitly asks for one.
- Lightweight checks such as `git diff --check`, link/path inspection, or reviewing rendered HTML source are enough before commit.

## Source and Output Model

- Markdown files are the source of truth and must be written in English.
- Do not create Japanese Markdown source files unless the user explicitly asks for them.
- HTML is the visualization output for GitHub Pages.
- English HTML is the master visualization output.
- Whenever a source Markdown file changes, regenerate or manually update the corresponding English HTML visualization in the same task.
- Whenever a source Markdown file changes, also regenerate or manually update the corresponding Japanese HTML visualization under `/ja/` in the same task.
- Whenever HTML visualization pages are created or materially changed, also create or update the Japanese HTML version under a `/ja/` path.
- Keep Japanese HTML as a localized output derived from the English Markdown source and English master HTML, not as an independent source of truth.

## Site Structure

- The root `index.html` is the GitHub Pages entry point.
- Product-specific files live under `products/<product-slug>/`.
- Each product directory should contain the English Markdown source, such as `architecture.md`, and the English visualization page, such as `index.html`.
- Japanese visualization pages should be accessible under `ja/`, mirroring the English page structure where practical, such as `ja/products/<product-slug>/index.html`.
- Each HTML visualization page must link back to its source Markdown file.
- Update `README.md` when product documents are added, moved, renamed, or materially reorganized.

## Content Rules

- Use Shopify developer documentation and relevant Shopify Help Center pages as references for Shopify product behavior.
- Prefer the existing English Markdown source when generating or updating HTML visualization pages.
- Keep diagrams and technical labels accurate to the source Markdown.
- Use Mermaid diagrams for architecture, sequence, state, and process-flow explanations when they help readability.
- Do not include internal Shopify information. Content should be based on public documentation or merchant-visible behavior that can be validated in a store.
- Keep repository documentation and HTML pages focused on product specifications, architecture, flows, references, and disclaimers.

## Disclaimer

- Keep a disclaimer in `README.md` and visible HTML pages.
- The disclaimer must state that the repository is not official Shopify documentation.
- It must also state that the maintainers do not accept responsibility for the accuracy, completeness, or consequences of using the content.
- It must say the content is supplemental material for understanding Shopify concepts and workflows, should be used at the reader's own discretion, and may change without notice.
