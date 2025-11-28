# Integration Status (Enabled vs Disabled)

Each Getint integration has an **Enabled** or **Disabled** status.  
These states determine whether the integration performs live synchronization.

Understanding these modes is essential for safe maintenance, migrations, and troubleshooting.

---

## Enabled Integrations

When an integration is **Enabled**, it will:

- Execute sync jobs  
- Process create/update events  
- Synchronize mapped fields, comments, attachments, statuses, hierarchy  
- Follow all type mappings and filters  
- Use configured sync direction  
- Log all runs and events  

Enabled mode is the default for “live” integrations.

---

## Disabled Integrations

When an integration is **Disabled**, it will:

- **Stop all live sync operations**  
- Not create new items  
- Not update counterparts  
- Not process attachments or comments  
- Not maintain counters or logs for new changes  

All configuration remains intact — but the integration becomes dormant.

This is the safest state for modification or system updates.

---

## When to Disable an Integration

You should disable an integration before:

### **1. Large-scale data migrations**
Examples:
- Jira project migration  
- Azure DevOps restructuring  
- ServiceNow instance reconfiguration  

### **2. Bulk-updating fields**
Such as:
- Reclassifying issue types  
- Bulk status changes  
- Label/tag cleanup  

### **3. Changing workflows**
Especially when:
- Adding/removing statuses  
- Changing transitions  
- Modifying hierarchy rules  

### **4. Updating type mappings**
Disable before changing:
- Status mapping  
- Field mapping  
- Attachment sync logic  

### **5. Performing maintenance**
During:
- Upgrades  
- Schema changes  
- Permission changes  
- API adjustments  

### **6. Troubleshooting unexpected sync behavior**
Pausing prevents further propagation of unwanted changes.

---

## When to Re-Enable an Integration

Re-enable only after verifying:

### **1. Field mappings are correct**  
New or changed fields should be validated.

### **2. Status mappings align with workflow changes**

Validate:
- No missing statuses  
- No deprecated workflow states  
- N→1 mapping still makes sense  

### **3. User mappings are valid**

For example:
- New employees  
- Role changes  
- Deactivated accounts  

### **4. Filters still allow the correct items**

Ensure filtering rules weren’t affected by workflow or field changes.

### **5. Both systems are stable**

If either Jira, ADO, ServiceNow, Monday, etc. is undergoing maintenance or throttling, wait.

---

## Safe Re-Enable Procedure

Before going live again:

1. Disable integration  
2. Make changes  
3. Enable integration in **test environment**  
4. Sync a few items  
5. Verify fields, statuses, hyperlinks  
6. Check logs  
7. Only then enable integration in **production**

This helps prevent accidental mass updates or loops.

---

## Important Note About Migration

**Disabled integrations do NOT sync old items automatically.**

If you:
- Disable an integration  
- Move items  
- Change fields  
- Re-enable

Those **old** items will not be updated unless:
- You manually trigger migration  
- Or modify and save them (some platforms send webhook events)

This is by design to avoid flooding systems with unwanted updates.

---

## Example Use Case

### *Large workflow redesign in Jira*

1. Disable the integration  
2. Implement workflow changes  
3. Update status mappings  
4. Update filters  
5. Test in a sandbox  
6. Re-enable in production after confirming expected behavior

---

## 🔍 Learn More

Refer to Getint documentation:  
https://docs.getint.io/getintio-platform/workflows/integration-status
