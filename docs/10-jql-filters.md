# JQL Filters for Jira Integrations

JQL (Jira Query Language) is a powerful way to filter Jira items that should be included in a Getint integration.  
Using JQL, you can precisely control which issues sync — based on fields, dates, components, priorities, statuses, and more.

This document provides reusable JQL patterns, examples, and best practices.

---

## Why Use JQL Filters?

JQL gives you:
- More flexibility than standard UI filters  
- Precise control over sync scope  
- Ability to target complex workstreams  
- Better performance when filtering large datasets  

JQL filters are applied in the integration’s **Item Filtering** section.

---

## Basic JQL Examples

### **1. Filter by Status**
status = "In Progress"

Multiple statuses:
status in ("In Progress", "QA", "Code Review")

---

### **2. Filter by Priority**

priority = High

Multiple:

priority in (High, Critical)

---

### **3. Filter by Issue Type**

issuetype in (Bug, Story, Task)

---

### **4. Filter by Component**

component = Backend

Multiple:

component in (Backend, API, Database)

---

## Date-Based JQL Examples

### **1. Recently updated issues**
updated >= -7d


### **2. Issues created after a specific date**
created >= "2023-01-01"

### **3. Issues resolved recently**

resolutiondate >= -30d

---

## User and Team JQL Examples

### **1. Assigned to a specific person**

assignee = "Anna"

### **2. Assigned to a team**

"Team[Dropdown]" = "Platform"

### **3. Unassigned issues**

assignee is EMPTY

---

## Label-Based JQL Examples

### **1. Issues with a specific label**

labels = customer

### **2. Issues with any of several labels**

labels in (customer, important, critical)

### **3. Issues without a label**

labels is EMPTY

---

## Project and Board JQL Examples

### **1. Filter by project**

project = "PROD"

### **2. Multiple projects**

project in (PROD, OPS, SEC)

### **3. Filter by sprint**

Sprint = "Sprint 15"

---

## 🔎 Advanced JQL Examples

### **1. Issues linked to others**

issueLinkType = "is blocked by"

### **2. Issues with attachments**

attachments IS NOT EMPTY

### **3. Issues with comments**

comment ~ "error"

### **4. Issues changed by a specific user**

status changed BY "developer1" AFTER -3d

---

## Using JQL with Getint

You can combine JQL filters with other filtering logic:

### Example:
Sync only customer-visible high-priority bugs:

issuetype = Bug
AND priority in (High, Critical)
AND labels in (customer, external)

---

## Recommended Best Practices

### **1. Keep JQL simple**
Overly complex JQL can:
- Reduce performance  
- Make debugging difficult  
- Accidentally exclude valid issues  

---

### **2. Document your JQL**
Add comments in your repository or integration description.

---

### **3. Test JQL in Jira first**
Use the Jira Issue Navigator:
- Paste your JQL  
- Check results  
- Adjust before using in Getint  

---

### **4. Combine JQL with UI filters when possible**
Best scenario:
- Use JQL for coarse filtering  
- Use UI filters for fine tuning  

---

## Testing JQL

1. Run your JQL in Jira  
2. Verify the items match expectations  
3. Paste it into the Getint integration filter  
4. Check that NEW/SYNCED views match  
5. Iterate until clean  

---

## 🔍 Learn More

Refer to Jira JQL documentation + Getint filtering docs:  
https://docs.getint.io/getintio-platform/workflows/how-to-use-jql-filters-for-jira-integrations
