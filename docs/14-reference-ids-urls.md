# Storing Reference IDs & URLs in Custom Fields

Instead of adding counterpart links in comments, Getint can store the **counterpart item ID** and/or **counterpart URL** in custom fields.  
This method is clean, silent, and widely used by teams that want traceability without generating comment-based notifications.

This document explains how the feature works, recommended field configurations, and system-specific notes.

---

## Why Store Reference IDs or URLs?

### **1. Avoid comment noise**
No notifications are triggered, unlike comment-based linking.

### **2. Provide a clear traceability path**
Users can easily open the related item directly from a custom field.

### **3. Enable automation**
Other systems can consume ID/URL fields for automation or reporting.

### **4. Improve reporting**
You can build dashboards and reports referencing linked items.

### **5. Ideal for high-volume integrations**
Avoids comment spam when syncing hundreds or thousands of items.

---

## What Can Be Stored?

### **1. Counterpart Item ID**
Example:
ADO ID: 1542
ServiceNow Ticket: INC0021510

### **2. Counterpart Item URL**
Example:
https://dev.azure.com/org/project/_workitems/edit/1542


### **3. Both**
Many teams store ID + URL side-by-side.

---

## How It Works in Getint

### Step 1 — Create custom fields on each side  
Example field names:
- `Counterpart ID`
- `Counterpart URL`
- `External Ticket ID`
- `Linked Work Item`

### Step 2 — Add the fields to your Type Mapping  
Map:
- ID → ID  
- URL → URL  

### Step 3 — Getint writes to these fields automatically  
Whenever a counterpart item is created or updated, Getint updates the reference fields.

---

## System-Specific Notes

### **Jira Cloud**
- Use “Text Field (single line)” for ID  
- Use “URL Field” or “Text Field” for URL  
- `accountId`-based user permission rules apply

### **Jira Data Center**
- Same as above, with more flexibility in custom fields

### **Azure DevOps**
- Use “Text (single line)” work item fields  
- URL field displays a clickable link automatically

### **ServiceNow**
⚠️ Very important:  
ServiceNow uses **"Number"** for ticket references — *not* the internal `sys_id`.

Correct mapping:
ServiceNow "Number" → Jira "Counterpart ID"

### **Asana**
- Use custom fields (text type)  
- URL will remain plain text (no hyperlink formatting)

### **Monday.com**
- Use “Text” column type  
- URLs are clickable in item view

---

## Example Field Mapping

| Jira Field | Azure DevOps Field | Purpose |
|------------|---------------------|---------|
| Counterpart ID | External ID | Store item ID |
| Counterpart URL | External URL | Quick access to counterpart |

---

## Example Use Cases

### **1. Support ↔ Engineering**
Support ticket ID stored in Jira issue’s “Customer Ticket ID” field.

### **2. DevOps ↔ ITSM**
Azure DevOps Work Item ID stored in ServiceNow’s “Work Notes” or custom field.

### **3. Multi-system chain syncs**
Example:
- Jira ↔ ADO  
- ADO ↔ ServiceNow  
- Jira ↔ ServiceNow  

Reference ID fields help maintain consistency across three systems.

---

## Testing Reference Fields

1. Enable ID/URL mapping  
2. Create a test item  
3. Sync it  
4. Check that the destination item contains the ID and URL of the source  
5. Update the counterpart and verify fields remain accurate  
6. Ensure field permissions allow writing

---

## Common Issues & Fixes

### **Issue: No value appears in the custom field**
- The field is not on the edit/view screen  
- The field is not mapped correctly  
- User permissions prevent updates

### **Issue: Wrong ID stored**
- ServiceNow mapping used `sys_id` instead of `Number`  
- Wrong type mapping selected  
- Integration created duplicates previously

### **Issue: URL not clickable**
- Platform uses plain-text fields (Asana, Monday)

---

## 🔍 Learn More

Refer to Getint documentation:  
https://docs.getint.io/getintio-platform/workflows/storing-reference-ids-urls-across-integrations
