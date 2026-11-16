# Visual Regression & Screenshot Diff for AI Agents

Two page URLs in (production and a preview deploy, or before and after a change), on desktop and phone sizes. Out come the percent of pixels changed, every changed region as a box, a diff image and PASS or FAIL against the change you allow. A check an agent cannot quietly patch to make it pass.

- Apify Store: https://apify.com/fluidfaith/visual-diff-gate
- MCP server (remote, streamable HTTP): `https://mcp.apify.com/?tools=fluidfaith/visual-diff-gate`
- Price: $0.005 per page pair per viewport. Pages that fail to load are free, and your maximum charge per run is never exceeded.

## Claude Code, Cursor, VS Code (MCP config)

```json
{
  "mcpServers": {
    "visual-diff-gate": {
      "url": "https://mcp.apify.com/?tools=fluidfaith/visual-diff-gate",
      "headers": { "Authorization": "Bearer ${APIFY_TOKEN}" }
    }
  }
}
```

Claude Code one-liner: `claude mcp add --transport http visual-diff-gate "https://mcp.apify.com/?tools=fluidfaith/visual-diff-gate" --header "Authorization: Bearer $APIFY_TOKEN"`

## Python (apify-client)

```python
import os
from apify_client import ApifyClient

client = ApifyClient(os.environ["APIFY_TOKEN"])
run = client.actor("fluidfaith/visual-diff-gate").call(run_input={
    "baselineOrigin": "https://www.example.com",
    "candidateOrigin": "https://preview.example.com",
    "paths": ["/", "/pricing"],
    "viewports": ["Desktop", "iPhone 15-16"],
})
for item in client.dataset(run["defaultDatasetId"]).iterate_items():
    print(item["name"], item["viewport"], item["verdict"], item["diffPercent"], item["regions"][:3])
```

## LangChain

```python
from langchain_apify import ApifyActorsTool
tool = ApifyActorsTool("fluidfaith/visual-diff-gate")
```

## JavaScript (apify-client)

```js
import { ApifyClient } from 'apify-client';
const client = new ApifyClient({ token: process.env.APIFY_TOKEN });
const run = await client.actor('fluidfaith/visual-diff-gate').call({
  pairs: [{ name: 'home', baseline: 'https://www.example.com/', candidate: 'https://preview.example.com/' }],
  viewports: ['Desktop', 'iPhone 15-16'],
  maskSelectors: ['.carousel'],
});
const { value } = await client.keyValueStore(run.defaultKeyValueStoreId).getRecord('OUTPUT');
console.log(value.verdict, value.results);
```

## Good agent instruction

"Before you report a front-end change as done, call visual-diff-gate with production as the baseline and your preview deploy as the candidate. Every changed region must be one you meant to change. Open diffImageUrl for any FAIL."
