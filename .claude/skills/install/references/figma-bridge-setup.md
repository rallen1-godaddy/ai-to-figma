# Figma Desktop Bridge Setup

The Figma Desktop Bridge plugin enables real-time communication between the AI system and Figma. Required for design creation and manipulation.

## What It Does

- Connects Figma Desktop to the MCP server
- Enables plugin API access (create designs, modify components, manage variables)
- Provides real-time design manipulation
- Monitors design changes and captures screenshots

## Installation

### 1. Extract the bridge

From repo root:
```bash
npm run setup:figma-bridge
```

This extracts the plugin to `assets/figma-desktop-bridge/`.

### 2. Import in Figma Desktop

**Important:** Must use Figma Desktop app, not browser.

1. Open Figma Desktop
2. Open any project
3. Click the **Plugins icon** in the bottom nav bar
4. Search for **"import"** and select **"Import plugin from manifest"**
5. Navigate to: `assets/figma-desktop-bridge/manifest.json`
6. Click Open/Import
7. Plugin appears in Development plugins list

### 3. Run the bridge

Every time you want to use the AI system with Figma:

1. Open your Figma file
2. Click the **Plugins icon** in the bottom nav bar
3. Search for **"Figma Desktop Bridge"** and click to run
4. Keep it running in the background (small window appears - don't close it)

## Usage

- **Start:** Run the plugin before using AI design features
- **Keep running:** Leave it open while working
- **Per file:** Must run it in each file you want to design in
- **Restart:** If connection drops, close and rerun the plugin

## Troubleshooting

**Plugin not appearing in menu:**
- Make sure you imported it correctly
- Check Development plugins list
- Reimport if needed

**Connection issues:**
- Restart Figma Desktop
- Rerun the plugin
- Check that figma-console MCP is running

**Token expired:**
- Run `/update-figma` to set new token
- Restart Figma Desktop
- Rerun the bridge plugin

**Can't find manifest.json:**
- Run `npm run setup:figma-bridge` again
- Check `assets/figma-desktop-bridge/` exists
- Verify you're in the correct repo root

## Technical Details

- **Protocol:** WebSocket communication
- **Port:** Dynamic (assigned by Figma)
- **Scope:** Single file per instance
- **Persistence:** Must restart for each Figma session
