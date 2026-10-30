# sc300-entra-lab

Hands-on **Microsoft Entra ID** identity and access management labs, built while preparing for **Microsoft SC-300: Identity and Access Administrator** over a 90-day study plan.

Each lab starts from a real-world requirement, then documents what I configured, **why I chose that design over the alternatives**, how I verified it, and what I learned.

> All tenant IDs, domains, usernames and other identifiers in this repo are redacted or replaced with placeholders (`contoso.onmicrosoft.com`). The labs ran in a personal test tenant, never a production environment.

## Skills demonstrated so far
- **Identity management:** users, bulk provisioning, joiner/mover/leaver handling, delete and restore, groups (including dynamic membership), group-based licensing
- **Least-privilege administration:** Entra RBAC, scoped role assignments, administrative units (dynamic and restricted management), custom roles
- **Tenant configuration:** custom domains, branding, tenant properties, default user permissions
- **Automation:** Microsoft Graph PowerShell

## Coming next in this plan
Device identities, hybrid identity and external identities (B2B, cross-tenant access) write-ups, then authentication (MFA, passwordless, SSPR), Conditional Access, Identity Protection, workload identities (app registrations, managed identities, consent), and identity governance (PIM, access reviews, entitlement management, lifecycle workflows).

## Lab index

| # | Lab | Domain | Status |
|---|---|---|---|
| 01 | [Tenant baseline, lab accounts and Graph PowerShell](labs/lab01-tenant-baseline/README.md) | D1 | ✅ |
| 02 | [Tenant configuration: domains, branding, properties, user settings](labs/lab02-tenant-configuration/README.md) | D1 | ✅ |
| 03 | [Entra RBAC and least-privilege role assignment](labs/lab03-entra-rbac/README.md) | D1 | ✅ |
| 04 | [Scoped helpdesk delegation with administrative units](labs/lab04-administrative-units/README.md) | D1 | ✅ |
| 05 | [User lifecycle and group-based licensing](labs/lab05-user-lifecycle-licensing/README.md) | D1 | ✅ |
| 06 | [Dynamic groups, naming and expiration policies](labs/lab06-dynamic-groups/README.md) | D1 | ✅ |
| 07–13 | Devices, hybrid identity (sync, PHS / PTA), external identities (B2B, cross-tenant) | D1 | ⏳ Write-ups in progress |

_The table grows weekly as labs are completed._

## Repo structure
```
sc300-entra-lab/
├── README.md
├── labs/
│   ├── lab01-tenant-baseline/
│   │   ├── README.md          # write-up (from LAB-WRITEUP-TEMPLATE.md)
│   │   └── screenshots/
│   └── ...
└── scripts/                   # reusable Graph PowerShell snippets (redacted)
```

## Lab environment
- Microsoft Entra ID test tenant (Free → P2 trial → M365 E5 trial over the plan)
- Microsoft Entra admin center, Azure portal
- Microsoft Graph PowerShell SDK

## Certification status
**SC-300: Microsoft Certified: Identity and Access Administrator Associate**, in progress. Target: January 2027.

## About me
Service desk leader with 8 years in identity and access operations, now moving into hands-on identity and access management. I work daily with Active Directory and Microsoft Entra ID administration (user lifecycle, MFA, Temporary Access Pass, password resets, just-in-time admin access through PIM), and I'm deepening that into IAM design and governance.
