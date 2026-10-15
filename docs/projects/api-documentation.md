# REST API Documentation — Portfolio Sample

**Status:** Work in progress · **Type:** Self-directed demonstration project

## Scenario

Document a fictional task-management API implemented with FastAPI.

## Intended audience

Developers integrating the API into applications.

## Planned deliverables

- Getting started and prerequisites
- Authentication and authorization
- Endpoint reference with HTTP methods and paths
- Tested request and response examples
- Error handling and troubleshooting
- OpenAPI specification

## Example reference template

### GET /tasks/{task_id}

**Purpose:** Retrieve one task by ID.

**Path parameter:** `task_id` (integer, required).

**Example request (illustrative; not yet verified):**

```bash
curl http://localhost:8000/tasks/1
```

**Example response (illustrative):**

```json
{"id": 1, "title": "Write API guide", "completed": false}
```

## Next steps

Build a matching FastAPI demo, verify the behavior, document errors, and link its repository here. Do not present untested examples as production-ready.
