# Day 5 – Azure RBAC & Identity Protection Flashcards

**Q1:** What does RBAC stand for in Azure?  
**A1:** Role-Based Access Control.

**Q2:** Difference between role definition vs role assignment?  
**A2:** Definition = permissions; Assignment = bind user/group to role at scope.

**Q3:** How does Conditional Access support Zero-Trust?  
**A3:** Enforces MFA and access rules by user/device/location/risk.

**Q4:** What detects risk-based sign-ins?  
**A4:** Microsoft Entra ID Identity Protection.

**Q5:** CLI to assign a role?  
**A5:** `az role assignment create --assignee <user> --role <role> --scope <scope>`
