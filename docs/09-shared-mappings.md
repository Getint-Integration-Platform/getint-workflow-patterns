# Shared Mappings

Shared Mappings allow you to define mapping rules once and reuse them across multiple integrations.  
This is especially useful for fields that rarely change — such as Users, Sprints, Versions, Components, and Iteration Paths.

Using shared mappings reduces duplication and ensures consistent behavior across all workflows.

---

## Why Use Shared Mappings?

### **1. Avoid duplication**
Instead of defining the same user or sprint mappings in 5 different integrations, define them once.

### **2. Ensure consistency across teams**
If one team updates a user's mapping or sprint name, all integrations automatically inherit the change.

### **3. Reduce maintenance**
Fewer mapping screens to monitor = fewer points of failure.

### **4. Reduce errors caused by outdated mappings**
Shared mappings prevent:
- Conflicting user assignments  
- Incorrect sprint/version sync  
- Missing mapping entries in some integrations  

---

## What Can Be Shared?

Common field types include:

### **1. Assignee / User Mapping**
Useful when:
- Multiple business units sync into the same engineering team  
- Service Desk → Jira → Azure DevOps combinations  

### **2. Sprint / Iteration Path Mapping**
For example:
- Jira Sprint ↔ Azure DevOps Iteration  
- Consistent naming across multiple teams/projects  

### **3. Fix Versions / Releases**
If several integrations rely on common release definitions.

### **4. Components / Areas**
Ensures cross-team component structures remain aligned.

### **5. Custom Field Mappings**
When multiple integrations reuse the same categorical value mapping.

---

## How Shared Mappings Work

Shared mappings are created in the **Shared Mappings** section of the platform.

Then inside each integration:

1. Navigate to **Field Mapping**  
2. Select “Use Shared Mapping”  
3. Choose which shared mapping to use  

The selected shared mapping replaces local mapping logic.

---

## Example Use Cases

### **Use Case 1 — Multiple Jira Projects → One Azure DevOps Team**

All Jira projects share:
- Sprint → Iteration mappings  
- User mappings  
- Version mappings  

Using Shared Mappings avoids repeating this configuration 10+ times.

---

### **Use Case 2 — Several ServiceNow queues → Single Jira Project**

All queues share the same:
- Priority mapping  
- Category mapping  
- Assignment group mapping (optional)

---

### **Use Case 3 — Multi-product organization**

Each product group can have a shared set of mapping templates:
- Product-specific labels  
- Product-specific components  
- Release trains  
- Teams

---

## Example: Shared User Mapping Table

| Source User | Destination User | Notes |
|-------------|------------------|-------|
| Anna (Jira) | Anna.B@ADO       | Developer |
| John (Jira) | IntegrationUser  | Service account |
| SupportQueue | HelpDeskTeam    | Group account |

---

## Example: Shared Sprint/Iteration Mapping

| Jira Sprint | Azure DevOps Iteration |
|-------------|------------------------|
| Sprint 1 | Product/Sprint 1 |
| Sprint 2 | Product/Sprint 2 |
| Sprint 3 | Product/Sprint 3 |

---

## Testing Shared Mappings

1. Update a value in the shared mapping  
2. Verify that dependent integrations:  
   - Show the updated value  
   - Sync without errors  
3. Create a test item and confirm mapping applies correctly  
4. Check logs to ensure no old value is referenced  

---

## Best Practices

### **1. Use shared mappings for all identity-related fields**
User and team mappings change rarely → perfect fit.

### **2. Version your shared mappings**
Example:
Shared Users v1
Shared Users v2 (after migration)

### **3. Tag shared mappings by integration type**
Examples:
- "Jira-to-ADO Shared Users"  
- "ServiceNow-to-Jira Categories"  

### **4. Document shared mappings**
Include a README or description so teams understand their purpose.

---

## 🔍 Learn More

Refer to Getint documentation:  
https://docs.getint.io/getintio-platform/workflows/shared-mappings-in-getint-centralized-mapping-for-efficient-integrations
