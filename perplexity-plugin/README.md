# WEM Price Compare for Perplexity

Import this folder: Plugins → Add custom → Import plugin from GitHub.

Repository: `TonyXhufi/wem-price-compare-mcp`

Folder: `perplexity-plugin`

`plugin.json` names the plugin. `mcp.json` connects the public server over streamable HTTP, with no authentication and no custom headers.

```
https://wem3.ai/api/mcp
```

The same server can be added as a custom connector: Settings → Connectors → Add connector → Custom. Authentication: none.

When a result includes `links`, the first line of a price answer is the cheapest of those lines. Each one is a wem3.ai URL for that shop and price.
