# Syncing Attachments

Attachments often contain important context such as logs, screenshots, specifications, and customer communication. Getint supports syncing attachments between many platforms, with configurable directions and practical limitations to consider.

This document explains recommended patterns, limitations, and examples.

---

## How Attachment Sync Works

Attachment sync is configured under **Type Mapping → Attachments**.  
Getint supports the following directions:

### **1. Bidirectional (↔)**
Attachments flow both ways.

### **2. Left → Right (one-way)**
Only attachments from the source system flow to the destination.

### **3. Right → Left (one-way)**  
Reverse direction if needed.

### **4. Disabled**
No attachments are synced.

---

## Recommended Best Practices

### **1. Prefer one-way sync unless bidirectional is required**
Bidirectional attachment sync can cause:
- Duplicates  
- Higher storage usage  
- Infinite loops in rare systems  
- Increased API consumption  

For most customers:
- **Customer system → Vendor system** is sufficient  
- Reverse direction is optional

---

### **2. Sync only relevant file types**
Do *not* sync:
- Executables  
- Large binaries  
- System-generated dumps  
- Temp files  

These add noise and slow jobs unnecessarily.

---

### **3. Avoid bidirectional sync in systems with limited attachment models**
Examples:
- Some tools strip metadata  
- Some tools re-upload modified images as new files  
- Monday.com does **not** support inline images through standard attachment endpoints  
- ServiceNow may restrict attachment sizes  

---

## Attachment Behavior by Platform (Summary)

| Platform | Notes |
|---------|-------|
| **Jira Cloud** | Supports full attachment sync; inline images allowed |
| **Jira DC** | No attachment limits; best for heavy use |
| **Azure DevOps** | Stores attachments as work item “files”; metadata preserved |
| **Monday.com** | No inline image support; attachments only in File column |
| **ServiceNow** | Size restrictions may apply depending on instance |
| **Asana** | Supports image and document attachments |

---

## SaaS vs Data Center Performance

### **SaaS environment**
- Attachment sync may be limited to prevent heavy API load  
- Some platforms impose rate limits  
- Faster for smaller attachments, but less ideal for bulk file transfers  

### **Data Center / On-Prem (Jira DC)**
- No hard attachment limits  
- Ideal for large enterprise data migration or heavy collaboration  

---

## Example Configuration Patterns

### **Pattern 1 — One-way attachment sync**
Recommended for most ITSM → Dev scenarios:

System A (left) → System B (right)
Attachments: Enabled
Direction: Left → Right

### **Pattern 2 — Bidirectional sync in collaboration environments**

Jira ↔ Azure DevOps
Attachments: Enabled
Direction: Bidirectional


Use only when both teams continuously share files.

---

### **Pattern 3 — Disable attachment sync**

Useful when:
- Attachments contain sensitive or internal-only files  
- No useful context is expected in attachments  
- Storage/API costs must be reduced  

---

## Testing Attachment Sync

Before enabling full sync:

1. Add several file types: PNG, JPEG, PDF, TXT  
2. Verify they appear in the counterpart  
3. Edit the description or comments but **not the file** to ensure no extra duplicates  
4. Test file removal (not all systems propagate deletes)  

---

## 🔍 Learn More

Refer to Getint documentation:  
https://docs.getint.io/getintio-platform/workflows/syncing-attachments
