# Courier Management System (Salesforce)

A Salesforce-based Courier Management System (CMS) designed to streamline end-to-end courier operations, from shipment booking through delivery confirmation and invoicing.

## 1) Project Overview & Business Objectives

### Overview
The CMS is implemented on Salesforce using custom objects, record-triggered automation, role-based access controls, and reporting dashboards. It centralizes customer, shipment, branch, delivery agent, and billing data in a single platform.

### Business Objectives
- Improve shipment lifecycle visibility from creation to delivery.
- Reduce manual handoffs through guided automation.
- Enable branch-level and organization-level operational reporting.
- Strengthen data security with clear ownership and access boundaries.
- Improve billing consistency via invoice traceability per shipment.

## 2) Data Architecture & Entity Relationship Summary

The solution uses the following custom objects:

- **Customer**: Stores customer profile and contact details.
- **Shipment**: Core transaction object containing shipment metadata, status, source/destination branch, and assigned delivery agent.
- **Delivery Agent**: Stores courier personnel details, assignment capacity, and operational status.
- **Branch**: Represents physical branch locations handling shipment intake and dispatch.
- **Delivery Update**: Event-style object capturing shipment status history (in transit, delayed, delivered, etc.).
- **Invoice**: Billing record linked to shipments and customers.

### Relationship Summary (Logical)
- One **Customer** can have many **Shipments**.
- One **Branch** can manage many **Shipments** (origin and/or destination context).
- One **Delivery Agent** can be assigned to many **Shipments** over time.
- One **Shipment** can have many **Delivery Updates**.
- One **Shipment** can have one (or more, if business allows) **Invoice** records.

### Typical Linkage Pattern
- `Shipment -> Customer` (Lookup/Master-Detail based on ownership model)
- `Shipment -> Branch` (Origin Branch, Destination Branch lookups)
- `Shipment -> Delivery Agent` (Lookup)
- `Delivery Update -> Shipment` (Master-Detail preferred for timeline integrity)
- `Invoice -> Shipment`, `Invoice -> Customer` (Lookup/Master-Detail based on billing policy)

## 3) Automation Rules (Record-Triggered Flows)

Shipment processing is automated with Salesforce **Record-Triggered Flows** to standardize status progression and reduce manual updates.

### Core Automation Behaviors
- On **Shipment create**:
  - Initialize default shipment status (e.g., `Booked`).
  - Optionally create first **Delivery Update** entry.
- On **Shipment status change**:
  - Create a corresponding **Delivery Update** timeline record.
  - Enforce valid state transitions (e.g., prevent `Delivered` directly from `Booked` without transit events).
- On **Assignment updates**:
  - Update shipment assignment fields when delivery agent changes.
  - Trigger branch/operations notifications where applicable.
- On **Delivery completion**:
  - Mark final status as `Delivered`.
  - Trigger downstream invoice readiness logic or invoice generation flow.

### Flow Design Notes
- Use before-save flows for fast field updates.
- Use after-save flows for related-record creation (Delivery Update, Invoice actions).
- Add decision branches for branch-specific processes and exception handling.

## 4) Security & Access Model

Security follows Salesforce layered controls: **Role Hierarchy + Profiles + OWD + Sharing Rules**.

### Roles (example)
- Operations Head
- Regional/Branch Manager
- Dispatcher
- Delivery Agent User
- Finance User

### Profiles (example access model)
- **Operations Profile**: Full create/read/update on Shipment and Delivery Update.
- **Delivery Agent Profile**: Read assigned shipments; update limited delivery status fields.
- **Finance Profile**: Read shipment/customer context; manage Invoice object.
- **Admin Profile**: Full object and field-level control.

### Organization-Wide Defaults (OWD) (recommended baseline)
- **Shipment**: Private
- **Delivery Update**: Controlled by Parent (Shipment)
- **Invoice**: Private
- **Customer**: Private or Public Read Only (based on compliance policy)
- **Branch**: Public Read Only
- **Delivery Agent**: Private or Public Read Only (depending on HR/privacy requirements)

### Additional Sharing Controls
- Criteria-based sharing for branch teams to view branch-relevant shipments.
- Role hierarchy visibility for management escalation.
- Optional manual sharing for cross-branch exceptions.

## 5) Reports & Analytics Dashboards

The CMS includes operational and management analytics using Salesforce Reports and Dashboards.

### Recommended Reports
- Shipments by Status (Booked/In Transit/Delayed/Delivered)
- Average Delivery Turnaround Time by Branch
- Delivery Agent Workload and Completion Rate
- Delayed Shipment Trend by Week/Month
- Invoice Status Summary (Pending/Paid/Overdue)

### Dashboard Components
- KPI tiles: Total active shipments, delivered today, delayed shipments, pending invoices.
- Trend charts: Delivery performance over time.
- Branch comparison charts: Throughput and SLA performance.
- Agent performance charts: Assignments vs successful deliveries.

## Repository Structure

```text
/
├── README.md
├── docs/
└── screenshots/
```

- **docs/**: Architecture diagrams, object model references, flow designs, and functional specifications.
- **screenshots/**: Salesforce configuration proof (object setup, flows, sharing settings, reports, and dashboards).

## Next Documentation Assets to Add

- ER diagram for all custom objects.
- Flow diagrams for each shipment status automation path.
- Security matrix (Roles x Profiles x Objects x Permissions).
- Screenshot evidence for objects, flows, reports, and dashboards.
