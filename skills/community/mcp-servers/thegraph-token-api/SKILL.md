---
name: thegraph-token-api
description: "MCP server for The Graph Token API by Pinax. Provides token data access via ClickHouse backend with SSE and HTTP streaming support."
version: 1.0.0
metadata:
  openclaw:
    tags: [the-graph, pinax, token-api, mcp, indexing, subgraph, data]
    official: true
    source: "https://github.com/pinax-network/mcp-token-api"
---

# The Graph Token API MCP Server

Official MCP server from Pinax (The Graph ecosystem).

An MCP server for The Graph Token API providing token data access through ClickHouse backend. Supports SSE and HTTP streaming modes for real-time token data queries and analytics.

## Installation

Requires [Bun](https://bun.sh):

```bash
git clone https://github.com/pinax-network/mcp-token-api.git
cd mcp-token-api
bun run index.ts
```

Server runs on `http://localhost:8080/sse` (SSE) and `http://localhost:8080/stream` (HTTP streaming).

Configure with environment variables or CLI options:
- `--port`: HTTP port (default: 8080)
- `--url`: Database HTTP hostname
- `--database`: ClickHouse database name
- `--username` / `--password`: Database credentials

## Links

- **GitHub**: https://github.com/pinax-network/mcp-token-api
