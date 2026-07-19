---
title: "Users"
description: "Create, retrieve, update, filter, and list user resources."
weight: 30
---

A user represents an authenticated principal in your account. This section
documents the full lifecycle of the user resource.

## Retrieve a user

{{< endpoint method="GET" path="/v2/users/{id}" auth="required" />}}

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
  "role": "admin",
  "status": "active"
}
```

## Create a user

{{< endpoint method="POST" path="/v2/users" auth="required" />}}

| Parameter | In   | Type   | Required | Description          |
| --------- | ---- | ------ | -------- | -------------------- |
| `email`   | body | string | yes      | Must be unique.      |
| `name`    | body | string | no       | Display name.        |
| `role`    | body | string | no       | `admin` or `member`. |

```bash
curl -X POST https://api.example.org/v2/users \
  -H "Authorization: Bearer sk_live_..." \
  -d '{"email":"john@example.org","name":"John Doe"}'
```

## Update a user

{{< endpoint method="PATCH" path="/v2/users/{id}" auth="required" />}}

Updates the specified user by setting the values of the parameters passed. Any
parameters not provided are left unchanged.

## Delete a user

{{< endpoint method="DELETE" path="/v2/users/{id}" auth="required" />}}

Permanently deletes a user. This cannot be undone.

## List users

{{< endpoint method="GET" path="/v2/users" auth="required" >}}
Cursor pagination replaces page numbers, pass `cursor` from the previous response.
{{< /endpoint >}}

Returns a paginated list of users, most recent first. Lists support filtering
and sorting.

| Parameter        | In    | Type    | Description                                            |
| ---------------- | ----- | ------- | ------------------------------------------------------ |
| `limit`          | query | integer | Page size, 1–100 (default 25).                         |
| `cursor`         | query | string  | Cursor from the previous response.                     |
| `filter[status]` | query | string  | `active`, `invited`, or `suspended`.                   |
| `sort`           | query | string  | `created_at`, `email` — prefix with `-` for descending. |
