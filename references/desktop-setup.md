# Claude Desktop → Apple Reminders setup

Claude Desktop on macOS does not have native Reminders access. To use Apple Brain from desktop, install an MCP server that bridges Claude to EventKit.

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

4. Verify: in a new Claude Desktop conversation, ask "list my reminder lists." It should return your `ab.knowledge`, `ab.entities`, and other lists.

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

## Side Reminder integration

If Side Reminder is already installed, the `sidereminder` CLI can be invoked from Claude Code via Bash. This isn't an MCP server — it's a separate path.

Useful Side Reminder slash commands inside Claude Code:
- `/side-reminder-add` — add reminder to a list
- `/side-reminder-gtd` — hand off a reminder as task context to Claude Code

This is the fastest path for "I'm at my MBP and want to write atoms" without any MCP setup.

---

## Once installed

Ask Claude Desktop to test the connection:

> "List the lists in my Apple Reminders."

If it returns `ab.knowledge`, `ab.entities`, etc., the bridge is working. You can now read and write atoms from desktop with the same syntax as voice/iOS.

## Updating this reference

If a new MCP server emerges that's better than the ones above, add it here and update the recommendation in the main SKILL.md.
