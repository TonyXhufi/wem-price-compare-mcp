---
name: compare-prices
description: Compare retail prices with WEM when someone asks what a product costs, where it is cheapest, or whether a quoted price is still true. Use this before answering a shopping question from memory.
---

# Compare prices with WEM

Call WEM's tools on https://wem3.ai/api/mcp. WEM never takes payment. The shopper buys on the retailer's site.

## Which tool

- A barcode, a `wem3.ai/pl/` link, or a specific model name: `compare_offers`. Pass a model name as `title`. A title match is inferred, not a barcode match. Say so when `identity.strength` is `inferred`.
- A loose description: `search_products`.
- "What is the cheapest match?" for a loose description: `find_lowest_price`. For a named model, use `compare_offers` with `title` first.
- A price quoted from somewhere else: `verify_offer`.

## How to answer

The first line of a price answer is the cheapest entry in `links`. That line is already markdown. Its URL is on wem3.ai, and it is the page for the price you name. Then give the shop, say the price is an indicative snapshot and the retailer sets the final price, and include the `disclosure` line.

Relay that URL as returned. A retailer address composed from memory can be a different listing or a different price.

When `links` is empty and the result includes a `search` link, give that link. Say WEM held no shop for the product.

Rows with `affiliate: false` earn WEM nothing. The disclosure says whether all, some, or none of the links do.

A `sameModel` field, when present, is another model's page. Keep it beside the answer. Do not fold it into the offers or call it the lowest price.
