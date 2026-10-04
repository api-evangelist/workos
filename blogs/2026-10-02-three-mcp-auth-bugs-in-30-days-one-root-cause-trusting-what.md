---
title: "Three MCP auth bugs in 30 days, one root cause: Trusting what the other side said"
url: "https://workos.com/blog/mcp-auth-bugs-trusting-the-other-side"
date: "2026-10-02"
feed_url: "https://workos.com/blog/rss.xml"
---
The MCP Python SDK, the Rust SDK (rmcp), and LiteLLM each accepted authentication input that nobody verified. Here is what broke, who is affected, and the checklist that closes the gap.
