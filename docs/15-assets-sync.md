# Syncing Assets (AQL & Asset Fields)

Jira Assets (formerly Insight), ServiceNow CMDB, and similar asset/data catalogs are commonly linked to issues through custom fields.  
Getint supports syncing asset references between systems, using AQL, ADO queries, and field-level mapping.

This document explains how asset sync works, how to configure AQL, and common use cases.

---

## What Are Assets?

Assets represent structured objects such as:
- Hardware (laptops, servers, printers)  
- Software licenses  
- Employee devices  
- Applications/services  
- Locations  
- Configuration items (CIs)  

They are usually stored in:
- **Jira Assets** (formerly Insight)  
- **ServiceNow CMDB**  
- **Custom CMDBs in other platforms**  

---

## What Does It Mean to Sync Assets?

Syncing assets means:
- When an item is synced across systems, its **linked asset** is also matched or mapped  
- The asset reference is stored as a field in both systems  
- Getint updates the destination field to maintain the correct relationship

Example:
Jira Issue → has asset "MacBook Pro 16"
ADO Work Item → gets asset field set to "MacBook Pro 16"


---

## Supported Asset Behavior in Getint

### **1. Basic Asset Reference Sync**
- Sync a single asset reference  
- Map Jira Asset → corresponding field in ADO/ServiceNow/Asana

### **2. Multiple Asset Values**
Sync lists of assets (depending on system limits).

### **3. AQL-based filtering**
Use AQL (Assets Query Language) to limit which assets are considered.

---

## Using AQL (Assets Query Language)

AQL allows filtering assets based on fields or hierarchical structures.

### **Basic Example**
Name = "MacBook Pro 16"

### **Filter by Type**
objectType = "Laptop"

### **Filter by Attribute**
"Assigned To" = "James Smith"

### **Filter by Location**
Location = "Berlin Office"

### **Partial match**
Name ~ "MacBook"

---

## Recommended Asset Mapping Strategies

### **1. Match asset by Name or Unique Key**
Most teams map assets using:
- Asset name  
- Serial number  
- Inventory code  
- CMDB ID  

Example:
Jira Asset (Name) ↔ ADO Custom Field (Text)

---

### **2. Avoid syncing complex Asset objects**
Getint syncs **references**, not full objects.  
Do not attempt to sync:
- Asset hierarchies  
- Attributes  
- Custom relations  
- Lifecycle states  

These are out of scope — only references are synced.

---

### **3. Use AQL to filter unwanted assets**
Examples:
- Only employee devices  
- Only active CIs  
- Only server assets  

Status = "Active"
AND
Type = "Device"

---

### **4. Keep asset structures consistent**
Different CMDB systems may use:
- Different naming conventions  
- Different ID formats  
- Different object types  

Normalize where possible.

---

## Example Use Cases

### **1. Employee device syncing**
Support tickets in ServiceNow linked to:
- Laptop  
- Phone  
- VPN Token  

Sync these references to Jira issues.

---

### **2. Application support**
Issues involving:
- Microservices  
- Applications  
- Infrastructure components  

Map Jira Asset fields → ADO or ServiceNow fields.

---

### **3. Incident & Problem management**
Linking assets to incidents and syncing between:
- Jira  
- ADO  
- ServiceNow  
- Asana  

---

## Testing Asset Sync

1. Create a Jira issue with an asset linked  
2. Sync the issue  
3. Confirm the correct asset appears in the destination system  
4. Update the asset in Jira (name, attributes)  
   - Confirm the *reference* stays consistent  
5. Try syncing multiple assets  
6. Test AQL filters with different queries  

---

## Limitations & Notes

- Only **references**, not asset objects, are synced  
- Not all platforms support multi-value asset fields  
- Incorrect field type → sync errors  
- ServiceNow CMDB requires correct table mapping  
- AQL applies only to Jira Assets  
- ADO requires custom fields for asset references  

---

## 🔍 Learn More

Refer to Getint documentation:  
https://docs.getint.io/getintio-platform/workflows/how-to-sync-assets-with-getint
