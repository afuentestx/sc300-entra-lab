# Lab 01: Tenant Baseline, Lab Accounts and Graph PowerShell

| | |
|---|---|
| **SC-300 domain** | D1: Implement and manage user identities |
| **Objective** | Configure and manage a Microsoft Entra tenant; manage users |
| **License needed** | Entra ID Free |

## 1. Requirement
Prepare a clean identity lab tenant: confirm administrative access, create a dedicated cloud-native admin account and test users, and connect with Microsoft Graph PowerShell for scripted administration.

## 2. What I configured
1. Ran a tenant health check in the Entra admin center: license tier (Free), Global Administrator assignment, security defaults (enabled).
2. Found that my sign-in account was a **personal Microsoft account** shown as an external (`#EXT#`) identity, so I created a **native cloud admin account** (`labadmin@contoso.onmicrosoft.com`) with Global Administrator and registered MFA.
3. Created test users with **Department** and **Usage location** set (needed for licensing in later labs).
4. Installed the Microsoft Graph PowerShell SDK, fixed the Windows **execution policy** that blocked the module from loading, and connected to the tenant.

```powershell
Set-ExecutionPolicy -Scope CurrentUser -ExecutionPolicy RemoteSigned
Connect-MgGraph -TenantId "contoso.onmicrosoft.com" -Scopes "User.Read.All","Organization.Read.All"
Get-MgUser -Filter "department eq 'Sales'" -ConsistencyLevel eventual -CountVariable c | Select-Object DisplayName
```

## 3. Why this design
| Option | Decision |
|---|---|
| Native cloud admin account | ✅ A tenant-owned identity; works reliably with licensing, PIM and Graph; acts as a second admin path |
| Keep using the personal (`#EXT#`) account only | ❌ An external identity, and a single point of failure |
| Microsoft Graph PowerShell | ✅ Supported SDK |
| AzureAD / MSOnline modules | ❌ Retired |

## 4. Verification
- The Graph connection reported **"Connected via delegated access"**, and the Sales filter returned the expected user.

## 5. Screenshots
_Add redacted screenshots to `screenshots/` (blur the tenant ID, domain, UPNs and your name)._

## 6. What I learned
- **Delegated permissions:** the app acts on behalf of the signed-in user and can never exceed that user's rights (app permissions ∩ user rights).
- Graph PowerShell is itself an app: **one application object** (Microsoft's tenant) and **a service principal in my tenant**.
- **Usage location** is required for direct license assignment. It's unrelated to Conditional Access locations.

## 7. Cleanup
Kept the admin account and test users for later labs.
