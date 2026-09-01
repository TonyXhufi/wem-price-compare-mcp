<img src="assets/icon-512.png" alt="WEM" width="96" align="right" />

# WEM Price Compare — MCP server

Compare retail prices across partner retailers from inside Claude, ChatGPT,
Cursor, Gemini CLI, or any Model Context Protocol client.

Free, read-only, no account, no API key.

```
https://wem3.ai/api/mcp
```

## Install

The server is remote and stateless, so there is nothing to run locally and no
credential to manage. Point your client at the URL above.

### Claude (claude.ai, Desktop, Code)

On claude.ai: **Settings → Connectors → Add custom connector**, then paste the
URL.

Claude Desktop and Claude Code take the same URL in their MCP config:

```json
{
  "mcpServers": {
    "wem": {
      "url": "https://wem3.ai/api/mcp"
    }
  }
}
```

### Cursor / VS Code / other MCP clients

Identical config. Any client that speaks Streamable HTTP works — the server
advertises protocol `2025-06-18` and falls back to `2025-03-26` and
`2024-11-05`.

### No MCP support?

The same tools are available over REST, described by an OpenAPI 3.1 spec you
can import directly into ChatGPT Actions, LangChain, or n8n:

- Spec: <https://wem3.ai/api/openapi.json>
- Endpoint: `https://wem3.ai/api/agent/products`

Rate limits are shared between the two — both spend the same retailer quota.

## Tools

Eight read-only tools. None of them write, purchase, or take payment.

| Tool | What it does |
|---|---|
| `search_products` | Keyword search across connected retailers |
| `semantic_search` | Find products from a natural-language description |
| `get_product` | Full detail for one product, by provider and ID |
| `compare_products` | Compare 2–5 products side by side |
| `find_lowest_price` | Single lowest-priced match under stated constraints |
| `compare_offers` | Multi-retailer offers for one product, cheapest first, with a 90-day price-history low |
| `verify_offer` | Check whether a price claim is still true before repeating it |
| `get_categories` | Category taxonomy with approximate price ranges |

`compare_offers` and `verify_offer` are the two worth knowing about. They
resolve a product identity (GTIN or WEM slug) rather than running a fresh
retailer search, so they answer "is this actually the best price" instead of
"what exists" — and they do not consume the daily product-lookup quota.

## Limits

The server is rate-limited per IP and holds a daily budget for product
lookups, which protects the upstream retailer API quota. `compare_offers`,
`verify_offer` and `get_categories` read WEM's own catalogue and do not count
against that budget. Current figures are reported by the server itself at
<https://wem3.ai/api/mcp>.

When a quota is hit the server returns a normal tool result with
`isError: true` and `_meta["wem/reason"] = "quota_denied"`, not a protocol
error, so a client can surface it as a message rather than a crash.

## What the server stores

The connection is stateless Streamable HTTP — no session is issued and no
`Mcp-Session-Id` is required.

Telemetry records the JSON-RPC method, the tool name, an assistant slug
derived from the User-Agent, and the outcome and duration. It does **not**
record tool arguments, IP addresses, raw User-Agent strings, or session
identifiers. In other words: the server knows that a search happened, not what
was searched for.

## Prices and disclosure

Prices returned are indicative, not live quotes. The retailer sets the final
price at checkout, and WEM never takes payment — users always complete the
purchase on the retailer's own site.

WEM is funded by disclosed affiliate commission, and links returned by these
tools are affiliate-tracked at no extra cost to the buyer.

- Disclosure: <https://wem3.ai/disclosure>
- Privacy: <https://wem3.ai/privacy>
- Setup guide: <https://wem3.ai/extension/ai>

## Registry

Published to the official MCP Registry as `ai.wem3/wem-price-compare`.
`server.json` in this repo is the manifest.

## Licence

MIT — see [LICENSE](LICENSE). The licence covers this manifest and
documentation; the hosted service itself is governed by the terms at
<https://wem3.ai/terms>.
