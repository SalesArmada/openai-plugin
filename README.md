# Meticulate Codex Plugin

This repo contains the Meticulate Codex plugin. It bundles Meticulate company-intelligence skills with the existing Meticulate app connector.

## Structure

- `.codex-plugin/plugin.json` is the plugin manifest.
- `.app.json` maps the plugin to the Meticulate app connector.
- `skills/` contains task-focused Codex skills copied from the existing MCP server.
- `assets/` contains Meticulate brand assets used by the manifest.
- `.agents/plugins/marketplace.json` exposes this repo-root plugin as a Codex marketplace entry for review and testing.

## Local Testing

From this repo, add the marketplace to Codex:

```bash
codex plugin marketplace add .
```

Then restart Codex and install or enable `Meticulate` from the plugin directory.

After changing plugin files, refresh the installed marketplace copy:

```bash
codex plugin marketplace upgrade meticulate
```
