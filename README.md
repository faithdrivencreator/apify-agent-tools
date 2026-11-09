# Apify agent tools by Fluid Faith Solutions

Small, dependable tools for AI agents, hosted on Apify and usable as remote MCP servers from Claude, ChatGPT, Cursor, VS Code, n8n and LangChain. JSON in, JSON out, pay per event, failed items are free and your maximum charge per run is never exceeded.

| Tool | What it does | MCP URL | Price |
|---|---|---|---|
| [Mobile Website Test](https://apify.com/fluidfaith/mobile-qa-gate) | PASS or FAIL per page on today's phones (iPhone, Galaxy, Pixel) with screenshots | `https://mcp.apify.com/?tools=fluidfaith/mobile-qa-gate` | $0.01 per page per phone |
| [Lighthouse & Accessibility Audit](https://apify.com/fluidfaith/lighthouse-gate) | Lighthouse scores, Core Web Vitals, axe accessibility issues, PASS/FAIL and top fixes | `https://mcp.apify.com/?tools=fluidfaith/lighthouse-gate` | $0.02 per URL per form factor |
| [Video Frame Extractor & Media Probe](https://apify.com/fluidfaith/media-probe) | ffprobe metadata, frames, scene cuts, contact sheet, loudness and MP3 from direct video or audio links | `https://mcp.apify.com/?tools=fluidfaith/media-probe` | $0.001 per frame |
| [PDF to Markdown with Tables](https://apify.com/fluidfaith/pdf-to-markdown-tables) | PDF, Word, PowerPoint, Excel to Markdown plus tables as JSON rows, OCR for scans | `https://mcp.apify.com/?tools=fluidfaith/pdf-to-markdown-tables` | $0.002 per page |

Load several at once: `https://mcp.apify.com/?tools=fluidfaith/mobile-qa-gate,fluidfaith/lighthouse-gate,fluidfaith/pdf-to-markdown-tables,fluidfaith/media-probe`

Each folder has copy-paste examples (MCP config, Python, JavaScript, LangChain) and the `server.json` used for the official MCP Registry.

Auth: an Apify API token (`Authorization: Bearer <token>`) or Apify OAuth. Use `APIFY_TOKEN` from your environment; never commit it.

Found a bug or want a check added? Open an issue here.

License: MIT (examples in this repo).
