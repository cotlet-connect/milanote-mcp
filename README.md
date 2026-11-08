# How to connect Milanote to Claude Code, ChatGPT and any AI agent

**Yes, Claude, ChatGPT and other AI agents can work in your Milanote account.** There is no official Milanote app in ChatGPT's apps directory and no official Milanote connector in Claude's directory. Cotlet.dev connects your own signed-in Milanote account to any AI agent, so you can ask in plain words and the AI sorts your ideas, notes and references into organized boards for you.

## What you can ask

> Create a board called "Spring launch 2027" with columns for Ideas, In progress and Done, then sort my loose notes into them.

> Turn the notes from Tuesday's meeting with Priya into a to-do list on the "Bloom Bakery" board.

> Add these 12 reference links to my "Brand moodboard" board, one card each with a short caption.

> Summarize everything on the "Q1 content plan" board in 5 bullet points and add the summary as a note at the top.

> Move every finished board with "2026" in the title into a new board called "Archive 2026".

## Connect in 2 minutes

Get your API key at https://cotlet.dev/app and export it as `COTLET_API_KEY`.

### Claude Code

```bash
claude mcp add --transport http cotlet https://cotlet.dev/mcp/v1 --header "Authorization: Bearer $COTLET_API_KEY"
```

### ChatGPT

Settings → Apps → add connector URL `https://cotlet.dev/mcp/v1`, then sign in with Cotlet.dev. No API key needed.

### Cursor

Copy `.cursor/mcp.json` from this repo into your project:

```json
{
  "mcpServers": {
    "cotlet": {
      "url": "https://cotlet.dev/mcp/v1",
      "headers": {
        "Authorization": "Bearer ${COTLET_API_KEY}"
      }
    }
  }
}
```

## Run it locally (stdio)

This repo is a real MCP server. It speaks MCP over stdio, lists its Milanote tools without any key, and forwards every tool call to the hosted Cotlet.dev server. The hosted URL above stays the recommended way. Use this when your client only starts local servers.

```json
{"mcpServers":{"milanote":{"command":"uvx","args":["milanote-mcp"],"env":{"COTLET_API_KEY":"your-key"}}}}
```

Or with Docker:

```bash
docker build -t milanote-mcp .
docker run -i --rm -e COTLET_API_KEY milanote-mcp
```

Tools: `milanote_guide`, `milanote_status`, `milanote_open`, `milanote_read`, `milanote_click`, `milanote_type`, `milanote_close`. Without `COTLET_API_KEY` a tool call answers: "Set COTLET_API_KEY. Get a key at https://cotlet.dev/app".

## Command line

Python 3.10+, nothing else to install. From PyPI:

```bash
pip install milanote-mcp        # or run it once: uvx milanote-mcp connect
milanote-mcp connect
```

Or straight from this repo:

```bash
export COTLET_API_KEY="your-key"
python3 milanote_agent.py connect   # ready config for Claude Code, Cursor, ChatGPT
python3 milanote_agent.py status    # is Milanote ready in your Cotlet.dev account
python3 milanote_agent.py guide     # Milanote screens and sign-in link
python3 milanote_agent.py read      # open Milanote, read the page, close the browser
python3 milanote_agent.py tools     # list Cotlet.dev tools
python3 milanote_agent.py serve     # start the stdio MCP server (same as no argument)
```

## Questions from Milanote users

**Does Milanote have an API?**

You don't need one. Cotlet.dev works in your own signed-in Milanote account, so your AI agent can create boards, add notes and organize cards without a Milanote API key.

**How do I connect Milanote to ChatGPT?**

Add Cotlet.dev as an app in ChatGPT (Settings → Apps, connector URL `https://cotlet.dev/mcp/v1`), sign in to Milanote once in your Cotlet.dev Cloud Browser, and ask ChatGPT in plain words. No code and no Milanote API key.

**Is there a way to use Claude with Milanote?**

Yes. In Claude Code run the one-line `claude mcp add` command above; in the Claude app add `https://cotlet.dev/mcp/v1` as a custom connector. Claude then works in your own Milanote account.

**Is there a Milanote MCP server?**

Milanote has no official MCP server listed in the ChatGPT or Claude directories. Cotlet.dev is a hosted MCP server that works in Milanote for you, 24/7, with Claude, ChatGPT, Cursor, Codex, n8n, Make and Zapier.

## Find it on

- [Milanote on Cotlet.dev](https://cotlet.dev/integrations/milanote-api-mcp-server?utm_source=github&utm_medium=readme&utm_campaign=milanote&utm_content=find)
- [PyPI package milanote-mcp](https://pypi.org/project/milanote-mcp/)
- [Step-by-step guide (PDF) on Internet Archive](https://archive.org/details/cotlet-connect-milanote-to-ai-agents-guide)

## Also works with

- [Mangomint MCP](https://github.com/cotlet-connect/mangomint-mcp)
- [Wanderlog MCP](https://github.com/cotlet-connect/wanderlog-mcp)
- [SmugMug MCP](https://github.com/cotlet-connect/smugmug-mcp)
- [Garmin Connect MCP](https://github.com/cotlet-connect/garmin-mcp)
- [Housecall Pro MCP](https://github.com/cotlet-connect/housecall-pro-mcp)
- [Medium MCP](https://github.com/cotlet-connect/medium-mcp)
- [Crexi MCP](https://github.com/cotlet-connect/crexi-mcp)
- [DistroKid MCP](https://github.com/cotlet-connect/distrokid-mcp)
- [LinkedIn MCP](https://github.com/cotlet-connect/linkedin-mcp)
- [EstimateOne MCP](https://github.com/cotlet-connect/estimateone-mcp)
- [Google Search Console MCP](https://github.com/cotlet-connect/google-search-console-mcp)
- [Lichess MCP](https://github.com/cotlet-connect/lichess-mcp)
- [Strava MCP](https://github.com/cotlet-connect/strava-mcp)
- [StreamElements MCP](https://github.com/cotlet-connect/streamelements-mcp)
- [Meetup MCP](https://github.com/cotlet-connect/meetup-mcp)
- [AccuRanker MCP](https://github.com/cotlet-connect/accuranker-mcp)
- [GetYourGuide MCP](https://github.com/cotlet-connect/getyourguide-mcp)
- [Idealista MCP](https://github.com/cotlet-connect/idealista-mcp)
- [Riverside MCP](https://github.com/cotlet-connect/riverside-mcp)
- [Udemy MCP](https://github.com/cotlet-connect/udemy-mcp)
- [Faire MCP](https://github.com/cotlet-connect/faire-mcp)
- [Teachable MCP](https://github.com/cotlet-connect/teachable-mcp)
- [Vagaro MCP](https://github.com/cotlet-connect/vagaro-mcp)
- [Buildertrend MCP](https://github.com/cotlet-connect/buildertrend-mcp)
- [Zoopla MCP](https://github.com/cotlet-connect/zoopla-mcp)
- [Dribbble MCP](https://github.com/cotlet-connect/dribbble-mcp)
- [Hostelworld MCP](https://github.com/cotlet-connect/hostelworld-mcp)
- [Mashvisor MCP](https://github.com/cotlet-connect/mashvisor-mcp)
- [Rent Manager MCP](https://github.com/cotlet-connect/rent-manager-mcp)
- [ThriveCart MCP](https://github.com/cotlet-connect/thrivecart-mcp)
- [Fresha MCP](https://github.com/cotlet-connect/fresha-mcp)
- [Booksy MCP](https://github.com/cotlet-connect/booksy-mcp)
- [BookingKoala MCP](https://github.com/cotlet-connect/bookingkoala-mcp)
- [Partiful MCP](https://github.com/cotlet-connect/partiful-mcp)
- [Contractor Foreman MCP](https://github.com/cotlet-connect/contractor-foreman-mcp)
- [Pixieset MCP](https://github.com/cotlet-connect/pixieset-mcp)
- [GlossGenius MCP](https://github.com/cotlet-connect/glossgenius-mcp)
- [ZenMaid MCP](https://github.com/cotlet-connect/zenmaid-mcp)
- [All apps connected through Cotlet.dev](https://github.com/cotlet-connect)

---

More: https://cotlet.dev/integrations/milanote-api-mcp-server?utm_source=github&utm_medium=readme&utm_campaign=milanote

Start free: https://cotlet.dev/signup?app=milanote&utm_source=github&utm_medium=readme&utm_campaign=milanote
