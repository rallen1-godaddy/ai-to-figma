# MCP Configuration Examples

Complete configuration examples for Cursor and Claude Code.

## Cursor (.cursor/mcp.json)

Project-level MCP configuration. Located at project root.

### Complete Example

```json
{
  "mcpServers": {
    "figma-console": {
      "command": "npx",
      "args": ["-y", "figma-console-mcp@latest"],
      "env": {
        "FIGMA_ACCESS_TOKEN": "figd_AbCdEf1234567890",
        "ENABLE_MCP_APPS": "true"
      }
    },
    "godaddy": {
      "url": "https://api.godaddy.com/v1/domains/mcp",
      "transport": "streamable-http"
    }
  }
}
```

### Figma Console Only

```json
{
  "mcpServers": {
    "figma-console": {
      "command": "npx",
      "args": ["-y", "figma-console-mcp@latest"],
      "env": {
        "FIGMA_ACCESS_TOKEN": "figd_YourActualTokenHere",
        "ENABLE_MCP_APPS": "true"
      }
    }
  }
}
```

### GoDaddy Only

```json
{
  "mcpServers": {
    "godaddy": {
      "url": "https://api.godaddy.com/v1/domains/mcp",
      "transport": "streamable-http"
    }
  }
}
```

### Using Environment Variable

Store token in environment instead of config:

```json
{
  "mcpServers": {
    "figma-console": {
      "command": "npx",
      "args": ["-y", "figma-console-mcp@latest"],
      "env": {
        "FIGMA_ACCESS_TOKEN": "${env:FIGMA_ACCESS_TOKEN}",
        "ENABLE_MCP_APPS": "true"
      }
    }
  }
}
```

Then set environment variable:
```bash
export FIGMA_ACCESS_TOKEN=figd_YourTokenHere
```

## Claude Code (~/.claude.json)

Global MCP configuration. Use CLI commands to manage.

### Add via CLI

**Figma Console:**
```bash
claude mcp add \
  -e "FIGMA_ACCESS_TOKEN=figd_YourTokenHere" \
  -e "ENABLE_MCP_APPS=true" \
  figma-console \
  -- npx -y figma-console-mcp@latest
```

**GoDaddy:**
```bash
claude mcp add --transport streamable-http godaddy https://api.godaddy.com/v1/domains/mcp
```

### Manual Configuration

If CLI doesn't support a feature, edit `~/.claude.json` (macOS/Linux) or `%USERPROFILE%\.claude.json` (Windows):

```json
{
  "mcpServers": {
    "figma-console": {
      "command": "npx",
      "args": ["-y", "figma-console-mcp@latest"],
      "env": {
        "FIGMA_ACCESS_TOKEN": "figd_YourTokenHere",
        "ENABLE_MCP_APPS": "true"
      }
    },
    "godaddy": {
      "url": "https://api.godaddy.com/v1/domains/mcp",
      "transport": "streamable-http"
    }
  }
}
```

## Notes

- **figma-console** uses `npx` to always get latest version
- **GoDaddy** is HTTP-based, no authentication needed
- **ENABLE_MCP_APPS** required for Figma Console features
- Config changes require full app restart
- Cursor: project-level (`.cursor/mcp.json`)
- Claude Code: global (`~/.claude.json`)

## Validation

After adding MCPs:

1. Restart your app completely
2. Open the project
3. Run `/mcp` to see available servers
4. Complete OAuth for figma-console if prompted
5. Test: "Design a button in Figma" or "Check if example.com is available"
