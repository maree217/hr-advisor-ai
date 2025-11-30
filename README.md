# HR Policy Assistant

**Status:** ✅ Production Ready | **Deployment:** Cloud, Hybrid, On-Premise

## Overview

AI-powered HR assistant providing instant, accurate answers to employee and manager queries about HR policies, leave entitlements, and workplace procedures. Integrates with iTrent, ResourceLink, and People HR.

## The Problem

- HR teams receive 50-100 queries/day per 1,000 employees
- 70% are repetitive questions about leave, sickness, pay
- £15-25 cost per HR service desk interaction
- 1-3 day response time for email queries
- No support outside office hours

## The Solution

**Instant HR Support:**
- 24/7 policy question answering
- Personalized leave balance calculations
- Step-by-step process guidance
- Manager coaching for people issues
- Seamless escalation to HR team

**Results:**
- 65% reduction in HR queries (£80k-200k savings)
- Instant response (vs 1-3 days)
- 4.2/5 employee satisfaction
- Consistent, policy-accurate answers

## Query Types Handled

| Category | Examples |
|----------|----------|
| Leave & Absence | "How much annual leave do I have?", "Can I carry over leave?" |
| Sickness | "When do I need a fit note?", "What's the absence policy?" |
| Pay & Benefits | "When is payday?", "How does my pension work?" |
| Flexible Working | "How do I request flexible working?" |
| Family Leave | "What's the maternity entitlement?", "Shared parental leave?" |
| Policies | "What's the disciplinary procedure?", "How do I raise a grievance?" |

## Integration

### Supported HR Systems

| System | Vendor | Integration |
|--------|--------|-------------|
| iTrent | MHR | REST API |
| ResourceLink | Advanced | REST API |
| People HR | Access | REST API |
| Oracle HCM | Oracle | OData |
| SuccessFactors | SAP | OData |

### Channels

- Microsoft Teams (embedded bot)
- Employee self-service portal
- Email (auto-response)
- SMS (for frontline workers)

## Architecture

```
┌─────────────────────────────────────────┐
│         Employee/Manager Query          │
│    Teams | Portal | Email | SMS         │
└──────────────────┬──────────────────────┘
                   │
            ┌──────▼──────┐
            │ Conversation │
            │   Engine    │
            └──────┬──────┘
                   │
     ┌─────────────┼─────────────┐
     │             │             │
┌────▼────┐  ┌─────▼─────┐  ┌────▼────┐
│ Policy  │  │    HR     │  │  Leave  │
│Knowledge│  │  System   │  │  Calc   │
│  Base   │  │   API     │  │ Engine  │
└─────────┘  └─────┬─────┘  └─────────┘
                   │
            ┌──────▼──────┐
            │   iTrent    │
            │ ResourceLink│
            │  People HR  │
            └─────────────┘
```

## Deployment

### Prerequisites
- Azure subscription (UK South) or AWS (eu-west-2)
- HR system API access
- SSO (Azure AD, ADFS, or Okta)

### Quick Start (Azure)
```bash
git clone https://github.com/maree217/hr-advisor-ai
cd hr-advisor-ai/terraform/azure-uk
terraform init && terraform apply
```

### Configuration
```yaml
# config/settings.yaml
hr_system:
  type: itrent  # or resourcelink, peoplehr
  api_url: https://your-hr-system.com/api
  auth: oauth2

knowledge_base:
  policies_path: /policies
  refresh_interval: daily

channels:
  teams: enabled
  portal: enabled
  email: enabled
```

## Compliance

- ✅ GDPR & UK DPA 2018 compliant
- ✅ ISO 27001 security controls
- ✅ Cyber Essentials Plus aligned
- ✅ Full audit logging
- ✅ Data residency: UK only

## Costs

| Organisation Size | Monthly Cost | Annual Savings |
|------------------|--------------|----------------|
| Small (<1,000 staff) | £800-1,500 | £40k-80k |
| Medium (1,000-5,000) | £1,500-4,000 | £80k-200k |
| Large (5,000+) | £4,000-10,000 | £200k-500k |

**Typical ROI:** 3-6 month payback

## Implementation

| Phase | Duration | Activities |
|-------|----------|------------|
| Discovery | 2 weeks | Requirements, DPIA, integration spec |
| Setup | 2 weeks | Deploy, configure, integrate HR system |
| Pilot | 4 weeks | Test with pilot group, refine |
| Rollout | 4 weeks | Full deployment, training |

## Support

- **Documentation:** [docs/](./docs/)
- **Issues:** [GitHub Issues](https://github.com/maree217/hr-advisor-ai/issues)
- **Discussions:** [GitHub Discussions](https://github.com/maree217/hr-advisor-ai/discussions)

## Related Solutions

- [Recruitment Screening AI](https://github.com/maree217/recruitment-screening-ai) - Automated candidate screening
- [Meeting Intelligence](https://github.com/maree217/meeting-intelligence-ai) - Meeting transcription and actions

## License

MIT License - See [LICENSE](./LICENSE)

---

*Production-ready HR AI for UK Public Sector | Integration-First | GDPR Compliant*
