# Meticulate Codex Plugin

This repo contains a Codex marketplace with one plugin: Meticulate. The plugin bundles Meticulate company-intelligence skills with the existing Meticulate app connector.

## Structure

- `.agents/plugins/marketplace.json` exposes the plugin to Codex.
- `plugins/meticulate/.codex-plugin/plugin.json` is the plugin manifest.
- `plugins/meticulate/.app.json` maps the plugin to the Meticulate app connector.
- `plugins/meticulate/skills/` contains task-focused Codex skills.
- `plugins/meticulate/assets/` contains Meticulate brand assets used by the manifest.

## Local Testing

From this repo, add the marketplace to Codex:

```bash
codex plugin marketplace add .
```

Then restart Codex and install or enable `Meticulate` from the plugin directory.

After changing plugin files, refresh the installed marketplace copy:

```bash
codex plugin marketplace remove meticulate
codex plugin marketplace add .
```
