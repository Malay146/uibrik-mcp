# uibrik MCP server

[![uibrik MCP connector](https://glama.ai/mcp/connectors/com.uibrik/components/badges/score.svg)](https://glama.ai/mcp/connectors/com.uibrik/components)

A remote [Model Context Protocol](https://modelcontextprotocol.io) server that lets AI coding agents search [uibrik](https://uibrik.com)'s animated React components and install them into your project.

- **Endpoint:** `https://uibrik.com/mcp` (Streamable HTTP)
- **Auth:** none, no API key
- **Registry name:** `com.uibrik/components` in the [official MCP Registry](https://registry.modelcontextprotocol.io)

The server is hosted by uibrik. This repository documents it and holds ready-to-copy client configs; the server's source is not included. The free components it serves are open source at [Malay146/uibrik](https://github.com/Malay146/uibrik).

## What it does

Ask your agent for UI ("add a pricing toggle", "an animated hero headline", "a dark shader background") and it can:

1. search the catalog by what a component does,
2. read its props, npm dependencies and import line,
3. install the source with the shadcn CLI, so the code lives in your repo with nothing to import at runtime.

Components are built with React, Tailwind CSS v4 and Motion.

## Tools

| Tool | Arguments | Returns |
| --- | --- | --- |
| `search_components` | `query`, `category?`, `limit?` | Components that match what you describe, with slugs |
| `get_component` | `slug`, `include_source?` | Description, install command, npm packages, import line, props and the source of every file |
| `list_categories` | none | The catalog by section and category, with every slug |
| `get_install_instructions` | `framework?` | Project setup for Next.js, Vite or a manual copy |

## Connect

### Claude Code

```bash
claude mcp add --transport http uibrik https://uibrik.com/mcp
```

### Cursor

Add to `.cursor/mcp.json` ([example](examples/cursor-mcp.json)):

```json
{
  "mcpServers": {
    "uibrik": {
      "url": "https://uibrik.com/mcp"
    }
  }
}
```

### VS Code

Add to `.vscode/mcp.json` ([example](examples/vscode-mcp.json)):

```json
{
  "servers": {
    "uibrik": {
      "type": "http",
      "url": "https://uibrik.com/mcp"
    }
  }
}
```

### Claude Desktop, Windsurf and other clients

Add a remote HTTP server named `uibrik` with the URL `https://uibrik.com/mcp`. For clients that only speak stdio, bridge it with [mcp-remote](https://www.npmjs.com/package/mcp-remote) ([example](examples/claude-desktop.json)):

```json
{
  "mcpServers": {
    "uibrik": {
      "command": "npx",
      "args": ["-y", "mcp-remote", "https://uibrik.com/mcp"]
    }
  }
}
```

### Check the connection

Ask your agent to call `list_categories`. It should answer with the uibrik catalog.

## Example prompts

- "Find a uibrik component for an OTP input and add it to the sign-in page."
- "Use uibrik to add an animated pricing toggle to the pricing section."
- "List uibrik's shader backgrounds and put a subtle one behind the hero."

## Without MCP

Every component also installs with the shadcn CLI:

```bash
npx shadcn@latest add https://uibrik.com/r/accordion.json
```

## Links

- Components and live demos: https://uibrik.com/components
- MCP docs: https://uibrik.com/docs/mcp
- Open-source components: https://github.com/Malay146/uibrik
- Issues: [open one here](../../issues)

## License

The documentation and examples in this repository are MIT licensed.
