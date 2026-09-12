---
title: "OAuth token refresh has a race condition. Fix it with a conditional write, not a distributed lock."
url: "https://workos.com/blog/oauth-refresh-token-race-condition"
date: "2026-08-31"
feed_url: "https://workos.com/blog/rss.xml"
---
Concurrent refreshes don't just fail. They can disconnect the user entirely. Here are four layers of defense, cheapest first, and why the Redis lock everyone reaches for isn't the one keeping you safe.
