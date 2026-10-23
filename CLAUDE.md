# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## This repo is generated. Do not edit it by hand.

It is the output of `connect/make.sh` in [ConniptionFit/career-architect](https://github.com/ConniptionFit/career-architect), run with this deployment's Obot address. Everything here (`.claude-plugin/*.json`, `skills/jobs/SKILL.md`, `README.md`, `LICENSE`) is copied from that template; only `.mcp.json` is deployment-specific (the `jobs` HTTP MCP server address). There is no application code, build, lint or test suite.

To change the plugin, change the template in `career-architect/connect/` (its tests, in `tests/test_connect_plugin.py`, keep it honest), then regenerate:

```
connect/make.sh <this repo's .mcp.json url> /tmp/regen   # in a checkout of career-architect
cp -r /tmp/regen/. .                                     # here; remove any file the template no longer has
```

The `.mcp.json` address is the one to reuse. Changing it breaks every installed connection, and the vMCP id is part of it, so never delete and recreate the vMCP.

## Where things live

- The launcher skill (`skills/jobs/SKILL.md`) is deliberately a ten-line launcher. It tells the assistant to call the connector's `guide` tool (`career_architect__guide`).
- The instructions, rules and workflows are **served live by the connector** from `career-architect/jobs/`: `start`, `workflows/*`, `references/*` (including `references/delegation.md` and the `subagent-*.md` prompts), `style/voice.md`, `assets/*`. To read one, call `guide` with the topic. To change one, edit it in `career-architect/jobs/`, add a `CHANGELOG.md` entry, and deploy the server (`deploy/update.sh`); that is what publishes it to everyone.
- Do not add instructions, templates or copies of guides to this repo. A copy is what goes stale, and `career-architect`'s tests require the launcher to stay under 20 lines with nothing deployment-specific or tool-specific in it.
- Leave `version` out of `plugin.json`. Without it, every commit is delivered as an update; with one, nobody receives a change until it is raised. The template's test enforces this.

## Working here

- Validate manifests: `python3 -m json.tool .claude-plugin/plugin.json` (same for `marketplace.json` and `.mcp.json`).
- Try it in Claude Code: `/plugin marketplace add <owner>/<this repository>`, `/plugin install jobs@career-architect-connect`, then `/mcp` to connect the Jobs connector (sign in with Google through Obot). Use the plugin or a copied skill, not both.
- Quickest connector health check once connected: the `info` and `guide` tools.
