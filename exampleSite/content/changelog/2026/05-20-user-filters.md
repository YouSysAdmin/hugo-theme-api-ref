---
title: "Filtering and sorting on user lists"
description: "List endpoints accept filter, sort, and cursor pagination parameters."
date: 2026-05-20
tags: ["users", "feature"]
authors:
  - name: YouSysAdmin
    link: https://github.com/YouSysAdmin
---

{{< endpoint method="GET" path="/v1/users?filter[status]=active&sort=-created_at" auth="required" >}}
Cursor pagination replaces page numbers, pass `cursor` from the previous response.
{{< /endpoint >}}

| Parameter | Description |
| --------- | ----------- |
| `filter[status]` | `active`, `invited`, or `suspended` |
| `sort` | `created_at`, `email` — prefix with `-` for descending |
| `limit` | 1–100, default 25 |

Offset pagination (`page`, `per_page`) keeps working for existing integrations.
