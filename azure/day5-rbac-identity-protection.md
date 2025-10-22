# 🔷 Day 5 – Azure RBAC & Identity Protection

## 🎓 Professor Mode: Concept Deep Dive

Azure uses **Microsoft Entra ID** (formerly Azure AD) for all identity and access control.  
IAM in Azure is built on **RBAC** (Role-Based Access Control) and **Conditional Access** for Zero Trust security.

### 🧩 Core Concepts

| Concept | Description |
|----------|--------------|
| **Azure AD Tenant** | Your identity boundary; like an AWS account’s root domain. |
| **User / Group / Service Principal** | Identities used by people or apps. |
| **Role Definition** | A JSON set of permissions (actions). |
| **Role Assignment** | Binds a role to a user/group at a scope (subscription, resource group, resource). |
| **Conditional Access Policy** | Defines when and how users must authenticate (e.g., MFA, location, device). |
| **Identity Protection** | Detects risk-based sign-ins and compromised accounts. |

---

## 🧱 Architect Mode: Hands-On Lab (Azure CLI)

### 1️⃣ Login and Set Subscription
```bash
az login
az account list --output table
az account set --subscription "<SUBSCRIPTION_NAME_OR_ID>"
2️⃣ Create a User and Group
bash
Copy code
az ad user create \
  --display-name "CloudOps Engineer" \
  --user-principal-name cloudops@<tenant>.onmicrosoft.com \
  --password "StrongP@ss!2025"

az ad group create --display-name "CloudAdmins" --mail-nickname "cloudadmins"

az ad group member add \
  --group "CloudAdmins" \
  --member-id $(az ad user show --id cloudops@<tenant>.onmicrosoft.com --query id -o tsv)
3️⃣ Assign a Built-in Role at Subscription Level
bash
Copy code
az role assignment create \
  --assignee cloudops@<tenant>.onmicrosoft.com \
  --role "Contributor" \
  --scope /subscriptions/<SUBSCRIPTION_ID>
✅ This grants Contributor access to the entire subscription.

4️⃣ Enable MFA for Users
bash
Copy code
az ad mfa policy create \
  --enforce on \
  --method appNotification
Or through Portal → Entra ID → Security → Conditional Access → Policies → Create “Require MFA for Admins”.

5️⃣ Create Conditional Access Policy Example
bash
Copy code
az ad conditional-access policy create \
  --display-name "BlockLegacyAuth" \
  --conditions '{"users":{"include":["All"]}}' \
  --grant-controls '{"builtInControls":["mfa"]}' \
  --state enabled
🧠 HR Mode: Resume + Interview Highlight
“Designed and implemented Azure RBAC and Conditional Access for secure identity governance and MFA enforcement using Microsoft Entra ID (Azure AD).”

📸 Take a screenshot of your Conditional Access Policy overview page and commit to GitHub.
