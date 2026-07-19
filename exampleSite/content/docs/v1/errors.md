---
title: "Errors"
description: "Standard HTTP status codes and structured error payloads."
weight: 40
---

The API uses conventional HTTP status codes to indicate success or failure.
Codes in the `2xx` range indicate success, `4xx` indicate a client error,
`5xx` indicate a server error.

## Status codes

| Code  | Meaning               | Notes                                   |
|-------|-----------------------|-----------------------------------------|
| `200` | OK                    | Request succeeded.                      |
| `201` | Created               | Resource created.                       |
| `400` | Bad Request           | Malformed request or invalid params.    |
| `401` | Unauthorized          | Missing or invalid API key.             |
| `403` | Forbidden             | Key lacks required scope.               |
| `404` | Not Found             | Resource does not exist.                |
| `429` | Too Many Requests     | Rate limit exceeded.                    |
| `500` | Internal Server Error | Something went wrong on our end.        |

## Error object

All errors return a consistent JSON envelope.

```json
{
  "error": {
    "type": "invalid_request_error",
    "code": "parameter_missing",
    "message": "Missing required parameter: email.",
    "param": "email"
  }
}
```

## Error types

| Type                   | Description                                  |
|------------------------|----------------------------------------------|
| `authentication_error` | The API key was missing or invalid.          |
| `invalid_request_error`| The request had bad or missing parameters.   |
| `rate_limit_error`     | Too many requests hit too quickly.           |
| `api_error`            | An internal error occurred (rare).           |
