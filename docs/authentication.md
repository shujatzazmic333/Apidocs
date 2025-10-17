

## 1. User Authentication

### 1.1 Generate User Token

**Endpoint:**  

POST https://rest.eazyops.cloud/api/v1/users

**Description:**  
Generates a temporary token for a user based on their email. This token is required for subsequent login.

**Request Headers:**

| Header        | Value             |
|---------------|-----------------|
| accept        | application/json |
| Content-Type  | application/json |

**Request Payload:**

```json
{
  "email": "muhammad.hussain@zazmic.com",
  "name": "",
  "receive_token": true,
  "send_email": false
}
```
⚠️ Important: Never set "send_email": true for existing customers. Doing so may trigger unintended email notifications.

**Response Example:**

```json
{
  "email": "muhammad.hussain@zazmic.com",
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
}
```
**Notes:**

The returned token is used for login in the next step.

This token has a short expiry and should be used immediately.

### 1.2 Login with Token

**Endpoint:**

GET https://rest.eazyops.cloud/api/v1/users/login

**Description:**
Exchanges the token from the previous step for a final access token (Bearer) to authenticate API requests.

**Request Headers:**

| Header        | Value             |
|---------------|-----------------|
| accept        | application/json |
| Authorization	| Bearer <token_from_previous_step> |

**Example cURL:**

```bash
curl -X 'GET' \
  'https://rest.eazyops.cloud/api/v1/users/login' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...'
```

**Response Example:**

```json
{
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
}
```
This token is the final Bearer token for all subsequent API requests.

```