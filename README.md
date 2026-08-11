# ASIMOV Skills

[Agent Skills](https://agentskills.io/) for [ASIMOV](https://github.com/asimov-platform), a platform that uses installable modules to fetch knowledge from your data sources, including mail, messages, documents, and public sources. ASIMOV builds a graph-based knowledge base from the results. Installing a skill teaches your agent to set up and drive the [ASIMOV CLI](https://github.com/asimov-platform/asimov-cli).

## Skills

| Skill                    | Teaches                                                            |
| ------------------------ | ------------------------------------------------------------------ |
| [asimov](skills/asimov/) | Find, install, and configure modules; retrieve knowledge with them |

## Installation

Use the [skills CLI](https://skills.sh/) to install them in any supported harness:

```bash
npx skills add asimov-platform/skills
```

Or just ask your agent:

```text
Install the ASIMOV Platform for me: https://github.com/asimov-platform/skills
```
