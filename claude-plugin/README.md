<img src="../assets/icon-512.png" alt="WEM" width="96" align="right" />

# WEM Price Compare — Claude Code plugin

Adds retail price comparison to Claude Code. Free, read-only, no account, no
API key.

```
https://wem3.ai/api/mcp
```

## Install

Two steps, because Claude Code installs plugins from marketplaces rather than
straight from a repository. This repo is its own marketplace, so adding it and
installing from it is the whole flow:

```bash
/plugin marketplace add TonyXhufi/wem-price-compare-mcp
/plugin install wem-price-compare@wem
```

Then:

```
/wem:compare Sony WH-1000XM5
/wem:deal Dior Fahrenheit Aftershave 100ml
/wem:verify AirPods Pro 2 at eBay for £199.99
```

## Just want the tools, not the commands?

The plugin is a thin wrapper around a remote MCP server — nothing runs locally.
If you would rather add the server directly:

```json
{
  "mcpServers": {
    "wem": {
      "url": "https://wem3.ai/api/mcp"
    }
  }
}
```

Same eight tools, no slash commands. The plugin exists to add the commands and
the result-reading guidance, not to add capability.

## Commands

| Command | What it does |
|---|---|
| `/wem:compare` | Prices across retailers for one product, cheapest first, with the 90-day low |
| `/wem:deal` | Lowest listed price for a search, with runners-up |
| `/wem:verify` | Checks whether a price claim is still true before you repeat it |

## Tools

Eight, all read-only. None writes, purchases, or takes payment.

`search_products` · `semantic_search` · `get_product` · `compare_products` ·
`find_lowest_price` · `compare_offers` · `verify_offer` · `get_categories`

Two are worth knowing about. `compare_offers` resolves a product identity — a
barcode (EAN/UPC/GTIN) or a `wem3.ai/pl/{slug}` URL — rather than running a
fresh retailer search, so it answers "is this actually the best price" instead
of "what exists". `verify_offer` checks a price you did not get from WEM, and
distinguishes **unverifiable** from **false**: a claim it cannot check comes
back as unchecked, never as refuted.

The bundled skill covers how to read those verdicts without overstating them.

## Prices and disclosure

Prices are indicative snapshots from partner feeds, not live quotes. The
retailer sets the final price at checkout, and WEM never takes payment — you
always complete the purchase on the retailer's own site.

WEM is funded by disclosed affiliate commission, and links returned by these
tools are affiliate-tracked at no extra cost to the buyer.

- Disclosure: <https://wem3.ai/disclosure>
- Privacy: <https://wem3.ai/privacy>
- Setup guide: <https://wem3.ai/extension/ai>

## Licence

MIT — see [LICENSE](LICENSE). The licence covers this plugin and its
documentation; the hosted service itself is governed by the terms at
<https://wem3.ai/terms>.
