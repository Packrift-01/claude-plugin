# Packrift plugin evals

Twelve cases: item fit (fragile and apparel), buying with a checkout link, delivered pricing, right-sizing, a printed-box quote (which must not carry a stock SKU), a box-strength question, bulk tape, a mailer comparison, a new candle business, and two requests the plugin should stay out of (carrier rate shopping and postage).

Run from the plugin root. The Packrift MCP tools are gated, so grant them for the run:

```bash
claude plugin eval . --allow-tools "mcp__plugin_packrift_packrift__*"
```

The tools are read-only; `create_cart_url` builds a link and places no order.
