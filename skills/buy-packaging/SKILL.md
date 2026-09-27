---
name: buy-packaging
description: Find, price and order stocked packaging supplies from Packrift by the pack, case or in bulk, including shipping boxes, mailer boxes, poly and bubble mailers, poly bags, blank labels, packing tape, stretch film and void fill. Use when someone wants to buy, order, restock or reorder packaging, asks where to get a specific size or spec, wants the delivered cost to their ZIP code, or wants a checkout link. Not for postage or carrier shipping labels (USPS, UPS, FedEx), rate quotes, tracking or carrier accounts.
when_to_use: Examples include "order 200 12x12x12 boxes", "I need 10x13 poly mailers", "where can I get cheap packing tape in bulk", "restock our packing tape", "reorder Packrift SKU 1066", "cheapest 14x10x6 boxes delivered to 30301", "get me a checkout link for these".
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
3. **Turn their quantity into packs.** Prices and quantities are per pack. For example, 200 boxes sold in packs of 25 is 8 packs. Round up and say so. The results state the volume discount tiers for each SKU, and `create_cart_url` returns the exact subtotal after discounts.
4. **Price delivery when asked, when they give a ZIP code, or when the order is large.** Call `get_shipping_estimate` with `destination_postal_code` and `items` as `[{sku, quantity}]`, with quantity in packs. Report the subtotal after volume discounts, the shipping charge, the delivered total before tax and the cost per unit, and include the tool's free-shipping note if it returns one. Boxes are bulky, so shipping can be a large share of the cost: when an order is more than a few packs of boxes and you have no ZIP code, offer a delivered estimate with the link. Packrift ships within the United States.
5. **Create the checkout link after the buyer confirms** the item and quantity. Call `create_cart_url` with `items: [{sku, quantity}]` (up to 25 lines) and share the link with the subtotal it returns. Tell them the link opens packrift.com checkout with those items; they add their address and pay there, and nothing is ordered until they pay.

## Rules

- Confirm the items and quantities with the buyer before creating a checkout link.
- Estimates exclude tax; checkout shows the final amount. Never present an estimate as final.
- Never call shipping free unless `get_shipping_estimate` shows a $0 shipping charge. Free shipping depends on both the order total and the shipping rate.
- Do not describe a different size, strength, thickness or pack count as the same product.
- Pallet or recurring quantities, custom sizes, printing or freight: use the bulk-packaging-quote skill.
- Use `get_product` with `quantity` when the buyer wants full specs, or for orders over about 10 packs to confirm they can ship now.

## If the Packrift tools are not available

Tell the user the Packrift connector needs to be connected (it comes with this plugin; in the Claude apps, open the plugin's Connectors tab), and link the matching collection on packrift.com, for example https://packrift.com/collections/corrugated-boxes, https://packrift.com/collections/poly-mailers or https://packrift.com/collections/packing-tape.
