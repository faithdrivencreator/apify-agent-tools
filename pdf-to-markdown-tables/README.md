# PDF to Markdown with Tables for AI Agents

PDF, Word, PowerPoint and Excel to clean Markdown plus every table as JSON rows, OCR for scans.

- Apify Store: https://apify.com/fluidfaith/pdf-to-markdown-tables
- MCP server (remote, streamable HTTP): `https://mcp.apify.com/?tools=fluidfaith/pdf-to-markdown-tables`
- Price: $0.008 per document + $0.002 per page + $0.002 per table. Failed items are free, and your maximum charge per run is never exceeded.

## Claude Code, Cursor, VS Code (MCP config)

```json
{
  "mcpServers": {
    "pdf-to-markdown-tables": {
      "url": "https://mcp.apify.com/?tools=fluidfaith/pdf-to-markdown-tables",
      "headers": { "Authorization": "Bearer ${APIFY_TOKEN}" }
    }
  }
}
```

Claude Code one-liner: `claude mcp add --transport http pdf-to-markdown-tables "https://mcp.apify.com/?tools=fluidfaith/pdf-to-markdown-tables" --header "Authorization: Bearer $APIFY_TOKEN"`

## Python (apify-client)

```python
import os
from apify_client import ApifyClient

client = ApifyClient(os.environ["APIFY_TOKEN"])
run = client.actor("fluidfaith/pdf-to-markdown-tables").call(run_input={"urls": ["https://www.census.gov/retail/mrts/www/data/pdf/ec_current.pdf"]})
for item in client.dataset(run["defaultDatasetId"]).iterate_items():
    print(item)
```

## LangChain

```python
from langchain_apify import ApifyActorsTool
tool = ApifyActorsTool("fluidfaith/pdf-to-markdown-tables")
```

## JavaScript (apify-client)

```js
import { ApifyClient } from 'apify-client';
const client = new ApifyClient({ token: process.env.APIFY_TOKEN });
const run = await client.actor('fluidfaith/pdf-to-markdown-tables').call({"urls": ["https://www.census.gov/retail/mrts/www/data/pdf/ec_current.pdf"]});
const { items } = await client.dataset(run.defaultDatasetId).listItems();
console.log(items);
```
