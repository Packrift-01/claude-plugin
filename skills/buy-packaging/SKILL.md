---
name: buy-packaging
description: Find, price and order packaging supplies from Packrift, including shipping boxes, mailer boxes, poly and bubble mailers, poly bags, labels, packing tape, stretch film and void fill. Use when someone wants to buy, order, restock or reorder packaging, asks where to get a specific size or spec, wants the delivered cost to their ZIP code, or wants a checkout link.
when_to_use: Examples include "order 200 12x12x12 boxes", "I need 10x13 poly mailers", "restock our packing tape", "reorder Packrift SKU 1066", "cheapest 14x10x6 boxes delivered to 30301", "get me a checkout link for these". Not for shipping labels, postage or carrier accounts.
argument-hint: "[what to buy, how many, delivery ZIP]"
allowed-tools: mcp__plugin_packrift_packrift__search_products mcp__plugin_packrift_packrift__get_product mcp__plugin_packrift_packrift__get_shipping_estimate mcp__plugin_packrift_packrift__create_cart_url
compatibility: Uses the Packrift MCP server (https://mcp.packrift.com/mcp) bundled with this plugin.
license: MIT
---

# Buy packaging from Packrift

Packrift's tools return live prices and stock, so a purchase takes two or three calls: search, an optional delivered price, then a checkout link. The buyer always completes checkout on packrift.com; these tools never place orders or take payment.

## Steps

1. **Find the product.** Call `search_products` with the size, spec or SKU in the buyer's words, such as "12x12x12 boxes", "10x13 white poly mailers" or "SKU 1066". If they describe the item they ship rather than the packaging, use the find-packaging skill first.
2. **Show the best matches.** List three to five, exact sizes first, with price per unit, pack size and stock. Say clearly when a result is a close size rather than an exact one.
3. **Turn their quantity into packs.** Prices and quantities are per pack. For example, 200 boxes sold in packs of 25 is 8 packs. Round up and say so. The search results state which volume discounts apply automatically at checkout.
4. **Price delivery when asked, or when they give a ZIP code.** Call `get_shipping_estimate` with `destination_postal_code` and `items` as `[{sku, quantity}]`, with quantity in packs. Report the subtotal after volume discounts, the shipping options, the delivered total before tax and the cost per unit. Include the free-shipping line if the tool returns one. Packrift ships within the United States.
5. **Create the checkout link after the buyer confirms** the item and quantity. Call `create_cart_url` with `items: [{sku, quantity}]` (up to 25 lines) and share the link. Tell them it opens their cart on packrift.com with those items, and that nothing is ordered until they check out.

## Rules

- Confirm the items and quantities with the buyer before creating a checkout link.
- Estimates exclude tax; checkout shows the final amount. Never present an estimate as final.
- Do not describe a different size, strength, thickness or pack count as the same product.
- Pallet or recurring quantities, custom sizes, printing or freight: use the bulk-packaging-quote skill.
- Use `get_product` when the buyer wants full specs, or to check that a larger quantity can ship now.

## If the Packrift tools are not available

Tell the user the Packrift connector needs to be connected (it comes with this plugin; in the Claude apps, open the plugin's Connectors tab), and link the matching collection on packrift.com, for example https://packrift.com/collections/corrugated-boxes, https://packrift.com/collections/poly-mailers or https://packrift.com/collections/packing-tape.
