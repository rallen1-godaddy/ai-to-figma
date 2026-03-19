---
name: uninstall
description: Remove Figma AI System MCP entries from the user's Claude config and Cursor's project MCP config. Use when user says uninstall, /uninstall.
---

# Uninstall

Remove the MCP servers that the Install skill adds (figma-console, godaddy). Config may be global or project-scoped.

## Inputs

None. User invokes with uninstall or /uninstall.

## Output

figma-console and godaddy removed from config. User must fully restart the app.

## Process

### Cursor

If the project has `.cursor/mcp.json`: remove `figma-console` and `godaddy` from `mcpServers`. If `mcpServers` is empty afterward, either delete `.cursor/mcp.json` or leave `{"mcpServers":{}}`. Tell user to fully restart Cursor.

### Claude Code

Do not edit the file by hand. Run from project root:

```bash
claude mcp remove figma-console
claude mcp remove godaddy
```

Tell user to fully restart Claude Code.

## Reference

[install-mcp](.claude/skills/install-mcp/SKILL.md) adds these MCPs. Uninstaller runs when the flow is uninstall.
