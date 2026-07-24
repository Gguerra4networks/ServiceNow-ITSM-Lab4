🎬 Watch Me Build This Lab!
https://www.loom.com/share/c337e2fee7a846d7a2e0f705b46b85de


(https://github.com/user-attachments/files/30327832/README_ServiceNow.md)




# Lab 04 — ServiceNow ITSM: Incident, Change & Service Catalog Management

*Hands-on ITIL workflow built from scratch on a free ServiceNow Personal Developer Instance (PDI) — Next Experience UI, 2026.*

🎥 **Full walkthrough (Loom):** [Watch the lab in action](https://www.loom.com/share/c337e2fee7a846d7a2e0f705b46b85de)

---

## 📌 Overview

Three people report the same server outage to three different IT team members. Nobody knows who's working it. The ticket doesn't exist. Four hours later, something that should've taken 45 minutes is still open.

That's what happens without a structured ITSM platform — and it's exactly the problem this lab is built to solve.

In this lab I requested a free ServiceNow PDI and built out the core ITIL workflow end-to-end:

- ✅ Incident creation, triage, and resolution — priority, SLA, work notes, resolution notes
- ✅ Self-service Service Catalog item with custom variables and a fulfillment group
- ✅ Change Request submission and approval using ITIL change management controls
- ✅ Reports on incident volume by priority, MTTR by team, and open incidents by agent
- ✅ A plain-English ITIL concept map — Incident vs. Problem vs. Change vs. Service Request

**Cost:** $0 · **Time:** 2–3 hours · **Aligns to:** CompTIA A+, Network+, and ITIL 4 Foundation

This is part of an ongoing hands-on IT & security operations lab series:
**AD → Wireshark → Splunk → ServiceNow.**

---

## 🧰 Environment

| Component | Details |
|---|---|
| Platform | ServiceNow Personal Developer Instance (PDI), Next Experience UI |
| Release | Latest available release at time of build (e.g., Zurich/Yokohama) |
| Cost | Free — no credit card required |
| Modules used | Incident, Problem, Change, Service Catalog, Reports |

A PDI is a free, private, full-featured copy of ServiceNow — pre-loaded with sample data (fake users, tickets, and hardware records) — that hibernates after 10 days of inactivity and is deleted after 30. It runs on a real ServiceNow release, so everything learned here transfers directly to a production instance.

---

## 🎫 Ticket Lifecycle at a Glance

```
Reported → Assigned → In Progress → Resolved → Closed
```

Every issue is logged as a ticket with a tracking number, assigned to one owner, and tracked start to finish — nothing falls through the cracks.

---

## 🛠️ What I Built

### 1. Incident Management
Simulated a real help desk scenario: a user's Outlook stops connecting to the Exchange server.
- Logged the incident with category, subcategory, priority, and assignment group
- Worked the ticket — added a private work note documenting triage steps
- Resolved with a customer-facing resolution note and closed with confirmation

**Screenshot:** `screenshots/01-incident-resolved.png`
*(ticket showing work note + resolution note)*

### 2. Self-Service Catalog Item
Built a "New Laptop Request" catalog item — the ServiceNow equivalent of an online order form.
- Configured name, category, description, and fulfillment group
- Added custom variables: requester name, business justification, required-by date, laptop model dropdown

**Screenshot:** `screenshots/02-catalog-item.png`

### 3. Change Management
Submitted and approved a Standard Change for a monthly security patch deployment (CVE-2024-0001).
- Set risk, impact, start/end maintenance window
- Filled out Test Plan and Backout Plan on the Planning tab
- Routed through Request Approval → self-approved as admin → Scheduled

**Screenshot:** `screenshots/03-change-approved.png`

### 4. Reporting
Used the guided (Data → Type → Configure → Style) report builder to chart:
- Incident Volume by Priority — last 30 days
- Mean Time to Resolution (MTTR) by team
- Open Incidents by Assigned Agent

**Screenshot:** `screenshots/04-incident-volume-chart.png`

---

## 📚 ITIL Concepts in Plain English

| Term | What it actually means |
|---|---|
| **Incident** | Something broke and needs fixing now. Goal: restore service fast. |
| **Problem** | The root cause behind repeat incidents. Goal: fix it permanently. |
| **Change** | A planned update, done carefully to avoid a new outage. |
| **Service Request** | Someone asking for something new — not something broken. |
| **SLA** | Service Level Agreement — a promise on response/resolution time. |
| **CMDB** | Configuration Management Database — every piece of tech the company owns. |
| **Knowledge Base** | Library of "here's how we fixed this before" articles. |
| **PDI** | Personal Developer Instance — a free, private ServiceNow sandbox. |

**Incident vs. Problem, the way it actually clicked:** an Incident is "Outlook is down for this user — restore it," closed in 30 minutes. A Problem is "why does Outlook keep breaking for users on this floor every Tuesday" — not closed until the root cause (a corrupted OST file, a flaky Exchange connector, whatever it turns out to be) is eliminated. They live in separate modules for a reason: Incidents are about speed, Problems are about permanence. Reading the definition never made that distinction real the way building both in the same platform did.

---

## 🔄 What I'd Do Differently

Next time, I'd write the Knowledge Base article *before* closing the incident — not as an afterthought. In a real environment, that's the step that compounds: the next analyst who hits the same corrupted-OST issue searches the KB, finds the documented fix, and resolves it in 10 minutes instead of escalating. Knowledge management isn't glamorous, but it's one of the first things that breaks down on teams that don't practice it — and one of the first things hiring managers ask about in ITIL interviews.

---

## 🧭 Navigating a Moving Target

The written SOP for this lab didn't fully match the live 2026-era Next Experience UI — modules weren't always where the docs said, and the classic report builder had been replaced with a guided wizard. Part of this lab was troubleshooting that gap in real time: using the Filter Navigator's search instead of a static left-nav, falling back to direct table URLs (e.g., `incident_list.do`) when a module didn't surface in search, and confirming whether a missing module was a role-visibility issue versus a plugin that simply wasn't active on that instance. Working around documentation that doesn't quite match what's on screen is itself a real help desk skill — and one worth showing, not just the finished tickets.

---

## 🎯 Why This Matters

ServiceNow shows up on more IT support and cloud ops job descriptions than almost any other ITSM platform. This lab is the exact day-one workflow most help desk and IT support teams run — incident triage, self-service requests, controlled change, and reporting — built hands-on, for free, before the first interview.

---

## 🔗 Related

- 🎥 Loom walkthrough: [https://www.loom.com/share/c337e2fee7a846d7a2e0f705b46b85de](https://www.loom.com/share/c337e2fee7a846d7a2e0f705b46b85de)
- 🧪 Other labs in this series: Active Directory (Lab 01) → Wireshark → Splunk SIEM Log Analysis (Lab 03) → ServiceNow ITSM (Lab 04)

---

## 👤 About

Built by **Giovanni Guerra** — IT & network infrastructure professional pivoting into cloud security and DevOps, documenting hands-on labs as part of a public portfolio.

📎 GitHub: [Gguerra4networks](https://github.com/Gguerra4networks)
