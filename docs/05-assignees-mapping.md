# Assignees Mapping (Users)

Different platforms identify users differently (email, username, accountId, displayName, or internal IDs).  
Getint provides a flexible user-mapping engine so items are always assigned to the right person — even across systems with incompatible identity models.

This document explains mapping strategies, examples, and best practices.

---

## What Is Assignee Mapping?

An **assignee mapping** connects a user in System A to a user in System B.

Example:
Jira: James Smith → Azure DevOps: jamess@ado.com

Once mapped, Getint can assign synced items to the correct counterpart automatically.

---

## Why Assignee Mapping Is Required

Because platforms use different identifiers:

| Platform | How users are identified |
|---------|---------------------------|
| Jira Cloud | `accountId` (unique) |
| Jira DC | username or email |
| Azure DevOps | email or descriptor |
| ServiceNow | sys_id |
| Asana | gid |
| Monday.com | internal user ID |
| Salesforce | user ID |

These differences mean assignees **cannot** be synced automatically without explicit mappings.

---

## Where Assignee Mapping Applies

- Assigning the correct user on item creation  
- Updating assignee on changes  
- Default/fallback user assignment  
- Shared mappings across multiple integrations  

---

## Types of Assignee Mappings

### **1. One-to-One Mapping (Most Common)**

Alice (Jira) ↔ Alice W. (Azure DevOps)


Direct 1:1 relationships.

---

### **2. One-to-Many Mapping**

Useful when:
- A shared queue is used  
- Only one side has distinct owners

Example:
All Jira users → ServiceNow: “Integration Handler”


---

### **3. Role-Based Mapping**

Instead of mapping individual people, map to role accounts:

Unassigned (Jira) → “Backlog Team” (ADO)


---

### **4. Default / Fallback User**

When a user is missing or unmapped:

- Getint can assign a **default user**
- The default is defined during mapping setup

**Recommended default:** a service or integration account  
(not a real person to avoid accidental assignment)

---

## 🧩 Recommended Best Practices

### **1. Always set a Default User**
This avoids:
- Sync errors caused by unmapped users  
- Items stuck in “pending” state  

---

### **2. Use Shared Mappings when multiple integrations use the same users**
Avoid duplicating user mappings for each integration.  
Shared mappings keep your identity layer consistent.

---

### **3. Avoid mapping to inactive or deactivated users**
This leads to:
- Errors  
- Incorrect assignments  
- Confusing work queues  

---

### **4. Maintain mappings regularly**
Because identities change:
- Email changes  
- People join/leave organizations  
- Migrations occur (e.g., Jira DC → Cloud)

---

## Example Assignee Mapping Table

| Jira User | Azure DevOps User | Notes |
|-----------|-------------------|-------|
| Alice Smith | alice.smith@ado.com | Standard 1:1 mapping |
| Bob (Contractor) | integration-handler@ado.com | Mapped to a role account |
| Unassigned | backlog-team@ado.com | Fallback |
| *any unmapped* | default-user@ado.com | Default user setup |

---

## Testing Assignee Sync

1. Assign a test item to “User A” in System A.  
2. Verify the item is assigned to the mapped user in System B.  
3. Change the assignee on both sides (if bidirectional).  
4. Confirm updates sync correctly.  
5. Test what happens with an unmapped user — should go to the default user.

---

## 🔍 Learn More

Refer to Getint documentation:  
[https://docs.getint.io/getintio-platform/workflows/assignee-mapping](https://docs.getint.io/getintio-platform/workflows/assignees-users-mapping)

