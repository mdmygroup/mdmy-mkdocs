# API Reference

## Introduction

The MDMY API allows you to programmatically access and control MDMY services. This reference documents all endpoints, parameters, and responses.

Base URL for all API calls:
```
https://api.example.com/v2
```

## Authentication

All API requests require authentication using an API key. You can obtain an API key from your MDMY dashboard.

Include your API key in the `Authorization` header:

```
Authorization: Bearer YOUR_API_KEY
```

## Response Format

All responses are returned in JSON format and include a standard structure:

```json
{
  "success": true,
  "data": {
    // Response data here
  },
  "meta": {
    "totalPages": 3,
    "currentPage": 1,
    "perPage": 10,
    "totalCount": 27
  }
}
```

Error responses follow this structure:

```json
{
  "success": false,
  "error": {
    "code": "invalid_request",
    "message": "Description of the error",
    "details": {
      // Additional error information if available
    }
  }
}
```

## Rate Limiting

API requests are subject to rate limiting to ensure fair usage and system stability. Current limits:

- 100 requests per minute for standard accounts
- 1000 requests per minute for enterprise accounts

Rate limit information is included in response headers:

- `X-RateLimit-Limit`: Total requests allowed per minute
- `X-RateLimit-Remaining`: Requests remaining in current window
- `X-RateLimit-Reset`: Unix timestamp when the rate limit resets

## Common Parameters

Many endpoints support these common query parameters:

| Parameter | Type | Description |
|-----------|------|-------------|
| `page` | integer | Page number for paginated results (default: 1) |
| `perPage` | integer | Number of results per page (default: 10, max: 100) |
| `sort` | string | Field to sort by (e.g., `name`, `createdAt`) |
| `order` | string | Sort order (`asc` or `desc`, default: `asc`) |
| `fields` | string | Comma-separated list of fields to include |

## Endpoints

### Projects

#### List Projects

```http
GET /projects
```

Query Parameters:

| Parameter | Type | Description |
|-----------|------|-------------|
| `status` | string | Filter by project status (`active`, `archived`, `draft`) |
| `createdAfter` | ISO date | Filter by creation date after specified date |
| `category` | string | Filter by project category |

Response:

```json
{
  "success": true,
  "data": [
    {
      "id": "proj_123abc",
      "name": "Sample Project",
      "description": "A sample project",
      "status": "active",
      "createdAt": "2025-03-15T14:30:00Z",
      "updatedAt": "2025-04-01T09:15:22Z"
    },
    // Additional projects...
  ],
  "meta": {
    "totalPages": 3,
    "currentPage": 1,
    "perPage": 10,
    "totalCount": 27
  }
}
```

#### Get a Project

```http
GET /projects/{projectId}
```

Path Parameters:

| Parameter | Description |
|-----------|-------------|
| `projectId` | The unique identifier of the project |

Response:

```json
{
  "success": true,
  "data": {
    "id": "proj_123abc",
    "name": "Sample Project",
    "description": "A sample project",
    "status": "active",
    "settings": {
      "visibility": "private",
      "notifications": true
    },
    "createdBy": "user_456def",
    "createdAt": "2025-03-15T14:30:00Z",
    "updatedAt": "2025-04-01T09:15:22Z"
  }
}
```

#### Create a Project

```http
POST /projects
```

Request Body:

```json
{
  "name": "New Project",
  "description": "Description of the new project",
  "status": "draft",
  "settings": {
    "visibility": "private",
    "notifications": true
  }
}
```

Response:

```json
{
  "success": true,
  "data": {
    "id": "proj_789ghi",
    "name": "New Project",
    "description": "Description of the new project",
    "status": "draft",
    "settings": {
      "visibility": "private",
      "notifications": true
    },
    "createdBy": "user_456def",
    "createdAt": "2025-04-28T10:00:00Z",
    "updatedAt": "2025-04-28T10:00:00Z"
  }
}
```

#### Update a Project

```http
PATCH /projects/{projectId}
```

Path Parameters:

| Parameter | Description |
|-----------|-------------|
| `projectId` | The unique identifier of the project |

Request Body:
```json
{
  "name": "Updated Project Name",
  "description": "Updated project description",
  "status": "active"
}
```

Response:
```json
{
  "success": true,
  "data": {
    "id": "proj_123abc",
    "name": "Updated Project Name",
    "description": "Updated project description",
    "status": "active",
    "settings": {
      "visibility": "private",
      "notifications": true
    },
    "createdBy": "user_456def",
    "createdAt": "2025-03-15T14:30:00Z",
    "updatedAt": "2025-04-28T11:15:00Z"
  }
}
```

#### Delete a Project

```http
DELETE /projects/{projectId}
```

Path Parameters:

| Parameter | Description |
|-----------|-------------|
| `projectId` | The unique identifier of the project |

Response:

```json
{
  "success": true,
  "data": {
    "message": "Project successfully deleted"
  }
}
```

### Users

#### Get Current User

```http
GET /users/me
```

Response:

```json
{
  "success": true,
  "data": {
    "id": "user_456def",
    "email": "user@example.com",
    "name": "John Doe",
    "role": "admin",
    "createdAt": "2024-10-12T08:30:00Z",
    "lastLoginAt": "2025-04-25T15:42:10Z"
  }
}
```

## Webhooks

You can configure webhooks to receive real-time notifications when events occur in your MDMY account.

### Webhook Event Types

| Event Type | Description |
|------------|-------------|
| `project.created` | Triggered when a new project is created |
| `project.updated` | Triggered when a project is updated |
| `project.deleted` | Triggered when a project is deleted |
| `user.login` | Triggered when a user logs in |
| `data.import.completed` | Triggered when a data import completes |

### Webhook Payload Example

```json
{
  "event": "project.created",
  "timestamp": "2025-04-28T10:00:00Z",
  "data": {
    "id": "proj_789ghi",
    "name": "New Project",
    "createdBy": "user_456def"
  }
}
```

## Error Codes

| Code | Description | HTTP Status |
|------|-------------|-------------|
| `authentication_required` | No API key provided | 401 |
| `invalid_api_key` | API key is invalid or expired | 401 |
| `permission_denied` | Insufficient permissions | 403 |
| `resource_not_found` | Requested resource not found | 404 |
| `validation_error` | Invalid request parameters | 400 |
| `rate_limit_exceeded` | Too many requests | 429 |
| `internal_error` | Internal server error | 500 |

## SDKs and Libraries

We provide official client libraries for several programming languages:

- [JavaScript/TypeScript](https://github.com/mdmy-group/mdmy-js)
- [Python](https://github.com/mdmy-group/mdmy-python)
- [PHP](https://github.com/mdmy-group/mdmy-php)
- [Ruby](https://github.com/mdmy-group/mdmy-ruby)
- [Java](https://github.com/mdmy-group/mdmy-java)

## API Versioning

The API version is included in the base URL. When we release a new incompatible API version, we will increment the version number (e.g., from `/v2` to `/v3`).

Previous versions remain available for at least 12 months after a new version is released.

## Security and Compliance

Our API adheres to industry security standards including:

- TLS 1.2+ encryption for all communications
- OAuth 2.0 for authorization
- GDPR-compliant data handling
- Regular security audits and penetration testing

## Support

If you encounter any issues or have questions about our API:

- Check our [API documentation](https://api.example.com/docs)
- Contact us at api-support@example.com
- Submit issues via our [GitHub repository](https://github.com/mdmy-group/api-issues)

---

*Last updated: April 2025*