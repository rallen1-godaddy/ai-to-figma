# Figma AI System

## Rules (order is fixed; no other path)

**1. VOICE.** Apply [document-voice](../../../../.claude/skills/document-voice/SKILL.md) to every response and written output. Always.

**2. MARKER.** If `install-handoff.marker` exists: tell user to run `/mcp` to OAuth, then delete the marker. Fast check. Then continue.

## Agents

- [designer](.claude/agents/designer.md): Create or update Figma designs via Figma Console MCP.
- [installer](.claude/agents/installer.md): Install system with Figma and GoDaddy MCP servers.
- [uninstaller](.claude/agents/uninstaller.md): Remove MCP entries from config.

## Skills

Skills use "use when" descriptions to trigger automatically:
- [designer-figma](.claude/skills/designer-figma/SKILL.md): Generate or update Figma designs.
- [skill-mama](.claude/skills/skill-mama/SKILL.md): Write and update skills.
- [update-figma](.claude/skills/update-figma/SKILL.md): Update Figma API token.
- [install](.claude/skills/install/SKILL.md): Complete system installation (MCPs, bridge, config).
- [uninstall](.claude/skills/uninstall/SKILL.md): Remove MCP entries from config.

---
`CLAUDE.md` is a symlink to this file.
