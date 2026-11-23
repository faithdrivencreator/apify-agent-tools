# Mermaid, Graphviz & Chart to PNG, SVG or PDF

Diagram or chart code in (Mermaid, Graphviz DOT, Vega-Lite, Vega, Chart.js config or SVG), a PNG, SVG or PDF link out. When the code is wrong it returns the parser's error, the line number and the text of that line, so the agent can fix it and call again. Errors are free.

- Apify Store: https://apify.com/fluidfaith/mermaid-chart-renderer
- MCP server (remote, streamable HTTP): `https://mcp.apify.com/?tools=fluidfaith/mermaid-chart-renderer`
- Price: $0.003 per diagram rendered. Errors are free, and your maximum charge per run is never exceeded.

## Claude Code, Cursor, VS Code (MCP config)

```json
{
  "mcpServers": {
    "diagram-renderer": {
      "url": "https://mcp.apify.com/?tools=fluidfaith/mermaid-chart-renderer",
      "headers": { "Authorization": "Bearer ${APIFY_TOKEN}" }
    }
  }
}
```

Claude Code one-liner: `claude mcp add --transport http diagram-renderer "https://mcp.apify.com/?tools=fluidfaith/mermaid-chart-renderer" --header "Authorization: Bearer $APIFY_TOKEN"`

## Python (apify-client)

```python
import os
from apify_client import ApifyClient

client = ApifyClient(os.environ["APIFY_TOKEN"])
run = client.actor("fluidfaith/mermaid-chart-renderer").call(run_input={
    "code": "flowchart LR\n  A[Write code] --> B{Valid?}\n  B -- yes --> C[PNG link]\n  B -- no --> D[Error with line]",
    "format": "png",
})
row = client.dataset(run["defaultDatasetId"]).list_items().items[0]
print(row["fileUrl"] if row["status"] == "OK" else f'line {row["errorLine"]}: {row["error"]}')
```

## curl (one call, waits for the result)

```bash
curl -s -X POST "https://api.apify.com/v2/acts/fluidfaith~mermaid-chart-renderer/run-sync-get-dataset-items?token=$APIFY_TOKEN" \
  -H 'Content-Type: application/json' \
  -d '{"code":"digraph { rankdir=LR; build -> test -> deploy }","format":"svg"}'
```

## Agent instruction that works

"When a diagram or chart would help, write it as Mermaid (or Vega-Lite for data), call mermaid-chart-renderer and share fileUrl. If status is ERROR, fix the line in errorLine and call again."
