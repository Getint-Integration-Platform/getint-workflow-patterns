# Filtering Items for Sync

Item filtering allows you to control **which items are included** in the integration workflow.  
Filters help reduce noise, improve performance, and prevent unwanted items from syncing across systems.

This document explains filtering types, best practices, and example configurations.

---

## What Are Filters?

Filters are rules that determine whether an item should be:

- Included in the sync  
- Excluded from the sync  
- Processed only under specific conditions  

Filters are configured in the **Filters** tab of each integration.

---

## 🔍 Types of Filters in Getint

### **1. ALL Items View**
Shows all items in your source system.

### **2. NEW Items**
Items that:
- Have not been synced
- Have no counterpart
- Are eligible for creation

### **3. SYNCED Items**
Items already synchronized:
- With an established counterpart
- With history and mapping tracked

---

## How Filters Work

A filter is created using three elements:

1. **Field**  
   Example: Priority, Component, Status, Custom Field

2. **Operator**  
   Examples:  
   - equals  
   - not equals  
   - contains  
   - greater/less than  
   - is empty / is not empty  
   - in list  
   - matches (advanced)

3. **Value**  
   Example: "High", "Backend", "Customer", "Bug"

Multiple filters can be combined using **AND/OR logic**.

---

## Recommended Best Practices

### **1. Filter out internal/noisy items**
Examples:
- Internal tasks  
- Developer-only subtasks  
- Tickets not meant for external teams

Rule example:
Component != Internal


---

### **2. Filter by priority or impact**
Sync only important items:

Priority in (High, Critical)


---

### **3. Sync only specific types**
If only some types should be exchanged:

Issue Type in (Bug, Story)


---

### **4. Avoid overly complex filter logic**
Too many AND/OR combinations may cause:
- Missed items  
- Hard-to-debug conditions  
- Confusing behavior

---

### **5. Test filters with NEW and SYNCED views separately**
They behave differently:
- NEW: looks for items not yet synced  
- SYNCED: looks for already linked items

---

## Example Filter Sets

### **Example 1 — Sync only customer-facing issues**
Labels contains customer
AND
Priority in (High, Critical)


---

### **Example 2 — Exclude internal engineering tasks**

Component not in (Internal, DevOps, Ops)


---

### **Example 3 — Sync only Jira issues assigned to a specific team**

Team = "Platform"

---

### **Example 4 — Sync only Azure DevOps items in specific areas**

Area Path contains "Product"

---

### **Example 5 — Only sync items in a defined workflow stage**

Status in (In Progress, QA)


---

## Testing Filters

1. Open the **NEW** tab  
2. Change or add labels/statuses/tags  
3. Confirm whether items appear or disappear based on rules  
4. Repeat the same with the **SYNCED** view  
5. Verify filters do not unintentionally block critical items  
6. Try removing filters to debug issues

---

## Useful Tips

- You can temporarily **disable** filters to diagnose missing items  
- Keep filters simple to make future maintenance easier  
- Document “why” a filter exists for future team members  
- Always review filters after major workflow updates

---

## 🔍 Learn More

Refer to Getint documentation:  
https://docs.getint.io/getintio-platform/workflows/filtering-items-for-integration-in-getint
