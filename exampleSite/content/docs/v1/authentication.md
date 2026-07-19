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

{{< endpoint method="GET" path="/v1/users/me" auth="required" />}}

```bash
curl https://api.example.org/v1/users/me \
  -H "Authorization: Bearer sk_live_51H..."
```

## Key types

| Prefix       | Environment | Scope                         |
|--------------|-------------|-------------------------------|
| `sk_live_`   | Production  | Full read/write               |
| `sk_test_`   | Sandbox     | Full read/write, test data    |
| `pk_live_`   | Production  | Publishable, read-only        |

## Errors

A missing or invalid key returns `401 Unauthorized`. A valid key without
sufficient scope returns `403 Forbidden`.

```json
{
  "error": {
    "type": "authentication_error",
    "message": "No valid API key provided."
  }
}
```
