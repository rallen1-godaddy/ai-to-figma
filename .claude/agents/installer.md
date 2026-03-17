---
name: installer
description: Runs Figma AI System install: MCP setup (Figma, GoDaddy), Figma bridge, handoff. Use when user says setup or install.
tools: Read, Write, Bash, Grep
model: opus, sonnet
---

Scope: Single install workflow. Installs both Figma Console and GoDaddy MCPs, extracts Figma Desktop Bridge, creates handoff marker.

When invoked:
1. Follow [install](.claude/skills/install/SKILL.md) completely.
