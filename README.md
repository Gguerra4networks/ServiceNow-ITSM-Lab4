🎬 Watch Me Build This Lab!
https://www.loom.com/share/c337e2fee7a846d7a2e0f705b46b85de


[README_ServiceNow.md](https://github.com/user-attachments/files/30327314/README_ServiceNow.md)
[Uplo# ServiceNow Help Desk Lab

Hands-on ITSM lab: a free ServiceNow Personal Developer Instance (PDI) used to run the full ticket lifecycle end to end — reporting and resolving an incident, building a self-service catalog request, routing a change through manager approval, and building reports on the results. Written and tested against a real 2026-era PDI on the **Next Experience UI**, with click-paths corrected wherever the original instructions didn't match what actually appears on screen.

**Environment:** Free ServiceNow PDI (developer.servicenow.com) · Browser-only, no local tooling required

---

## What This Lab Demonstrates

- Standing up a Personal Developer Instance and understanding its lifecycle (10-day hibernation, 30-day deletion)
- Navigating the Next Experience UI's Filter Navigator, including working around search results that don't surface a module (role-visibility gaps, inactive plugins) via direct list-view URLs
- Reporting, working, and closing an **Incident** — including the distinction between private Work Notes and customer-facing Resolution Notes
- Building a **Service Catalog** item (a self-service request form) with custom variables for end users to fill in
- Routing a **Change Request** through Planning → Approval → Scheduled, including self-approval as the PDI admin
- Building charts in the wizard-style Report Builder (Data → Type → Configure → Style), including how to avoid accidentally picking a Performance Analytics data source instead of a plain table

## Ticket Lifecycle at a Glance

```
Reported → Assigned → In Progress → Resolved → Closed
   │                                    │
   └── Work Notes (internal only)       └── Resolution Notes (customer-visible)
```

## Core ITSM Concepts

| Term | What it actually means |
|---|---|
| Incident | Something broke and needs fixing now — goal is to restore service fast |
| Problem | The deeper root cause behind repeat incidents |
| Change | A planned, carefully-approved modification, done to avoid causing a new outage |
| Service Request | Someone asking for something new — not something broken |
| SLA | Service Level Agreement — a promised response/resolution time |
| CMDB | Configuration Management Database — every piece of tech the company owns |
| Knowledge Base | Library of "here's how we fixed this before" articles |
| PDI | Personal Developer Instance — a free, private, disposable ServiceNow sandbox |
| Filter Navigator | The search panel (opened via the **All** menu) used to jump to any module by name |

## Lab Walkthrough

1. **Get a free PDI** — sign up at developer.servicenow.com, request an instance on the newest release available, wait ~10–15 minutes for provisioning.
2. **Navigate the Next Experience UI** — open the Filter Navigator via **All** (top-left), and fall back to direct list-view URLs (e.g. `incident_list.do`) when a module doesn't surface in search.
3. **Report and resolve an incident** — log a fake ticket (`Abel Tuter`, broken Outlook), work it with a Work Note, close it with customer-facing Resolution Notes.
4. **Build a self-service catalog item** — a "New Laptop Request" form with required text, paragraph, date-picker, and dropdown variables.
5. **Route a change through approval** — a Standard change with a test plan and backout plan, self-approved as admin, moving from Pending Approval to Scheduled.
6. **Build reports** — an "Incident Volume by Priority, Last 30 Days" bar chart using the guided wizard, correctly scoped to the plain Incident table rather than a Performance Analytics source.

## Real Gotchas Hit Building This

| Problem | Root cause | Fix |
|---|---|---|
| Filter Navigator search returns dozens of irrelevant results | A generic term like "change" or "report" matches many unrelated modules | Use a specific phrase instead — "change request," "reports" (plural) |
| A module doesn't appear in search at all | Either a role-visibility gap or the plugin genuinely isn't active on that PDI | Try the module's direct list-view URL (e.g. `change_request_list.do`) — if it loads, the data model exists even though search didn't surface it |
| Report Builder pulls in unexpected SLA/Stage filters | Accidentally selected a "PA.Source" (Performance Analytics) data source instead of the plain table | Reopen the Data Source dropdown and pick the plain "Incidents.Open (Incident)" option — conditions panel should show only `Active = true` |
| Only a 90-day preset shows in the relative date picker, not 30 | Not every PDI's date picker offers the same interval presets | Either keep the available interval and rename the report to match, or enter the day count manually if a numeric field is offered |
| Typed a search term into the wrong field on an open form | Easy to type into a form field instead of the top search box | Nothing saves until Submit is clicked — just clear the field and retry |

## Portfolio Checklist

Screenshot each of the following, with 2–3 sentences in your own words on what it does and why it matters:

- [ ] Completed incident ticket (with Work Note + Resolution Notes)
- [ ] New Laptop Request catalog form
- [ ] Approved change request
- [ ] One report/chart (e.g. Incident Volume by Priority)

Worth a short note on any point where you had to navigate around a UI that didn't match written instructions — troubleshooting mismatched documentation is itself a real help desk skill worth demonstrating.

## Notes on PDI Behavior

- PDIs hibernate after 10 days of inactivity and are deleted after 30 — log in weekly to keep it alive.
- Not every PDI is configured identically: active plugins, visible modules, and even which report-builder UI appears can vary by instance and release. Screenshots in the full guide reflect one real instance — minor differences on yours are normal.
- You have full admin rights in your own PDI, so steps like self-approving a change are expected here and would not be normal practice on a production instance.

## Full Guide

The complete walkthrough — every click, every field, every screenshot-verified path through the Next Experience UI — lives in [`ServiceNow_Lab_Updated_UI.docx`](./ServiceNow_Lab_Updated_UI.docx).

---

*Part of a home-lab series building SOC analyst and cloud/IT operations skills, one deployable project at a time.*
ading README_ServiceNow.md…]()

<img width="2720" height="2320" alt="servicenow_itsm_architecture" src="https://github.com/user-attachments/assets/8a966cd2-08b3-4e9f-81ba-786986cc4b8c" />[post strategy for Lab 04 — ServiceNow ITSM.docx](https://github.com/user-attachments/files/30171416/post.strategy.for.Lab.04.ServiceNow.ITSM.docx)
[Copy of lab-04-servicenow ITSM.docx](https://github.com/user-attachments/files/30171415/Copy.of.lab-04-servicenow.ITSM.docx)
