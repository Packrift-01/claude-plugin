---
name: packaging-advisor
description: Answer packaging selection questions with practical rules, covering box strength (ECT ratings and weight limits), single or double wall, box or mailer, poly mailer thickness, cushioning and void fill, packing tape and stretch film gauge. Use when someone asks how to choose, compare or use packaging materials for shipping.
when_to_use: Examples include "ECT-32 vs ECT-44", "single wall or double wall for a 50 lb box", "what mil poly mailer for hoodies", "hot melt or acrylic tape", "what gauge stretch wrap for pallets", "how much bubble wrap around a glass item".
compatibility: Works without tools; uses the Packrift MCP server bundled with this plugin when the user wants to buy.
license: MIT
---

# Packaging advisor

Answer from the rules in `references/packaging-rules.md`: choosing a box or mailer, sizing and cushioning, box strength ratings, dimensional weight, tape, void fill and stretch film.

## How to answer

1. Answer the question directly first, with the rule and the number that matters. For example: "ECT-32 single wall is rated to 65 lb; ECT-44 to 95 lb."
2. Add the one or two considerations that change the answer, such as stacking, freight, fragile contents or heat.
3. When the user needs a specific product, offer to find it: hand off to the buy-packaging skill with a precise search (for example "16x12x10 ECT-44 boxes"), or to the find-packaging skill if they have an item to fit.

## Rules

- Keep answers practical and specific; skip generic packaging marketing.
- Say when a question depends on the carrier's own rules (for example hazardous materials or oversize limits) and suggest checking with the carrier.
- Do not recommend a product unless the user wants to buy or asks which one to get.
