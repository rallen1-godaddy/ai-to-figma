<p align="center"><strong>Figma AI System</strong><br/>Simplified agent system for AI-powered Figma design workflows</p>

> Streamlined system with Figma Console MCP and GoDaddy domain search. Create designs, manage tokens, and explore domains through natural language.

---

## What's Included

**Agents:**
- **[designer](.claude/agents/designer.md)** – Create or update Figma designs via Figma Console MCP
- **[installer](.claude/agents/installer.md)** – Install system with Figma and GoDaddy MCP servers
- **[uninstaller](.claude/agents/uninstaller.md)** – Remove MCP entries from config

**Skills:**

All skills use "use when" descriptions to trigger automatically.

- **[designer-figma](.claude/skills/designer-figma/SKILL.md)** – Generate or update Figma designs via MCP
- **[skill-mama](.claude/skills/skill-mama/SKILL.md)** – Write and update skills
- **[update-figma](.claude/skills/update-figma/SKILL.md)** – Update Figma API token
- **[install](.claude/skills/install/SKILL.md)** – Complete system installation (MCPs, bridge, config)
- **[uninstall](.claude/skills/uninstall/SKILL.md)** – Remove MCP entries from config

**MCP Servers:**
- **Figma Console** – Full Figma API and Plugin API access for design creation and manipulation
- **GoDaddy** – Domain search and availability checking

---

## Installation

From the system directory:

```bash
# Run installer agent
/install
```

The installer will:
1. Show hidden files for easier navigation
2. Collect your Figma personal access token
3. Install both MCP servers (Figma Console + GoDaddy)
4. Extract Figma Desktop Bridge plugin
5. Guide you through importing the bridge in Figma Desktop
6. Create handoff marker for OAuth

After install, fully restart your app, then run `/mcp` for OAuth where needed.

---

## Quick Start

**Design with Figma:**
```
Design a landing page hero in Figma
```

**Check domain availability:**
```
Check if myawesomesite.com is available
```

**Update Figma token:**
```
Update my Figma API token
```

---

## System Rules

The system follows these rules (defined in [AGENTS.md](AGENTS.md)):

**1. VOICE** – Apply [document-voice](../../../../.claude/skills/document-voice/SKILL.md) to every response and written output. Always.

**2. MARKER** – If `install-handoff.marker` exists: tell user to run `/mcp` to OAuth, then delete the marker. Fast check. Then continue.

---

## Structure

```
.
├── AGENTS.md              # Main system instructions
├── CLAUDE.md              # Symlink to AGENTS.md
├── README.md              # This file
└── .claude/
    ├── agents/            # Agent definitions
    │   ├── designer.md
    │   ├── installer.md
    │   └── uninstaller.md
    └── skills/            # Skill definitions
        ├── designer-figma/
        ├── skill-mama/
        ├── update-figma/
        ├── install/       # Complete install workflow
        │   ├── SKILL.md
        │   └── references/  # Detailed guides
        └── uninstall/
```

---

## MCP Servers

### Figma Console

Full Figma API and Plugin API access. Create designs, manipulate components, manage variables, and execute arbitrary Figma plugin code.

**Requirements:**
- Figma personal access token (get from Figma → Settings → Security)
- Figma Desktop Bridge plugin (for Prompt to Figma features)

**Setup:** Run `npm run setup:figma-bridge` to extract the bridge plugin, then import in Figma Desktop → Plugins → Development → Import plugin from manifest.

**Documentation:** [Figma Console MCP](https://github.com/thatguyinabeanie/figma-mcp-server)

### GoDaddy

Domain search and availability checking. Public API, no authentication required.

**Features:**
- Domain suggestions based on keywords or seed domains
- Availability checking for single or bulk domains
- Direct registration links

**Documentation:** [GoDaddy MCP](https://developer.godaddy.com/mcp)

---

## Uninstall

To remove all MCP servers:

```bash
/uninstall
```

This removes Figma Console and GoDaddy from your config. Fully restart your app after uninstalling.

---

## License

Same as parent repository.

---

<p align="center">Built with Claude Code</p>
