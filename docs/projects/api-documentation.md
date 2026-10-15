# Task API: developer reference sample

**Sample type:** Self-directed portfolio demonstration · **Status:** Complete as a writing sample; examples are illustrative and are not connected to a running service.

This sample shows how an API reference can combine an integration path, endpoint details, and practical error guidance. The Task API is fictional. Confirm behavior against a real implementation before reusing this content.

[Download the matching OpenAPI 3.1 sample](../assets/task-api-openapi.yaml)

## At a glance

| Item | Details |
| --- | --- |
| Audience | Developers integrating a task-management service |
| Authentication | Bearer token (illustrative) |
| Base URL | `https://api.example.test/v1` |
| Format | JSON over HTTPS |

## Quickstart

Send a request with a bearer token and JSON content type. Replace the sample token with a credential issued for your account.

```bash
curl --request GET \
  --url https://api.example.test/v1/tasks \
  --header 'Authorization: Bearer YOUR_API_TOKEN' \
  --header 'Accept: application/json'
```

An illustrative successful response:

```json
{
  "data": [
    { "id": "tsk_1042", "title": "Review release notes", "completed": false }
  ],
  "next_cursor": null
}
```

## Authentication

Send credentials in the `Authorization` header using the bearer scheme:

```http
Authorization: Bearer YOUR_API_TOKEN
```

Do not put tokens in URLs or commit them to source control. A real API should document token creation, scopes, expiry, and rotation here.

## List tasks

`GET /tasks` returns tasks visible to the authenticated account. Results are ordered by creation time, newest first (illustrative behavior).

### Query parameters

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| `limit` | integer | No | Maximum number of results. Default `20`; maximum `100`. |
| `cursor` | string | No | Cursor returned by the previous response. Omit on the first request. |
| `completed` | boolean | No | Filter by completion state. |

### Example request

```bash
curl --get 'https://api.example.test/v1/tasks' \
  --data-urlencode 'limit=20' \
  --data-urlencode 'completed=false' \
  --header 'Authorization: Bearer YOUR_API_TOKEN'
```

### Example response

```json
{
  "data": [
    { "id": "tsk_1042", "title": "Review release notes", "completed": false },
    { "id": "tsk_1038", "title": "Update integration guide", "completed": false }
  ],
  "next_cursor": "cD0yMDI1LTAxLTAx"
}
```

When `next_cursor` is `null`, there are no more results. Otherwise, pass its value as `cursor` to retrieve the next page.

## Retrieve a task

`GET /tasks/{task_id}` returns one task by ID.

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| `task_id` | string | Yes | Task identifier, for example `tsk_1042`. |

```bash
curl --request GET \
  --url https://api.example.test/v1/tasks/tsk_1042 \
  --header 'Authorization: Bearer YOUR_API_TOKEN'
```

```json
{
  "id": "tsk_1042",
  "title": "Review release notes",
  "completed": false
}
```

## Create a task

`POST /tasks` creates a task and returns it with status `201 Created`.

```bash
curl --request POST \
  --url https://api.example.test/v1/tasks \
  --header 'Authorization: Bearer YOUR_API_TOKEN' \
  --header 'Content-Type: application/json' \
  --data '{"title":"Review release notes"}'
```

`title` is required and must contain 1–200 characters after trimming whitespace.

```json
{
  "id": "tsk_1043",
  "title": "Review release notes",
  "completed": false
}
```

## Error responses

Errors use a consistent JSON envelope in this sample.

```json
{
  "error": {
    "code": "validation_error",
    "message": "The request could not be processed.",
    "details": [{ "field": "title", "issue": "This field is required." }]
  }
}
```

| HTTP status | Error code | Meaning | What to do |
| --- | --- | --- | --- |
| `400` | `validation_error` | A request field is missing or invalid. | Correct the fields listed in `details`. |
| `401` | `unauthorized` | The token is missing, invalid, or expired. | Check the token and send it in the bearer header. |
| `404` | `task_not_found` | The task does not exist or is not visible to this account. | Check the task ID and account access. |
| `429` | `rate_limited` | The request limit was reached. | Wait before retrying; follow `Retry-After` if provided. |
| `5xx` | `server_error` | The service encountered an unexpected error. | Retry with backoff; contact support if it continues. |

## Sample scope and validation

This is a complete content sample for a fictional API contract, not a tested integration guide. The host, authentication scheme, limits, payloads, and error behavior are illustrative. A production reference should be generated or checked against the API's OpenAPI contract and verified with working credentials in a safe environment.

[Explore the setup guide sample](installation-guide.md) · [Discuss API documentation](../contact.md)
