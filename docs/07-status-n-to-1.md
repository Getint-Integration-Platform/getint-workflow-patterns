# Status Mapping: Multiple Statuses to One (N → 1)

Different systems and teams often use different workflow structures.  
Getint allows you to map multiple statuses from one system to a single status in another system — known as **N→1 mapping**.

This helps simplify workflows, align teams, and avoid sync errors when one system is more complex than the other.

---

## Why Use N→1 Status Mapping?

### **1. Simplify workflows when syncing with a less complex system**
Example:
- Jira has 12 workflow statuses  
- Azure DevOps has 4 built-in states  
- Monday has only 3–5 default statuses

### **2. Standardize workflow across departments**
Development team may use:
- "In Progress", "Code Review", "In QA", "Ready for Release"

Support or external team may only need:
- "Active"

### **3. Remove unnecessary noise**
Sync only meaningful status milestones, not internal steps.

---

## Common Examples of N→1 Mappings

### **Example 1 — Jira → Azure DevOps**

Jira: To Do, Selected for Dev, Ready → ADO: New
Jira: In Progress, Code Review, QA → ADO: Active
Jira: Done, Released → ADO: Closed


---

### **Example 2 — Jira → Monday**

Jira: To Do, Backlog → Monday: "Planned"
Jira: In Progress, Code Review → Monday: "Working on it"
Jira: Done, Released → Monday: "Done"


---

### **Example 3 — ADO → Jira**

Multiple ADO states → one Jira status:

ADO: Active, Resolved → Jira: In Progress


---

## How N→1 Mapping Works in Getint

In the status mapping UI:

1. You select a **target status** on the destination system  
2. You assign **multiple source statuses** to map into that target  
3. Getint handles directionality depending on sync settings

Example configuration:

Target status: Active (ADO)
Source statuses:
In Progress (Jira)
Code Review (Jira)
QA (Jira)


---

## Behavior in Bidirectional Sync

### **If both systems update statuses:**

- When Jira moves from "Code Review" → "QA" → "Tested",  
  all map to **ADO: Active** (no change visible on ADO side)

- When ADO moves from "Active" → "Closed",  
  Getint maps this to **one chosen destination** of the N→1 group  
  (usually the "Done" / "Closed" status in Jira)

### **Important note:**
N→1 mappings are **lossy** — meaning:
- You cannot recover the *exact* original Jira status once mapped into a single ADO state

This is expected and often desired.

---

## Recommended Best Practices

### **1. Group statuses based on meaning**
Example grouping:

Open group: "To Do", "Selected for Dev", "Ready"
In Progress group: "In Progress", "Review", "QA"
Done group: "Done", "Released"


### **2. Always define a clear end-state mapping**
Ensure finished statuses map consistently:

Done (Jira) → Closed (ADO)


### **3. Avoid grouping transition statuses with final states**
Bad pattern:

"In Progress", "Review", "Done" → "Active"


Better pattern:

"In Progress", "Review" → "Active"
"Done" → "Closed"


---

## Example Mapping Table

| Source Statuses (N) | Destination Status (1) | Notes |
|---------------------|-------------------------|-------|
| To Do, Ready        | New                     | Standard grouping |
| In Progress, QA     | Active                  | Multiple workflow stages |
| Done, Released      | Closed                  | Completed work |

---

## Testing N→1 Behavior

1. Move an item through several statuses in System A  
2. Verify the item remains stable in System B  
3. Change status in System B  
4. Verify it syncs to the **chosen** status in System A  
5. Confirm no loops occur (e.g., toggling back and forth)

---

## 🔍 Learn More

Refer to Getint documentation:  
https://docs.getint.io/getintio-platform/workflows/mapping-multiple-statuses-to-one-n-to-1-in-getint
