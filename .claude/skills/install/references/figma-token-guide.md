# Getting a Figma Personal Access Token

Figma Console MCP requires a personal access token to interact with your Figma files.

## Steps

1. **Open Figma** (web or desktop)
2. **Click your profile icon** (top right)
3. **Settings** → **Security** tab
4. **Personal access tokens** section
5. **Create new token:**
   - **Name:** "Figma Console MCP" (or any descriptive name)
   - **Scopes:** Select all scopes - full access needed for design creation, variable management, and plugin API
   - **Expiration:** Up to 90 days (Figma's maximum)
6. **Copy the token** - starts with `figd_`

## Important Notes

- Save the token immediately - Figma only shows it once
- Token expires in 90 days max
- When it expires, create a new one and run `/update-figma`
- Never commit tokens to git or share publicly
- Each team member needs their own token

## Renewal

When your token expires (about every 90 days):

1. Create a new token (same steps above)
2. Run `/update-figma` or "Update my Figma API token"
3. Paste the new token
4. Restart your app

## Security

Personal access tokens have full access to your Figma account. Treat them like passwords:
- Store securely (never in code)
- Don't share with others
- Rotate regularly
- Revoke unused tokens in Figma Settings
