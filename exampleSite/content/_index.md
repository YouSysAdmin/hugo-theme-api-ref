---
title: "API Reference"
description: "A monospace, datasheet-style reference for the Example REST API. Predictable resource-oriented URLs, JSON payloads, and standard HTTP verbs."
---

The Example API is organized around REST. It has predictable resource-oriented
URLs, accepts JSON-encoded request bodies, returns JSON-encoded responses, and
uses standard HTTP response codes, verbs, and authentication.

## Conventions

All requests are made to the base URL and must be sent over HTTPS. Requests
made over plain HTTP are rejected.

| Field        | Value                          |
|--------------|--------------------------------|
| Base URL     | `https://api.example.org/v2`   |
| Protocol     | HTTPS only                     |
| Payloads     | `application/json`             |
| Auth         | Bearer token (see below)       |
| Rate limit   | 1000 req / min / key           |

## Quick start

Authenticate with a bearer token and request the current user:

```bash
curl https://api.example.org/v2/users/me \
  -H "Authorization: Bearer sk_live_..." \
  -H "Content-Type: application/json"
```

## Versioning

The API version is pinned in the URL path (`/v2`). Breaking changes are shipped
under a new path segment. Additive changes may appear within a version. See the
individual endpoint pages in the sidebar for the full contract.
