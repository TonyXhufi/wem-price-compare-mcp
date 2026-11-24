# WEM Price Compare for Muse

WEM Price Compare for Muse Code and for Muse (Meta).

Muse Code reads `~/.config/muse/settings.json`. Merge the
`wem-price-compare` entry from `settings.json` into
`mcp_servers` there, and keep any servers already in the file.

The server is `https://wem3.ai/api/mcp`. Authentication: none.
The header `X-Wem-Client: muse` is how Muse Code names itself
on the call.

In the Muse app, ask Muse to create a custom connector with
that server URL, authentication none, and privacy policy
`https://wem3.ai/privacy`. There is no public directory
listing yet — that is a separate submission at
platform.muse.ai, by the founder. See
`integrations/muse/CONNECTOR_SUBMISSION.md` in the WEM
repo for the paste-ready answers.

When a result includes `links`, the first line of a price
answer is the cheapest of those lines. Each one is a
wem3.ai URL for that shop and price.

## Install — Muse Code

1. Copy `settings.json` from this folder.
2. Open `~/.config/muse/settings.json` (macOS and Linux)
   or `%APPDATA%\muse\settings.json` (Windows).
3. Merge the `wem-price-compare` entry into `mcp_servers`.
   Do not replace the whole file if you already have
   other servers.
4. Restart Muse Code.

`settings.json` in this folder is the complete entry:

```json
{
  "schema_version": 1,
  "mcp_servers": {
    "wem-price-compare": {
      "transport": "streamable_http",
      "url": "https://wem3.ai/api/mcp",
      "enabled": true,
      "mode": "optional",
      "headers": {
        "X-Wem-Client": "muse"
      }
    }
  }
}
```

`mode: "optional"` means Muse Code keeps working if WEM
is unavailable. It will warn, not block startup.

## Install — Muse app

Ask Muse:

> Create a custom connector named WEM Price Compare.
> MCP server: https://wem3.ai/api/mcp
> Authentication: none
> Privacy policy: https://wem3.ai/privacy

Or in the app: Settings → Connectors, add a custom
connector with those details.

## What it does

WEM Price Compare looks up retailer prices and checks a
claimed price against its catalogue. Free, no account.
Read-only: compare and verify prices, no checkout,
no payment, no order. Checkout always completes on
the retailer.

Default currency is GBP. UK shops first.

## Tools — 11, all over MCP

- `search_products` — search by name or identifier:
  barcode (EAN/UPC/GTIN), Amazon ASIN, MPN, merchant
  SKU, WEM ID, or a `wem3.ai/pl/` URL.
- `semantic_search` — search by a plain-language need,
  for example "comfortable shoes for standing all day".
- `get_categories` — electronics, fashion, beauty,
  home, sports, collectibles.
- `get_product` — needs `wem_id`, or `provider`
  and `product_id`.
- `compare_products` — lay 2 to 5 listings side by side.
- `find_lowest_price` — pick one listing for a kind
  of product within the shopper's constraints.
- `compare_offers` — retailer offers for one product,
  cheapest first, with a 90-day price-history low.
  Needs `gtin`, `slug`, `wem_id`, or `title`.
- `verify_offer` — check a claimed price for one
  product at one retailer. Stores an evidence receipt.
- `lookup_products` — look up to 20 identifiers at once.
- `get_evidence_receipt` — fetch a receipt by id,
  `wem-evr-` followed by 32 hex characters.
- `search_promotions` — current promotions for the
  shopper's market.

## Try it

```
Using WEM Price Compare, compare Sony DualSense
Cosmic Red controller prices.
```

```
What is the cheapest current price for Sony DualSense
Cosmic Red, GTIN 00711719575924, in GBP?
```

Verified 2026-11-24, `compare_offers` by that GTIN:
Sony DualSense PlayStation Cosmic Red Wireless
Controller PS5, £54.99 at deals.gi, in stock,
last seen 2026-11-19, current; £66.22 at
tradegoods.co.uk, last seen 2026-11-21, current.

## How to read a price

Prices are indicative snapshots, refreshed from
partner feeds. The retailer sets the final price
at checkout.

- A price is current only when WEM read it within
  14 days and the shop was not out of stock at
  that read. Only a current price may lead, be
  called cheapest, or enter a saving.
- `verified: true` means WEM recently observed
  that price at the retailer. `verified: false`
  means indicative, or a live listing not resolved
  to a catalogue product.
- Identity is separate from price: `exact` is a
  barcode match, `catalogued` is a WEM key,
  `inferred` is matched by name, MPN, or SKU.
- Give the retailer URL from the result when you
  name a price. A different URL can be a different
  listing or price.
- Rows with `affiliate: false` earn WEM nothing.
  Disclosure says whether all, some, or none of
  the links are affiliate-tracked.

## Limits

- 60 requests per minute per IP; 500 live product
  lookups per day per IP, 1000 per day total for
  retailer APIs. Catalogue reads, categories,
  receipts, and promotions: 500 per IP per day.
- Server: wem-marketplace v1.0.4. Protocol
  2025-06-18, 2025-03-26, 2024-11-05. Stateless,
  no Mcp-Session-Id required.
- A live search can time out after 9s on WEM's
  side. That is not "no product". Use
  `compare_offers` by GTIN for a deterministic
  check, and give the shopper the WEM search link
  if a name search times out:
  `https://wem3.ai/shop?q=<product>`

## Privacy, terms, disclosure

- Privacy: https://wem3.ai/privacy
- Terms: https://wem3.ai/terms
- Disclosure: https://wem3.ai/disclosure
- Human setup page: https://wem3.ai/extension/ai
- OpenAPI, for clients without MCP:
  https://wem3.ai/api/openapi.json
- Source: https://github.com/TonyXhufi/wem-price-compare-mcp
