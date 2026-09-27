---
name: find-packaging
description: Recommend the right shipping box or mailer for a specific item from Packrift's live catalog. Use when someone asks what size box or mailer to use, how to pack or ship a particular item (a mug, candle, clothing, books, electronics, parts, posters), or gives an item's dimensions and needs packaging that fits.
when_to_use: Examples include "what size box do I need for this", "what's the best mailer for a hoodie", "how should I ship a ceramic mug", "packaging for my 9x6x4 product", "will this fit in a poly mailer". Not for comparing carrier rates or buying shipping labels.
argument-hint: "[item size, weight and what it is]"
allowed-tools: mcp__plugin_packrift_packrift__find_packaging_for_item mcp__plugin_packrift_packrift__get_product mcp__plugin_packrift_packrift__get_shipping_estimate
compatibility: Uses the Packrift MCP server (https://mcp.packrift.com/mcp) bundled with this plugin.
license: MIT
---

# Find packaging that fits an item

Packrift's `find_packaging_for_item` tool does the fit math against the live catalog: inside dimensions, cushioning space for the item type, box strength against the weight, and billable shipping weight. Your job is to gather the item details, call it, and explain the choice.

## Steps

1. **Get the item details.** You need length, width and height in inches, the weight in pounds, and what the item is.
   - Convert metric units (1 in = 2.54 cm, 1 lb = 0.4536 kg).
   - If a dimension is missing, ask for it once. If the weight is unknown, estimate it and say you did.
   - Several items shipped together: use the dimensions of the packed bundle.
2. **Call `find_packaging_for_item`** with `item_length_in`, `item_width_in`, `item_depth_in`, `item_weight_lb` and `use_case`. Put the user's own words for the item in `use_case` (for example "ceramic mug" or "folded hoodie"); the tool reads it to decide how much cushioning is needed. Set `packaging` to `box` or `mailer` only if the user asked for one.
3. **Recommend.** Lead with the best option and one sentence on why it fits. Then show two or three options in a compact table: SKU and name, inside size, fit and cushioning, strength (for boxes), billable weight, price per unit and pack price, stock.
4. **Explain how to pack it** in plain words, using the advice the tool returns (cushioning, void fill, double boxing for very fragile items).
5. **Offer the next step:** the delivered cost to their ZIP code (`get_shipping_estimate` with the SKU and number of packs), more detail on one option (`get_product`), or a checkout link once they choose a quantity (see the buy-packaging skill).

## Rules

- Prices are per pack. State the pack count and the price per unit.
- Never describe a different size as an exact match, and never invent specs the tool did not return.
- When nothing fits, share the quote link the tool returns: Packrift can quote custom sizes.
- Items over 150 lb are beyond parcel packaging; the tool returns a freight quote link.

## If the Packrift tools are not available

Tell the user the Packrift connector needs to be connected (it comes with this plugin; in the Claude apps, open the plugin's Connectors tab). Meanwhile, work out the inside size they need: add about 1/2 in per side for sturdy items, 1 to 2 in per side for electronics and 2 in per side for fragile items, then point them to https://packrift.com/collections/corrugated-boxes or https://packrift.com/collections/mailers-envelopes.
