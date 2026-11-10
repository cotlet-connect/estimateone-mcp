# How to connect EstimateOne to Claude Code, ChatGPT and any AI agent

**Yes, Claude, ChatGPT and other AI agents can work in your EstimateOne account.** EstimateOne's External API is read-only, partner-only and returns Speci-finder matches. Cotlet.dev connects your own signed-in EstimateOne account to any AI agent, so the AI finds, sorts and tracks tenders for you.

## What you can ask

> Find open tenders in Melbourne for electrical work closing in the next 14 days.

> Which new Speci-finder matches came in this week? Rank them by project value.

> Download the documents for the Westgate school tender and list the files.

> Mark these 5 tenders as quoting and remind me 3 days before each closes.

> Which builders invited us to quote this month?

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

This repo is a real MCP server. It speaks MCP over stdio, lists its EstimateOne tools without any key, and forwards every tool call to the hosted Cotlet.dev server. The hosted URL above stays the recommended way. Use this when your client only starts local servers.

```json
{"mcpServers":{"estimateone":{"command":"uvx","args":["estimateone-mcp"],"env":{"COTLET_API_KEY":"your-key"}}}}
```

Or with Docker:

```bash
docker build -t estimateone-mcp .
docker run -i --rm -e COTLET_API_KEY estimateone-mcp
```

Tools: `estimateone_guide`, `estimateone_status`, `estimateone_open`, `estimateone_read`, `estimateone_click`, `estimateone_type`, `estimateone_close`. Without `COTLET_API_KEY` a tool call answers: "Set COTLET_API_KEY. Get a key at https://cotlet.dev/app".

## Command line

Python 3.10+, nothing else to install. From PyPI:

```bash
pip install estimateone-mcp        # or run it once: uvx estimateone-mcp connect
estimateone-mcp connect
```

Or straight from this repo:

```bash
export COTLET_API_KEY="your-key"
python3 estimateone_agent.py connect   # ready config for Claude Code, Cursor, ChatGPT
python3 estimateone_agent.py status    # is EstimateOne ready in your Cotlet.dev account
python3 estimateone_agent.py guide     # EstimateOne screens and sign-in link
python3 estimateone_agent.py read      # open EstimateOne, read the page, close the browser
python3 estimateone_agent.py tools     # list Cotlet.dev tools
python3 estimateone_agent.py serve     # start the stdio MCP server (same as no argument)
```

## Questions from EstimateOne users

**Does EstimateOne have an API?**

EstimateOne has an External API for partner software: read-only, set up by EstimateOne per customer, returning Speci-finder matches. Cotlet.dev works in your own EstimateOne account, so your AI agent can do more without partner access.

**Is there an EstimateOne connector for ChatGPT or Claude?**

EstimateOne has no connector of its own for ChatGPT or Claude. Cotlet.dev adds one to both.

**How do I connect EstimateOne to ChatGPT?**

Add Cotlet.dev as an app in ChatGPT (Settings → Apps, connector URL `https://cotlet.dev/mcp/v1`), sign in to EstimateOne once in your Cotlet.dev Cloud Browser, and ask ChatGPT in plain words. No code and no EstimateOne API key.

**Is there a way to use Claude with EstimateOne?**

Yes. In Claude Code run the one-line `claude mcp add` command above; in the Claude app add `https://cotlet.dev/mcp/v1` as a custom connector. Claude then works in your own EstimateOne account.

## Find it on

- [EstimateOne on Cotlet.dev](https://cotlet.dev/integrations/estimateone-api-mcp-server?utm_source=github&utm_medium=readme&utm_campaign=estimateone&utm_content=find)
- [PyPI package estimateone-mcp](https://pypi.org/project/estimateone-mcp/)
- [Glama](https://glama.ai/mcp/servers/cotlet-connect/estimateone-mcp)
- [LobeHub](https://lobehub.com/mcp/cotlet-connect-estimateone-mcp)
- [Step-by-step guide (PDF) on Internet Archive](https://archive.org/details/cotlet-connect-estimateone-to-ai-agents-guide)

## Also works with

- [Housecall Pro MCP](https://github.com/cotlet-connect/housecall-pro-mcp)
- [Mangomint MCP](https://github.com/cotlet-connect/mangomint-mcp)
- [Wanderlog MCP](https://github.com/cotlet-connect/wanderlog-mcp)
- [SmugMug MCP](https://github.com/cotlet-connect/smugmug-mcp)
- [Garmin Connect MCP](https://github.com/cotlet-connect/garmin-mcp)
- [Medium MCP](https://github.com/cotlet-connect/medium-mcp)
- [Crexi MCP](https://github.com/cotlet-connect/crexi-mcp)
- [DistroKid MCP](https://github.com/cotlet-connect/distrokid-mcp)
- [LinkedIn MCP](https://github.com/cotlet-connect/linkedin-mcp)
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
- [Buildertrend MCP](https://github.com/cotlet-connect/buildertrend-mcp)
- [Fresha MCP](https://github.com/cotlet-connect/fresha-mcp)
- [Booksy MCP](https://github.com/cotlet-connect/booksy-mcp)
- [BookingKoala MCP](https://github.com/cotlet-connect/bookingkoala-mcp)
- [Milanote MCP](https://github.com/cotlet-connect/milanote-mcp)
- [Partiful MCP](https://github.com/cotlet-connect/partiful-mcp)
- [Contractor Foreman MCP](https://github.com/cotlet-connect/contractor-foreman-mcp)
- [Pixieset MCP](https://github.com/cotlet-connect/pixieset-mcp)
- [GlossGenius MCP](https://github.com/cotlet-connect/glossgenius-mcp)
- [ZenMaid MCP](https://github.com/cotlet-connect/zenmaid-mcp)
- [FieldEdge MCP](https://github.com/cotlet-connect/fieldedge-mcp)
- [Phorest MCP](https://github.com/cotlet-connect/phorest-mcp)
- [DINGG MCP](https://github.com/cotlet-connect/dingg-mcp)
- [Invoice Simple MCP](https://github.com/cotlet-connect/invoice-simple-mcp)
- [PhotoShelter MCP](https://github.com/cotlet-connect/photoshelter-mcp)
- [RazorSync MCP](https://github.com/cotlet-connect/razorsync-mcp)
- [ShootProof MCP](https://github.com/cotlet-connect/shootproof-mcp)
- [Invoice2go MCP](https://github.com/cotlet-connect/invoice2go-mcp)
- [Appointy MCP](https://github.com/cotlet-connect/appointy-mcp)
- [Contractor+ MCP](https://github.com/cotlet-connect/contractor-plus-mcp)
- [Teachers Pay Teachers MCP](https://github.com/cotlet-connect/teachers-pay-teachers-mcp)
- [Bloom MCP](https://github.com/cotlet-connect/bloom-mcp)
- [All apps connected through Cotlet.dev](https://github.com/cotlet-connect)

---

More: https://cotlet.dev/integrations/estimateone-api-mcp-server?utm_source=github&utm_medium=readme&utm_campaign=estimateone

Start free: https://cotlet.dev/signup?app=estimateone&utm_source=github&utm_medium=readme&utm_campaign=estimateone
