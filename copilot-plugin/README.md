# WEM Price Compare for GitHub Copilot

Install the plugin:

```bash
copilot plugin install TonyXhufi/wem-price-compare-mcp:copilot-plugin
```

This directory is an Agent Plugins 1.0 package. `plugin.json` names it. `mcp.json` connects the public server. The `compare-prices` skill tells Copilot how to read a price result.

```
https://wem3.ai/api/mcp
```

No account, no API key, no authentication.

When a result includes `links`, the first line of a price answer is the cheapest of those lines. Each one is a wem3.ai URL for that shop and price.
