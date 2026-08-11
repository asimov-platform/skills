---
name: asimov
description: Use the ASIMOV CLI and its modules to access the user's knowledge, including mail, messages, documents, and public data sources. Use when the user mentions ASIMOV or wants data from their own sources in the task.
compatibility: Requires shell and network access
---

# ASIMOV

ASIMOV fetches knowledge from the user's data sources, personal and public, through installable modules, and builds a graph-based knowledge base on top. `asimov help` and each subcommand's `--help` are the authority on syntax.

## Setup

```bash
asimov --version
```

If missing, ask for the user's approval, then follow <https://github.com/asimov-platform/asimov-cli#installation>.

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

`inspect` prints a hint for anything that still needs doing. Configuration lives under `asimov module config` (`show`, `get`, `set`, `setup`, `unset`). For secret-bearing or interactive setup, prefer asking the user to run `asimov module config setup <name>` in their own terminal rather than handling secrets yourself.

## Retrieve

A module's programs (listed by `inspect`) name its operations:

| Program       | Command        | Function                                                            |
| ------------- | -------------- | ------------------------------------------------------------------- |
| `*-cataloger` | `asimov list`  | Enumerates the resources a source URL contains (mailbox, feed, ...) |
| `*-fetcher`   | `asimov fetch` | Retrieves a single resource by URL                                  |
| `*-reader`    | `asimov read`  | Imports data from a local file or standard input                    |
| `*-prompter`  | `asimov ask`   | Sends a prompt to the model provider the module wraps               |

## Example

The user wants their browser bookmarks in context:

```console
$ asimov module search bookmarks
chromium  Chromium (and Brave, Google Chrome, Arc) bookmark import.

$ asimov module install chromium   # auto-enables when there is nothing to configure

$ asimov module resolve chrome://bookmarks
chromium

$ asimov list chrome://bookmarks   # also chromium://, brave://, arc://, …
{"@context":{…},"items":[{"@id":"urn:uuid:","@type":"know:Bookmark","created":"2025-09-27T04:30:00.000000Z","title":"ASIMOV Platform · GitHub","link":"https://github.com/asimov-platform"},…]}

$ asimov list -M chromium chrome://bookmarks   # same, with the module pinned explicitly
```

URLs resolve to modules automatically. The `resolve` check and `-M` are optional.

## Links

- <https://github.com/asimov-platform>
- <https://github.com/asimov-modules>
- <https://github.com/asimov-systems>
