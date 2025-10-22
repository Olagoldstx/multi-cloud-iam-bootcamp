# Day 7 – GCP IAM Basics & Service Accounts Flashcards

**Q1:** What are the three key IAM elements in GCP?  
**A1:** Members, Roles, and Policies.

**Q2:** What command creates a service account?  
**A2:** `gcloud iam service-accounts create <name> --display-name "<desc>"`

**Q3:** What is the purpose of a service account key?  
**A3:** It authenticates applications or tools to access GCP resources securely.

**Q4:** Where should you store service account keys?  
**A4:** In a secure secrets manager (never in GitHub or public repositories).

**Q5:** What’s the default IAM behavior in GCP?  
**A5:** Deny all — you must explicitly grant access via IAM policy bindings
