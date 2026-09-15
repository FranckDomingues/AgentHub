# AgentHub Admin Dashboard — Product Specification

## 1. Product Overview

AgentHub is a SaaS platform where businesses rent preconfigured AI agents equipped with skills such as web browsing, document reading, calendar management, and business-specific tasks.

This deliverable specifies an internal administration dashboard prototype. The eventual prototype will demonstrate navigation, inspection, configuration, and local administrative actions using hardcoded data. It is not a customer storefront or a production administration system.

This phase produces only this specification. Do not implement HTML, CSS, or JavaScript, install dependencies, or commit changes during this phase. Implementation requires separate approval.

The future prototype must expose revenue, discount/coupon losses, customers, agent operational status, available skills, active and historical rentals, and execution errors. Authentication, billing processing, actual agent execution, and backend connectivity are out of scope.

## 2. Target User

The primary user is an AgentHub internal administrator who needs to:

- Review monthly revenue and discounts at a glance.
- Identify active and failing rented agents.
- Inspect customer records and rental terms.
- Inspect available skills and their usage.
- Review and locally edit an agent's system prompt.
- Inspect execution traces and acknowledge errors as resolved.

All actions are demonstrations with session-local effects, not real customer or billing operations. Show a persistent top-bar label: "Prototype - changes reset on reload".

## 3. Technical Stack and Constraints

- Future implementation: one HTML document using semantic HTML, Tailwind CSS through CDN only, and vanilla JavaScript embedded in the document.
- Use the Tailwind v3 Play CDN at `https://cdn.tailwindcss.com` and its class-based dark-mode configuration. This explicit version choice supports toggling a root `dark` class with `dark:` utilities without author-written CSS. Do not substitute Tailwind v4's default media-based dark-mode behavior.
- Tailwind CDN loading is the sole required external resource. Do not load external fonts, icon packages, images, chart libraries, or other scripts. Use system fonts and small embedded decorative SVG icons.
- Do not use React, Vue, jQuery, frontend frameworks, npm packages, package installation, build tools, or a compilation step.
- Do not create custom CSS files, author custom CSS rules or style blocks, or use inline `style` attributes. Layout, transitions, colors, focus states, and responsive behavior must use Tailwind utilities. Tailwind's own CDN-generated styles are permitted.
- Use `dark:` utilities for every theme-sensitive interface surface; do not implement dark mode with custom CSS.
- Use hardcoded local records only. No backend integration, API calls, fetch/XHR, WebSockets, analytics, external form submissions, or real payment processing.
- Hold navigation, edits, deletion results, error resolutions, and theme state in memory. Reload restores the fixture, Dashboard selection, collapsed skill lists, and light mode. Cross-reload persistence is not required; do not use local storage.
- Tailwind utility names used for data-driven badges and states must be complete literal class names, not dynamically assembled fragments.
- The prototype assumes an internet connection only to load Tailwind. Do not promise offline styling.
- This specification overrides conflicting generic starter README suggestions, including suggestions to create CSS files or use a different Tailwind setup.

## 4. Information Architecture

The sidebar contains exactly these six navigation destinations, in this order:

| Destination | Section identifier | Purpose |
| --- | --- | --- |
| Dashboard | dashboard | Financial and operational overview |
| User Management | users | Customer accounts and account details |
| Agent Management | agents | Agent status, skills, and system prompts |
| Skills | skills | Skill catalog and usage |
| Agent Rentals | rentals | Active and historical contracts |
| Error Log | errors | Execution failures and resolution state |

Dashboard is selected initially. Selecting a destination shows its section and hides all other sections without reloading the document or making a request. Hidden sections must not remain keyboard-focusable or appear in the accessibility tree. No additional sidebar destinations, routing library, URL routing, or browser-history behavior are required.

## 5. Global Layout and Navigation

1. **Application shell:** Use a full-height application with a fixed left sidebar, a top bar offset by the sidebar width, and a main content region below the top bar. The top bar and sidebar remain visible while the main document scrolls. Use slate-50 backgrounds, white panels, slate-200 borders, and slate-900 text in light mode; use slate-950 backgrounds, slate-900 panels, slate-700 borders, and slate-100 text in dark mode.
2. **Sidebar:** Display the AgentHub wordmark above six vertically stacked navigation buttons, each with an icon and its exact destination label. The active button has an indigo tinted background, a left accent border, and stronger text weight, using dark equivalents. Inactive buttons have visible hover and focus states. Selecting a button updates the active indicator, top-bar title, and visible section together.
3. **Top bar:** Use a 64px-high header with the current section title on the left and the prototype notice and light/dark toggle on the right. At tablet widths, the notice may wrap within its allotted space; it must not overlap the title or toggle. The toggle remains visible in every section.
4. **Content hierarchy:** Every section starts with one prominent section heading and a short muted description. Use approximately 24px bold section headings, 18px semibold panel headings, 14px body/table text, and 12px metadata. Panels use rounded corners, a subtle border, and restrained shadows. Main content is full width with no artificial narrow reading column.
5. **Navigation state:** Returning to a section preserves in-memory edits, resolution state, and expanded skill lists. Changing sections closes any dropdown, resets the main scroll position to the section start, and moves focus to the new section heading. Modal overlays block interaction with navigation until closed.

## 6. Dashboard Specification

1. **Four metric cards:** Show exactly four equally sized cards at the top, each with a decorative icon, visible label, and prominent hardcoded value. Cards form four columns at widths of 1024px or more and two columns from 768px to 1023px. Maintain at least 16px gaps, consistent padding, and a minimum height of 128px. Values are approximately 30px bold; labels are 14px. Cards are informational, not buttons.

   | Label | Initial value | Icon concept | Accent |
   | --- | --- | --- | --- |
   | Total revenue generated this month | $1,345.00 | Currency | Emerald |
   | Total loss caused by discounts and coupons | $105.00 | Discount tag | Amber |
   | Number of active agents across all customers | 2 | Agent/processor | Indigo |
   | Number of agents currently marked as failing | 1 | Warning triangle | Rose |

2. **Metric context and emphasis:** Put "September 2026 - USD" in the section description. Add "Net payments received this month" to revenue and "Discounts and coupons applied this month" to loss as muted supporting text. Active means status exactly `active`; failing agents are not included in that count. Use tinted icon containers and a thin top accent border rather than fully saturated card backgrounds. Dark variants retain readable labels and distinguishable accents.
3. **Weekly activity placeholder:** Below the cards, place a full-width panel with the heading "Weekly activity", range "September 7-13, 2026", and a visible "Placeholder - sample visualization only" label. Reserve a 256px-high chart area containing a static chart/grid icon and the centered text "Weekly agent activity chart". Below it, show evenly spaced Mon-Sun labels. The panel is static: no real counts, axes implying measured values, hover tooltips, loading spinner, animation, clicks, or chart dependencies.
4. **Fixture semantics:** Display the four specified values on initial load. Revenue and loss reconcile with the September contract payments in Section 14; operational counts reconcile with current agent statuses. Do not use the browser's current date to change the reporting month. Error resolution and prompt editing do not change these values.

## 7. User Management Specification

1. **Customer table:** Display all five users defined in Section 14, in ascending user-ID order, with columns Name, Email, Plan, Status, and Actions. Names are medium-weight, emails are muted plain text, and plan labels are text rather than links. Use a contrasting header background, row separators, comfortable cell padding, and subtle row hover backgrounds in both themes. Do not add sorting, filtering, pagination, or selection controls.
2. **Status badges:** Render Active in emerald, Suspended in amber, and Invited in slate. Always include the written status inside the rounded badge; color alone must not carry meaning. The status column remains distinct from the plan column.
3. **Row actions:** Each row has one trailing `⋮` button with an accessible label identifying the user. Its dropdown contains exactly "View Details" and "Delete", with Delete styled as destructive. View Details closes the dropdown and opens the corresponding user modal. Delete follows the global confirmation and referential-integrity rules; it never silently removes a linked customer.
4. **User details modal:** Show "User details" and the customer's name in the header. The body is a labeled record summary containing ID, name, company, email, plan, status badge, and joined date, followed by assigned agent names and rental contract IDs (or "None"). Display all user record fields from Section 14; do not provide editable account inputs. Use two columns for short fields where space permits and full-width email/relationship rows where needed. Include a top-right close button and a footer "Close" button. Backdrop click and Escape also close it.

## 8. Agent Management Specification

1. **Agent list:** Render the four agents in ascending agent-ID order as full-width stacked panels. Each panel header includes agent name, owner name and company, textual current status inside a badge, a skill-expansion button with skill count and chevron, and a trailing `⋮` button. Use emerald for Active, slate for Inactive, and rose for Failing. At tablet widths the owner and expansion control wrap below the name without overlapping actions.
2. **Collapsed skill state:** Each agent's skills start collapsed on initial load, with the button labeled "Show skills (N)" and a downward chevron. The skill body takes no visible vertical space and is absent from the accessibility tree and tab order. Agent name, owner, status, and actions remain visible. Each agent expands independently; opening one must not collapse another.
3. **Expanded skill state and transition:** Clicking the expansion control reveals named skill chips matching the catalog, changes the label to "Hide skills (N)", rotates the chevron, and updates `aria-expanded`. Use Tailwind's grid-row transition from zero fractional rows to one fractional row, with an overflow-hidden, minimum-height-zero inner wrapper and opacity transition. Normal-motion duration is 250ms with ease-in-out; reverse the same transition on collapse. Do not use abrupt display toggling during animation, arbitrary fixed-height clipping, custom CSS, or inline styles. Hide/inert the collapsed body accessibly and coordinate final hidden state with transition completion. Rapid repeated clicks must settle in the last requested state.
4. **Agent actions:** Every agent's dropdown contains exactly "Configure" and "Delete". Configure opens that agent's modal. Delete uses the global confirmation and relationship guard; because every initial agent has a rental history, initial agent deletions are blocked with a stated reason.
5. **Configuration modal:** Header reads "Configure [agent name]". Show read-only agent ID, owner, status, and associated skill names, followed by a visible "System prompt" label and editable `<textarea>` initialized with the full prompt in Section 14. Use a full-width, bordered, theme-aware textarea with at least eight visible rows and no resize-dependent layout assumptions. Footer actions are "Cancel" and "Save changes", plus a header close button.
6. **Save and discard:** Save requires a prompt containing at least one non-whitespace character and no more than 4,000 characters. Show a character count; invalid input keeps the modal open with an inline error connected to the textarea. Valid Save updates that agent's prompt in memory, closes the modal, and announces "System prompt saved for [agent name]." Reopening shows the saved prompt. Cancel, either close button, backdrop click, or Escape discards unsaved edits without an additional confirmation. Never execute or send the prompt.

## 9. Skills Specification

1. **Explanation panel:** Above the catalog, show the heading "What is a skill?" and this explanatory copy: "A skill is a reusable capability assigned to an AI agent, such as browsing the web, reading documents, or managing a calendar. Rental contracts specify which skills are included and their prices." Use a muted indigo information panel; it has no action.
2. **Catalog grid:** Display all four skills from Section 14 in ascending skill-ID order. Use two columns on desktop and tablet, with consistent panel padding, borders, and heading alignment. Each card contains a skill name, short description, and "Used by N agents" usage label, plus a top-right `⋮` action. Usage counts distinct currently registered agents assigned that skill across all statuses, not contracts or active agents only.
3. **Skill actions:** Each dropdown contains exactly "View Details" and "Delete". Delete uses the global relationship guard, preventing removal of a skill attached to any agent or referenced in any historical/current contract. All initial skills are therefore protected. View Details opens a read-only modal; neither action navigates to a seventh section.
4. **Skill details modal:** Show ID, name, short description, detailed capability description, reference monthly price in USD, usage count, and the names of assigned agents from Section 14. State that reference pricing is illustrative and each contract retains its own price snapshot. Include header and footer close controls and the standard backdrop behavior.

## 10. Agent Rentals Specification

1. **Rental table:** Show all four contracts in ascending contract-ID order with columns Customer, Rented agent, Contracted skills, Start date, End date, Total paid, Status, and Actions. Customer cells include name and company; skill names appear as wrapping chips. Dates use "Sep 01, 2026" formatting and amounts use two-decimal USD formatting. Right-align amounts and keep Actions narrow. No payment or contract-edit controls are offered.
2. **Lifecycle display:** Show Active contracts with an emerald badge and Expired contracts with a slate badge. Classify using the fixed prototype date September 15, 2026 and inclusive contract start/end dates. The three September contracts are Active; the August contract is Expired. Contract state is distinct from agent operational status, so an Active rental may have a Failing agent.
3. **Rental actions:** Every row has a `⋮` dropdown containing only "View Details". Selecting it closes the dropdown and opens the correct rental modal. Do not add a Delete action or imply contracts can be canceled.
4. **Contract detail modal:** Header identifies the contract ID and status. Show customer name, company, email, agent ID/name, start/end dates, payment date, and "USD". Below, display a price-breakdown table with a base-agent line and one individual line for each contracted skill, showing its name and price. Then show gross subtotal, coupon code (or "None"), discount deduction, contract total, and total paid. Emphasize the final total with a separator and bold text. Totals equal base plus skill prices minus discount; total paid equals contract total in this fixture. Use the exact amounts in Section 14 without proration, taxes, or hidden fees.
5. **Modal layout:** Keep customer and dates above the breakdown, never replacing individual skill prices with a single bundled skills amount. The body scrolls if necessary while the header and footer close controls remain reachable. The modal is read-only and follows all global dismissal rules.

## 11. Error Log Specification

1. **Execution log table:** Display all six records from Section 14, newest timestamp first, with columns Timestamp (UTC), Agent, Error type, Severity, Description, Resolution, and Actions. Use readable short descriptions in the table, not full traces. Show timestamps as "2026-09-14 14:32:10 UTC". Long content wraps; do not truncate away the only available description.
2. **Badge differentiation:** Use Critical in rose, Warning in amber, and Info in sky, always with textual labels. Open uses a neutral outlined resolution badge; Resolved uses an emerald badge. Keep severity and resolution separate: resolving an error does not recolor its original severity or remove the record.
3. **Error actions:** Every entry's `⋮` dropdown contains exactly "View Details" and "Mark as Resolved". View Details opens the complete error modal. Mark as Resolved immediately changes an Open record to Resolved in memory, closes the dropdown, updates the badge, and announces "Error [ID] marked as resolved." For already-resolved records, keep the same action visible but disabled and expose its disabled state accessibly.
4. **Error detail modal:** Show error ID, timestamp, agent name/ID, error type, severity badge, short description, and resolution state. Under "Complete error trace", show every trace line from Section 14 in a bordered, monospaced, preformatted area, with wrapping for long lines and internal scrolling for overflow. Render trace content as text, never HTML. Include header and footer close buttons and backdrop dismissal. No stack frames or diagnostic lines may be omitted.
5. **Resolution semantics:** Marking a record resolved acknowledges that individual log entry; it does not repair or change the agent, remove historical errors, or decrement the failing-agent dashboard metric. The initially Open warnings on Active agents represent recoverable errors; the Failing agent has a separate current health state.

## 12. Global Interaction Rules

### Action dropdowns

- Use a literal `⋮` button in every specified row/card action position. The button has a minimum 44px by 44px hit target and an entity-specific accessible label.
- Clicking a closed trigger opens only its associated dropdown. Clicking it again closes it. Opening another dropdown closes the previous one; at most one dropdown may be visible across the application.
- Position the dropdown adjacent to the trigger, right-aligned by default, with a bordered rounded panel, shadow, theme-aware colors, and vertically stacked action buttons.
- Place each action trigger inside a relative positioning container. Its dropdown uses normal Tailwind absolute positioning, for example `absolute right-0 top-full mt-2 z-50`. No body-level portal, trigger-coordinate measurement, or dynamically generated positional classes are required. No inline style attributes are allowed.
- Clicking outside both the open dropdown and its trigger closes it. Clicking inside the dropdown must not be mistaken for an outside click before its action executes.
- Selecting an enabled action closes the dropdown before the action runs. Escape closes it and returns focus to the trigger. Tab navigation can enter action buttons; moving focus outside closes it. Enter and Space activate native buttons.
- Treat these as button disclosure panels, not ARIA menu widgets; standard Tab navigation is sufficient. Set `aria-expanded` and `aria-controls` on the trigger. Do not use menu roles without implementing their additional keyboard model.

### Modals

- Use one reusable dialog-like overlay with a translucent backdrop covering the whole viewport, including the sidebar/top bar. Stack the backdrop above navigation and the dialog above the backdrop. Only one modal may be open at a time.
- Give the dialog a theme-aware panel, clear title, top-right close button, scrollable body, and footer actions. Use a default maximum width of 640px and an expanded maximum width of 768px for rental breakdowns and error traces.
- Clicking the close button or the backdrop closes every modal. A backdrop click means the backdrop itself was the pointer target; clicking inside the panel or dragging a selection from it must not accidentally dismiss it.
- Escape closes the dialog. Footer Close or Cancel also closes it. Closing an unsaved agent configuration discards the draft as defined above; no implicit save occurs.
- Move focus to the title or first meaningful control on open, trap Tab/Shift+Tab within the dialog, make background content inert, and lock background scrolling with utilities. Restore focus to the originating action trigger on close; if the originating row was deleted, focus the section heading.
- Associate the dialog with its heading and description, using appropriate dialog semantics and `aria-modal`. Keep the title and close controls accessible when the body overflows.

### Delete actions and feedback

- Delete first opens the shared confirmation modal with "Delete [entity name]?", a clear relationship explanation, and "Cancel" plus a destructive "Delete" button. No native browser confirmation dialogs.
- Block deletion when a user owns agents or has contracts, an agent is referenced by any contract or error, or a skill is assigned to an agent or included in any contract. Historical references count. Show the IDs/names of blocking records and disable the confirmation Delete button; never silently return or cascade-delete.
- The unlinked invited user U005 is the fixture's successful deletion example. Its confirmation says "This removes the user from this prototype session only." Confirming removes its table row and closes the dialog. Cancel, close, backdrop, and Escape leave records unchanged.
- Recheck relationships before confirming deletion. Keep all linked entities protected so labels, counts, and historical views cannot become dangling references.
- Show success messages in a visible, theme-aware section-level status banner announced through a polite live region. Leave the message until dismissed or replaced by another action; give its dismiss button an accessible label. Show blocking reasons and validation failures visibly where the action occurs, not only in the console.
- If a list becomes empty in a future fixture variation, retain its section heading and show "No [users/agents/skills/contracts/errors] to display." Do not render orphan action controls.

### Collapsible skills

- Initial state is collapsed for all four agents. Use one independent state per agent ID.
- The whole labeled expansion button activates the transition, not just the chevron. Repeat clicks reverse the transition. Expansion state persists when navigating away and back.
- Use the animation and accessibility behavior defined in Section 8. For users requesting reduced motion, suppress the animation while preserving the same end states.

### Dark mode

- Start in light mode on each page load. A top-bar button with a sun/moon icon toggles the root `dark` class; give it the accessible label "Dark mode" and `aria-pressed` reflecting whether dark mode is active.
- Keep theme state independent from the active section. Navigating must not reinitialize or remove it.
- Theme all backgrounds, text, borders, icons, cards, tables, chips, badges, dropdowns, inputs, textareas, modals, chart placeholder, confirmations, feedback, hover states, and focus indicators using `dark:` variants.
- Toggle instantly without page reload, requests, or a theme animation requirement. A dark dropdown/modal must not flash a light surface when opened.

## 13. Responsive Behavior

Desktop and tablet are primary targets. Verify at viewport sizes 1440x900, 1024x768, and 768x1024, including both themes.

| Surface | Desktop: at least 1024px wide | Tablet: 768-1023px wide |
| --- | --- | --- |
| Sidebar | Fixed 240px width; wordmark, icons, and full labels | Fixed 192px width; keep all six labels visible; allow long labels to wrap |
| Header and main | Offset by 240px; never under sidebar | Offset by 192px; never under sidebar |
| Content spacing | 32px outer padding, 24px section gaps | 16px outer padding, 16px section gaps |
| Metric cards | Four equal columns | Two equal columns, two rows |
| Skills catalog | Two equal columns | Two equal columns; descriptions wrap |
| Agent panels | Header content primarily in one row | Header content wraps into clear rows |
| Tables | Fill available width; overflow locally if needed | Horizontally scroll within a labeled table wrapper; do not hide columns |
| Modals | Centered, 640px or 768px maximum width | Fit viewport width minus 32px; same maximum widths |

- Use minimum table widths of 640px for users, 960px for rentals, and 1000px for errors so cells remain readable. Table wrappers, not the entire page, own horizontal overflow. Make scrollable wrappers keyboard-focusable with a visible focus outline and an accessible label.
- Sidebar content can scroll vertically if necessary; it must never push the theme control or page content offscreen.
- Modal maximum height is 90 viewport-height units, with independently scrollable body content, at least 16px viewport clearance, and no offscreen close controls. Long emails, prompts, and trace content must not widen the dialog.
- Avoid body-level horizontal scrolling at the three target sizes. Action dropdowns appear adjacent to their triggers without obscuring their action buttons and remain usable in the desktop and tablet layouts.
- Below 768px, mobile polish is out of scope, but use a persistent compact icon-only sidebar with accessible labels and one-column card grids as a basic fallback. Do not introduce a seventh destination or a separate mobile-only workflow.

## 14. Sample Data Consistency Rules

### Fixture conventions

- Use the following records as the single authoritative fixture. IDs are stable; agent ownership, skills, contracts, and errors reference those IDs rather than independently duplicating names.
- All customer/agent/skill names shown in other sections resolve to these records. The UI must not display unresolved IDs in place of required names.
- Reference date: September 15, 2026. Reporting month: September 2026. Week placeholder: September 7-13, 2026. Timestamps use UTC; calendar dates are date-only values and must not shift with browser timezone.
- All money is USD. Store fixture monetary values in integer cents in the future implementation; displayed figures below are dollar amounts. Contract amounts are fixed prices for the entire stated term, not per-day rates.
- Revenue means paid receipts whose payment date is in September, after discounts. Discount loss means the reductions on those same receipts, not all historical discounts.
- The records are synthetic. Example-domain emails and diagnostic traces contain no credentials, real customer data, or external endpoints.

### Users: complete records

| ID | Name | Company | Email | Plan | Status | Joined date |
| --- | --- | --- | --- | --- | --- | --- |
| U001 | Maya Chen | Northstar Retail | maya.chen@northstar.example | Growth | Active | 2026-06-10 |
| U002 | Luis Ortega | Harbor Finance | luis.ortega@harbor.example | Enterprise | Active | 2026-05-18 |
| U003 | Priya Shah | Cedar Legal | priya.shah@cedar.example | Starter | Suspended | 2026-07-01 |
| U004 | Noah Williams | Atlas Logistics | noah.williams@atlas.example | Growth | Active | 2026-06-22 |
| U005 | Emma Dubois | Lumen Studio | emma.dubois@lumen.example | Starter | Invited | 2026-09-12 |

Plans are descriptive account tiers, not additional billable line items. U005 has no agents or contracts and may be deleted locally. U003's expired rental and inactive agent remain visible despite the suspended account.

### Skills: complete records

| ID | Name | Short description | Detailed capability description | Reference monthly price | Assigned agent count |
| --- | --- | --- | --- | --- | --- |
| S001 | Web Browsing | Collect information from approved websites. | Research approved public sources and summarize findings with source references. | $60.00 | 2 |
| S002 | Document Reading | Extract and summarize document content. | Read supplied business documents, identify key facts, and summarize their contents. | $40.00 | 3 |
| S003 | Calendar Management | Organize events and scheduling requests. | Prepare scheduling suggestions and manage approved calendar events without double booking. | $50.00 | 2 |
| S004 | Business Reporting | Prepare structured business summaries. | Turn supplied operational data into structured reports highlighting trends and exceptions. | $100.00 | 1 |

### Agents: identity, ownership, status, and assignments

| ID | Agent name | Owner ID | Status | Skill IDs |
| --- | --- | --- | --- | --- |
| A001 | Retail Concierge | U001 | active | S001, S002, S003 |
| A002 | Finance Analyst | U002 | active | S002, S004 |
| A003 | Legal Document Assistant | U003 | inactive | S002 |
| A004 | Logistics Coordinator | U004 | failing | S001, S003 |

Complete initial system prompts, displayed literally in each configuration textarea:

- **A001:** "You are Retail Concierge for Northstar Retail. Research approved public product sources, summarize supplied documents, and propose calendar events. Ask for administrator approval before changes affecting customers. Report missing information clearly."
- **A002:** "You are Finance Analyst for Harbor Finance. Read supplied financial documents and prepare structured business reports. Distinguish documented facts from assumptions. Do not execute payments or provide unsupported figures."
- **A003:** "You are Legal Document Assistant for Cedar Legal. Summarize supplied documents and identify clauses needing human review. Do not present summaries as legal advice. Do not access materials outside the supplied collection."
- **A004:** "You are Logistics Coordinator for Atlas Logistics. Review approved public logistics information and prepare scheduling updates. Require approval before calendar changes. Surface timeouts and scheduling conflicts without hiding failures."

### Rental contracts: complete identity and payment records

| ID | Customer ID | Agent ID | Start date | End date | Payment date | Status | Base agent price | Coupon | Discount | Gross subtotal | Contract total / total paid |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| R001 | U001 | A001 | 2026-09-01 | 2026-09-30 | 2026-09-01 | Active | $300.00 | WELCOME45 | $45.00 | $450.00 | $405.00 |
| R002 | U002 | A002 | 2026-09-01 | 2026-09-30 | 2026-09-01 | Active | $400.00 | None | $0.00 | $540.00 | $540.00 |
| R003 | U003 | A003 | 2026-08-01 | 2026-08-31 | 2026-08-01 | Expired | $250.00 | LEGAL20 | $20.00 | $290.00 | $270.00 |
| R004 | U004 | A004 | 2026-09-01 | 2026-09-30 | 2026-09-02 | Active | $350.00 | ATLAS60 | $60.00 | $460.00 | $400.00 |

Each contract retains these individual contracted-skill price snapshots:

| Contract | Skill ID | Skill name | Price for contract term |
| --- | --- | --- | --- |
| R001 | S001 | Web Browsing | $60.00 |
| R001 | S002 | Document Reading | $40.00 |
| R001 | S003 | Calendar Management | $50.00 |
| R002 | S002 | Document Reading | $40.00 |
| R002 | S004 | Business Reporting | $100.00 |
| R003 | S002 | Document Reading | $40.00 |
| R004 | S001 | Web Browsing | $60.00 |
| R004 | S003 | Calendar Management | $50.00 |

Reconciliation checks:

- September net revenue: $405.00 + $540.00 + $400.00 = **$1,345.00**.
- September discount/coupon loss: $45.00 + $0.00 + $60.00 = **$105.00**.
- September gross subtotal: $450.00 + $540.00 + $460.00 = $1,450.00; gross minus loss equals net revenue.
- August R003's $270.00 payment and $20.00 discount are excluded from September cards.
- Active agents: A001 and A002, giving **2**. Failing agents: A004, giving **1**. Inactive agents: A003.
- S001 is assigned to A001/A004; S002 to A001/A002/A003; S003 to A001/A004; S004 to A002.
- Each rental's customer matches its agent owner, and each contracted skill exists in the catalog and is assigned to that agent.

### Execution errors: complete summary records

| ID | Timestamp (UTC) | Agent ID | Error type | Severity | Short description | Resolution |
| --- | --- | --- | --- | --- | --- | --- |
| E001 | 2026-09-14 14:32:10 | A004 | UpstreamTimeout | Critical | Route research exceeded its execution deadline. | Open |
| E002 | 2026-09-14 14:25:00 | A001 | RateLimitExceeded | Warning | Product research was delayed by a source rate limit. | Open |
| E003 | 2026-09-13 09:10:05 | A002 | DocumentParseError | Warning | A supplied report contained an unreadable table. | Open |
| E004 | 2026-09-12 16:45:20 | A004 | CalendarConflict | Warning | A proposed dispatch slot overlapped an existing event. | Open |
| E005 | 2026-09-10 11:02:00 | A001 | RetryRecovered | Info | A document read succeeded after one retry. | Resolved |
| E006 | 2026-08-28 08:20:15 | A003 | DocumentParseError | Warning | An archived agreement could not be decoded. | Resolved |

The following are the complete synthetic trace payloads. In the future modal, render each numbered item as a separate plain-text line without list numbering. These are diagnostic fixture text, not executable implementation code.

**E001**
1. UpstreamTimeout: route research exceeded 30000ms.
2. Execution exec-4001; agent A004; skill S001.
3. at WebBrowsing.collectSources (skills/web-browsing:42)
4. at LogisticsCoordinator.run (agents/logistics-coordinator:18)
5. Outcome: execution stopped after 3 attempts; operator review required.

**E002**
1. RateLimitExceeded: approved product source returned a rate-limit response.
2. Execution exec-1002; agent A001; skill S001.
3. at WebBrowsing.collectSources (skills/web-browsing:42)
4. at RetailConcierge.run (agents/retail-concierge:21)
5. Outcome: retry queued for a later execution; agent remains active.

**E003**
1. DocumentParseError: unreadable table in quarterly-summary.pdf, page 4.
2. Execution exec-2003; agent A002; skill S002.
3. at DocumentReading.parseTable (skills/document-reading:63)
4. at FinanceAnalyst.run (agents/finance-analyst:27)
5. Outcome: document skipped; remaining reports processed.

**E004**
1. CalendarConflict: proposed dispatch slot overlaps event dispatch-217.
2. Execution exec-4004; agent A004; skill S003.
3. at CalendarManagement.validateSlot (skills/calendar-management:35)
4. at LogisticsCoordinator.run (agents/logistics-coordinator:24)
5. Outcome: proposed change rejected; existing calendar unchanged.

**E005**
1. RetryRecovered: document read succeeded on attempt 2.
2. Execution exec-1005; agent A001; skill S002.
3. at DocumentReading.read (skills/document-reading:28)
4. at RetailConcierge.run (agents/retail-concierge:29)
5. Outcome: execution completed; informational record acknowledged.

**E006**
1. DocumentParseError: unsupported encoding in archived-agreement.pdf.
2. Execution exec-3006; agent A003; skill S002.
3. at DocumentReading.decode (skills/document-reading:19)
4. at LegalDocumentAssistant.run (agents/legal-document-assistant:16)
5. Outcome: document returned for manual review; historical record acknowledged.

E006 occurred during R003's August rental, before the agent became inactive. Other traces fall within their respective September rental terms. Trace paths are fictional diagnostic labels, not repository files to create.

## 15. Reusable Component Inventory

This is section 15 of the specification.

| Component | Purpose and content | Visual behavior | Interaction behavior |
| --- | --- | --- | --- |
| Sidebar | Persistent AgentHub branding and exactly six section buttons | Fixed-width rail; icon and label; indigo active indicator; theme-aware hover/focus | Select one section, update active state, preserve session state |
| Top bar | Current section title, prototype notice, theme control | Fixed 64px header offset by sidebar; border and themed surface | Hosts the always-available theme toggle |
| Metric card | Icon, label, value, and optional context | Equal-height bordered panel; type-specific accent; responsive grid | Informational only; not focusable as an action |
| Status badge | Operational, account, contract, severity, or resolution label | Compact rounded treatment with mapped color and visible text in both themes | Static label; never communicates state solely through color |
| Action dropdown | Entity-specific trigger and defined action buttons | Absolutely positioned panel adjacent to its trigger within a relative container; destructive and disabled styles | One open at a time; toggle, outside-click, Escape, and focus-out dismissal |
| Modal | Title, optional description, body, close control, footer actions | Backdrop plus centered themed panel; bounded scrollable body | Focus trap, inert background, close/backdrop/Escape dismissal, focus restoration |
| Collapsible skills list | Agent's skill count, chevron, and catalog-name chips | Initially zero-height; 250ms grid/opacity transition; reduced-motion alternative | Independent expand/collapse; accurate accessible expanded state |
| Dark mode toggle | Sun/moon icon and accessible "Dark mode" label | 44px minimum target; obvious selected/focus state | Toggles root theme class; persists across section changes |
| Data table | Caption, column headers, record rows, action cells | Full width with row separators and local horizontal scrolling | Native table reading order; keyboard-accessible overflow and actions |
| Section header | Section title and explanatory subtitle | Consistent spacing, heading scale, muted supporting text | Receives focus after navigation; no speculative action buttons |
| Feedback banner | Action confirmation or error explanation and dismiss control | Theme-aware inline status surface; text and icon instead of color alone | Announces result; explicitly dismissible |
| Skill chip | Catalog skill name inside agents and rentals | Wrapping compact neutral badge; consistent padding | Read-only, not a navigation destination |

## 16. Accessibility and Semantic HTML

- Use `nav` for sidebar navigation, `header` for the top bar, one `main`, and a labeled `section` for each destination. Use a coherent heading hierarchy with the visible section heading as the primary content heading.
- Use real `table`, `caption`, `thead`, `tbody`, and column-header cells with `scope="col"` for user, rental, error, and contract-breakdown tables. Captions may be visually hidden when a nearby visible title is sufficient.
- Use native `button` elements for navigation, dropdowns, expansion, dismissal, save, delete, and theme controls. Set button types explicitly so actions cannot accidentally submit a form.
- Provide dialog semantics using a native dialog or an equivalent `role="dialog"` structure with `aria-modal`, associated title, focus containment, and inert background. Backdrop behavior must match Section 12 regardless of the chosen semantic structure.
- Label the configuration textarea explicitly and associate validation text with it. Use `aria-invalid` while invalid. Use `aria-expanded`/`aria-controls` on disclosure triggers and `aria-current` on the active navigation destination.
- Keep every interactive target at least 44px high and wide where icon-only. Support keyboard operation with Tab, Shift+Tab, Enter, Space, and Escape as specified. Always provide visible focus rings in both themes.
- Decorative SVG icons are hidden from assistive technology. Icon-only buttons have descriptive accessible names identifying both the action and entity.
- Aim for WCAG AA contrast: at least 4.5:1 for normal text, 3:1 for large text, and 3:1 for meaningful interface boundaries and focus indicators. Check badge text in both themes rather than assuming accent colors are sufficient.
- Honor reduced-motion preferences through Tailwind motion-reduction utilities. This is the only exception to the required visible expansion animation.
- Render prompts, record fields, and traces as text. Do not interpolate record content into executable markup. Preformatted traces may use semantic `pre` and `code` elements with wrapping utilities.
- Announce completed local actions through a polite live region and validation errors through an associated error message. Hidden sections, collapsed content, and closed overlays must not be reachable by keyboard.

## 17. Acceptance Criteria

Specification-phase checks apply now. Prototype checks apply after implementation is separately authorized; documenting them does not mean the UI has been built.

1. SPECS.md defines all six required sections by name and no additional navigation destinations.
2. Each of the six application section specifications contains at least three numbered, concrete requirements describing component content, visual behavior, and applicable interactions.
3. This phase creates or modifies only SPECS.md, starts no HTML/CSS/JavaScript implementation, installs no dependencies, and creates no commit.
4. On initial prototype load, Dashboard is visible; the persistent sidebar offers all six destinations in the required order, and exactly one has an active indicator.
5. Navigating through all six destinations changes the visible section and top-bar title without reloading; hidden sections are absent from keyboard navigation.
6. Dashboard displays exactly four metric cards, each with an icon, label, and value: $1,345.00 revenue, $105.00 loss, 2 active agents, and 1 failing agent.
7. Metric cards use four columns at 1024px and 1440px widths and two columns at 768px; their accents and labels remain distinguishable in both themes.
8. A full-width weekly activity placeholder appears below the cards with the specified week, Mon-Sun labels, and explicit placeholder text; it makes no data requests and has no interactive chart behavior.
9. User Management initially displays all five specified users with name, email, plan, and textual status badge.
10. Agent Management initially displays all four specified agents with owner/customer, current status badge, skill count, and action trigger.
11. Skills initially displays all four catalog records with descriptions and usage counts 2, 3, 2, and 1 respectively, plus the explanatory skill panel.
12. Agent Rentals displays all four specified contracts, including three Active and one Expired, with customer, agent, skills, dates, and total paid.
13. Error Log displays all six specified records newest first, with timestamp, agent, type, severity badge, description, and resolution.
14. User and skill dropdowns contain View Details/Delete; agent dropdowns contain Configure/Delete; rental dropdowns contain View Details only; error dropdowns contain View Details/Mark as Resolved.
15. Clicking any `⋮` trigger opens only that entity's dropdown; clicking it again closes it; opening another closes the first.
16. Clicking outside the open dropdown and its trigger closes it. Escape and focus leaving the panel also close it, and enabled action selection executes exactly once.
17. Action dropdowns appear adjacent to their triggers without obscuring their action buttons and remain usable in the desktop and tablet layouts.
18. Each user's View Details opens the matching complete record with all seven fixture fields and assigned-agent/contract references, including "None" for U005.
19. Each agent's Configure opens its full initial system prompt in an editable, labeled textarea with Cancel and Save changes controls.
20. Saving a valid edited prompt updates only that agent in memory and reopening shows it; empty/whitespace-only or over-4,000-character prompts produce a visible validation error without closing.
21. Dismissing a configuration modal without saving discards the draft and preserves the last saved prompt.
22. Each skill's View Details shows its complete catalog record, correct usage count, reference price, and assigned agent names.
23. Each rental's View Details shows the correct customer, agent, dates, each individual skill and price, base price, coupon, discount, subtotal, contract total, and total paid.
24. For every rental, base plus individual skill prices minus discount equals the displayed contract total and total paid.
25. Each error's View Details displays its complete matching metadata and all five trace lines in a text-only preformatted area.
26. Every modal has a backdrop and functioning close button; footer Close/Cancel and Escape also dismiss it.
27. Clicking each modal's backdrop closes it; clicking inside its content does not. For confirmation dialogs, backdrop dismissal performs no deletion.
28. Opening a modal moves focus inside, traps Tab/Shift+Tab, prevents background interaction and scrolling, and closing restores focus appropriately.
29. All four agent skill lists are collapsed on initial load and their hidden contents cannot receive focus.
30. Each expansion button reveals the correct catalog skill names with a visible 250ms transition; clicking again smoothly collapses them and updates label, chevron, and accessible state.
31. Agent expansions are independent, persist across section navigation, and settle correctly after rapid toggling; reduced-motion preference suppresses animation without breaking state.
32. The top-bar theme toggle changes the complete interface using Tailwind `dark:` utilities, including subsequently opened dropdowns, modals, textarea, and confirmation surfaces.
33. Selecting dark mode and visiting every section leaves dark mode active; toggling back restores light mode without a reload.
34. All displayed customers, agents, skill names, counts, contract references, and error relationships match the authoritative fixture and its reconciliation rules.
35. Revenue and loss include only September payments; R003's August payment and discount are excluded. Active and failing counts use distinct exact statuses.
36. Mark as Resolved changes only the selected Open error's resolution and announces success; the record remains visible, agent statuses and metrics do not change, and the action becomes disabled.
37. Delete opens an entity-specific confirmation. Linked users, agents, and skills show blocking references and cannot be deleted; confirming U005 deletion removes only U005 and announces success.
38. Canceling or dismissing deletion leaves all records unchanged. Reload restores deleted U005, initial prompts/resolutions, collapsed skills, light mode, and Dashboard.
39. Tailwind is loaded only through the specified CDN; there are no custom CSS files, author-written CSS rules/style blocks, or inline style attributes.
40. All interaction logic uses vanilla JavaScript; there are no frontend frameworks, jQuery, third-party runtime libraries other than Tailwind, installed packages, or build tools.
41. The network log contains no backend/API, fetch/XHR, WebSocket, analytics, or external form requests; the only required external dependency request is Tailwind CDN loading.
42. The document uses appropriate nav, header, main, section, table, thead, tbody, button, and dialog-like semantics, with labels, captions, header scopes, and focus states as specified.
43. At 1440x900, 1024x768, and 768x1024, sidebar navigation remains visible, table columns remain accessible through local scrolling, content does not overlap the shell, and the page has no body-level horizontal overflow.
44. At every target size, modal content fits within the viewport with reachable close controls, scrollable long bodies, and no clipped prompts, traces, or contract totals.
45. Keyboard-only users can navigate all sections, operate dropdowns, expand skills, edit/save prompts, dismiss modals, and toggle theme; icon-only controls have descriptive accessible names.
46. Text, status badges, hover states, and focus indicators meet the stated contrast targets in both light and dark modes; severity/status meaning remains understandable without color.
