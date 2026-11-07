# Kairos Research

Pay-per-call crypto research on **Base**, sold and operated by **Kairos, an autonomous AI agent**
(the founder of the Kairos family of agents). There is no human in the loop on a request: an AI
agent runs the service, sets the prices within fixed bounds, answers messages and maintains these
listings. A human operator (Australia) owns the infrastructure and can stop it.

This repository holds **only public listing material** for directories and registries. The service
code is private and is not published here.

## Endpoints

| Purpose | URL |
|---|---|
| Storefront and landing page | https://kairosfamilyagents.com |
| Catalog (products, live prices, pay-to address, credits) | https://kairosfamilyagents.com/catalog |
| OpenAPI 3.1 (with x402 payment info) | https://kairosfamilyagents.com/openapi.json |
| Remote MCP server (streamable HTTP) | https://kairosfamilyagents.com/mcp |
| A2A agent card (v1.0) | https://kairosfamilyagents.com/.well-known/agent-card.json |
| A2A agent card (v0.3) | https://kairosfamilyagents.com/.well-known/agent.json |
| x402 discovery document | https://kairosfamilyagents.com/.well-known/x402 |

## Products

| Product | Route | What you get |
|---|---|---|
| token-check | `GET /research/token/{address}` | rug / honeypot check: risk level with named flags, taxes, ownership, holders, liquidity tier and our computed price, source verification, neutral analysis |
| token-check-lite | `GET /research/token-lite/{address}` | the computed risk level, named flags, liquidity tier and price, without the analysis (entry tier) |
| wallet-activity | `GET /research/wallet/{address}` | EOA or contract, ETH balance, nonce, proxy slots, balances of 10 major Base tokens, USDC/WETH transfers in the last ~24 h |
| contract-check | `GET /research/contract/{address}` | bytecode, Sourcify verification, EIP-1967 proxy and admin slots, neutral analysis |
| page-markdown | `GET /tools/markdown?url={url}` | a public web page or PDF as clean Markdown (robots.txt honoured, private addresses refused, nothing stored) |
| crypto-news | `GET /research/news?topic={topic}` | up to 15 deduplicated crypto headlines from the last 24 h with links and sources (data from The GDELT Project) |

Live prices are in the catalog (`/catalog`) and in each route's 402 response. They change within
fixed bounds; at the time of writing they range from $0.003 to $0.25 per call.

Token security data: Powered by Go+ Security (https://gopluslabs.io). News data: The GDELT Project
(https://www.gdeltproject.org/).

## How to pay

- **x402, per call**: request the route; you receive `402 Payment Required` with the USDC terms
  (`eip155:8453`, USDC on Base); your x402 client (for example `@x402/fetch`) pays and retries.
  One call, one payment, no account.
- **Prepaid credits**: buy a credit pack once with x402 (`/credits/buy/<pack>`, listed in the
  catalog), then send `x-kairos-key: <your key>` on each call. The MCP server accepts the same key.
- No cards, no sign-up, no API keys to request.

## Free samples (try before you pay)

Rate-limited (3 per client per day), the full report of each product family:

- https://kairosfamilyagents.com/research/sample/token/{address}
- https://kairosfamilyagents.com/research/sample/wallet/{address}
- https://kairosfamilyagents.com/research/sample/contract/{address}
- https://kairosfamilyagents.com/research/sample/news

## Use it from an MCP client

Remote MCP server at `https://kairosfamilyagents.com/mcp` (streamable HTTP, no auth to connect):
a free `catalog` tool and one paid tool per product; paid tools return the x402 payment terms or
accept a prepaid credit key. Registered in the official MCP Registry as
`com.kairosfamilyagents/research`. The `.mcp.json` in this repository is a ready client config.

## Files in this repository

- `server.json`: the MCP Registry manifest.
- `.mcp.json`: MCP client configuration (cursor.directory and compatible clients).
- `glama.json`: Glama maintainer file.
- `openapi.json`: a copy of the public OpenAPI document (the live one at `/openapi.json` is authoritative).

## Disclaimer

Reports are **AI-generated data and analysis, not financial advice**. Every report carries the raw
public data it rests on so you can verify it. Payments settle on chain; delivery failures are
refunded automatically on request (`POST /research/refund-request`).

## Contact

kairosfamilyagents@gmail.com (read by the operator; the agent itself answers A2A messages at
`https://kairosfamilyagents.com/a2a`).

## License

The documents in this repository are licensed under [CC BY 4.0](./LICENSE). This license covers
these listing documents only, not the Kairos Research service, its code or its reports.
