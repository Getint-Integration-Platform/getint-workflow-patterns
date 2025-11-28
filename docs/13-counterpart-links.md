# Storing Counterpart Links in Comments

Getint can automatically insert a comment into an item that contains a direct link to its synced counterpart.  
This improves transparency, collaboration, and traceability between teams working in different systems.

This document explains how it works, when to use it, and recommended best practices.

---

## What Are Counterpart Links?

When enabled, Getint will add a comment like:

This item is synced with: https://<destination-system>/item/12345

This helps users quickly access the corresponding item in the other system.

---

## Why Use Counterpart Links?

### **1. Improve collaboration**
Teams can instantly jump to the related item without searching.

### **2. Reduce uncertainty**
Support, development, and QA teams see which item their issue is synced to.

### **3. Save time**
Fewer manual lookups and less cross-system navigation.

### **4. Increase transparency**
Provides a clear audit trail of how items are connected.

---

## How It Works

### **When an item is created on the destination side:**

Once the source item maps to a new destination item, Getint:

1. Generates the counterpart URL  
2. Adds a comment to the source item containing the URL  
3. Optionally adds the reverse comment on the destination side (if enabled)

### **Comment direction can be:**
- One-way (recommended)  
- Bidirectional (optional)  
- Disabled  

---

## Why It’s Disabled by Default

Counterpart link comments often **send notifications** to users.

Some teams prefer:
- Minimal noise  
- No automated comments  
- Reduced risk of spam  

You can enable or disable this feature depending on your workflow needs.

---

## Recommended Best Practices

### **1. Enable for cross-team collaborations**
Especially useful when:
- Support → Development integrations  
- Customer-facing teams need visibility  
- Multiple systems are involved (Jira → ADO → ServiceNow)

---

### **2. Disable in high-volume integrations**
If you sync:
- Thousands of items  
- Many daily updates  
- High-frequency event flows  

…then the number of comments can become significant.

---

### **3. Use bidirectional comments only if necessary**
Most teams only need the **source → destination** link.

Bidirectional examples:
- Jira ↔ Jira cross-project sync  
- Jira ↔ Asana collaboration boards  

---

### **4. Avoid triggering automation rules**
Some systems (like Jira or ServiceNow) may have automation triggered by comments.  
Ensure automated comments are excluded from such rules.

---

## Example Output

### **One-way comment (most common)**

This item is synced with:
https://dev.azure.com/company/project/_workitems/edit/1024


### **Bidirectional comment (optional)**

Source:
Synced with ADO: https://dev.azure.com/project/1024


Destination:

Synced with Jira: https://jira.company.com/browse/PROJ-115

---

## Testing Counterpart Comments

1. Enable the feature in the integration settings  
2. Sync a new item  
3. Check whether the comment appears in the source system  
4. Confirm the URL is correct and accessible  
5. If bidirectional, check the reverse comment  
6. Ensure no duplicate comments are generated

---

## Notes and Limitations

- Comments may trigger notifications depending on system rules  
- Inline links may format differently in different platforms  
- Some systems restrict comment length or formatting  
- Comments are not removed when disabling the feature — they remain as history

---

## 🔍 Learn More

Refer to Getint documentation:  
https://docs.getint.io/getintio-platform/workflows/storing-counterpart-link-in-the-task-comment
