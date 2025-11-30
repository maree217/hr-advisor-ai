# Deployment Guide

## Prerequisites

- Azure subscription with UK South region access (or AWS eu-west-2)
- HR system API credentials
- Azure AD tenant for SSO
- Domain for hosting (optional)

## Azure Deployment

### 1. Clone Repository
```bash
git clone https://github.com/maree217/hr-advisor-ai
cd hr-advisor-ai
```

### 2. Configure Environment
```bash
cp .env.example .env
# Edit .env with your settings
```

### 3. Deploy Infrastructure
```bash
cd terraform/azure-uk
terraform init
terraform plan -var-file="prod.tfvars"
terraform apply
```

### 4. Deploy Application
```bash
az acr build --registry $ACR_NAME --image hr-advisor:latest .
az containerapp update --name hr-advisor --image $ACR_NAME.azurecr.io/hr-advisor:latest
```

### 5. Configure HR Integration
```bash
az keyvault secret set --vault-name $KEYVAULT_NAME --name hr-api-key --value $HR_API_KEY
```

### 6. Enable SSO
- Register app in Azure AD
- Configure redirect URIs
- Add users/groups

## AWS Deployment

```bash
cd terraform/aws-london
terraform init
terraform apply -var-file="prod.tfvars"
```

## Verification

```bash
# Health check
curl https://your-hr-advisor.azurewebsites.net/health

# Test query
curl -X POST https://your-hr-advisor.azurewebsites.net/api/query \
  -H "Authorization: Bearer $TOKEN" \
  -d '{"query": "How much annual leave do I have?"}'
```

## Monitoring

- Application Insights for logs and metrics
- Azure Monitor alerts for errors
- Custom dashboard for KPIs
