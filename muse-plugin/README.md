# WEM Price Compare for Muse

Muse Code reads `~/.config/muse/settings.json`. Merge the `wem-price-compare` entry from `settings.json` into `mcp_servers` there, and keep any servers already in the file.

The server is `https://wem3.ai/api/mcp`. Authentication: none. The header `X-Wem-Client: muse` is how Muse Code names itself on the call.

In the Muse app, ask Muse to create a custom connector with that server URL, authentication none, and privacy policy `https://wem3.ai/privacy`.

When a result includes `links`, the first line of a price answer is the cheapest of those lines. Each one is a wem3.ai URL for that shop and price.
