

## 2. Reports API
After obtaining the final access token, use it to fetch cost reports for organizations, projects, or individual resources.

### 2.1 Get Organization Report
**Endpoint:**

GET https://rest.eazyops.cloud/api/reports/organisation/{id}

**Description:**
Fetches the cost and savings report for an entire organization.

**Request Headers:**

| Header        | Value             |
|---------------|-----------------|
| accept        | application/json, text/plain, */* |
| Authorization	| Bearer <final_token> |

**Example cURL:**

```bash
curl 'https://rest.eazyops.cloud/api/reports/organisation/7bbc83cd-ba37-4f8a-9e34-3d1e24701678' \
  -H 'accept: application/json, text/plain, */*' \
  -H 'Authorization: Bearer <final_token>'
```

**Response Example:**

```json
{
  "account_name": "eazy_547574100405",
  "id": "7bbc83cd-ba37-4f8a-9e34-3d1e24701678",
  "monthly_saving": 65.98,
  "annual_saving": 791.76,
  "monthly_spend": 114.09,
  "annual_spend": 1369.08,
  "resource_count": 16,
  "savings_percentage": 57.83,
  "resources": {
    "disks": { "monthly_saving": 9.6, "annual_saving": 115.2 },
    "static_ips": { "monthly_saving": 28.8, "annual_saving": 345.6 },
    "disk_snapshots": { "monthly_saving": 5.32, "annual_saving": 63.84 },
    "databases": { "monthly_saving": 22.26, "annual_saving": 267.12 }
  },
  "implementation_complexity": { "disks": "Medium", "static_ips": "Low", "disk_snapshots": "Low", "databases": "High" },
  "strategic_recommendations": {
    "immediate_actions": ["Delete unused static IPs.", "Delete unused disk snapshots."],
    "mid_term_actions": ["Resize or delete unused disks."],
    "long_term_actions": ["Optimize database configurations or migrate to cost-effective instances."]
  },
  "projects": [
    { "project_name": "dev-ezo", "resources_count": 7, "monthly_spending": 21.86, "monthly_saving": 21.86 },
    { "project_name": "stg-ezo", "resources_count": 2, "monthly_spending": 70.37, "monthly_saving": 22.26 }
  ]
}
```

### 2.2 Get Project Report
**Endpoint:**

GET https://rest.eazyops.cloud/api/reports/project/{id}

**Description:**
Fetches cost and savings report for a specific project.

**Example cURL:**

```bash
curl 'https://rest.eazyops.cloud/api/reports/project/940f1136-b310-463a-ae48-020e2ef1ad73' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer <final_token>'
```

**Response Example:**

```json
{
  "account_name": "eazy_547574100405",
  "id": "940f1136-b310-463a-ae48-020e2ef1ad73",
  "monthly_saving": 21.86,
  "annual_saving": 262.32,
  "monthly_spend": 21.86,
  "annual_spend": 262.32,
  "resource_count": 7,
  "resources": {
    "disks": { "monthly_saving": 4.8, "annual_saving": 57.6 },
    "static_ips": { "monthly_saving": 14.4, "annual_saving": 172.8 },
    "disk_snapshots": { "monthly_saving": 2.66, "annual_saving": 31.92 }
  },
  "strategic_recommendations": {
    "immediate_actions": ["Delete unused static IPs.", "Delete unused disk snapshots."],
    "mid_term_actions": ["Resize or delete unused disks."]
  }
}
```

### 2.3 Get Resource Report
**Endpoint:**

GET https://rest.eazyops.cloud/api/reports/resource/{id}

**Description:**
Fetches cost and saving report for a specific resource (disk, static IP, database, etc.).

**Example cURL:**

```bash
curl 'https://rest.eazyops.cloud/api/reports/resource/4d722ce9-e552-4aca-a39b-f3c2b98771a6' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer <final_token>'
```

**Response Example:**

```json
{
  "project_name": "dev-ezo",
  "id": "4d722ce9-e552-4aca-a39b-f3c2b98771a6",
  "monthly_saving": 0.8,
  "annual_saving": 9.6,
  "monthly_spend": 0.8,
  "annual_spend": 9.6,
  "savings_percentage": 100.0,
  "action": { "scaling": 0, "delete": 1 },
  "resource_name": "pvc-1bdb7e1e-3ab2-4f65-8b77-1b6fead3221b",
  "resource_type": "compute#disk"
}
```

### 2.4 Path Parameters for Reports API

| Parameter | Description | Example |
|---|---|---|
| type | Entity type for report. One of organisation, project, resource | organisation |
| id | UUID of the entity | 7bbc83cd-ba37-4f8a-9e34-3d1e24701678 |

**Example Endpoints:**

- Organization report: `/api/reports/organisation/{id}`
- Project report: `/api/reports/project/{id}`
- Resource report: `/api/reports/resource/{id}`

```