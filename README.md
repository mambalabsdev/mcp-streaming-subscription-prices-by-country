# Streaming Subscription Prices by Country MCP Server

[![npm version](https://img.shields.io/npm/v/@mambalabsdev/mcp-streaming-subscription-prices-by-country)](https://www.npmjs.com/package/@mambalabsdev/mcp-streaming-subscription-prices-by-country) [![license](https://img.shields.io/github/license/mambalabsdev/mcp-streaming-subscription-prices-by-country)](https://github.com/mambalabsdev/mcp-streaming-subscription-prices-by-country/blob/main/LICENSE)

An MCP server for the Mamba Labs Streaming Subscription Prices by Country actor on Apify. Streaming plan prices by country, as rows.

## What's Inside

- [What it does](#what-it-does)
- [Quick start](#quick-start)
- [Prerequisites](#prerequisites)
- [Example prompts](#example-prompts)
- [Tool](#tool)
- [Inputs](#inputs)
- [Pricing](#pricing)
- [Full actor documentation](#full-actor-documentation)
- [License](#license)

## What it does

Takes 2 letter country codes and returns Spotify and Netflix monthly plan prices in local currency, one row per plan, with the price text exactly as shown.

All of the work runs on Apify. This package is a thin client that starts the actor run, waits for it, and hands back the dataset rows.

## Quick start

You need Node.js 18 or newer and an Apify account with an API token.

Add this to your Claude Desktop config (`claude_desktop_config.json`), Cursor, or any MCP client:

```json
{
  "mcpServers": {
    "mamba-streaming-subscription-prices-by-country": {
      "command": "npx",
      "args": [
        "-y",
        "@mambalabsdev/mcp-streaming-subscription-prices-by-country"
      ],
      "env": {
        "APIFY_TOKEN": "your-apify-token"
      }
    }
  }
}
```

Restart the client. The `get_streaming_prices_by_country` tool appears.

## Prerequisites

- Node.js 18 or newer.
- An Apify API token from [console.apify.com/account/integrations](https://console.apify.com/account/integrations), set as `APIFY_TOKEN`. The server lists its tool without a token; a call needs one.

## Example prompts

- "What does Spotify Premium cost in India, Brazil, and Japan?"
- "Compare Netflix plan prices in the US and Germany."

## Tool

`get_streaming_prices_by_country`. One tool. Example arguments:

```json
{
  "countries": [
    "US",
    "DE"
  ],
  "services": [
    "spotify"
  ]
}
```

## Inputs

Every buyer facing input of the actor. Omitted inputs take the actor's own defaults.

| Input | Type | Required | Description |
|---|---|---|---|
| `countries` | array | no | 2 letter country codes, such as US, DE, IN, BR, or JP. UK and GB both mean the United Kingdom. Up to 250. Each country is read once per service. |
| `services` | array | no | spotify, netflix, or both. Default both. Spotify rows cost less, because Netflix must be read from an address in each country. |
| `max_charge_usd` | number | no | Optional. The run stops before a charge that would pass this amount. Summary rows are always returned. |

## Pricing

Pay per event on Apify, billed to your Apify account. Prices in USD.

| Event | Free plan | Bronze | Silver | Gold |
|---|---|---|---|---|
| `plan-row`, one Spotify plan in one country | $0.003 | $0.00285 | $0.0027 | $0.00255 |
| `netflix-plan-row`, one Netflix plan in one country | $0.005 | $0.00475 | $0.0045 | $0.00425 |
| `apify-actor-start`, per run start | $0.004 | $0.004 | $0.004 | $0.004 |

Country summaries and refused input are free. Mamba Labs pays the platform costs of the run, Apify proxy traffic included.

## Full actor documentation

[apify.com/mambalabs/streaming-subscription-prices-by-country](https://apify.com/mambalabs/streaming-subscription-prices-by-country)

## License

MIT. See [LICENSE](LICENSE).
