# Azure Policy Assignment at Subscription Level

##  Objective:
Create a custom or built-in Azure Policy and assign it at the **Subscription level** to enforce governance and compliance.

---

##  Tools Used:
- Azure Portal: https://portal.azure.com
- Azure Policy Service

---

##  Steps Performed:

###  Step 1: Log in to Azure Portal
- Open a browser and go to: https://portal.azure.com
- Sign in with your Azure account.

---

###  Step 2: Select Subscription
- In the left-hand navigation, click on **"Subscriptions"**.
- Choose the target subscription (*Azure for Students*).

---

###  Step 3: Open Policy Service
- In the search bar, type **“Policy”** and click on it.
- This opens the **Azure Policy dashboard**.

---

###  Step 4: (Optional) Create a Custom Policy Definition

#### ➤ Navigate to Definitions
- Click on **“Definitions”** from the left panel.
- Click on **“+ Policy definition”**.

#### ➤ Fill the Form:
- **Name**: `Allow only East US`
- **Definition Location**: Select your subscription.
- **Description**: "Allows resource creation only in East US."
- **Category**: Create or select one.
- **Policy Rule**:

```json
{
  "if": {
    "field": "location",
    "notEquals": "eastus"
  },
  "then": {
    "effect": "deny"
  }
}
Click Save.



### Step 5: Assign the Policy
➤ Navigate to Assignments
Go back to the Policy dashboard.

Click on “Assignments”.

Click on “+ Assign Policy”.

➤ Fill the Assignment Details:
Scope: Select the subscription.

Policy Definition: Choose either a built-in policy or the custom one you just created.

Assignment Name: e.g., Restrict to East US

➤ (Optional) Configure Parameters:
If using a parameterized policy (e.g., allowed regions, tags), set the required values.

Click Next → Next → Review + Create → Create

Result:
The policy is now active and assigned at the subscription level. It enforces rules on all resource deployments under that subscription.

Notes:
You can monitor policy compliance from the Compliance tab under Policy.

Policy effects include: Deny, Audit, Append, DeployIfNotExists, etc.
