---
title: "API Reference"
category: "Development"
date: 2024-12-28
author: "Development Team"
tags: [api, reference, endpoints, authentication]
excerpt: "Complete API reference documentation for ProcStudio services including authentication, endpoints, and examples."
breadcrumbs: ["Development", "API Reference"]
related_docs: ["getting-started", "authentication-guide"]
---

# API Reference

This document provides comprehensive reference documentation for the ProcStudio API. Our REST API allows you to programmatically interact with ProcStudio services.

## Base URL

```
https://api.procstudio.com.br/v1
```

## Authentication

All API requests require authentication using API keys. Include your API key in the request header:

```http
Authorization: Bearer YOUR_API_KEY
Content-Type: application/json
```

### Getting an API Key

1. Log into your ProcStudio dashboard
2. Navigate to Settings > API Keys
3. Click "Generate New Key"
4. Copy and securely store your key

## Rate Limiting

API requests are limited to:
- **100 requests per minute** for standard accounts
- **500 requests per minute** for premium accounts

Rate limit headers are included in all responses:

```http
X-RateLimit-Limit: 100
X-RateLimit-Remaining: 95
X-RateLimit-Reset: 1640995200
```

## Documents API

### List Documents

Retrieve a list of documents with optional filtering.

**Endpoint:** `GET /documents`

**Parameters:**
- `page` (integer, optional): Page number (default: 1)
- `limit` (integer, optional): Items per page (default: 20, max: 100)
- `status` (string, optional): Filter by status (`draft`, `active`, `archived`)
- `type` (string, optional): Filter by document type
- `created_after` (string, optional): ISO 8601 date string

**Example Request:**
```bash
curl -X GET "https://api.procstudio.com.br/v1/documents?page=1&limit=10" \
  -H "Authorization: Bearer YOUR_API_KEY"
```

**Example Response:**
```json
{
  "data": [
    {
      "id": "doc_123456789",
      "title": "Contract Template",
      "type": "contract",
      "status": "active",
      "created_at": "2024-12-28T10:00:00Z",
      "updated_at": "2024-12-28T10:00:00Z",
      "author": {
        "id": "user_987654321",
        "name": "João Silva",
        "email": "joao@example.com"
      }
    }
  ],
  "pagination": {
    "current_page": 1,
    "total_pages": 5,
    "total_items": 50,
    "items_per_page": 10
  }
}
```

### Get Document

Retrieve a specific document by ID.

**Endpoint:** `GET /documents/{id}`

**Example Request:**
```bash
curl -X GET "https://api.procstudio.com.br/v1/documents/doc_123456789" \
  -H "Authorization: Bearer YOUR_API_KEY"
```

**Example Response:**
```json
{
  "id": "doc_123456789",
  "title": "Contract Template",
  "content": "Document content here...",
  "type": "contract",
  "status": "active",
  "metadata": {
    "version": "1.2",
    "template_id": "tpl_987654321",
    "tags": ["contract", "template", "legal"]
  },
  "created_at": "2024-12-28T10:00:00Z",
  "updated_at": "2024-12-28T10:00:00Z",
  "author": {
    "id": "user_987654321",
    "name": "João Silva",
    "email": "joao@example.com"
  }
}
```

### Create Document

Create a new document.

**Endpoint:** `POST /documents`

**Request Body:**
```json
{
  "title": "New Document",
  "content": "Document content...",
  "type": "contract",
  "status": "draft",
  "metadata": {
    "template_id": "tpl_987654321",
    "tags": ["contract", "new"]
  }
}
```

**Example Request:**
```bash
curl -X POST "https://api.procstudio.com.br/v1/documents" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "title": "New Contract",
    "content": "This is a new contract...",
    "type": "contract",
    "status": "draft"
  }'
```

### Update Document

Update an existing document.

**Endpoint:** `PUT /documents/{id}`

**Request Body:**
```json
{
  "title": "Updated Document Title",
  "content": "Updated content...",
  "status": "active"
}
```

### Delete Document

Delete a document.

**Endpoint:** `DELETE /documents/{id}`

**Example Request:**
```bash
curl -X DELETE "https://api.procstudio.com.br/v1/documents/doc_123456789" \
  -H "Authorization: Bearer YOUR_API_KEY"
```

## Templates API

### List Templates

**Endpoint:** `GET /templates`

**Parameters:**
- `category` (string, optional): Filter by category
- `active_only` (boolean, optional): Show only active templates

### Get Template

**Endpoint:** `GET /templates/{id}`

### Create Template

**Endpoint:** `POST /templates`

**Request Body:**
```json
{
  "name": "Invoice Template",
  "category": "financial",
  "content": "Template content with {{variables}}",
  "variables": [
    {
      "name": "client_name",
      "type": "string",
      "required": true
    },
    {
      "name": "amount",
      "type": "number",
      "required": true
    }
  ]
}
```

## Users API

### Get Current User

**Endpoint:** `GET /user`

**Example Response:**
```json
{
  "id": "user_987654321",
  "name": "João Silva",
  "email": "joao@example.com",
  "role": "admin",
  "plan": "premium",
  "created_at": "2024-01-15T08:00:00Z",
  "settings": {
    "timezone": "America/Sao_Paulo",
    "language": "pt-BR"
  }
}
```

### Update User Settings

**Endpoint:** `PATCH /user`

**Request Body:**
```json
{
  "settings": {
    "timezone": "America/Sao_Paulo",
    "language": "pt-BR",
    "notifications": {
      "email": true,
      "push": false
    }
  }
}
```

## Webhooks API

### List Webhooks

**Endpoint:** `GET /webhooks`

### Create Webhook

**Endpoint:** `POST /webhooks`

**Request Body:**
```json
{
  "url": "https://your-app.com/webhook",
  "events": ["document.created", "document.updated"],
  "secret": "your_webhook_secret"
}
```

**Supported Events:**
- `document.created`
- `document.updated`
- `document.deleted`
- `template.created`
- `template.updated`
- `user.updated`

## Error Handling

The API uses conventional HTTP response codes:

- `200` - Success
- `201` - Created
- `400` - Bad Request
- `401` - Unauthorized
- `403` - Forbidden
- `404` - Not Found
- `422` - Validation Error
- `429` - Rate Limited
- `500` - Internal Server Error

**Error Response Format:**
```json
{
  "error": {
    "code": "validation_failed",
    "message": "The request failed validation",
    "details": [
      {
        "field": "title",
        "message": "Title is required"
      }
    ]
  }
}
```

## SDKs and Libraries

Official SDKs are available for:

- **JavaScript/Node.js**: `npm install procstudio-sdk`
- **Python**: `pip install procstudio-python`
- **PHP**: `composer require procstudio/sdk`
- **Ruby**: `gem install procstudio-ruby`

### JavaScript Example

```javascript
const ProcStudio = require('procstudio-sdk');

const client = new ProcStudio({
  apiKey: 'YOUR_API_KEY'
});

// List documents
const documents = await client.documents.list({
  page: 1,
  limit: 10
});

// Create document
const newDoc = await client.documents.create({
  title: 'New Document',
  content: 'Document content...',
  type: 'contract'
});
```

### Python Example

```python
import procstudio

client = procstudio.Client(api_key='YOUR_API_KEY')

# List documents
documents = client.documents.list(page=1, limit=10)

# Create document
new_doc = client.documents.create(
    title='New Document',
    content='Document content...',
    type='contract'
)
```

## Testing

### Sandbox Environment

Use the sandbox environment for testing:

```
https://api-sandbox.procstudio.com.br/v1
```

Sandbox API keys are prefixed with `sk_test_`.

### Postman Collection

Download our Postman collection for easy API testing:
[ProcStudio API Collection](https://api.procstudio.com.br/postman)

## Support

For API support:
- Email: api-support@procstudio.com.br
- Documentation: https://docs.procstudio.com.br
- Status Page: https://status.procstudio.com.br

---

*This API documentation is confidential and intended for internal development use only.*