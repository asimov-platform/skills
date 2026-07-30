# Module registry

Live index: `https://raw.githubusercontent.com/asimov-modules/asimov-modules/master/index.jsonl` — one manifest-derived JSON record per module.

Fields worth reading when comparing candidates:

- `summary` — what the module does
- `handles` — URL schemes, protocols, and file types it accepts; construct source URLs from these
- `provides.programs` — operations it ships (`*-cataloger`, `*-fetcher`, `*-reader`, `*-prompter`)
- `config`, `uses` — declared configuration variables and environment
- `links` — repository and documentation

Search with alternation across the whole record:

```bash
curl -fsSL "$REGISTRY" | jq -c 'select(tostring | test("signal|messenger"; "i")) | {name, summary, handles}'
```

Before installing, open the repository from `links` and read its `.asimov/module.yaml` and `README.md` — the manifest for machine-readable capabilities, the README for provider-specific setup.

## Caveats

- `asimov module list -o jsonl` reports installed modules and their enabled state only, despite its help text.
- `asimov module resolve "$URL"` matches enabled installed modules only. An empty result does not mean no module exists — search the registry.
- If the installed CLI has grown a `module search` or `module inspect` command, prefer it over raw registry queries.
