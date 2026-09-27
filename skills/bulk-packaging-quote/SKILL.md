---
name: bulk-packaging-quote
description: Request a quote from Packrift for pallet or recurring quantities, custom sizes, printed or branded packaging, or freight orders. Use when someone needs a pallet or more, a scheduled recurring supply, a size Packrift does not stock, or custom printing. For case or bulk amounts of a stocked item, use buy-packaging.
when_to_use: Examples include "5,000 custom printed mailer boxes", "a pallet of 18x18x18 boxes every month", "a custom 17x11x9 box", "pricing for a truckload of stretch film".
argument-hint: "[spec, quantity, delivery ZIP]"
allowed-tools: mcp__plugin_packrift_packrift__search_products mcp__plugin_packrift_packrift__get_product mcp__plugin_packrift_packrift__get_bulk_quote_link
compatibility: Uses the Packrift MCP server (https://mcp.packrift.com/mcp) bundled with this plugin.
license: MIT
---

# Request a bulk or custom packaging quote

## Steps

1. **Check stock first** for unprinted items. Call `search_products` for the spec. A stocked item in large quantity can often be ordered directly with automatic volume discounts, which is faster than a quote; `get_product` with `quantity` confirms it can ship now. If a stocked item fits, say so and offer that path.
2. **Collect the details a quote needs,** but don't hold the link back for them. Use what the buyer has given, and list what is still missing so they can add it on the form:
   - Exact spec: inside dimensions; board strength (for example ECT-32 or ECT-44) or film/bag thickness; style (shipping box, mailer box, bag); color.
   - Printing: where it goes (lid only, two sides, all over), number of ink colors, and logo size. Artwork goes by email to support@packrift.com after the request is submitted.
   - Quantity per order and how often they reorder.
   - Delivery ZIP code and the date they need it by.
3. **Call `get_bulk_quote_link`** with `requested_spec` (the spec in under about 200 characters), plus `quantity`, `delivery_zip` and `needed_by` when known. Pass `sku` only for a stocked, unprinted item; never for custom, printed or branded work, which Packrift's team quotes by hand. Share the link and repeat what the tool says the buyer still needs to add before submitting on packrift.com.

## Rules

- Do not promise prices, lead times or minimums for custom work; Packrift replies to the quote by email.
- Keep the spec specific. "2,000 18x12x12 ECT-44 kraft boxes, one-color logo on two sides, monthly to 60601" gets a faster, more accurate quote than "big boxes".
