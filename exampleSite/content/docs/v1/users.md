---
title: "Users"
description: "Create, retrieve, update, and list user resources."
weight: 30
---

A user represents an authenticated principal in your account. This section
documents the full lifecycle of the user resource.

## Retrieve a user

{{< endpoint method="GET" path="/v1/users/{id}" auth="required" />}}

Returns the user object for the supplied identifier.

| Parameter | In    | Type   | Description                |
| --------- | ----- | ------ | -------------------------- |
| `id`      | path  | string | Unique user identifier.    |
| `expand`  | query | array  | Related objects to inline. |

```json
{
  "id": "1",
  "object": "user",
  "email": "john@example.org",
  "name": "John Doe",
  "created": 1689600000,
  "role": "admin"
}
```

## Create a user

{{< endpoint method="POST" path="/v1/users" auth="required" />}}

| Parameter | In   | Type   | Required | Description          |
| --------- | ---- | ------ | -------- | -------------------- |
| `email`   | body | string | yes      | Must be unique.      |
| `name`    | body | string | no       | Display name.        |
| `role`    | body | string | no       | `admin` or `member`. |

```bash
curl -X POST https://api.example.org/v1/users \
  -H "Authorization: Bearer sk_live_..." \
  -d '{"email":"john@example.org","name":"John Doe"}'
```

## Update a user

{{< endpoint method="PATCH" path="/v1/users/{id}" auth="required" />}}

Updates the specified user by setting the values of the parameters passed. Any
parameters not provided are left unchanged.

## Delete a user

{{< endpoint method="DELETE" path="/v1/users/{id}" auth="required" />}}

Permanently deletes a user. This cannot be undone.

## List users

{{< endpoint method="GET" path="/v1/users" auth="required" />}}

Returns a paginated list of users, most recent first.

| Parameter        | In    | Type    | Description                    |
| ---------------- | ----- | ------- | ------------------------------ |
| `limit`          | query | integer | Page size, 1–100 (default 20). |
| `starting_after` | query | string  | Cursor for pagination.         |
