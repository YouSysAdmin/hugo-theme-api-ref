---
title: "Standard rate limit headers"
description: "All responses now include RateLimit-* headers alongside the legacy X-RateLimit-* set."
date: 2026-03-02
tags: ["api", "deprecation"]
authors:
  - "API Platform Team"
---

Every response now carries the IETF standard headers:

```http
RateLimit-Limit: 1000
RateLimit-Remaining: 942
RateLimit-Reset: 27
```

The legacy `X-RateLimit-*` headers are still sent but are **deprecated** and will be
removed on **2027-01-01**. Update any client code that parses them.
