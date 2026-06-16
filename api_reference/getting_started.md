# Getting Started

## Base URL

```
https://api.unified.com
```

Use this as `{base_url}` in the steps below.

## Authentication

All requests require a JWT access token in the `Authorization` header:

```
Authorization: Bearer <access_token>
```

To obtain a token, see [Authentication](authentication.md).

---

## Making a request

```bash
curl -X GET "{base_url}/reporting/v1.0/report-templates" \
  -H "Authorization: Bearer <access_token>"
```

```bash
curl -X POST "{base_url}/v2.0/reports" \
  -H "Authorization: Bearer <access_token>" \
  -H "Content-Type: application/json" \
  -d '{
    "report_template_id": "b62fc3d6-63f9-4e06-9fdb-ae5d24d1f5a9",
    "daterange_preset": "last_30_days",
    "start_date": null,
    "end_date": null,
    "object_type": "initiative",
    "object_ids": ["855916d3-c33a-488e-9885-360086a46cc6"],
    "response_format": "json"
  }'
```

---

## Response format

All responses are JSON.

| Status | Meaning |
|---|---|
| `200` | Success |
| `202` | Request accepted, still processing |
| `400` | Invalid request |
| `401` | Missing or invalid token |
| `404` | Resource not found |
