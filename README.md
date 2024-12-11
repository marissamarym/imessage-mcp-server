# AppleScript MCP Server

⚠️ DISCLAIMER - USE AT YOUR OWN RISK ⚠️
This software is provided as-is, without any warranties or guarantees.

An MCP server that uses AppleScript to send iMessages and manage contacts.

This server uses AppleScript to interface with macOS Messages and Contacts apps through the Model Context Protocol (MCP). It wraps AppleScript commands in a TypeScript server to allow you to:

- View and search your contacts
- Send iMessages to contacts or phone numbers
- Get confirmation when messages are sent

## Features

### Resources

- Access your contacts via `contacts://all`
- View contact details including names, phone numbers, and email addresses
- All data stays local on your machine

### Tools

- `search_contacts` - Find contacts by name, phone, or email

  - Takes a search query and returns matching contacts
  - Searches across names, phone numbers, and email addresses

- `send_message` - Send an iMessage
  - Takes recipient (phone/email) and message content
  - Sends through your local Messages app
  - Returns confirmation or error details

## Installation

1. Install dependencies:

```bash
npm install
```

2. Build the server:

```bash
npm run build
```

3. Configure Claude Desktop to use the server:

On MacOS: `~/Library/Application Support/Claude/claude_desktop_config.json`

```json
{
  "mcpServers": {
    "applescript": {
      "command": "node",
      "args": ["/path/to/applescript-server/build/server.js"]
    }
  }
}
```

4. Restart Claude Desktop

5. Grant permissions when prompted for:
   - Contacts access
   - Messages access

## Usage

Once installed, you can talk to Claude Desktop naturally:

- "Show me my contacts"
- "Search for contacts named Marissa"
- "Send a message to 555-0123 saying I'll be there in 10 minutes"
- "Send Alice an iMessage asking if we're still on for lunch"

## Security Notes

- All operations happen locally on your machine
- No contact or message data is sent to external servers
- The server requires macOS permissions for Contacts and Messages access
- Messages are sent through your iMessage account

## Development

For development and debugging, use the MCP Inspector:

```bash
npx @modelcontextprotocol/inspector node build/server.js
```

## Requirements

- macOS (for Messages and Contacts integration)
- Node.js 18 or higher
- Claude Desktop
- Active iMessage account

## Troubleshooting

If messages aren't sending:

1. Check Messages app is signed in
2. Verify permissions are granted
3. Look for errors in Claude Desktop logs:

```bash
tail -f ~/Library/Logs/Claude/mcp*.log
```
