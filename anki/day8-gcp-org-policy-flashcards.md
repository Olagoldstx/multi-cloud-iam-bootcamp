# Day 8 – GCP Organization Policies & Custom Roles Flashcards

**Q1:** What is a GCP Organization Policy?  
**A1:** A rule that enforces or restricts behavior across your GCP organization, folders, or projects.

**Q2:** What is a constraint in GCP IAM?  
**A2:** A predefined policy condition, e.g., disabling external IPs or SA key creation.

**Q3:** What command lists available constraints?  
**A3:** `gcloud org-policies list-constraints --organization <ORG_ID>`

**Q4:** How do you enforce least privilege in GCP?  
**A4:** By creating and assigning custom roles with minimal permissions.

**Q5:** What is inheritance in GCP policies?  
**A5:** Organization-level constraints automatically apply to all child folders and projects.
