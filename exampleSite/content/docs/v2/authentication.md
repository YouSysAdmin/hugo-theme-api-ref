---
title: "Authentication"
description: "Authenticate requests with a secret API key sent as a bearer token."
weight: 20
---

The API authenticates requests using API keys. Each key carries a set of
permissions, keep secret keys confidential and never expose them in client-side
code.

## Bearer tokens

Provide your secret key in the `Authorization` header of every request.

{{< endpoint method="GET" path="/v2/users/me" auth="required" />}}

```bash
curl https://api.example.org/v2/users/me \
  -H "Authorization: Bearer sk_live_51H..."
```

## Key types

| Prefix       | Environment | Scope                         |
|--------------|-------------|-------------------------------|
| `sk_live_`   | Production  | Full read/write               |
| `sk_test_`   | Sandbox     | Full read/write, test data    |
| `pk_live_`   | Production  | Publishable, read-only        |

## Key rotation

Rotate a key without downtime. The previous key stays valid for a grace period
(1–24 hours, default 24) unless revoked explicitly.

{{< endpoint method="POST" path="/v2/keys/rotate" auth="required" >}}
Returns a new key. Rotation events appear in the audit log as `key.rotated`.
{{< /endpoint >}}

## Errors

A missing or invalid key returns `401 Unauthorized`. A valid key without
sufficient scope returns `403 Forbidden`.

```json
{
  "error": {
    "type": "authentication_error",
    "code": "api_key_invalid",
    "message": "No valid API key provided."
  }
}
```
