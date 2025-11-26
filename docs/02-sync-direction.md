# Sync Direction (Bidirectional & Unidirectional)

Sync direction defines **how data flows between two systems** connected through Getint. 
You can configure direction at the **integration level** or **per individual field**, allowing deep control over what changes are exchanged.

This guide summarizes patterns, best practices, and common configurations.

---

## What Is Sync Direction?

Each field and data type can be synced in one of three modes:

### **1. Bidirectional (↔)**
Changes flow **both ways**.  
Examples:
- Title ↔ Title  
- Description ↔ Description  
- Comments ↔ Comments (common in collaboration environments)

### **2. Left → Right (One-Way)**
Source system is the *single source of truth*.  
Examples:
- Severity from ITSM tool → Development tool  
- Customer Impact field → Engineering team only

### **3. Right → Left (One-Way)**
Destination system is the source of truth.  
Less common, but useful when:
- Developers control workflow  
- ITSM analysts shouldn’t override engineering data

---

## Where Sync Direction Applies

- Field Mapping  
- Comments  
- Attachments  
- Status Mapping  
- Hierarchy (Epics / Subtasks)  
- Assignee / Reporter  
- Labels / Tags  

Each mapping pair supports different direction options depending on the platform.

---

## Recommended Best Practices

### **1. Keep status mapping bidirectional (↔) when both teams manage workflow**
Use when:
- Both Jira and Azure DevOps are actively updating work  
- Both teams track progress in real time

### **2. Use one-way sync for system-specific fields**
Examples:
- Azure DevOps Iteration Path → Jira Fix Version (one-way L → R)  
- ServiceNow “Customer Priority” → Jira custom field

### **3. Use one-way sync for sensitive or regulated fields**
E.g. fields that:
- Should only be updated inside ITSM  
- Are tied to approvals or compliance rules  
- Contain customer PII (stored only on one side)

### **4. Treat comments carefully**
Recommended:
- Customer → Vendor: enable  
- Vendor → Customer: optional  
- Developer-only discussion: disable

### **5. Attachments usually work best in one direction**
This avoids:
- Infinite loops  
- Storage explosions  
- Duplicate attachments caused by updates

---

## Example Sync Pattern Table

| Field | Jira → ADO | ADO → Jira | Notes |
|------|-------------|-------------|-------|
| Summary | ✔️ | ✔️ | Usually bidirectional |
| Description | ✔️ | ✔️ | Recommended ↔ |
| Status | ✔️ | ✔️ | Use mapped status pairs |
| Labels/Tags | ✔️ | ✔️ | Be aware of platform limitations |
| Assignee | ✔️ | ✔️ | Needs user mapping |
| Fix Version / Iteration | ✔️ | ❌ | Often one-way |
| Attachments | ✔️ | Optional | One-way preferred |
| Comments | ✔️ | Optional | Optional reverse direction |

---

## Testing Sync Direction

Before enabling full sync, test:

1. Create an item in System A  
2. Check what fields appear in System B  
3. Modify fields on each side  
4. Observe what syncs back  
5. Validate no loops or noise occur

---

## 🔍 Learn More

Refer to Getint documentation:  
[https://docs.getint.io/getintio-platform/workflows/configuring-your-data-sync](https://docs.getint.io/getintio-platform/workflows/configuring-your-data-sync-bidirectional-and-unidirectional-options)
