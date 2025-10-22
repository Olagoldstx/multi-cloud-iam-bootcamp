# Day 2 – AWS IAM Users, Groups & Policies Flashcards

**Q1:** What does “implicit deny” mean in AWS IAM?  
**A1:** By default, all actions are denied unless explicitly allowed by a policy.

**Q2:** What is the difference between a group and a role?  
**A2:** Groups are for permanent human users; roles are for temporary access by trusted entities or services.

**Q3:** What command lists users in a group?  
**A3:** `aws iam get-group --group-name <groupname>`

**Q4:** What are AWS managed policies?  
**A4:** Predefined permission sets maintained by AWS, such as `AdministratorAccess`.

**Q5:** Why use groups instead of attaching policies directly to users?  
**A5:** To simplify management and enforce consistent permissions across teams.
