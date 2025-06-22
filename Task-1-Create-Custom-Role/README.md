# Azure Entra ID & RBAC Configuration 

#Performed By:
Vaishnavi Borase  
Azure Account: 221106014@rcpit.ac.in  
Custom Directory: vaishnaviDirectory (vaishnavidirectory.onmicrosoft.com)

---

#Task Objective:
Perform the following tasks to understand Azure identity and access control:
1. Observe assigned subscriptions
2. Observe or create an Azure Entra ID (formerly Azure AD)
3. Create test users and groups
4. Assign RBAC roles to test users or groups
5. Create and assign a custom role

---

#Task Steps Performed

##1. Observe Assigned Subscriptions
- Logged into Azure Portal: https://portal.azure.com
- Verified active subscription: **Azure for Students**
- Confirmed subscription ownership under primary directory (`221106014@rcpit.ac.in`)

---

##2. Create Own Azure Entra ID (Directory)
- Created a new Entra ID tenant named: **vaishnaviDirectory**
- Default domain: `vaishnavidirectory.onmicrosoft.com`
- Switched directory context to `vaishnaviDirectory`

---

##3. Transfer Subscription to New Directory
- Transferred **Azure for Students** subscription from `rcpit.ac.in` to `vaishnaviDirectory`
- Verified subscription appears under new directory
- Confirmed visibility in "Subscriptions" under `vaishnaviDirectory`

---

##4. Create Test Users and Groups
- Created test user:
  - Username: `testuser01@vaishnavidirectory.onmicrosoft.com`
  - Temporary password set and provided
- Created group:
  - Group name: `TestGroup01`
  - Added `testuser01` as a member

---

##5. Assign Built-in RBAC Role to User
- Role assigned: **Contributor**
- Scope: **Subscription level** (Azure for Students)
- Assigned to: `testuser01`
- Verified via: Subscriptions → Access Control (IAM) → Role Assignments

---

##6. Create and Assign a Custom Role
- Created custom role: `CustomRGReader`
  - Permissions:
    - `Microsoft.Resources/subscriptions/resourceGroups/read`
  - Assignable scope: `/subscriptions/{subscription-id}`
- Assigned role to: `testuser01`
- Verified role assignment from Role Assignment panel

---

##7. Verify Role Access
- Logged in as: `testuser01@vaishnavidirectory.onmicrosoft.com`
- Verified:
  - Access to Azure Portal
  - Limited access per role permissions (Reader or Contributor)
  - Unable to change RBAC or billing settings

---

##Outcome
All required objectives completed successfully:
- Azure Entra ID created and configured
- Test identities and groups configured
- Subscription access assigned and validated
- Role-based access control (RBAC) tested
- Custom role created and applied

---
##Notes:
- All actions tested via incognito window for test user login
- Passwords securely stored or reset post-login
- All changes made using Azure Portal UI

---

##References:
- Azure Portal: https://portal.azure.com
- Entra ID Docs: https://learn.microsoft.com/en-us/entra/
- RBAC Overview: https://learn.microsoft.com/en-us/azure/role-based-access-control/overview

