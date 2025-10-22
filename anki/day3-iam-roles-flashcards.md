# Day 3 – IAM Roles & Trust Relationships Flashcards

**Q1:** What is the purpose of an IAM Role?  
**A1:** To grant temporary permissions to trusted entities without using long-term credentials.

**Q2:** What service provides temporary credentials for roles?  
**A2:** AWS Security Token Service (STS).

**Q3:** What’s the difference between a permission policy and a trust policy?  
**A3:** Permission policy defines what the role can do; trust policy defines who can assume it.

**Q4:** Why is it bad practice to give EC2 instances IAM user credentials?  
**A4:** It exposes long-term credentials, increasing the risk of compromise. Roles provide temporary, revocable access.

**Q5:** How can you check which policies are attached to a role?  
**A5:** `aws iam list-attached-role-policies --role-name <RoleName>`
