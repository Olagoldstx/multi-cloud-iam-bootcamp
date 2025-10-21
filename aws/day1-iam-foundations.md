# 🌍 Day 1 — Multi-Cloud IAM Foundations  

## 🎓 Professor Mode: Concept Deep Dive  
Identity and Access Management (IAM) is the **core of all cloud security**.  
It defines **who** (identity) can do **what** (action) on **which resource** (scope).  

### 🔑 Key Building Blocks
| Cloud | Primary Identity Objects | Policy Model | Root Authority |
|-------|--------------------------|--------------|----------------|
| AWS | Users, Roles, Groups, Policies | JSON-based Policy (Allow/Deny) | Root Account |
| Azure | Users, Roles, Managed Identities, Entra ID | RBAC + Conditional Access | Global Admin |
| GCP | Members, Roles, Bindings | IAM Policy (YAML/JSON) | Organization Owner |

---

## 🧱 Architect Mode: Hands-On Setup  

### 1️⃣ Create Folder Structure Locally
```bash
mkdir -p ~/multi-cloud-iam-bootcamp/{aws,azure,gcp,diagrams,anki}
cd ~/multi-cloud-iam-bootcamp
git add .
git commit -m "Day1: Project scaffold + folder setup"
2️⃣ Initialize AWS CLI Profile (sandbox)
bash
Copy code
aws configure --profile sandbox
# Enter keys (use IAM user with limited permissions)
# Default region: us-east-1
# Output: json
3️⃣ Test Authentication
bash
Copy code
aws sts get-caller-identity --profile sandbox
✅ You should see your AWS account, user ARN, and ID.

🧠 HR Mode: Resume + Interview Highlights
“Configured secure multi-cloud IAM lab with AWS, Azure AD (Entra), and GCP to study identity lifecycle, least privilege, and cross-cloud access control.”

Add screenshot of your folder tree to GitHub commit.
