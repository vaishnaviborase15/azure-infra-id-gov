# Azure Key Vault Setup and Secret Management using Azure CLI

## Objective

This guide provides step-by-step instructions to:
1. Create an Azure Key Vault
2. Store a secret in the Key Vault
3. Configure access policies for users or applications
4. Retrieve the secret using Azure CLI

**Reference Video:** [Azure Key Vault Tutorial](https://www.youtube.com/watch?v=JDRixckApxM&pp=ygUPYXp1cmUga2V5IHZhdWx0)

---

##  Prerequisites

- Active Azure Subscription
- Azure CLI installed and logged in (`az login`)
- Sufficient permissions (Owner/Contributor or Key Vault Secrets Officer)
- Set your subscription (if required):

```bash
az account set --subscription "Azure Student Subscription"
```

---

##  Step-by-Step Implementation

###  Step 1: Create a Resource Group

```bash
az group create \
  --name MyResourceGroup \
  --location eastus
```

---

###  Step 2: Create an Azure Key Vault

```bash
az keyvault create \
  --name MyKeyVaultName123 \
  --resource-group MyResourceGroup \
  --location eastus
```

> `MyKeyVaultName123` must be **globally unique**.

---

###  Step 3: Store a Secret in the Key Vault

```bash
az keyvault secret set \
  --vault-name MyKeyVaultName123 \
  --name MySecretName \
  --value "ThisIsMySecretValue"
```

---

###  Step 4: Configure Access Policies

####  For Yourself (Signed-in User)

1. Get your Azure AD Object ID:

```bash
az ad signed-in-user show --query objectId -o tsv
```

2. Grant access to secrets:

```bash
az keyvault set-policy \
  --name MyKeyVaultName123 \
  --object-id <your-object-id> \
  --secret-permissions get list set delete
```

####  For an Application (Service Principal) — Optional

1. Create service principal:

```bash
az ad sp create-for-rbac --name MyApp
```

2. Grant secret access to the app:

```bash
az keyvault set-policy \
  --name MyKeyVaultName123 \
  --spn <app-client-id> \
  --secret-permissions get list
```

---

###  Step 5: Retrieve a Secret from the Key Vault

```bash
az keyvault secret show \
  --name MySecretName \
  --vault-name MyKeyVaultName123 \
  --query value -o tsv
```

📥 Output:
```
ThisIsMySecretValue
```

---

##  Summary Table

| Step                        | Command or Action                                   |
|-----------------------------|-----------------------------------------------------|
| Create Resource Group       | `az group create`                                   |
| Create Key Vault            | `az keyvault create`                                |
| Store Secret                | `az keyvault secret set`                            |
| Configure Access (User)     | `az keyvault set-policy` with `--object-id`         |
| Configure Access (App)      | `az ad sp create-for-rbac`, then `set-policy`       |
| Retrieve Secret             | `az keyvault secret show`                           |

---

## Author

**Vaishnavi Borase**  
Azure Account: `221106014@rcpit.ac.in`  
Custom Directory: `vaishnaviDirectory (vaishnavidirectory.onmicrosoft.com)`

---
