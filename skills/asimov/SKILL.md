---
name: asimov
description: Use the ASIMOV CLI and its modules to access the user's personal knowledge such as mail, messages, documents, or public data sources. Use when the user mentions ASIMOV or wants data from their own sources in the task.
compatibility: Requires shell and network access
---

# ASIMOV

ASIMOV fetches knowledge from the user's data sources, personal and public, through installable modules, and builds a graph-based knowledge base on top. `asimov help` and each subcommand's `--help` are the authority on syntax.

## Setup

```bash
asimov --version
```

If missing, install per <https://github.com/asimov-platform/asimov-cli#installation> — ask the user before installing.

## Modules

One module per data source. The lifecycle:

```bash
asimov module search <terms...>   # find modules in the live index
asimov module install <name>
asimov module inspect <name>      # manifest, state, config status
asimov module doc <name>          # the module's README: provider specifics, source URL formats
asimov module enable <name>
asimov module resolve <url>       # which enabled module handles this source
asimov module uninstall <name>
```

`inspect` prints a hint for anything that still needs doing. Configuration lives under `asimov module config` (`show`, `get`, `set`, `setup`, `unset`). For secret-bearing or interactive setup, prefer asking the user to run `asimov module config setup <name>` in their own terminal and report back.

## Retrieve

A module's programs (listed by `inspect`) name its operations:

| Program       | Command        |
| ------------- | -------------- |
| `*-cataloger` | `asimov list`  |
| `*-fetcher`   | `asimov fetch` |
| `*-reader`    | `asimov read`  |
| `*-prompter`  | `asimov ask`   |
