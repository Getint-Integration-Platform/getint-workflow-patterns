# Labels / Tags / Components Mapping

Labels, tags, and similar categorical fields help classify work items across systems.  
Getint supports syncing these fields, but functionality varies depending on the platform.

This document explains how label mapping works, recommended patterns, platform limitations, and example configurations.

---

## What Are Labels / Tags?

Different tools use different terms for item categorization:

| Platform | Field Name |
|----------|------------|
| Jira | Labels, Components |
| Azure DevOps | Tags |
| Asana | Tags, Custom Fields |
| Monday.com | Labels Column |
| ServiceNow | Categories / Subcategories |
| Salesforce | Picklists / Tags |

Getint treats these as **categorical fields** that can be synced between systems.

---

## How Label Mapping Works in Getint

Labels/tags mapping is configured as a **field mapping** under each Type Mapping.

Key rules:

1. Labels are often **free text** (Jira, ADO tags)  
2. Some tools support **only predefined values** (e.g., Monday Label column)  
3. Some tools allow labels only from one direction

---

## Recommended Best Practices

### **1. Use free-text systems as the source where possible**

Systems like:
- Jira Labels  
- Azure DevOps Tags  
- Asana Tags  

are more flexible, so using them as the *source* reduces mapping issues.

---

### **2. Normalize labels when syncing into structured systems**

When syncing into Monday or ServiceNow:

- Map incoming labels to predefined values  
- Use fallbacks for unknown labels  
- Avoid creating too many new labels automatically

---

### **3. Keep naming conventions consistent**

Example:
Frontend, Backend, DevOps, High Priority, Customer-Reported


Avoid inconsistent variants:
frontend, Front-end, front_end


---

### **4. Sync labels one-way when platforms are incompatible**

Examples of when **one-way sync is recommended**:

- Jira Labels → Monday Labels  
- Jira Labels → ServiceNow categories  
- Azure DevOps Tags → Asana Tags  

Reverse directions may not support free text.

---

### **5. Avoid syncing sensitive labels**

Many teams use labels for internal processes like:
- “internal-only”  
- “security”  
- “customer-complaint”  
- “blocked-by-legal”  

These should stay within one system only.

---

## Platform Limitations

### **Jira**
- Labels are free text.
- Components are structured but not auto-created via API in all cases.

### **Azure DevOps**
- Tags are free text.
- Tags are always created automatically.

### **Asana**
- Tags require workspace-level creation.
- In some cases, creating tags automatically may be restricted.

### **Monday.com**
- Labels Column requires **predefined values**.
- Systems cannot create new labels automatically.

### **ServiceNow**
- Categories/Subcategories must exist before sync.
- Cannot create categories on-the-fly.

---

## Example Mapping Patterns

### **Pattern 1 — Jira Labels → ADO Tags (bidirectional)**

Jira Labels: ["backend", "security"]
ADO Tags: ["backend", "security"]
Direction: ↔


---

### **Pattern 2 — Jira Labels → Monday Labels (one-way)**

Jira Labels (free text) → Monday Labels (predefined)
Direction: Jira → Monday


Use transformation rules to map unexpected values.

---

### **Pattern 3 — Tag consolidation**

When source systems use many custom labels:

"frontend", "front-end", "UI" → "Frontend"
"backend", "api", "server" → "Backend"


Use mapping tables or transformation scripts to normalize.

---

## Example Mapping Table

| Source Label | Destination Label | Notes |
|--------------|-------------------|-------|
| frontend | Frontend | Normalized |
| ui | Frontend | Consolidated |
| bug | Bug | Standardized value |
| urgent | High Priority | Custom logic |
| unknown | Not Mapped | Fallback |

---

## Testing Label/Tag Sync

1. Add multiple labels to an item in System A  
2. Verify they appear correctly in System B  
3. Test removing labels (some systems do not support label removal)  
4. Try sending unexpected labels to ensure fallback logic works  
5. Validate no sensitive labels sync unintentionally  

---

## 🔍 Learn More

Refer to Getint documentation:  
https://docs.getint.io/getintio-platform/workflows/mapping-labels
