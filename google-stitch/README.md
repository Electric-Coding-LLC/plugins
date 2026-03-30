# Google Stitch Codex Plugin

Community-maintained Codex plugin for Google's hosted Stitch MCP server.
Maintained by Electric Coding LLC.

## Disclaimer

This project is unofficial. It is not affiliated with, endorsed by, or supported by Google.
It is provided as-is, without warranty or guaranteed support.

## What it includes

- `.codex-plugin/plugin.json`
- `.mcp.json.example`

## Install

1. Copy the `google-stitch` folder from this repo into your local Codex plugins directory as `plugins/google-stitch`.
2. Copy `.mcp.json.example` to `.mcp.json`.
3. Replace `YOUR_API_KEY` in `.mcp.json` with a real Stitch API key from Stitch Settings > API Keys.
4. Point your local marketplace entry at that plugin directory if it is not already registered.

Example marketplace entry:

```json
{
  "name": "google-stitch",
  "source": {
    "source": "local",
    "path": "./plugins/google-stitch"
  },
  "policy": {
    "installation": "AVAILABLE",
    "authentication": "ON_INSTALL"
  },
  "category": "Design"
}
```

## Development

- `.mcp.json` is ignored so local API keys do not get committed.
- The hosted MCP server URL is `https://stitch.googleapis.com/mcp`.
- This repo ships a community wrapper for the hosted Stitch MCP endpoint, not an official Google plugin package.

## License

Apache-2.0. See `../LICENSE`.
