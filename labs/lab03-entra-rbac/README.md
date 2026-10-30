# Lab 03: Entra RBAC and Least-Privilege Role Assignment

| | |
|---|---|
| **SC-300 domain** | D1: Implement and manage user identities |
| **Objective** | Manage Entra built-in roles; apply least privilege |
| **License needed** | Entra ID Free |

## 1. Requirement
A helpdesk agent must reset passwords for regular users but must **not** be able to take over administrator accounts.

## 2. What I configured
1. Compared **Password Administrator**, **Helpdesk Administrator** and **Authentication Administrator** (descriptions + permission lists).
2. Assigned **Helpdesk Administrator** to the test user `paris.helpdesk@contoso.onmicrosoft.com`.
3. Listed every role assignment with Graph PowerShell to see the RBAC model (role + principal + scope).

```powershell
Connect-MgGraph -TenantId "contoso.onmicrosoft.com" -Scopes "RoleManagement.Read.Directory","Directory.Read.All"
Get-MgRoleManagementDirectoryRoleAssignment -All | Select-Object RoleDefinitionId, DirectoryScopeId
```

## 3. Why this design
| Role | Decision |
|---|---|
| Helpdesk Administrator | ✅ Resets passwords for non-admins and can revoke sessions |
| User Administrator | ❌ Can also create and delete users and manage groups: more than needed |
| Global Administrator | ❌ Never for helpdesk tasks |

## 4. Verification
- As the helpdesk user: resetting a **regular user's** password ✅ succeeded.
- Resetting a **Global Administrator's** password ❌ was blocked by the privileged-role hierarchy.
- PowerShell showed `DirectoryScopeId = /` (tenant-wide) for every assignment.

## 5. Screenshots
_Add redacted screenshots of the role assignment and the blocked reset._

## 6. What I learned
- **RBAC = role definition + principal + scope** (tenant `/`, administrative unit, or a single app).
- Only **Privileged Authentication Administrator** (or Global Admin) can reset a Global Admin's password.
- Pick the **narrowest role that works** (Password Admin < Helpdesk Admin < User Admin; Application Developer for registering apps).
- Role-assignable groups are set at creation only, can't be dynamic, and are managed only by Global Admin / Privileged Role Admin. **PIM for Groups** can grant several roles with one activation.
- "Scope" means two things: the **RBAC scope** (`DirectoryScopeId`) vs **OAuth permission scopes** (e.g. `Directory.Read.All`).
