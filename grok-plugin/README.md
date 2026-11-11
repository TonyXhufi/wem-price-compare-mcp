# WEM Price Compare for Grok

Grok Build installs this directory. It is the plugin: `.grok-plugin/plugin.json` names it, and `.mcp.json` connects the public server.

```
https://wem3.ai/api/mcp
```

No account, no API key, no authentication.

Grok on the web adds the same server at grok.com/connectors → New connector → Custom. Authentication: none.

When a result includes `links`, the first line of a price answer is the cheapest of those lines. Each one is a wem3.ai URL for that shop and price. The `compare-prices` skill says how to read the rest.
