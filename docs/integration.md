# Integration Guide

## Supported HR Systems

### iTrent (MHR)
- **API:** REST API v2
- **Auth:** OAuth 2.0
- **Data:** Employee records, leave balances, absences, contracts
- **Setup:** Contact MHR for API credentials

### ResourceLink (Advanced)
- **API:** REST API
- **Auth:** API Key + OAuth 2.0
- **Data:** Employee data, leave, pay information
- **Setup:** Request API access from Advanced

### People HR
- **API:** REST API
- **Auth:** API Key
- **Data:** Employee records, leave, documents
- **Setup:** Generate API key in People HR admin

## Configuration

```yaml
# config/hr-integration.yaml
hr_system:
  provider: itrent  # itrent | resourcelink | peoplehr
  api_url: https://api.your-hr-system.com
  auth:
    type: oauth2
    client_id: ${HR_CLIENT_ID}
    client_secret: ${HR_CLIENT_SECRET}
  endpoints:
    employees: /api/v2/employees
    leave: /api/v2/leave
    absences: /api/v2/absences
```

## Data Mapping

| HR System Field | Internal Field | Purpose |
|----------------|----------------|---------|
| employee_id | user_id | Unique identifier |
| grade | pay_grade | Terms lookup |
| contract_type | employment_type | Entitlement calc |
| start_date | service_start | Service length |
| leave_balance | annual_leave_remaining | Leave queries |

## Testing

```bash
# Test HR system connectivity
./scripts/test-hr-connection.sh

# Verify data mapping
./scripts/verify-data-mapping.sh --sample-size 100
```
