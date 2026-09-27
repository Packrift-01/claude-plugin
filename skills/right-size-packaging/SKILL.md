---
name: right-size-packaging
description: Lower shipping costs by right-sizing boxes and mailers. Use when someone wants to cut dimensional-weight charges, asks whether their current box is too big for what they ship, or wants to compare the billable weight of different box sizes.
when_to_use: Examples include "dim weight charges are killing us", "is a 12x12x12 box too big for this", "what's the billable weight of a 14x10x8 box at 3 lb", "can I ship this in something smaller". For carrier rate shopping or labels, use a shipping-label tool instead.
argument-hint: "[item size and weight, current box size]"
allowed-tools: mcp__plugin_packrift_packrift__find_packaging_for_item mcp__plugin_packrift_packrift__search_products mcp__plugin_packrift_packrift__get_shipping_estimate
compatibility: Uses the Packrift MCP server (https://mcp.packrift.com/mcp) bundled with this plugin.
license: MIT
---

# Right-size packaging to cut shipping costs

Carriers bill the greater of actual weight and dimensional weight, so an oversized box often costs more to ship than the item weighs. This skill compares the box the user ships in now with the smallest safe option Packrift stocks.

## Billable weight

1. Use outside dimensions: for corrugated boxes, add about 1/4 in to each inside dimension.
2. Round each side up to the next whole inch.
3. Multiply length x width x height to get cubic inches.
4. UPS and FedEx: divide by 139 and round up. USPS: divide by 166 and round up, but only when the package is over 1,728 cubic inches (one cubic foot). Below that, USPS bills actual weight.
5. Billable weight is the higher of that result and the actual weight, rounded up.

Example: a box measuring 12 x 12 x 12 in on the outside, holding a 3 lb item, bills at 13 lb with UPS or FedEx (1,728 / 139 = 12.4, rounded up). One measuring 10 x 8 x 6 in bills at 4 lb. Box sizes are listed as inside dimensions, so a 12 x 12 x 12 box is about 12.25 in outside, which rounds up to 13 x 13 x 13 and bills at 16 lb.

## Steps

1. **Collect** the item's size, weight and type, and the inside size of the box or mailer they use now.
2. **Compute the current billable weight** with the method above and show the arithmetic briefly.
3. **Find the right size.** Call `find_packaging_for_item` with the item details and a `use_case` in the user's words; fragile items keep their cushioning. The results include billable weight for each option.
4. **Compare** current and recommended billable weight for UPS/FedEx and USPS, and the difference per package. If the user shares their carrier rates or monthly volume, estimate the saving; otherwise give the weight reduction only.
5. **Offer next steps:** price the new box (`search_products`, or `get_shipping_estimate` for a delivered total) and a checkout link through the buy-packaging skill.

## Rules

- Never cut cushioning below the minimum for fragile items to save dimensional weight.
- Do not quote carrier postage; this skill works with billable weight unless the user supplies rates.
- Poly mailers and small flat packages rarely trigger dimensional weight; say so when it applies.
