# Auto Ticket Classification using Flow Designer
 
An automated incident-classification workflow built on **ServiceNow Flow Designer** for a school IT helpdesk. When a student or teacher submits an incident, the flow reads keywords in the *Short Description* and *Description* fields, assigns the Category, Subcategory and Priority, routes the ticket to the right IT support group, and notifies the requester, with no manual triage.
 
**Author:** AATHITHYA K V
**Repository:** https://github.com/aathithyakumar-techy/Auto-Ticket-Classification-using-FLOW-DESIGNER
 
---
 
## Problem
 
The school IT helpdesk receives many incidents every day: Wi-Fi issues, projector failures, password problems, slow computers. IT staff read each ticket and assign a category by hand, which causes:
 
- Delays in assignment and resolution
- Misclassified or misrouted tickets
- No real-time visibility for requesters
- Repetitive workload for IT staff
## Solution
 
A Flow Designer workflow triggers as soon as an incident is created and:
 
1. Validates mandatory fields (Short Description cannot be blank)
2. Scans Short Description and Description for target keywords
3. Auto-assigns **Category**, **Subcategory** and **Priority**
4. Routes the ticket to the matching **IT Support Assignment Group**
5. Sends a notification to the requester with the ticket number and category
6. Records everything in the incident log for audit and reporting
Tickets with no keyword match fall back to manual review.
 
### Example
 
| Input (Short Description) | Category | Assignment Group |
|---|---|---|
| Wi-Fi not connecting in Lab 2 | Network / Wi-Fi | Network support group |
| Password reset request | Account / Access | Identity and Access IT Group |
| Projector not displaying in Classroom 3B | Hardware / Classroom AV | AV Tech Support Team |
 
## Architecture
 
```
Student / Teacher
       |
ServiceNow Service Portal (Incident Form)
       |
Flow Designer + Business Rules  -->  Keyword Analysis (Wi-Fi, Projector, Password, Slow PC)
       |
Auto Classification and Assignment Group Routing
       |
Incident Table / Audit Log  -->  Notifications  -->  IT Support Team  -->  Reports and Dashboards
```
 
| Tier | Layer | Components |
|---|---|---|
| 1 | Presentation | Service Portal / Incident Form |
| 2 | Business Logic | Flow Designer, Business Rules, Script Includes |
| 3 | Data | Incident, User and Group tables |
 
## Tech Stack
 
- **Platform:** ServiceNow (Utah / Vancouver instance), hosted on the ServiceNow cloud
- **Automation:** Flow Designer actions, Business Rules, UI Policies, Client Scripts
- **Scripting:** JavaScript, Glide System APIs, Script Includes
- **Data:** ServiceNow tables (`incident`, `sys_user`, `sys_user_group`)
- **Security:** Role-based access control and ACLs
- **Optional:** REST API / IntegrationHub, Predictive Intelligence
## Features
 
- Simple incident intake form on the Service Portal
- Mandatory-field validation
- Keyword-based Category / Subcategory / Priority assignment
- Automatic assignment group routing
- Email and portal notifications at creation, classification and resolution
- Work notes and classification logs for IT staff
- Reports and dashboards for ticket volume, classification accuracy and resolution time
- Audit log of automatic classifications and workflow triggers
## Results
 
From the project report and UAT:
 
| Metric | Value |
|---|---|
| Categorization accuracy | 96.8% |
| Routing precision | 0.96 |
| Workflow execution success rate | 100% |
| End-to-end classification time (50-user load) | 0.85 s |
| Average latency (100 concurrent ticket creations) | 180 ms |
| UAT test cases passed | 78 / 78 |
 
## Project Structure
 
```
.
├── update-set/        # ServiceNow Update Set XML (Flow Designer actions, Business Rules)
├── docs/              # Project phase documents (PDF)
│   ├── Ideation (Problem Statement, Empathy Map, Brainstorm)
│   ├── Project Design (Solution Architecture, Data Flow, Tech Stack, Requirements)
│   ├── Project Planning
│   ├── Acceptance Testing
│   └── FINAL_PROJECT_REPORT.pdf
└── README.md
```
 
Adjust the folder names above to match the actual layout of the repository.
 
## Setup
 
1. Log in to your ServiceNow instance as an admin (a free Personal Developer Instance works).
2. Go to **System Update Sets > Retrieved Update Sets > Import Update Set from XML** and upload the Update Set from this repo.
3. Open the imported update set, **Preview** it, resolve any conflicts, then **Commit**.
4. Open **Flow Designer** and check that the classification flow is **Active**.
5. Create assignment groups matching the routing rules (for example Network, Identity and Access, AV Tech Support) and add members.
6. Submit a test incident from the Service Portal, for example *"Wi-Fi not connecting in Lab 2"*, and confirm the category, group and notification.
## Maintaining the Keyword Dictionary
 
Classification depends on clear keywords in the ticket text. As new issue types appear, add their keywords and the matching category and group to the flow's keyword logic.
 
## Limitations
 
- Ambiguous descriptions with no matching keyword need fallback or manual routing.
- The keyword dictionary needs regular maintenance.
## Future Scope
 
- **Virtual Agent integration** for conversational troubleshooting
- **Predictive Intelligence / ML** to classify complex, unstructured tickets
- Wider scope: software installation, lab equipment maintenance, administrative requests
## Documentation
 
Ideation, design, planning, testing and the final report are in the `docs/` folder. Start with `FINAL_PROJECT_REPORT.pdf`.
 
## Author
 
**AATHITHYA K V**
GitHub: [aathithyakumar-techy](https://github.com/aathithyakumar-techy)
