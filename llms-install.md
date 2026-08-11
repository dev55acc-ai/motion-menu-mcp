# Installing the Motion Menu MCP server in Cline

Remote server, streamable-http, no API key required for the free tier (26 of 596 patterns,
`list_patterns`, `list_themes`, `get_kit`, `recommend_patterns`, `validate_combination`).

## Install

```
cline mcp install motion-menu https://motion-menu-two.vercel.app/api/mcp --transport streamable-http --yes
```

This writes a `streamableHttp` entry to Cline's MCP settings:

```json
{
  "mcpServers": {
    "motion-menu": {
      "transport": {
        "type": "streamableHttp",
        "url": "https://motion-menu-two.vercel.app/api/mcp"
      }
    }
  }
}
```

No further configuration is needed to use the free tier.

Two things were separately verified 2026-08-10, not conflated:

- **The install command itself**, in a fresh isolated Cline CLI profile
  (`cline --config <empty dir> --data-dir <empty dir> mcp install …`): it returns
  `{"status":"installed","warnings":[]}` and writes exactly the `streamableHttp` config block
  above. `cline mcp install` writes local config only — it does not itself call the server.
- **The endpoint**, with a direct JSON-RPC 2.0 handshake over curl (not through Cline):
  `initialize` succeeds, `tools/list` returns 11 tools, and a `tools/call` against the free
  `list_patterns` tool returns pattern rows — all with no key.

## Add a paid key (optional)

To unlock the rest of the 596-pattern catalogue ($149 once, lifetime — see
[/store](https://motion-menu-two.vercel.app/store)), edit the entry above to add a header:

```json
{
  "mcpServers": {
    "motion-menu": {
      "transport": {
        "type": "streamableHttp",
        "url": "https://motion-menu-two.vercel.app/api/mcp",
        "headers": { "Authorization": "Bearer mm_live_..." }
      }
    }
  }
}
```

## What it is

596 motion/3D UI patterns — scroll-driven WebGL, shader passes, spring choreography — as
transplantable HTML/CSS/JS an agent reads directly and drops into a page. See
[README.md](./README.md) for the full call order and other ways to connect.
