---
title: "Clearing up (my own) OAuth misunderstandings"
url: "https://workos.com/blog/clearing-up-my-own-oauth-misunderstandings"
date: "2026-06-04"
author: "Quentin Balin"
feed_url: "https://workos.com/blog"
---
This article explores OAuth's design principles, explaining why authorization and resource servers remain separate, why authorization codes exist rather than direct token issuance, and how access/refresh token pairs enhance security. The author clarifies that bearer tokens' short lifespan mitigates leak risks, while refresh tokens require client credentials, making them unsuitable for single-page applications lacking secure backends.
