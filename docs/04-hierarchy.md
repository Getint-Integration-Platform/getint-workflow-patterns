# Hierarchy (Epics, Stories, Tasks, Subtasks)

Many tools support multi-level work item hierarchies. Getint can synchronize these structures so teams keep consistent parent/child relationships across platforms.

This document explains how hierarchy sync works, recommended mapping patterns, and common pitfalls.

---

## What Is Hierarchy Sync?

Hierarchy sync preserves **parent → child** relationships between work items, such as:

- Epic → Story  
- Story → Subtask  
- Feature → User Story → Task  
- Incident → Work Notes (ServiceNow)

In Getint, hierarchy behaviors are configured in **Type Mapping**, under each mapped type pair.

---

## Supported Hierarchy Operations

1. **Sync parent links**  
   - Epics → Stories  
   - Features → User Stories  
   - Tasks → Subtasks  

2. **Sync child links**  
   - Stories → Subtasks  
   - Tasks → Checklists / Custom Subtasks (depending on platform)

3. **Recreate missing parent items**  
   (optional; depends on pattern)

4. **Update parent when child changes**  
   (status, fields, comments — if enabled)

---

## Recommended Mapping Patterns

### **Pattern 1 — Jira ↔ Azure DevOps**

| Jira | Azure DevOps |
|------|--------------|
| Epic | Epic |
| Story / Task | User Story |
| Subtask | Task |

This mapping is the **industry-standard cross-team collaboration setup**.

Notes:
- Use **one Epic mapping**.
- ADO Task maps cleanly to Jira Subtask.
- Keep statuses mapped consistently across all levels.

---

### **Pattern 2 — Jira ↔ Jira (Cross-Project)**

| Project A | Project B |
|-----------|-----------|
| Epic | Epic |
| Story / Task | Story / Task |
| Subtask | Subtask |

Best use cases:
- Shared engineering teams  
- Multi-department collaboration  
- Migrations or transitions  

---

### **Pattern 3 — Jira ↔ Monday.com**

| Jira | Monday |
|------|--------|
| Epic | Group / Board (optional pattern) |
| Story / Task | Item |
| Subtask | Subitem |

Notes:
- Monday does not support a native "Epic" type.  
- Two recommended patterns:
  1. Use Monday **Groups** as “Epic containers”
  2. Create a custom “Epic” item type  
- Subitems sync cleanly to Jira Subtasks.

---

## How Getint Syncs Hierarchy Internally

### **1. Parent Items Are Synced First**
To avoid orphan children:
- Epic sync → Story sync → Subtask sync

### **2. Children Inherit Parent Mappings**
Children use the same field/status rules as their type mapping.

### **3. Re-parenting behavior**
If a child is moved under a new parent:
- Getint updates the parent link  
- Or creates the new parent (if enabled)

### **4. Missing parents**
If a parent is missing on the destination side:
- You can **create missing parents automatically**
- Or **link to existing parents** using rules

---

## Common Pitfalls (and Fixes)

### **❗ Child syncs before parent**
Fix:
- Ensure Epic type mapping is placed above Story/Task in mapping order.

### **❗ Monday board/group mismatch**
Fix:
- Use consistent grouping patterns per integration.

### **❗ ADO Task used incorrectly**
Fix:
- Map Jira Subtasks → ADO Tasks  
- Map Jira Tasks → ADO User Stories

### **❗ Status loops caused by child updates**
Fix:
- Avoid syncing status from Subtasks → Stories directly.

---

## Example Hierarchy Configuration
Jira → Azure DevOps
Epic ↔ Epic
Story ↔ User Story
Subtask ↔ Task


---

## Testing Your Hierarchy Sync

Before enabling for production:

1. Create a simple Epic → Story → Subtask structure  
2. Sync the Epic  
3. Confirm Story appears and is linked  
4. Confirm Subtask appears and is linked  
5. Reparent Story under another Epic and check the sync  
6. Try deletion behavior (note: some systems don’t propagate deletes)

---

## 🔍 Learn More

Refer to Getint documentation:  
https://docs.getint.io/getintio-platform/workflows/hierarchy

