# Motion Menu — MCP server metadata

This repository holds only the public metadata for the Motion Menu MCP server
(`server.json`, registry id `io.github.dev55acc-ai/motion-menu`) plus this README. It exists
so directories that require a **public** GitHub repository URL to review a listing — mcp.pub,
Glama, mcp.directory — have somewhere to point.

**The pattern library itself is not in this repository.** See [LICENSE](./LICENSE).

## What Motion Menu is

596 motion/3D UI patterns — scroll-driven WebGL, shader passes, spring choreography — as
transplantable HTML/CSS/JS an agent reads directly and drops into a page. Filed into 26
collections by page role. Served over MCP, plain HTTP, and a shadcn registry.

- **Free tier**: 26 patterns, no card, no expiry.
- **Lifetime**: $149 once — all 596 patterns, all themes, compose, publish, yours forever. No
  subscriptions, no seats, no renewal.

(Both figures as stated live on [/store](https://motion-menu-two.vercel.app/store) and
[/connect](https://motion-menu-two.vercel.app/connect).)

## MCP endpoint

```
https://motion-menu-two.vercel.app/api/mcp
```

JSON-RPC 2.0, streamable-http, single POST. `initialize` returns teaching instructions; no key
needed to initialize, list tools, or call the free ones.

## Connect

Claude Code:

```
claude mcp add --transport http motion-menu https://motion-menu-two.vercel.app/api/mcp \
  --header "Authorization: Bearer ${MOTION_MENU_KEY}"
```

Cursor / Windsurf (`mcp.json`):

```json
{
  "mcpServers": {
    "motion-menu": {
      "url": "https://motion-menu-two.vercel.app/api/mcp",
      "headers": { "Authorization": "Bearer ${MOTION_MENU_KEY}" }
    }
  }
}
```

Plain HTTP, no MCP client needed:

```
curl -H "Authorization: Bearer mm_live_..." https://motion-menu-two.vercel.app/p/150.json
curl https://motion-menu-two.vercel.app/kit.md   # public index + rules, no key
```

shadcn registry:

```
npx shadcn@latest add "https://motion-menu-two.vercel.app/r/<slug>.json?framework=react"
```

## Workflow

`initialize` (read the instructions) → `get_design_digest` → `recommend_patterns` →
`validate_combination` → `compose_page` → `get_pattern`. `get_kit` is the one-call overview —
design laws plus the full index in a single response.

`list_patterns`, `list_themes`, `get_kit`, `recommend_patterns`, and `validate_combination` cost
nothing regardless of pattern count.

## Install as a Claude Code plugin

This repo is also a Claude Code plugin marketplace — it points at the same hosted MCP endpoint
above, no local server, nothing to build.

```
/plugin marketplace add dev55acc-ai/motion-menu-mcp
/plugin install motion-menu@motion-menu
```

That registers the `motion-menu` MCP server (`.mcp.json` at repo root, streamable-http, no key
needed to initialize / list tools / call the free ones) as a Claude Code plugin. See
`.claude-plugin/plugin.json` and `.claude-plugin/marketplace.json` for the manifest.

## Links

- [/store](https://motion-menu-two.vercel.app/store) — get a key, pricing, integration snippets
- [/connect](https://motion-menu-two.vercel.app/connect) — this content, for humans
- [/catalogue](https://motion-menu-two.vercel.app/catalogue) — browse the library
- [/docs](https://motion-menu-two.vercel.app/docs) — quickstart and the full HTTP surface reference

## This repo

Contents are limited to `server.json` and this README — nothing else. No pattern source, no
compiled library modules, no internal documentation. Kept in sync by hand when `server.json`
changes on `main` of the private product repository.
