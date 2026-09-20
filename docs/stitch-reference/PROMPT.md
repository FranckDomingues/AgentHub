# Google Stitch Prompt

## Purpose

This prompt was supplied to Google Stitch after the AgentHub specification
had been defined. Stitch was used only for visual design exploration.

The existing application implementation was not intended to be replaced.

## Prompt

Create a visual design proposal for the AgentHub Admin Dashboard.

IMPORTANT PROCESS CONSTRAINT:

This is a DESIGN-REFERENCE exercise only.

A fully functional implementation of AgentHub already exists and has passed
functional QA.

DO NOT redesign the product requirements.
DO NOT generate replacement application code.
DO NOT change the information architecture.
DO NOT add new features.
DO NOT remove required features.
DO NOT connect to or modify a GitHub repository.

The provided SPECS.md is the source of truth.

PRODUCT:

AgentHub is a SaaS platform where businesses rent preconfigured AI agents
equipped with reusable skills.

The interface is an internal administration dashboard.

The administrator monitors:

- revenue
- discounts and coupon losses
- customers
- AI agents
- agent operational status
- available skills
- rental contracts
- execution errors

REQUIRED INFORMATION ARCHITECTURE:

Use exactly these six sidebar destinations:

1. Dashboard
2. User Management
3. Agent Management
4. Skills
5. Agent Rentals
6. Error Log

Do not add additional primary navigation items.

GLOBAL LAYOUT:

Create a professional desktop-first SaaS administration interface.

Use:

- persistent left sidebar
- top navigation/header
- main content area
- clear visual hierarchy
- restrained enterprise styling
- slate/neutral surfaces
- indigo primary accent
- emerald active/success states
- amber warning states
- rose/red failure or destructive states
- rounded panels
- subtle borders
- restrained shadows

Primary target:
1440px desktop.

The design should also support:
1024px desktop/tablet
768px tablet.

Avoid:

- marketing landing-page layouts
- excessive gradients
- glassmorphism
- decorative illustrations unrelated to administration
- oversized typography
- unnecessary navigation
- framework-specific UI concepts

DASHBOARD:

Show four metric cards:

Total revenue this month
$1,345.00

Discounts / coupon losses
$105.00

Active agents
2

Failing agents
1

Each card contains:

- icon
- label
- prominent value
- restrained accent treatment

Below them show:

Weekly activity
September 7–13, 2026

Create a full-width chart placeholder rather than a real analytical chart.

USER MANAGEMENT:

Create a table showing:

- Name
- Email
- Plan
- Status
- Actions

Use status badges.

Each row has a vertical three-dot action trigger.

Show a representative visual state for a User Details modal.

AGENT MANAGEMENT:

Create agent management panels showing:

- agent name
- owner/company
- operational status
- skill count
- expandable skills
- action menu

Statuses:

Active
Inactive
Failing

Show at least one expanded example with skill chips visible.

Also show the visual concept for an Agent Configuration modal containing
a large editable System Prompt textarea.

SKILLS:

Include a short information panel titled:

"What is a skill?"

Below it show a two-column skill catalog.

Each skill card includes:

- name
- description
- number of agents using it
- action trigger

AGENT RENTALS:

Create a table showing:

- Customer
- Rented agent
- Skills
- Start date
- End date
- Total paid
- Status
- Actions

Show a representative Contract Details modal containing an itemized price
breakdown.

ERROR LOG:

Create a table showing:

- Timestamp
- Agent
- Error type
- Severity
- Description
- Resolution
- Actions

Severity states:

Critical
Warning
Info

Show an Error Details modal containing a monospaced execution trace.

TOP BAR:

Include:

- current section title
- "Prototype - changes reset on reload"
- light/dark mode control

IMPLEMENTATION AWARENESS:

The existing implementation uses:

- semantic HTML
- Tailwind CSS via CDN
- vanilla JavaScript
- no UI component framework

Keep the visual proposal realistically implementable using simple HTML and
Tailwind utilities.

Do not propose visual patterns that require a complex component library or
custom frontend framework.

DELIVERABLE:

Produce a cohesive VISUAL REFERENCE only.

Prioritize:

1. clarity
2. consistency
3. usability
4. visual hierarchy
5. realistic SaaS administration patterns
6. compatibility with the supplied specification

The final design will be reviewed against SPECS.md.

It will NOT automatically replace the existing AgentHub implementation.
