# Lighthouse & Accessibility Audit for AI Agents

Lighthouse scores, Core Web Vitals and axe accessibility issues, median of 3 runs, PASS/FAIL and top fixes.

- Apify Store: https://apify.com/fluidfaith/lighthouse-gate
- MCP server (remote, streamable HTTP): `https://mcp.apify.com/?tools=fluidfaith/lighthouse-gate`
- Price: $0.02 per URL per form factor. Failed items are free, and your maximum charge per run is never exceeded.

## Claude Code, Cursor, VS Code (MCP config)

```json
{
  "mcpServers": {
    "lighthouse-gate": {
      "url": "https://mcp.apify.com/?tools=fluidfaith/lighthouse-gate",
      "headers": { "Authorization": "Bearer ${APIFY_TOKEN}" }
    }
  }
}
```

Claude Code one-liner: `claude mcp add --transport http lighthouse-gate "https://mcp.apify.com/?tools=fluidfaith/lighthouse-gate" --header "Authorization: Bearer $APIFY_TOKEN"`

## Python (apify-client)

```python
import os
from apify_client import ApifyClient

client = ApifyClient(os.environ["APIFY_TOKEN"])
run = client.actor("fluidfaith/lighthouse-gate").call(run_input={"urls": ["https://example.com/"], "formFactors": ["mobile"]})
for item in client.dataset(run["defaultDatasetId"]).iterate_items():
    print(item)
```

## LangChain

```python
from langchain_apify import ApifyActorsTool
tool = ApifyActorsTool("fluidfaith/lighthouse-gate")
```

## JavaScript (apify-client)

```js
import { ApifyClient } from 'apify-client';
const client = new ApifyClient({ token: process.env.APIFY_TOKEN });
const run = await client.actor('fluidfaith/lighthouse-gate').call({"urls": ["https://example.com/"], "formFactors": ["mobile"]});
const { items } = await client.dataset(run.defaultDatasetId).listItems();
console.log(items);
```
