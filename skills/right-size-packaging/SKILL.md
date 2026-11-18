---
name: right-size-packaging
description: Lower shipping costs by right-sizing boxes and mailers. Use when someone wants to cut shipping or dimensional-weight charges, asks whether their current box is too big for what they ship, wants to audit the boxes for several products at once, or wants to compare the billable weight of different box sizes. For carrier rate shopping or postage labels, use a shipping-label tool instead.
when_to_use: Examples include "how do I cut our shipping costs", "dim weight charges are killing us", "is a 12x12x12 box too big for this", "check the boxes for our five best sellers", "what's the billable weight of a 14x10x8 box at 3 lb", "can I ship this in something smaller".
argument-hint: "[item size and weight, current box size]"
allowed-tools: mcp__plugin_packrift_packrift__right_size_packaging mcp__plugin_packrift_packrift__find_packaging_for_item mcp__plugin_packrift_packrift__search_products mcp__plugin_packrift_packrift__get_shipping_estimate
compatibility: Uses the Packrift MCP server (https://mcp.packrift.com/mcp) bundled with this plugin.
license: MIT
---

# Right-size packaging to cut shipping costs

Carriers bill the greater of actual weight and dimensional weight, so an oversized box often costs more to ship than the item weighs. This skill compares the box the user ships in now with the smallest safe option Packrift stocks.

## Billable weight

1. Use outside dimensions: for corrugated boxes, add about 1/4 in to each inside dimension.
2. Round each side up to the next whole inch.
3. Multiply length x width x height to get cubic inches.
4. Divide by 139 and round up. UPS and FedEx apply this to every package. USPS has used the same divisor since July 12, 2026, but only for packages over 1,728 cubic inches (one cubic foot); below that, USPS bills actual weight.
5. Billable weight is the higher of that result and the actual weight (item, packaging and cushioning), rounded up.

Example: box sizes are listed as inside dimensions, so a listed 12 x 12 x 12 box is about 12.25 in outside. That rounds up to 13 x 13 x 13 = 2,197 cubic inches, which bills at 16 lb with UPS, FedEx and USPS even for a 3 lb item. A listed 10 x 7 x 4 box rounds up to 11 x 8 x 5 = 440 cubic inches: 4 lb with UPS or FedEx, and actual weight with USPS.

## Steps

1. **Collect** the item's size, weight and type, and the inside size of the box or mailer they use now. If they don't say what the item is, ask once whether it is fragile; if they don't answer, show a sturdy option and a fragile option side by side.
2. **Compare in one call.** When the user knows the inside size of the box they use now, call `right_size_packaging` with up to 10 products (name, size, weight, current box inside size, `fragile`, and `monthly_shipments` if they share volume). It returns the current and recommended billable weight for UPS/FedEx and USPS, the pounds saved per shipment and per month, and product links, using the method above. Show one product's arithmetic briefly so the user can check it.
3. **No current box size?** Call `find_packaging_for_item` with the item details and a `use_case` in the user's words (set `packaging` to `box` if they ship in boxes); fragile items keep their cushioning. Its results include billable weight for each option, counting the packaging.
4. **Explain the saving.** Report the difference per package and per month. If the user shares their carrier rates, estimate the dollar saving; otherwise give the weight reduction only.
5. **Offer next steps:** price the new box (`search_products`, or `get_shipping_estimate` for a delivered total) and a checkout link through the buy-packaging skill.

## Rules

- Never cut cushioning below the minimum for fragile items to save dimensional weight.
- Do not quote carrier postage; this skill works with billable weight unless the user supplies rates.
- With USPS, poly mailers and other packages under one cubic foot bill by actual weight. UPS and FedEx apply dimensional weight to every package, including a filled poly mailer.
