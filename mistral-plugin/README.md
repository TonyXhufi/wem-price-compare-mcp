# WEM Price Compare for Mistral

This directory is the plugin: `plugin.json` names it, and `mcp.json` connects the public server over streamable HTTP.

```
https://wem3.ai/api/mcp
```

Le Chat registers that server as a custom connector: Intelligence → Connectors → Custom MCP Connector. Name: WEM Price Compare. Authentication: none.

When a result includes `links`, the first line of a price answer is the cheapest of those lines. Each one is a wem3.ai URL for that shop and price.
