# 🧠 Day 4 — AWS IAM Best Practices & Policy Boundaries

## 🎓 Professor Mode: Concept Deep Dive

After mastering IAM users, groups, and roles, it’s time to **tighten control** and apply governance-level best practices.

Think of IAM governance as the **guardrails** that prevent misuse — even by admins.

### 🧩 Key Best Practices

| Category | Best Practice | Why It Matters |
|-----------|----------------|----------------|
| **Root Account** | Never use root for daily tasks | Root has unrestricted power |
| **MFA** | Enforce MFA on all users & root | Prevents credential theft |
| **Least Privilege** | Give only what’s needed | Reduces attack surface |
| **Access Reviews** | Rotate keys & review access quarterly | Detect privilege creep |
| **Policy Boundaries** | Cap permissions users or roles can have | Enforces max permission limits |
| **IAM Access Analyzer** | Detect overly permissive policies | Prevents accidental exposure |

---

## 🧱 Architect Mode: Hands-On Lab

### 1️⃣ Create a Policy Boundary (Permission Guardrail)
```bash
nano policy-boundary.json
Paste:

json
Copy code
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "ec2:*",
        "s3:*"
      ],
      "Resource": "*"
    },
    {
      "Effect": "Deny",
      "Action": [
        "iam:*",
        "organizations:*"
      ],
      "Resource": "*"
    }
  ]
}
2️⃣ Upload Policy Boundary
bash
Copy code
aws iam create-policy \
  --policy-name DeveloperBoundary \
  --policy-document file://policy-boundary.json
Copy the returned ARN — you’ll use it below.

3️⃣ Attach the Boundary to a User
bash
Copy code
aws iam put-user-permissions-boundary \
  --user-name CloudEngineer \
  --permissions-boundary arn:aws:iam::<ACCOUNT_ID>:policy/DeveloperBoundary
✅ Now even if CloudEngineer tries to attach admin policies, AWS blocks it.

4️⃣ Verify
bash
Copy code
aws iam get-user --user-name CloudEngineer
You’ll see "PermissionsBoundary" in the output.

5️⃣ Audit Access with IAM Access Analyzer
bash
Copy code
aws accessanalyzer create-analyzer \
  --analyzer-name BoundaryAudit \
  --type ACCOUNT
Then:

bash
Copy code
aws accessanalyzer list-findings --analyzer-name BoundaryAudit
🧠 HR Mode: Resume + Interview Highlight
“Implemented IAM permission boundaries and Access Analyzer for proactive privilege control, enforcing least privilege and preventing privilege escalation.”

✅ Take a screenshot of your AWS IAM boundary and findings, add to your repo
