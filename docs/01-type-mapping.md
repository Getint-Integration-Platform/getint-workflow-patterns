# Type Mapping

Type mapping in Getint defines which item types correspond between connected platforms. 
Each pair of types has its own independent configuration for fields, statuses, comments, 
attachments, and hierarchy.

This document provides reusable patterns and examples for common integrations.

---

## What is Type Mapping?

A **type mapping** pairs items of one type (e.g., Jira Story) with items of another type 
(e.g., Azure DevOps User Story). Each mapping includes:

- Field mapping  
- Status mapping  
- Comment sync  
- Attachment sync  
- Hierarchy configuration  
- Assignee / label / tag mapping  

Each type pairing is configured independently to give fine-grained control.

---

## Recommended Type Pairs (Examples)

### **Jira → Azure DevOps**

| Jira | Azure DevOps |
|------|---------------|
| Epic | Epic |
| Story / Task | User Story |
| Subtask | Task |
| Bug | Bug |

---

### **Jira → Asana**

| Jira | Asana |
|------|--------|
| Epic | Portfolio / Project |
| Story / Task | Task |
| Subtask | Subtask |
| Bug | Task (with label `bug`) |

---

## Example Files

Browse `/examples/<integration>/type-mapping` for ready-to-use YAML patterns.

Examples include:
- Epic ↔ Epic mapping  
- Story ↔ User Story mapping  
- Bug ↔ Bug mapping  
- Subtask ↔ Task mapping  

---

## Checklist When Creating a Type Mapping

- [ ] Define type pairings (one or many)
- [ ] Configure field mapping  
- [ ] Add status mapping  
- [ ] Enable/disable comment sync  
- [ ] Enable/disable attachment sync  
- [ ] Configure hierarchy (Epics/Subtasks)
- [ ] Review assignee + label mappings  
- [ ] Test using sample items  

---

## 🔍 Learn More

Refer to Getint documentation:  
https://docs.getint.io/getintio-platform/workflows/type-mapping
