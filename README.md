# Motion Menu — MCP server

597 motion/3D UI patterns — scroll-driven WebGL, shader passes, spring choreography — as
transplantable HTML/CSS/JS an agent reads directly and drops into a page. Filed into 26
collections by page role. Served over MCP, plain HTTP, and a shadcn registry.

- **Free**: 26 patterns, no card, no expiry.
- **Lifetime**: $149 once — all 597 patterns, every framework wrapper, yours forever.
  No subscriptions, no seats, no renewal.

## MCP endpoint

```
https://www.motionmenu.ca/api/mcp
```

JSON-RPC 2.0, streamable-http, single POST. `initialize` returns teaching instructions; no key
needed to initialize, list tools, or call the free ones.

## Connect

Claude Code:

```
claude mcp add --transport http motion-menu https://www.motionmenu.ca/api/mcp \
  --header "Authorization: Bearer ${MOTION_MENU_KEY}"
```

Cursor / Windsurf (`mcp.json`):

```json
{
  "mcpServers": {
    "motion-menu": {
      "url": "https://www.motionmenu.ca/api/mcp",
      "headers": { "Authorization": "Bearer ${MOTION_MENU_KEY}" }
    }
  }
}
```

Cline: see [llms-install.md](./llms-install.md).

Plain HTTP, no MCP client needed:

```
curl -H "Authorization: Bearer mm_live_..." https://www.motionmenu.ca/p/150.json
curl https://www.motionmenu.ca/kit.md   # public index + rules, no key
```

shadcn registry:

```
npx shadcn@latest add "https://www.motionmenu.ca/r/<slug>.json?framework=react"
```

Claude Code plugin (optional — same endpoint, plus a skill teaching the workflow):

```
/plugin marketplace add dev55acc-ai/motion-menu-plugin
/plugin install motion-menu-patterns@motion-menu
```

## Workflow

`initialize` (read the instructions) → `get_design_digest` → `recommend_patterns` →
`validate_combination` → `compose_page` → `get_pattern`. `get_kit` is the one-call overview —
design laws plus the full index in a single response.

`list_patterns`, `list_themes`, `get_kit`, `recommend_patterns`, and `validate_combination` cost
nothing regardless of pattern count.

## Links

- [/store](https://www.motionmenu.ca/store) — get a key, pricing, integration snippets
- [/catalogue](https://www.motionmenu.ca/catalogue) — browse the library
- [/docs](https://www.motionmenu.ca/docs) — quickstart and the full HTTP surface reference

---

This repository is the server's public metadata (`server.json`, registry id
`io.github.dev55acc-ai/motion-menu`) and install docs. The pattern library is commercial and
lives at [www.motionmenu.ca](https://www.motionmenu.ca) — see
[LICENSE](./LICENSE).
