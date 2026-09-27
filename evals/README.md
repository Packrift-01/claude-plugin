# Packrift plugin evals

Eight cases covering item fit (fragile and apparel), buying with a checkout link, delivered pricing, right-sizing, a bulk quote, a packaging question and one request the plugin should not act on (carrier rate shopping).

Run from the plugin root. The Packrift MCP tools are gated, so grant them for the run:

```bash
claude plugin eval . --allow-tools "mcp__plugin_packrift_packrift__*"
```

The tools are read-only; `create_cart_url` builds a link and places no order.
