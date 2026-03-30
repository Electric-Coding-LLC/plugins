# Google Stitch Codex Plugin

Community-maintained Codex plugin for Google's hosted Stitch MCP server.
Maintained by Electric Coding LLC.

## Disclaimer

This project is unofficial. It is not affiliated with, endorsed by, or supported by Google.
It is provided as-is, without warranty or guaranteed support.

## What this is

This repo does not reimplement Stitch. It gives Codex a local plugin wrapper around Google's hosted Stitch MCP endpoint.

The working setup is:

- a local plugin folder at `plugins/google-stitch`
- a plugin manifest at `.codex-plugin/plugin.json`
- a local MCP config file at `.mcp.json`
- an HTTP MCP server definition pointing at `https://stitch.googleapis.com/mcp`
- an API key passed as the `X-Goog-Api-Key` header
- a marketplace entry that points Codex at the local plugin folder

## Files

- `.codex-plugin/plugin.json`: Codex plugin metadata and marketplace-facing description
- `.mcp.json.example`: template for the local MCP server config
- `README.md`: setup and troubleshooting notes

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

## Why this works

The key pieces that made this work in Codex were:

- `plugin.json` uses `"mcpServers": "./.mcp.json"` so the plugin manifest resolves its MCP config from the plugin folder itself
- `.mcp.json` uses Codex's local hosted-server pattern:

```json
{
  "mcpServers": {
    "stitch": {
      "type": "http",
      "url": "https://stitch.googleapis.com/mcp",
      "headers": {
        "X-Goog-Api-Key": "YOUR_API_KEY"
      }
    }
  }
}
```

- the real API key stays local and untracked
- the marketplace entry advertises the plugin as installable from a local path

## Security

- `.mcp.json` is gitignored so real API keys do not get committed
- only `.mcp.json.example` is tracked
- you should create the real key in Stitch Settings > API Keys and keep it local

## Troubleshooting

- If the plugin appears in the Codex marketplace but does not show up under Manage > MCPs, verify that the local marketplace entry points to the correct `plugins/google-stitch` directory.
- Make sure `.mcp.json` exists next to `.mcp.json.example` inside the plugin folder.
- Make sure the API key header is present and the server URL is exactly `https://stitch.googleapis.com/mcp`.
- If the plugin was moved or edited while Codex was open, restart Codex and check again.
- If install/runtime recognition still fails after publish, the remaining issue is likely load/discovery behavior rather than the Stitch server config itself.

## License

MIT. See `../LICENSE`.
