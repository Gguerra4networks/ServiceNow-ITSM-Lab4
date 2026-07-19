# Lab 4 — ServiceNow ITSM

![Certification](https://img.shields.io/badge/CompTIA-A%2B-blue) ![Certification](https://img.shields.io/badge/CompTIA-Network%2B-blue) ![Certification](https://img.shields.io/badge/ITIL-4%20Foundation-informational) ![Cost](https://img.shields.io/badge/Cost-%240-brightgreen) ![Duration](https://img.shields.io/badge/Duration-2--3%20hours-yellow) ![Tool](https://img.shields.io/badge/Tool-ServiceNow%20PDI-green)

**Stack:** ServiceNow Personal Developer Instance (free) · No credit card · No expiration  
**Roles:** IT Support · Help Desk · Sysadmin · ITSM Platform Administrator · Cloud Operations

---

## About this lab

When users report IT problems, those problems need to be tracked, routed, prioritised, assigned, worked, and resolved — consistently and auditably. Without a structured system, things fall through the cracks. A server goes down, three people report it to three different team members, nobody knows who is working on it, and it takes four hours to fix something that should have taken one.

ServiceNow is how most enterprise IT organisations solve this. It is the most widely deployed IT Service Management platform in the world. If you are going into IT support, you will use it — or something that works exactly like it — from your first week on the job. Having hands-on experience before you start is a meaningful differentiator.

---

## Architecture — How the four ITIL process flows work in ServiceNow

```
  ┌─────────────────────────────────────────────────────────────────────┐
  │   End user                              IT staff / manager          │
  └───┬──────────────────────┬─────────────────────┬──────────────┬────┘
      │                      │                     │              │
      ▼                      ▼                     ▼              ▼
  ┌──────────┐        ┌──────────────┐      ┌──────────────┐  ┌──────────┐
  │ Incident │        │Service request│      │Change request│  │ Problem  │
  │Unplanned │        │Catalogue item│      │Planned modif.│  │Root cause│
  │ outage   │        │              │      │              │  │analysis  │
  └────┬─────┘        └──────┬───────┘      └──────┬───────┘  └────┬─────┘
       │                     │                     │               │
       ▼                     ▼                     ▼               ▼
  ┌──────────┐        ┌──────────────┐      ┌──────────────┐  ┌──────────┐
  │ Triage   │        │Approval gate │      │  CAB review  │  │Investig- │
  │Priority ·│        │Manager       │      │Risk · impact │  │ation     │
  │assignment│        │sign-off      │      │assessment    │  │Known err │
  └────┬─────┘        └──────┬───────┘      └──────┬───────┘  └────┬─────┘
       │                     │                     │               │
       ▼                     ▼                     ▼               ▼
  ┌──────────┐        ┌──────────────┐      ┌──────────────┐  ┌──────────┐
  │Resolution│        │  Fulfilment  │      │Implementat'n │  │Fix /     │
  │Work notes│        │Provision ·   │      │Scheduled     │  │workaround│
  │· close   │        │deliver       │      │window        │  │KB article│
  └────┬─────┘        └──────┬───────┘      └──────┬───────┘  └────┬─────┘
       │                     │                     │               │
       └─────────────────────┴─────────────────────┴───────────────┘
                                       │
                                       ▼
                        ┌──────────────────────────────┐
                        │    Reports & dashboards       │
                        │  Volume · MTTR · SLA compliance│
                        └──────────────────────────────┘
```

**How the flows connect:**  
All four ITIL process types — Incident, Service Request, Change, and Problem — live inside ServiceNow and share the same underlying platform. Each has its own module, its own workflow, and its own state machine, but they all feed into the same reporting layer. An Incident can spawn a Problem record. A Problem's fix can trigger a Change request. A Change that fails can become a new Incident. Understanding how these four types relate is the foundational skill for every IT operations role.

---

## What you will be able to do after completing this lab

| Skill | Real-world application |
|---|---|
| Create and resolve an incident | The most common task in every IT support role — done from day one |
| Set ticket priority and SLA | Priority determines response time; SLAs define the business commitment — you need to understand both |
| Assign tickets to queues and individuals | Routing is critical in a team environment — the wrong person on a ticket wastes time and delays resolution |
| Build a service catalogue item | Lets users self-serve common requests without calling the help desk for every ticket |
| Create an approval workflow on a change request | Change requests require manager sign-off before work begins — this is a core ITIL control |
| Run reports on ticket volume and resolution time | Metrics drive IT operations decisions at every level |
| Explain ITIL incident vs problem vs change | The three core ITIL process types used in every enterprise IT conversation |

---

## Prerequisites

- A free ServiceNow developer account (sign up at [developer.servicenow.com](https://developer.servicenow.com))
- A browser — no local software required
- No prior ServiceNow experience needed

---

## Step 1 — Get your free instance

1. Go to [developer.servicenow.com](https://developer.servicenow.com)
2. Click **Sign Up** — email and password only, no credit card
3. Once logged in, click **Request Instance**
4. Select the latest stable release (Washington or newer)
5. Click **Request** — your instance provisions in 10–15 minutes
6. You will receive an email with your instance URL (format: `dev12345.service-now.com`) and login credentials

> **Keep your instance active.** ServiceNow hibernates Personal Developer Instances that have not been accessed in 10 days and reclaims instances inactive for more than 30 days. Log in at least once a week to keep it live. If it is reclaimed you can request a new one for free, but you lose your work.

---

## Step 2 — Navigate the platform

When you first log in you are in the ServiceNow admin interface. The left navigation panel gives you access to all modules.

| Module | Where it is | What it does |
|---|---|---|
| Incident | Service Desk → Incidents | Primary module for IT support tickets |
| Problem | Service Desk → Problems | Root cause analysis for recurring incidents |
| Change | Change → Changes | Planned modifications to IT infrastructure |
| Service Catalog | Service Catalog → Catalogs | The user-facing self-service request portal |
| Reports | Reports → Create New | Analytics and metrics dashboards |
| Workflow Editor | Process Automation → Flow Designer | Visual workflow builder for approvals |

---

## Step 3 — Create and work an incident

### Create the incident

Navigate to **Service Desk → Incidents → New** and fill in the form:

| Field | Value |
|---|---|
| Caller | Search for and select `Abel Tuter` (built-in test user) |
| Category | Software |
| Subcategory | Email |
| Short description | `User cannot access Outlook — error: Cannot connect to server` |
| Description | User reports Outlook stopped working at approximately 9am. Error: "Cannot connect to the Exchange server. Verify your network settings." Other users in the same building are not affected. User is on a laptop, Wi-Fi connected. |
| Priority | 3 — Moderate (one user affected, workaround available via webmail) |
| Assignment Group | Service Desk |

Click **Submit** and note the ticket number (format: `INC0001234`).

### Work the incident

1. Open the incident you just created
2. Change **State** to `In Progress`
3. Assign it to yourself — click the **Assigned to** field and search your username
4. Add a **Work Note** (visible to IT staff only):

```
Contacted user. Confirmed error message. Outlook profile appears corrupted.
Attempting profile repair. Instructed user to use OWA (webmail) in the interim.
Resolution ETA: 30 minutes.
```

5. Add a **Resolution Note**:

```
Rebuilt Outlook profile. Removed and re-added the Exchange account.
User confirmed Outlook is working. Issue was a corrupted OST file.
Closed with user confirmation.
```

6. Change **State** to `Resolved` → `Closed`

---

## Step 4 — Build a service catalogue item

Service catalogue items let users request common IT services through a self-service portal, reducing ticket volume for routine requests and speeding up fulfilment.

Navigate to **Service Catalog → Catalogs → Service Catalog → Maintain Items → New**:

| Field | Value |
|---|---|
| Name | New Laptop Request |
| Category | Hardware |
| Short description | Request a new or replacement laptop |
| Description | Use this form to request a new laptop for a new hire or to replace a failed or end-of-life device. Requests reviewed within 2 business days. Delivery 5–7 business days after approval. |
| Fulfillment group | IT Hardware Team |

Click **Submit**, then open the **Variables** tab and add these form fields:

| Variable name | Type | Mandatory |
|---|---|---|
| Requester Name | Single Line Text | Yes |
| Business Justification | Multi Line Text | Yes |
| Required By Date | Date | Yes |
| Laptop Model Preference | Select Box (Standard / Developer / Executive) | No |

Click **Save** and **Preview** — the item now appears in the service catalogue portal.

---

## Step 5 — Create an approval workflow on a change request

Change requests require manager approval before work begins. This is a core ITIL control — uncoordinated changes to production infrastructure are one of the leading causes of outages.

Navigate to **Change → Changes → New (Standard)** and fill in:

| Field | Value |
|---|---|
| Short description | Deploy security patch MS24-001 to all Windows workstations |
| Category | Software |
| Risk | Low |
| Impact | 2 — Medium |
| Start date | Next Saturday at 2:00 AM |
| End date | Next Saturday at 6:00 AM |
| Description | Monthly security patch deployment. Patch addresses CVE-2024-0001 rated CVSS 7.8. Workstations require one reboot. Deployed via WSUS. Rollback: uninstall via WSUS if issues reported post-deployment. |

Under the **Planning** tab, add a Test Plan and Backout Plan.

Then:
1. Click **Request Approval** — moves the change to `Pending Approval` state
2. Navigate back to the change and open the **Approvals** tab
3. Approve it as the admin user — the change moves to `Scheduled` state

---

## Step 6 — Build reports

Navigate to **Reports → Create New** and build the following three reports for your portfolio:

### Report 1 — Incident volume by priority

| Setting | Value |
|---|---|
| Name | Incident Volume by Priority — Last 30 Days |
| Data | Incident [incident] |
| Type | Bar Chart |
| Group by | Priority |
| Condition | Created is on or after 30 days ago |

Click **Save and Run**.

### Report 2 — Mean time to resolution by team

| Setting | Value |
|---|---|
| Name | MTTR by Assignment Group |
| Data | Incident [incident] |
| Type | Bar Chart |
| Group by | Assignment Group |
| Aggregate | Average of Resolve time |

### Report 3 — Open incidents by assigned agent

| Setting | Value |
|---|---|
| Name | Open Incidents by Assigned Agent |
| Data | Incident [incident] |
| Type | Column Chart |
| Group by | Assigned to |
| Condition | State is not Closed / Resolved |

This report is used for workload balancing — identifying agents carrying too many open tickets before queues back up.

---

## ITIL concepts mapped to ServiceNow

These terms come up in every IT support interview and are tested in the ITIL 4 Foundation exam. Mapping them to ServiceNow modules makes them concrete.

| ITIL term | Definition | ServiceNow module |
|---|---|---|
| Incident | An unplanned interruption to a service. Goal: restore service as fast as possible, not necessarily fix the root cause. | Service Desk → Incidents |
| Problem | The underlying root cause of one or more incidents. Goal: eliminate the cause permanently. | Service Desk → Problems |
| Change | A planned modification to infrastructure or applications. Goal: implement safely with minimum risk. | Change → Changes |
| Service Request | A user request for something new — access, hardware, information. Not a break/fix. | Service Catalog |
| SLA | Service Level Agreement — the committed response and resolution time for each priority level. Breached SLAs are flagged automatically. | SLA → SLA Definitions |
| CMDB | Configuration Management Database — the authoritative record of every IT asset and its relationships to other assets. | Configuration → CIs |
| Knowledge Base | Articles documenting known issues and their solutions, reducing repeat incident volume and enabling self-service. | Knowledge → Articles |

### Priority matrix — how priority maps to SLA response time

| Priority | Criteria | Typical response target | Typical resolution target |
|---|---|---|---|
| 1 — Critical | Multiple users / business-critical system down | 15 minutes | 4 hours |
| 2 — High | Single critical user or significant degradation | 1 hour | 8 hours |
| 3 — Moderate | Single user affected, workaround available | 4 hours | 24 hours |
| 4 — Low | Cosmetic issue, no business impact | 8 hours | 72 hours |

---

## Verification checklist

| Check | How to verify |
|---|---|
| Incident created and closed | Open your incident — State shows Closed, resolution notes are populated, work notes visible in the Activity section |
| Catalogue item published | Navigate to the Service Catalog portal as a non-admin user — the New Laptop Request item appears and is submittable |
| Change request approved | Open your change record — the Approvals tab shows an approved entry and State is Scheduled |
| Reports run and populated | All three reports return data and render charts when saved and run |

---

## How this applies to cloud environments

| ServiceNow skill | Cloud / enterprise equivalent |
|---|---|
| Incident management workflow | Azure Incident Management in Monitor · PagerDuty incidents · AWS Systems Manager OpsItems |
| Change request with CAB approval | Azure DevOps change management gates · AWS Change Manager |
| Service catalogue | Azure Service Management · AWS Service Catalog |
| MTTR reporting | Azure Monitor workbooks · CloudWatch Contributor Insights |
| CMDB asset relationships | Azure Resource Graph · AWS Config resource relationships |

---

## Portfolio artefacts from this lab

Capture screenshots of the following and commit them to this repo in a `screenshots/` folder with a written summary for each:

| Artefact | What to capture | Why it matters |
|---|---|---|
| Completed incident | Full incident form showing work notes, resolution notes, and Closed state | Demonstrates the full incident lifecycle — the most common daily task in help desk and SOC roles |
| Service catalogue item | Preview of the New Laptop Request form as it appears in the portal | Shows ability to build self-service tools that reduce ticket volume |
| Approved change request | Change record with the Approvals tab showing manager approval and Scheduled state | Demonstrates understanding of change control — a required process in every regulated environment |
| MTTR report | Bar chart showing mean resolution time by assignment group | Shows ability to extract operational metrics — expected in any IT operations or SOC role |

---

## Resources

- [ServiceNow developer documentation](https://developer.servicenow.com/dev.do)
- [ServiceNow product documentation](https://docs.servicenow.com)
- [ITIL 4 Foundation overview — Axelos](https://www.axelos.com/certifications/itil-service-management/itil-4-foundation)
- [CompTIA A+ certification](https://www.comptia.org/certifications/a)
- [CompTIA Network+ certification](https://www.comptia.org/certifications/network)
