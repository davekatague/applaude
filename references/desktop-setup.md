# Claude Desktop → Apple Reminders setup

Claude Desktop on macOS does not have native Reminders access. To use Applaudé from desktop, install an MCP server that bridges Claude to EventKit.

## Recommended: `mcp-server-apple-events`

Native Swift + EventKit. Supports both Reminders and Calendar. macOS 14+. Best performance and reliability.

### Install

1. Edit `~/Library/Application Support/Claude/claude_desktop_config.json`:

```json
{
  "mcpServers": {
    "apple-events": {
      "command": "npx",
      "args": ["-y", "mcp-server-apple-events"]
    }
  }
}
```

2. Restart Claude Desktop.

3. On first call, macOS will prompt for Reminders + Calendar permission. Approve both.

4. Verify: in a new Claude Desktop conversation, ask "list my reminder lists." It should return your `Captures`, `Knowledge`, `Goals`, `Projects`, and any other lists you've created.

### Troubleshooting

If you see "Failed to read calendar events" or similar:
- Open System Settings → Privacy & Security → Calendars (and Reminders)
- Find the launching app (likely Claude Desktop or Terminal) and grant Full Access
- The repo has a `check-permissions.sh` script that validates both

---

## Alternative: `apple-reminders-mcp` (TypeScript + AppleScript)

Simpler install but slightly slower due to AppleScript overhead. Useful if Swift toolchain is unavailable.

```json
{
  "mcpServers": {
    "reminders": {
      "command": "node",
      "args": ["/absolute/path/to/apple-reminders-mcp/dist/index.js"]
    }
  }
}
```

Setup steps:
1. `git clone https://github.com/dbmcco/apple-reminders-mcp.git`
2. `cd apple-reminders-mcp && npm install && npm run build`
3. Update the path in the config above to the absolute path of your clone.
4. Restart Claude Desktop.

---

## Once installed

Ask Claude Desktop to test the connection:

> "List the lists in my Apple Reminders."

If it returns your lists (`Captures`, `Knowledge`, `Goals`, `Projects`), the bridge is working. You can now read and write atoms from desktop with the same syntax as voice/iOS.

## Updating this reference

If a new MCP server emerges that's better than the ones above, add it here and update the recommendation in the main SKILL.md.
