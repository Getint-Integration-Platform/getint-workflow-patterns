# getint-workflow-patterns

**Getint** is a powerful integration platform that synchronizes tasks, tickets, workflows, and project structures across systems like Jira, Azure DevOps, ServiceNow, Asana, Monday, Salesforce and more. It enables teams to collaborate seamlessly across tools by providing field mapping, hierarchy sync, attachments sync, automation, and real-time bidirectional updates.

This repository gathers reusable workflow patterns, examples, and best-practice configurations to help you build integrations faster and with higher quality.

---

## Purpose

This repository is designed to help:

- **Customers** configure integrations efficiently  
- **Partners** build consistent, maintainable integration patterns  
- **Solutions / Support teams** speed up delivery  
- **Anyone** who needs clear examples of mapping, filtering, and sync strategies  

Everything inside is focused on *real-world* work: templates, mappings, recommended best practices, and ready-to-use examples.

---

## Repository Structure

```
docs/                      → Detailed explanations of each workflow topic
examples/                  → Integration-specific templates (YAML, JSON)
snippets/                  → JQL, AQL, filters, mapping shortcuts
.github/                   → Issue templates, CI linting, etc.
```

### **Docs**
Contains one Markdown file per Getint workflow concept, such as:

- Type Mapping  
- Sync Direction  
- Attachment Sync  
- Hierarchy  
- Assignee/Label Mapping  
- Status N→1 Mapping  
- Item Filtering  
- JQL Filters  
- Shared Mappings  
- Reference IDs / URLs  
- Asset Sync (AQL)  

Each doc contains explanations + best practice recommendations.

### **Examples**
Integration-by-integration configuration templates, including:

- Jira ↔ Azure DevOps  
- Jira ↔ ServiceNow  
- Jira ↔ Asana  
- Jira ↔ Jira (cross-project or cloud ↔ DC)  

Example types include:

- type-mapping YAML  
- status mapping  
- field mapping  
- label/tag mapping  
- hierarchy templates  
- filters  

### **Snippets**
Quick reference snippets broken down into:

- JQL  
- UI Filters  
- AQL (Assets Query Language)  
- Reference Field patterns  

---

## Goals

- Make Getint integrations easier to configure  
- Standardize patterns across teams and partners  
- Share best practices openly  
- Reduce repetitive setup work  

---

## Contributing

Contributions are very welcome!  
You can:

- Add new integration examples  
- Expand docs  
- Add useful JQL/AQL patterns  
- Create new mapping templates  

Please submit a PR or open an issue before large changes.

---

## License

This project is licensed under the **MIT License** — feel free to use these examples in your own integrations.
