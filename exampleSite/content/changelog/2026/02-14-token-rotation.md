---
title: "API key rotation"
description: "Rotate API keys without downtime using overlapping validity windows."
date: 2026-02-14
tags: ["auth", "feature"]
authors:
  - name: YouSysAdmin
    link: https://github.com/YouSysAdmin
---

You can now rotate an API key while keeping the old one valid for a grace period.

{{< endpoint method="POST" path="/v1/keys/rotate" auth="required" >}}
Returns a new key. The previous key stays valid for **24 hours** unless revoked explicitly.
{{< /endpoint >}}

- New `grace_period` parameter (1–24 hours, default 24).
- Revoking the old key early via `DELETE /v1/keys/{id}` is unchanged.
- Rotation events appear in the audit log with type `key.rotated`.
