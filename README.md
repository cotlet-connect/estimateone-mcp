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

## Also works with

- [Housecall Pro MCP](https://github.com/cotlet-connect/housecall-pro-mcp)
- [All apps connected through Cotlet.dev](https://github.com/cotlet-connect)

---

More: https://cotlet.dev/integrations/estimateone-api-mcp-server?utm_source=github&utm_medium=readme&utm_campaign=estimateone

Start free: https://cotlet.dev/signup?app=estimateone&utm_source=github&utm_medium=readme&utm_campaign=estimateone
