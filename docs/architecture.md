# Architecture

## Overview

The HR Policy Assistant uses a microservices architecture with an AI conversation engine at its core, connecting to HR systems via secure APIs.

## Components

### Conversation Engine
- **Technology:** Azure OpenAI / AWS Bedrock
- **Purpose:** Natural language understanding and response generation
- **Features:** Intent recognition, entity extraction, context management

### Knowledge Base
- **Technology:** Azure Cognitive Search / Elasticsearch
- **Content:** HR policies, procedures, FAQs, terms and conditions
- **Updates:** Automated refresh from document repositories

### HR System Integration
- **Connectors:** Pre-built for iTrent, ResourceLink, People HR
- **Data:** Employee records, leave balances, employment terms
- **Auth:** OAuth 2.0, API keys, SAML

### Leave Calculation Engine
- **Purpose:** Calculate entitlements based on employment terms
- **Inputs:** Grade, contract type, length of service, working pattern
- **Outputs:** Annual leave, sick pay entitlement, notice periods

## Data Flow

```
User Query → Channel Gateway → Conversation Engine
                                      ↓
                              Intent Classification
                                      ↓
                    ┌─────────────────┼─────────────────┐
                    ↓                 ↓                 ↓
              Knowledge Base    HR System API    Calculation Engine
                    ↓                 ↓                 ↓
                    └─────────────────┼─────────────────┘
                                      ↓
                              Response Generation
                                      ↓
                                 User Response
```

## Security

- All data encrypted in transit (TLS 1.3) and at rest (AES-256)
- API authentication via OAuth 2.0 or API keys
- Role-based access control
- Full audit logging
- UK data residency (Azure UK South / AWS eu-west-2)

## Scalability

- Horizontal scaling via Kubernetes / Azure Container Apps
- Auto-scaling based on query volume
- Target: 10,000 concurrent users
