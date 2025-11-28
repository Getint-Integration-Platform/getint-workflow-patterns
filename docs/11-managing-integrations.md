# Managing Integrations

Managing integrations in Getint involves organizing, monitoring, filtering, and exporting integrations to ensure they run efficiently and remain maintainable over time.

This document provides best practices for managing multiple integrations across teams or environments.

---

## The Integrations List

The **Integrations List** displays all existing integrations with key information such as:
- Name  
- Status (Enabled/Disabled)  
- Last run timestamp  
- Owner  
- Source and destination systems  
- Group (optional categorization)

This is your command center for monitoring integration health.

---

## Integration Status Indicators

### **Enabled**
The integration is active and sync jobs will run according to configuration.

### **Disabled**
The integration is paused — useful during:
- Maintenance  
- Data migrations  
- Large-scale edits  
- Troubleshooting  

---

## Filtering Integrations

You can filter integrations using:

- Integration name  
- Owner  
- Source system (Jira, ADO, ServiceNow, etc.)  
- Destination system  
- Status (Enabled/Disabled)  
- Group tags  

Filtering is useful in large environments with dozens or hundreds of integrations.

---

## Grouping Integrations

Groups help organize integrations by logic such as:

### **1. By Product/Domain**
- CRM Integrations  
- ITSM Integrations  
- Engineering Integrations  

### **2. By Team**
- Platform Team  
- Support Team  
- R&D Team  

### **3. By Customer / External Partner**
Useful for MSPs or teams working with multiple clients.

### **4. By Environment**
- Production  
- UAT  
- Staging  
- Sandbox  

---

## Exporting & Importing Integrations

Getint supports exporting complete integrations into reusable files.

### **You can use export/import to:**
- Migrate integrations between environments  
- Clone integrations for similar projects  
- Back up configuration  
- Share templates with teams or partners  

### **Best Practices:**
1. Keep exported integrations in version control (e.g., GitHub)
2. Document changes inside pull requests
3. Tag exported files with environment and version (e.g., `jira-ado-sync-v3-prod.json`)

---

## Naming Conventions (Highly Recommended)

Consistent naming makes large environments far easier to manage.

### **Recommended naming pattern:**

<source>-<destination>-<project/team>-<environment>

Examples:

jira-ado-platform-prod
servicenow-jira-support-uat
asana-jira-marketing-prod

### Why this helps:
- Easy filtering  
- Clear ownership  
- Less ambiguity  
- Clean export/import behavior  

---

## Monitoring Integration Runs

Each integration includes run logs showing:
- Execution time  
- Items synced  
- Errors or warnings  
- Detailed event history  

### **Tips:**
- Investigate repeated errors immediately  
- Watch for unexpected volume changes  
- Use filters to view runs per integration or per project  

---

## Maintenance Checklist

Perform the following regularly:

### **Every week:**
- Review errors  
- Monitor item volume  
- Confirm correct sync direction  
- Check for new fields in source systems

### **Every month:**
- Revalidate user mappings  
- Check for deprecated fields  
- Test filters to avoid unexpected exclusions  

### **Every quarter:**
- Clean up unused integrations  
- Archive or export historical integrations  
- Validate shared mappings still apply  
- Optimize status and type mappings  

---

## When to Disable an Integration

Disable the integration before:
- Large data migrations  
- Bulk field updates  
- Changes to status workflows  
- Modifying type mappings  
- Major system configuration changes (e.g., Jira workflow update)  

This prevents unexpected sync loops or incorrect data propagation.

---

## When to Re-Enable the Integration

Only re-enable after verifying:
- Field mappings are still correct  
- User mappings are still valid  
- Status mappings align with new workflows  
- Filters still capture the right items  

---

## 🔍 Learn More

Refer to Getint documentation:  
https://docs.getint.io/getintio-platform/workflows/managing-and-exporting-integrations-in-getint
