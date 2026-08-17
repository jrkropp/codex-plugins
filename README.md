# Codex Plugins

A public marketplace for Codex plugins maintained by Justin Kropp.

## Install the marketplace

```sh
codex plugin marketplace add jrkropp/codex-plugins
```

The catalog is intentionally empty until the first plugin is ready.

## Repository layout

```text
.agents/plugins/marketplace.json  Marketplace catalog
plugins/<name>/                   Installable plugins
```

Every plugin must include a manifest at
`plugins/<name>/.codex-plugin/plugin.json`. Add the corresponding entry to
`.agents/plugins/marketplace.json` when the plugin is ready to install.

See the [OpenAI plugin documentation](https://learn.chatgpt.com/docs/plugins)
for packaging and distribution guidance.

## License

[MIT](LICENSE)
