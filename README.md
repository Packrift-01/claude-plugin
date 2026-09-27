# Packrift Packaging for Claude

![Packrift](assets/packrift-logo.png)

Packaging supplies inside Claude. Tell Claude what you ship and it finds the right shipping box or mailer from Packrift's in-stock catalog of 20,000+ products, checks the fit, cushioning and box strength, shows live prices and stock, works out the delivered cost to your ZIP code, and gives you a checkout link on packrift.com. Packrift ships within the United States.

## What you can ask

- "What box should I use to ship a ceramic mug that's 4.5 x 3.5 x 4 inches?"
- "Find 12x12x12 shipping boxes and show me the cheapest per box."
- "I need poly mailers for folded t-shirts. What size, and what would 500 cost delivered to 75201?"
- "Our shipping bills are high. Are we using boxes that are too big for 9 x 6 x 3 in items at 1.5 lb?"
- "Reorder 10 packs of Packrift SKU 1066 and give me a checkout link."
- "I need 2,000 printed 18x12x12 boxes every month. How do I get a quote?"
- "ECT-32 or ECT-44 for a 50 lb box?"

## Skills

| Skill | What it does |
|---|---|
| `find-packaging` | Recommends the box or mailer that fits an item, with cushioning by item type, box strength against weight and billable shipping weight. |
| `buy-packaging` | Finds products by size, spec or SKU, converts your quantity into packs, prices delivery to your ZIP code and creates a checkout link. |
| `right-size-packaging` | Compares the billable weight of the box you use now with the smallest safe option, to cut dimensional-weight charges. |
| `bulk-packaging-quote` | Prepares a quote request for pallet or recurring quantities, custom sizes, printing or freight. |
| `packaging-advisor` | Answers packaging questions: box strength ratings, box or mailer, poly mailer thickness, tape, void fill and stretch film. |

Claude picks the right skill from your request. In Claude Code you can also run one directly, for example `/packrift:find-packaging 9x6x4 in, 2 lb, ceramic mug`.

## Install

**Claude, Cowork and Claude Code:** add Packrift from the plugin directory in Customize, then connect the Packrift connector from the plugin's Connectors tab. No account or API key is needed.

**Claude Code from this repository:**

```bash
claude plugin marketplace add Packrift/claude-plugin
claude plugin install packrift@packrift
```

## What the plugin connects to and sends

The plugin bundles one remote MCP server, Packrift's public catalog server at `https://mcp.packrift.com/mcp` (Streamable HTTP, no authentication). The skills call its tools: `search_products`, `find_packaging_for_item`, `get_product`, `get_shipping_estimate`, `create_cart_url` and `get_bulk_quote_link`.

When a skill runs, Claude sends the server only the tool arguments needed for your request: search text, item dimensions and weight, SKUs and quantities, and a US ZIP code (and optional state) for delivered pricing. The plugin has no hooks, runs no local code and reads no files. The tools are read-only: they never place an order or take payment. A checkout link opens packrift.com checkout with the items you chose, where you add your address and pay.

Packrift keeps usage records (tool, time, search text, SKUs returned, assistant type) for up to 90 days to improve results, and does not store names, email addresses, phone numbers, street addresses or IP addresses from these requests. Full notice: https://mcp.packrift.com/privacy. Orders on packrift.com follow the [Packrift privacy policy](https://packrift.com/policies/privacy-policy).

## Troubleshooting

- **Claude says the Packrift tools aren't available:** connect the Packrift connector from the plugin's Connectors tab, or in Claude Code run `/mcp` and check that `packrift` is connected.
- **A size isn't stocked:** Claude shows the closest sizes, labeled as not exact, and a quote link for the exact size.
- **Totals:** delivered prices are estimates from Packrift's checkout rates and exclude tax; checkout shows the final amount.

## Support

support@packrift.com · +1 (302) 216-2975 · https://packrift.com

Packrift LLC, 300 Delaware Ave, Wilmington, DE 19801, US

## License

MIT
