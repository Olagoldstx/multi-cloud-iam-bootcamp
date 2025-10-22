# 🧩 Day 3 – AWS IAM Roles & Trust Relationships

## 🎓 Professor Mode: Concept Deep Dive

In AWS, **roles** allow trusted entities (users, applications, or services) to temporarily assume specific permissions.

Roles eliminate the need to store long-term credentials and enforce **principle of least privilege** through **trust policies**.

### 🔑 Core IAM Role Concepts

| Concept | Description |
|----------|--------------|
| **Role** | A set of permissions to perform specific actions. |
| **Trust Policy** | Defines *who* can assume the role. |
| **Permission Policy** | Defines *what* the role can do once assumed. |
| **STS (Security Token Service)** | Issues temporary credentials when a role is assumed. |

---

## 🧱 Architect Mode: Hands-On Lab

### 1️⃣ Create a Trust Policy File
```bash
nano trust-policy.json
Paste this:

json
Copy code
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": { "Service": "ec2.amazonaws.com" },
      "Action": "sts:AssumeRole"
    }
  ]
}
2️⃣ Create the Role
bash
Copy code
aws iam create-role \
  --role-name EC2S3AccessRole \
  --assume-role-policy-document file://trust-policy.json
✅ This role allows EC2 instances to assume the role and get temporary permissions.

3️⃣ Attach a Policy to the Role
bash
Copy code
aws iam attach-role-policy \
  --role-name EC2S3AccessRole \
  --policy-arn arn:aws:iam::aws:policy/AmazonS3ReadOnlyAccess
4️⃣ Verify Role and Policies
bash
Copy code
aws iam get-role --role-name EC2S3AccessRole
aws iam list-attached-role-policies --role-name EC2S3AccessRole
5️⃣ Attach Role to EC2 Instance
bash
Copy code
aws ec2 associate-iam-instance-profile \
  --instance-id <EC2_INSTANCE_ID> \
  --iam-instance-profile Name=EC2S3AccessRole
💡 Replace <EC2_INSTANCE_ID> with your test EC2 instance ID.

🧠 HR Mode: Resume + Interview Highlight
“Implemented AWS IAM roles and trust relationships to enable secure temporary access using STS tokens, minimizing credential exposure and enabling least-privilege automation.”

📸 Add a screenshot of your AWS Console showing the EC2 role trust relationship tab.

