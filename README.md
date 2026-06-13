# sk-mcp-server-google-calendar

A lightweight Model Context Protocol (MCP) server for reading Google Calendar events by date. This package is intended to be published to npm and run through an MCP client with `npx`.

## What it does

This server exposes one tool:

- `getMyCalendarDataByDate` - fetches calendar events and meetings for a specific date

It returns matching events as simple text entries in the form:

- `Meeting title at 2026-06-16T11:30:00Z`

## Requirements

- Node.js 18 or newer
- A Google Calendar API key
- A Google Calendar ID

## Installation

```bash
npm install
```

If you want to test the published package directly, you can run it with:

```bash
npx -y sk-mcp-server-google-calendar
```

## Environment Variables

Create a `.env` file in the project root with:

```env
GOOGLE_PUBLIC_API_KEY=your_google_api_key
CALENDAR_ID=your_calendar_id
```

## Running the server

Start the MCP server with:

```bash
npm start
```

Or run the executable directly:

```bash
node server.js
```

If installed globally or linked as a package bin, the command is:

```bash
google-calendar-mcp
```

## MCP Tool

### `getMyCalendarDataByDate`

Retrieves Google Calendar events for a given date.

#### Input

- `date` - a valid date string, such as `2026-06-16`

#### Output

Returns JSON text with either:

- `meetings`: an array of event strings
- `error`: an error message if the request fails

## Example MCP Client Configuration

If you are connecting this server from an MCP client after publishing it to npm, use the package name as the command target.

Example:

```json
{
  "mcpServers": {
    "My Calendar": {
      "command": "npx",
      "args": [
        "-y",
        "sk-mcp-server-google-calendar"
      ],
      "env": {
        "GOOGLE_PUBLIC_API_KEY": "your_google_api_key",
        "CALENDAR_ID": "your_calendar_id"
      }
    }
  }
}
```

## Notes

- Event lookup is performed using UTC day boundaries.
- The tool returns up to 10 events for the requested date.
- The server uses standard input/output transport for MCP compatibility.

## License

ISC
