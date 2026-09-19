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
/plugin install wem@wem3
```

Then:

```
/wem:compare Dyson V15 Detect
/wem:deal Dior Fahrenheit Aftershave 100ml
/wem:verify Dyson V15 Detect at Amazon for £599
```

## Installing on claude.ai (not Claude Code)

**Customize → Plugins → Add → Add from a repository**, then
`TonyXhufi/wem-price-compare-mcp`. Install **WEM Price Compare** from the
marketplace that appears.

Then two steps that are easy to miss, and skipping either makes the plugin look
broken rather than unconfigured:

1. **Connect the bundled connector.** Open the plugin's **Connectors** tab and
   press Connect. The tab says "Connect each one so Claude can use it" for a
   reason: a plugin may declare an MCP server, but only you can approve talking
   to it. The plugin is inert until you do.

2. **Enable it in the conversation.** Connector access is per-chat, not
   per-account. A brand-new chat starts without it even though the connector is
   connected at account level, so turn WEM on in that chat's connector controls.

The failure mode if you skip step 2 is quiet and misleading: Claude recognises
the price question, reaches for WEM, finds nothing, and falls back to a web
search — reporting, correctly, that the WEM tools "aren't reachable in this
session". That is not WEM being down. Check the server yourself if unsure:

```bash
curl -s https://wem3.ai/api/mcp -H 'content-type: application/json' \
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/list"}' | head -c 200
```

## Just want the tools, not the commands?

The plugin is a thin wrapper around a remote MCP server — nothing runs locally.
If you would rather add the server directly, keep the `"type": "http"` line —
Claude Code rejects a `url` entry without it:

```json
{
  "mcpServers": {
    "wem": {
      "type": "http",
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
barcode (EAN/UPC/GTIN), a `wem3.ai/pl/{slug}` URL, or a specific model name
as `title` — rather than running a fresh retailer search, so it answers "is
this actually the best price" instead of "what exists". A title match is
inferred, not barcode-exact. `verify_offer` checks a price you did not get
from WEM, and distinguishes **unverifiable** from **false**: a claim it cannot
check comes back as unchecked, never as refuted.

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

MIT — see [LICENSE](../LICENSE). The licence covers this plugin and its
documentation; the hosted service itself is governed by the terms at
<https://wem3.ai/terms>.
