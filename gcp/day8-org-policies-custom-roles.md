# 🏗️ Day 8 – GCP Organization Policies & Custom Roles

## 🎓 Professor Mode: Concept Deep Dive

In Google Cloud, **Organization Policies** and **Custom Roles** give you control and precision.  
They’re the foundation of **governance-as-code** and **Zero-Trust compliance** at scale.

---

### 🧩 Core Concepts

| Concept | Description |
|----------|--------------|
| **Organization Policy** | A rule that restricts or enforces behavior across your org, folders, or projects. |
| **Constraint** | A specific restriction, like disabling external IPs or enforcing CMEK for encryption. |
| **Custom Role** | A fine-grained set of permissions tailored for a specific job. |
| **Inheritance** | Policies cascade down: Organization → Folder → Project. |
| **Policy Hierarchy** | Prevents child resources from violating parent constraints. |

---

## 🧱 Architect Mode: Hands-On Lab

### 1️⃣ List All Organization Policies
```bash
gcloud org-policies list --organization <ORG_ID>
2️⃣ View Available Constraints
bash
Copy code
gcloud org-policies list-constraints --organization <ORG_ID> | head -n 20
Common constraints:

constraints/iam.disableServiceAccountKeyCreation

constraints/compute.disableSerialPortAccess

constraints/sql.restrictAuthorizedNetworks

3️⃣ Enforce a Constraint (Example: Disable External SA Keys)
bash
Copy code
gcloud org-policies set-policy disable-sa-key.yaml --organization <ORG_ID>
Create disable-sa-key.yaml:

yaml
Copy code
name: organizations/<ORG_ID>/policies/iam.disableServiceAccountKeyCreation
spec:
  rules:
  - enforce: true
✅ Prevents all service accounts in the organization from creating keys.

4️⃣ Create a Custom Role
bash
Copy code
gcloud iam roles create customViewer \
  --project <PROJECT_ID> \
  --title "Custom Viewer" \
  --description "Viewer with limited permissions" \
  --permissions "compute.instances.get,storage.buckets.list" \
  --stage GA
5️⃣ Assign the Custom Role
bash
Copy code
gcloud projects add-iam-policy-binding <PROJECT_ID> \
  --member="user:devops@company.com" \
  --role="projects/<PROJECT_ID>/roles/customViewer"
✅ Now devops@company.com can only view compute instances and list storage buckets.

6️⃣ Audit Role Usage
bash
Copy code
gcloud policy-intelligence explain grant \
  --member user:devops@company.com \
  --full-resource-name //cloudresourcemanager.googleapis.com/projects/<PROJECT_ID>
🧠 HR Mode: Resume + Interview Highlight
“Enforced GCP organization-level IAM policies and built custom roles for least privilege compliance, implementing constraints-as-code and audit-based governance.”

📸 Add a screenshot of your GCP Organization Policy page and Custom Role configuration.
