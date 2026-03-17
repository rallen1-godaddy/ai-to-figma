---
name: install
description: Install Figma AI System with Figma Console and GoDaddy MCPs. Sets up tokens, bridge, and config. Use when user says install, setup, /install.
disable-model-invocation: true
---

# Install

Complete install of Figma AI System. Installs Figma Console and GoDaddy MCPs, extracts Figma Desktop Bridge, and sets up config.

## Inputs

None. User invokes with install, setup, or /install.

## Output

System installed: both MCPs added to config, Figma Desktop Bridge ready to import, handoff marker created. User must restart app and run `/mcp` for OAuth.

## Process

### 1. Show hidden files

Makes `.claude/` folder visible for easier navigation.

**macOS:**
```bash
defaults write com.apple.finder AppleShowAllFiles TRUE && killall Finder
```
If it fails due to permissions, continue anyway.

**Windows:**
File Explorer → View → Show → Hidden items. (Or Folder Options → View → Show hidden files and folders.)

### 2. Collect Figma token

Get the user's Figma personal access token. See [references/figma-token-guide.md](references/figma-token-guide.md) for detailed instructions.

**Tell user:**
1. Go to Figma → profile icon → Settings → Security
2. Personal access tokens section
3. Create new token:
   - Name: "Figma Console MCP"
   - Scopes: All scopes (full access needed for design creation)
   - Expiration: Up to 90 days
4. Copy the token

**Ask:** Paste your Figma token (starts with `figd_`)

Store the token for step 3.

### 3. Install MCPs

Add both MCPs to config. Always installs both figma-console and godaddy.

#### Cursor (project config)

Read `.cursor/mcp.json` if exists, otherwise start with `{"mcpServers":{}}`.

Add entries:
```json
{
  "mcpServers": {
    "figma-console": {
      "command": "npx",
      "args": ["-y", "figma-console-mcp@latest"],
      "env": {
        "FIGMA_ACCESS_TOKEN": "figd_xxx",
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

Replace `figd_xxx` with the token from step 2. Write `.cursor/mcp.json`, merging with existing servers.

See [references/mcp-config-examples.md](references/mcp-config-examples.md) for complete examples.

#### Claude Code (global config)

Do not edit config files by hand. Use CLI commands only.

**figma-console:**
```bash
claude mcp add -e "FIGMA_ACCESS_TOKEN=figd_xxx" -e "ENABLE_MCP_APPS=true" figma-console -- npx -y figma-console-mcp@latest
```
Replace `figd_xxx` with actual token.

**godaddy:**
```bash
claude mcp add --transport streamable-http godaddy https://api.godaddy.com/v1/domains/mcp
```

If the CLI doesn't support `--transport`, add manually to global config (`~/.claude.json` on macOS/Linux, `%USERPROFILE%\.claude.json` on Windows).

### 4. Extract Figma Desktop Bridge

Run from repo root:
```bash
npm run setup:figma-bridge
```

This extracts the bridge plugin to `assets/figma-desktop-bridge/`.

See [references/figma-bridge-setup.md](references/figma-bridge-setup.md) for detailed setup.

### 5. Import bridge in Figma Desktop

**Show user these steps:**

1. Open Figma Desktop (not browser)
2. Open any project
3. Click the **Plugins icon** in the bottom nav bar
4. Search for **"import"** and select **"Import plugin from manifest"**
5. Navigate to: `assets/figma-desktop-bridge/manifest.json`
6. Import the plugin
7. Run the plugin: Click Plugins icon → Search for "Figma Desktop Bridge" → Click to run
8. Keep the plugin running (small window will appear)

**Important:** The bridge must be running in any file you want to design in with this system. When your token expires (about every 90 days), run [update-figma](../update-figma/SKILL.md) to set a new token, then restart the app.

**Wait for user:** Say "Tell me when you're ready to proceed." Continue only after they confirm.

### 6. Create handoff marker

Create marker file at `.claude/skills/install/install-handoff.marker`. This tells the system install is complete.

**Tell user:**
- Fully restart your app (Cursor, Claude Code, etc.)
- Open the project
- Run `/mcp` to complete OAuth for Figma Console
- GoDaddy needs no sign-in (public API)


## Reference

[designer-figma](../designer-figma/SKILL.md) uses the bridge. [update-figma](../update-figma/SKILL.md) renews token. [uninstall](../uninstall/SKILL.md) removes MCPs.
