# Installing the Motion Menu MCP server in Cline

Remote server, streamable-http, no API key required for the free tier (26 of 597 patterns,
`list_patterns`, `list_themes`, `get_kit`, `recommend_patterns`, `validate_combination`).

## Install

```
cline mcp install motion-menu https://www.motionmenu.ca/api/mcp --transport streamable-http --yes
```

This writes a `streamableHttp` entry to Cline's MCP settings:

```json
{
  "mcpServers": {
    "motion-menu": {
      "transport": {
        "type": "streamableHttp",
        "url": "https://www.motionmenu.ca/api/mcp"
      }
    }
  }
}
```

No further configuration is needed to use the free tier.

## Add a paid key (optional)

To unlock the rest of the 597-pattern catalogue ($149 once, lifetime — see
[/store](https://www.motionmenu.ca/store)), edit the entry above to add a header:

```json
{
  "mcpServers": {
    "motion-menu": {
      "transport": {
        "type": "streamableHttp",
        "url": "https://www.motionmenu.ca/api/mcp",
        "headers": { "Authorization": "Bearer mm_live_..." }
      }
    }
  }
}
```

## What it is

597 motion/3D UI patterns — scroll-driven WebGL, shader passes, spring choreography — as
transplantable HTML/CSS/JS an agent reads directly and drops into a page. See
[README.md](./README.md) for the full call order and other ways to connect.
