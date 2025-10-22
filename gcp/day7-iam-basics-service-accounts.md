# 🌐 Day 7 – GCP IAM Basics & Service Accounts

## 🎓 Professor Mode: Concept Deep Dive

Google Cloud IAM governs **who (identity)** can do **what (role/action)** on **which resource (scope)** — just like AWS IAM and Azure RBAC.

It enforces security via **members**, **roles**, and **policy bindings**.

---

### 🧩 Key Concepts

| Concept | Description |
|----------|--------------|
| **Member** | An identity (user, group, service account, or domain) performing an action. |
| **Role** | A collection of permissions (e.g., `roles/viewer`, `roles/editor`). |
| **Policy** | JSON/YAML file binding members to roles for specific resources. |
| **Service Account** | Non-human identity used by applications or services to authenticate to GCP APIs. |
| **Principle of Least Privilege** | Always assign only the roles necessary for a specific job. |

---

## 🧱 Architect Mode: Hands-On Lab

### 1️⃣ Authenticate and Set Project
```bash
gcloud auth login
gcloud projects list
gcloud config set project <PROJECT_ID>
2️⃣ View IAM Policy (who has access)
bash
Copy code
gcloud projects get-iam-policy <PROJECT_ID> --format=json
3️⃣ Create a Service Account
bash
Copy code
gcloud iam service-accounts create devops-agent \
  --display-name "DevOps Automation Agent"
4️⃣ Grant Role to Service Account
bash
Copy code
gcloud projects add-iam-policy-binding <PROJECT_ID> \
  --member="serviceAccount:devops-agent@<PROJECT_ID>.iam.gserviceaccount.com" \
  --role="roles/viewer"
5️⃣ Generate and Download a Key (JSON)
bash
Copy code
gcloud iam service-accounts keys create ~/devops-agent-key.json \
  --iam-account devops-agent@<PROJECT_ID>.iam.gserviceaccount.com
⚠️ Store securely! Never commit this key to GitHub.

6️⃣ Use the Service Account
Example using the key:

bash
Copy code
export GOOGLE_APPLICATION_CREDENTIALS="~/devops-agent-key.json"
gcloud auth activate-service-account --key-file=$GOOGLE_APPLICATION_CREDENTIALS
7️⃣ Verify Identity
bash
Copy code
gcloud auth list
✅ Should show “devops-agent@project-id.iam.gserviceaccount.com” as active.

🧠 HR Mode: Resume + Interview Highlight
“Implemented secure IAM access in Google Cloud using service accounts and least-privilege role assignments, integrating with CI/CD automation pipelines.”

📸 Add a screenshot of your IAM roles view from GCP Console → IAM & Admin → IAM.
