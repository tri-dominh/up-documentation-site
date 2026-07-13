# Authentication

All API endpoints require a valid JWT passed as `Authorization: Bearer <token>`.

Tokens are issued by the Unified Authentication service (OAuth 2.0) using the Authorization Code flow described below.

---

## Authentication hostname

The Unified Authentication service hostname is:

```
https://unified-prod.auth.us-east-1.amazoncognito.com
```

Use this as `{auth_token_url}` in the steps below.

---

## Step 1 — Browser login

Direct the user to the Unified Authentication login page (`{auth_token_url}/oauth2/authorize`) with the following query parameters:

| Parameter | Required | Value |
|---|---|---|
| `response_type` | Yes | `code` |
| `client_id` | Yes | Your application's client ID |
| `redirect_uri` | Yes | Your registered callback URL |
| `scope` | Yes | `openid` |

**Example:**

```
{auth_token_url}/oauth2/authorize?response_type=code&client_id=CLIENT_ID&redirect_uri=https://your-callback-url&scope=openid
```

After a successful login, the service redirects to your `redirect_uri` with a one-time `code` in the query string:

```
https://your-callback-url?code=6bfb35a7-373f-4273-8ec7-042cab70f0ac
```

---

## Step 2 — Exchange code for tokens

Send a `POST` request to the token endpoint to receive an access token and refresh token.

**Headers:**

| Header | Value |
|---|---|
| `Authorization` | `Basic base64(client_id:client_secret)` |
| `Content-Type` | `application/x-www-form-urlencoded` |

**Body:**

| Parameter | Value |
|---|---|
| `grant_type` | `authorization_code` |
| `code` | The one-time code from Step 1 |
| `redirect_uri` | The same callback URL used in Step 1 |

**Example (curl):**

```bash
curl -X POST "{auth_token_url}/oauth2/token" \
  -H "Content-Type: application/x-www-form-urlencoded" \
  -u "CLIENT_ID:CLIENT_SECRET" \
  -d "grant_type=authorization_code" \
  -d "code=6bfb35a7-373f-4273-8ec7-042cab70f0ac" \
  -d "redirect_uri=https://your-callback-url"
```

**Response:**

| Field | Description |
|---|---|
| `access_token` | JWT — use as `Authorization: Bearer <token>` for all API calls |
| `id_token` | JWT containing user identity claims |
| `refresh_token` | Long-lived token — save this to issue new access tokens without re-logging in |
| `expires_in` | Access token lifetime in seconds (default: `3600`) |

---

## Issuing a new access token via refresh token

When the access token expires (default: 1 hour), use the refresh token to get a new one without requiring the user to log in again.

**Headers:**

| Header | Value |
|---|---|
| `Authorization` | `Basic base64(client_id:client_secret)` |
| `Content-Type` | `application/x-www-form-urlencoded` |

**Body:**

| Parameter | Value |
|---|---|
| `grant_type` | `refresh_token` |
| `refresh_token` | The refresh token from Step 2 |

**Example (curl):**

```bash
curl -X POST "{auth_token_url}/oauth2/token" \
  -H "Content-Type: application/x-www-form-urlencoded" \
  -u "CLIENT_ID:CLIENT_SECRET" \
  -d "grant_type=refresh_token" \
  -d "refresh_token=YOUR_REFRESH_TOKEN"
```

**Response:**

| Field | Description |
|---|---|
| `access_token` | New JWT — replace the expired token in your `Authorization` header |
| `id_token` | New JWT containing user identity claims |
| `expires_in` | Access token lifetime in seconds (default: `3600`) |

> **Note:** A new `refresh_token` is not returned. Continue using the same refresh token until it expires (default: 30 days) or is revoked.
