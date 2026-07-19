---
title: "Machine-readable error codes"
description: "Error responses gain a stable code field, messages are no longer part of the contract."
date: 2026-07-10
tags: ["errors", "breaking"]
authors:
  - name: YouSysAdmin
    link: https://github.com/YouSysAdmin
  - "API Platform Team"
---

Error bodies now include a stable `code` you can branch on:

```json
{
  "error": {
    "code": "user_suspended",
    "message": "This account has been suspended.",
    "doc_url": "https://api.example.org/docs/errors/#user_suspended"
  }
}
```

**Breaking:** `message` wording may change at any time — match on `code`, not on text.
The full code catalogue is listed on the [Errors](/docs/v2/errors/) page.
