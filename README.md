# Codex Plugins

A public marketplace for Codex plugins maintained by Justin Kropp.

## Install the marketplace

```sh
codex plugin marketplace add jrkropp/codex-plugins
```

Then install a plugin from the marketplace:

```sh
codex plugin add simplify@jrkropp-plugins
```

## Plugins

### Simplify

Simplify code by reducing the reasoning required to understand and safely
change it. The skill favors clear ownership and direct data flow, preserves
useful boundaries, and asks for concrete benefits before refactoring.

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
