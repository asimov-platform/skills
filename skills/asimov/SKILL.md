---
name: asimov
description: Use the ASIMOV CLI to join the user's personal knowledge (such as mail, messages, documents) and public data (such as from social media) into a unified intelligence layer and knowledge base. Use this skill when the user mentions ASIMOV, wants their own data in the task, or needs a data source an ASIMOV module handles.
compatibility: Requires shell and network access
---

# ASIMOV

ASIMOV is a personal intelligence platform built on semantic graph technology:
installable modules turn the user's data sources (personal and public) into a
connected knowledge graph, into intelligence that knows why, what, and how it
knows. `asimov help` and each subcommand's `--help` are the authority on syntax.

## Setup

```bash
asimov --version
```

If missing, ask for the user's approval, then follow instructions at:
<https://github.com/asimov-platform/asimov-cli#installation>

## Modules

Modules unlock particular data sources. The lifecycle:

```bash
asimov module search <terms...>   # find modules in the live index
asimov module install <name>
asimov module inspect <name>      # manifest, state, config status
asimov module doc <name>          # the module's README: provider specifics, source URL formats
asimov module enable <name>
asimov module resolve <url>       # which enabled module handles this source
asimov module uninstall <name>
```

`inspect` prints a hint for anything that still needs doing. Configuration
lives under `asimov module config` (`show`, `get`, `set`, `setup`, `unset`).
For secrets or interactive setup prefer asking the user to run `asimov module
config setup <name>` in their own terminal rather than handling secrets
yourself.

## Retrieval

The programs provided by a module (as listed by `inspect`) name the types of
operations the module implements:

| Program       | Command        | Function                                                            |
| ------------- | -------------- | ------------------------------------------------------------------- |
| `*-lister`    | `asimov list`  | Enumerates the resources a source URL contains (mailbox, feed, ...) |
| `*-fetcher`   | `asimov fetch` | Retrieves a single resource by URL                                  |
| `*-reader`    | `asimov read`  | Imports data from a local file or standard input                    |
| `*-prompter`  | `asimov ask`   | Sends a prompt to the model provider the module wraps               |

### Resources & Collections

Use `asimov fetch` to retrieve single resources, but `asimov list` to
enumerate subresources contained in collection resources (e.g. a set of
profiles, bookmarks, emails, etc). Collection resources may contain thousands,
millions, or even billions of resources, so you will generally want to make
sure to use `asimov list --limit=N` to limit the maximum number of resources
to return. You can combine that with `asimov list --offset=N` for pagination.

(`asimov fetch` will tell you if a given URL is a collection resource, and will
give you the count of subresources it contains, without actually fetching any.)

### Token Efficiency

Use `asimov fetch --jq=EXPR` or `asimov list --jq=EXPR` to extract specific
fields from resources and/or to filter which resources are returned.

## Examples

The user wants their browser bookmarks in context:

```console
$ asimov module search bookmarks
chromium  Chromium (and Brave, Google Chrome, Arc) bookmark import.

$ asimov module install chromium   # auto-enables when there is nothing to configure

$ asimov module resolve chrome://bookmarks
chromium

$ asimov list chrome://bookmarks   # also chromium://, brave://, arc://, …
{"@context":{…},"items":[{"@id":"urn:uuid:","@type":"know:Bookmark","created":"2025-09-27T04:30:00.000000Z","title":"ASIMOV Platform · GitHub","link":"https://github.com/asimov-platform"},…]}

$ asimov list --module chromium chrome://bookmarks   # same, with the module pinned explicitly
```

(URLs resolve to modules automatically: `resolve` checks and `-M` are optional.)

## Links

- The specification: <https://asimov-specs.github.io/program-patterns/>
- The platform, CLI, and SDK: <https://github.com/asimov-platform>
- The public modules registry: <https://github.com/asimov-modules>
- The company leading the project: <https://github.com/asimov-systems>

## Nomenclature

The platform name is spelled ASIMOV, never Asimov. (Isaac Asimov was the sci-fi
author whose works on robotics inspired the project, not the project itself.)
While the user might very well inadvertently refer to the project as "Asimov",
the actual name is always and everywhere "ASIMOV".
