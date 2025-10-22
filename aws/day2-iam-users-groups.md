# ☁️ Day 2 — AWS IAM: Users, Groups & Policies

## 🎓 Professor Mode: Understanding IAM Hierarchy
AWS IAM operates on the principle of **explicit allow** and **implicit deny**.  
This means a user can do nothing unless explicitly allowed by a policy.

### 🔑 IAM Hierarchy Overview
- **Users** → Represent individual identities (humans, apps, services).  
- **Groups** → Logical collections of users for permission management.  
- **Policies** → JSON documents defining allowed or denied actions.  
- **Roles** → Temporary permissions assumed by trusted entities.

---

## 🧱 Architect Mode: Hands-On Lab

### 1️⃣ Create a Group
```bash
aws iam create-group --group-name CloudAdmins
2️⃣ Create a User and Add to the Group
bash
Copy code
aws iam create-user --user-name CloudEngineer
aws iam add-user-to-group \
  --user-name CloudEngineer \
  --group-name CloudAdmins
3️⃣ Attach AWS-Managed Policy to the Group
bash
Copy code
aws iam attach-group-policy \
  --group-name CloudAdmins \
  --policy-arn arn:aws:iam::aws:policy/AdministratorAccess
4️⃣ Verify Group Membership
bash
Copy code
aws iam get-group --group-name CloudAdmins
✅ Expected output includes CloudEngineer under "Users".

⚙️ Step-Up: Create Custom Policy
bash
Copy code
nano admin-read-only-policy.json
Paste:

json
Copy code
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "ec2:Describe*",
        "s3:List*",
        "iam:Get*"
      ],
      "Resource": "*"
    }
  ]
}
Attach it:

bash
Copy code
aws iam put-group-policy \
  --group-name CloudAdmins \
  --policy-name AdminReadOnly \
  --policy-document file://admin-read-only-policy.json
🧠 HR Mode: Resume + Interview Highlight
“Created AWS IAM architecture with user, group, and policy segmentation enforcing least privilege and role-based access control (RBAC).”

Add screenshot of the IAM group policy page to your GitHub repo.
