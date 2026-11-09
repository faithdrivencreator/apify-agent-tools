# Video Frame Extractor & Media Probe for AI Agents

Direct video or audio file link in: ffprobe metadata (duration, codecs, resolution, fps, rotation, 9:16 check), frames at set times, every N seconds or at scene cuts, a contact sheet sized for vision models, EBU R128 loudness and MP3 audio. Direct file links only (no YouTube, TikTok or Instagram pages).

- Apify Store: https://apify.com/fluidfaith/media-probe
- MCP server (remote, streamable HTTP): `https://mcp.apify.com/?tools=fluidfaith/media-probe`
- Price: $0.002 per file probed, $0.001 per frame, $0.005 per contact sheet. Failed items are free, and your maximum charge per run is never exceeded.

## Claude Code, Cursor, VS Code (MCP config)

```json
{
  "mcpServers": {
    "media-probe": {
      "url": "https://mcp.apify.com/?tools=fluidfaith/media-probe",
      "headers": { "Authorization": "Bearer ${APIFY_TOKEN}" }
    }
  }
}
```

Claude Code one-liner: `claude mcp add --transport http media-probe "https://mcp.apify.com/?tools=fluidfaith/media-probe" --header "Authorization: Bearer $APIFY_TOKEN"`

## Python (apify-client)

```python
import os
from apify_client import ApifyClient

client = ApifyClient(os.environ["APIFY_TOKEN"])
run = client.actor("fluidfaith/media-probe").call(run_input={"urls": ["https://example.com/video.mp4"], "frames": "count", "frameCount": 6})
for item in client.dataset(run["defaultDatasetId"]).iterate_items():
    print(item)
```

## LangChain

```python
from langchain_apify import ApifyActorsTool
tool = ApifyActorsTool("fluidfaith/media-probe")
```

## JavaScript (apify-client)

```js
import { ApifyClient } from 'apify-client';
const client = new ApifyClient({ token: process.env.APIFY_TOKEN });
const run = await client.actor('fluidfaith/media-probe').call({"urls": ["https://example.com/video.mp4"], "frames": "count", "frameCount": 6});
const { items } = await client.dataset(run.defaultDatasetId).listItems();
console.log(items);
```
