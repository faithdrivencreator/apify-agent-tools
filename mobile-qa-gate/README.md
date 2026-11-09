# Mobile Website Test on iPhone & Android for AI Agents

PASS or FAIL per page per phone with screenshots: sideways scroll, split phone numbers, unreadable text.

- Apify Store: https://apify.com/fluidfaith/mobile-qa-gate
- MCP server (remote, streamable HTTP): `https://mcp.apify.com/?tools=fluidfaith/mobile-qa-gate`
- Price: $0.01 per page per phone. Failed items are free, and your maximum charge per run is never exceeded.

## Claude Code, Cursor, VS Code (MCP config)

```json
{
  "mcpServers": {
    "mobile-qa-gate": {
      "url": "https://mcp.apify.com/?tools=fluidfaith/mobile-qa-gate",
      "headers": { "Authorization": "Bearer ${APIFY_TOKEN}" }
    }
  }
}
```

Claude Code one-liner: `claude mcp add --transport http mobile-qa-gate "https://mcp.apify.com/?tools=fluidfaith/mobile-qa-gate" --header "Authorization: Bearer $APIFY_TOKEN"`

## Python (apify-client)

```python
import os
from apify_client import ApifyClient

client = ApifyClient(os.environ["APIFY_TOKEN"])
run = client.actor("fluidfaith/mobile-qa-gate").call(run_input={"urls": ["https://example.com"]})
for item in client.dataset(run["defaultDatasetId"]).iterate_items():
    print(item)
```

## LangChain

```python
from langchain_apify import ApifyActorsTool
tool = ApifyActorsTool("fluidfaith/mobile-qa-gate")
```

## JavaScript (apify-client)

```js
import { ApifyClient } from 'apify-client';
const client = new ApifyClient({ token: process.env.APIFY_TOKEN });
const run = await client.actor('fluidfaith/mobile-qa-gate').call({"urls": ["https://example.com"]});
const { items } = await client.dataset(run.defaultDatasetId).listItems();
console.log(items);
```
