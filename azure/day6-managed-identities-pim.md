# 🔐 Day 6 – Azure Managed Identities & Privileged Identity Management (PIM)

## 🎓 Professor Mode: Concept Deep Dive

Azure provides **Managed Identities** to eliminate the need for storing credentials in code,  
and **Privileged Identity Management (PIM)** to grant *time-bound* administrative access.

Together, they form the backbone of **Zero-Trust automation**.

---

### 🧩 Key Concepts

| Concept | Description |
|----------|--------------|
| **Managed Identity** | An identity automatically managed by Azure for apps or VMs to access other Azure resources. |
| **System-Assigned Identity** | Tied to a single resource (e.g., VM, App Service). Deleted when resource is deleted. |
| **User-Assigned Identity** | Independent identity that can be shared across resources. |
| **PIM (Privileged Identity Management)** | Enables JIT elevation for admin roles (temporary permissions). |
| **Activation** | Process of requesting and approving elevated access. |

---

## 🧱 Architect Mode: Hands-On Lab

### 1️⃣ Enable Managed Identity for a VM
```bash
# Login and set your subscription
az login
az account set --subscription "<SUBSCRIPTION_ID>"

# Enable System-Assigned Managed Identity on VM
az vm identity assign \
  --name myVM \
  --resource-group MyResourceGroup
✅ Output should include "type": "SystemAssigned" and "principalId".

2️⃣ Assign Role to Managed Identity
bash
Copy code
az role assignment create \
  --assignee $(az vm show --name myVM --resource-group MyResourceGroup --query "identity.principalId" -o tsv) \
  --role "Reader" \
  --scope /subscriptions/<SUBSCRIPTION_ID>/resourceGroups/MyResourceGroup
💡 The VM can now read resources within the group using its managed identity.

3️⃣ Create a User-Assigned Managed Identity
bash
Copy code
az identity create --name myAppIdentity --resource-group MyResourceGroup
Attach it to another service (e.g., Web App):

bash
Copy code
az webapp identity assign \
  --resource-group MyResourceGroup \
  --name MyWebApp \
  --identities myAppIdentity
4️⃣ Enable Privileged Identity Management (PIM)
bash
Copy code
az role assignment create \
  --assignee <User_Object_ID> \
  --role "User Access Administrator" \
  --scope /subscriptions/<SUBSCRIPTION_ID>
Then go to Portal → Entra ID → Privileged Identity Management → Roles → Azure AD roles

Assign “Global Administrator” as eligible (not active).

Configure approval workflow and time-based activation (e.g., 1-hour window).

5️⃣ Activate Role (JIT)
When a user needs admin access:

bash
Copy code
az role assignment activate \
  --assignee <User_Object_ID> \
  --role "Global Administrator"
✅ They’ll receive temporary privileges that expire automatically.

🧠 HR Mode: Resume + Interview Highlight
“Implemented Azure Managed Identities and PIM for secure automation and JIT access, eliminating stored credentials and enforcing least privilege in enterprise environments.”

📸 Add screenshots of your PIM activation request and Managed Identity overview page.

