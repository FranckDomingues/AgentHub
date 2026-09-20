---
name: Autonomous Operations Console
colors:
  surface: '#faf8ff'
  surface-dim: '#d2d9f4'
  surface-bright: '#faf8ff'
  surface-container-lowest: '#ffffff'
  surface-container-low: '#f2f3ff'
  surface-container: '#eaedff'
  surface-container-high: '#e2e7ff'
  surface-container-highest: '#dae2fd'
  on-surface: '#131b2e'
  on-surface-variant: '#464555'
  inverse-surface: '#283044'
  inverse-on-surface: '#eef0ff'
  outline: '#777587'
  outline-variant: '#c7c4d8'
  surface-tint: '#4d44e3'
  primary: '#3525cd'
  on-primary: '#ffffff'
  primary-container: '#4f46e5'
  on-primary-container: '#dad7ff'
  inverse-primary: '#c3c0ff'
  secondary: '#006c49'
  on-secondary: '#ffffff'
  secondary-container: '#6cf8bb'
  on-secondary-container: '#00714d'
  tertiary: '#684000'
  on-tertiary: '#ffffff'
  tertiary-container: '#885500'
  on-tertiary-container: '#ffd4a4'
  error: '#ba1a1a'
  on-error: '#ffffff'
  error-container: '#ffdad6'
  on-error-container: '#93000a'
  primary-fixed: '#e2dfff'
  primary-fixed-dim: '#c3c0ff'
  on-primary-fixed: '#0f0069'
  on-primary-fixed-variant: '#3323cc'
  secondary-fixed: '#6ffbbe'
  secondary-fixed-dim: '#4edea3'
  on-secondary-fixed: '#002113'
  on-secondary-fixed-variant: '#005236'
  tertiary-fixed: '#ffddb8'
  tertiary-fixed-dim: '#ffb95f'
  on-tertiary-fixed: '#2a1700'
  on-tertiary-fixed-variant: '#653e00'
  background: '#faf8ff'
  on-background: '#131b2e'
  surface-variant: '#dae2fd'
typography:
  headline-lg:
    fontFamily: Inter
    fontSize: 32px
    fontWeight: '600'
    lineHeight: 40px
    letterSpacing: -0.02em
  headline-lg-mobile:
    fontFamily: Inter
    fontSize: 24px
    fontWeight: '600'
    lineHeight: 32px
    letterSpacing: -0.015em
  headline-md:
    fontFamily: Inter
    fontSize: 24px
    fontWeight: '600'
    lineHeight: 32px
    letterSpacing: -0.015em
  headline-sm:
    fontFamily: Inter
    fontSize: 18px
    fontWeight: '600'
    lineHeight: 26px
    letterSpacing: -0.01em
  title-md:
    fontFamily: Inter
    fontSize: 16px
    fontWeight: '600'
    lineHeight: 24px
    letterSpacing: -0.005em
  title-sm:
    fontFamily: Inter
    fontSize: 14px
    fontWeight: '600'
    lineHeight: 20px
  body-lg:
    fontFamily: Inter
    fontSize: 15px
    fontWeight: '400'
    lineHeight: 24px
  body-md:
    fontFamily: Inter
    fontSize: 14px
    fontWeight: '400'
    lineHeight: 20px
  body-sm:
    fontFamily: Inter
    fontSize: 13px
    fontWeight: '400'
    lineHeight: 18px
  label-md:
    fontFamily: Inter
    fontSize: 12px
    fontWeight: '500'
    lineHeight: 16px
    letterSpacing: 0.01em
  label-sm:
    fontFamily: Inter
    fontSize: 11px
    fontWeight: '500'
    lineHeight: 14px
    letterSpacing: 0.02em
  code-md:
    fontFamily: JetBrains Mono
    fontSize: 13px
    fontWeight: '400'
    lineHeight: 20px
  code-sm:
    fontFamily: JetBrains Mono
    fontSize: 11px
    fontWeight: '400'
    lineHeight: 16px
rounded:
  sm: 0.125rem
  DEFAULT: 0.25rem
  md: 0.375rem
  lg: 0.5rem
  xl: 0.75rem
  full: 9999px
spacing:
  gutter: 1.5rem
  gutter-mobile: 0.75rem
  margin: 2rem
  margin-mobile: 1rem
  space-xs: 0.25rem
  space-sm: 0.5rem
  space-md: 1rem
  space-lg: 1.5rem
  space-xl: 2rem
---

## Brand & Style
The design system establishes an ultra-refined, utilitarian enterprise control plane for deploying, monitoring, and orchestrating autonomous AI agent fleets. The visual direction merges enterprise SaaS precision with technical developer tooling ergonomics: structured, data-dense, and highly legible without visual clutter.

The aesthetic follows a modern, restrained corporate ethos. It communicates technical reliability, low latency, and audit-level transparency. Interfaces should feel composed, engineered, and quiet, allowing complex runtime metrics, cost telemetry, and execution traces to surface effortlessly.

## Colors
The system employs a calibrated palette grounded in neutral slate foundations, offset by purposeful semantic accents:

- **Primary (`#4f46e5` / Indigo 600):** Governs interactive elements, active navigation indices, focused form rings, and high-priority platform triggers.
- **Surfaces & Canvas:** Foundation canvas uses Slate 50 (`#f8fafc`). Structural card panels use pure white (`#ffffff`), partitioned by subtle border strokes in Slate 200 (`#e2e8f0`). Secondary container fills and header bands utilize Slate 100 (`#f1f5f9`).
- **Text Hierarchy:** High-emphasis primary headings and key values map to Slate 900 (`#0f172a`), secondary body labels to Slate 600 (`#475569`), and muted metadata or disabled states to Slate 400 (`#94a3b8`).
- **Functional Semantics:**
  - **Success / Active (`#10b981` / Emerald 500):** Agent runtime operational status, successful invocations, and credit allocations.
  - **Warning / Quota (`#f59e0b` / Amber 500):** Latency spikes, rate-limit thresholds, and awaiting authorization states.
  - **Destructive / Terminated (`#f43f5e` / Rose 500):** Agent runtime crashes, fatal exceptions, instance teardown triggers, and depleted balance alerts.

## Typography
Typography is split into two complementary roles:

- **Primary Interface (Inter):** Applied across global structural elements, data tables, navigation, and dialogs. Tight letter tracking is applied across headings to retain crisp vertical rhythm and eliminate visual drift in dense configurations.
- **Telemetry & Execution Trace (JetBrains Mono):** Applied to agent instance IDs, token usage counts, JSON parameters, webhook URLs, and terminal-style runtime step inspection. Maintains strict tabular numerals (`font-feature-settings: 'tnum'`) across both fonts to align financial figures and metrics cleanly in tables.

## Layout & Spacing
The layout follows an asynchronous fixed-fluid administration shell:
- **Navigation Shell:** Fixed-width 260px collapsible sidebar anchored to the viewport edge, paired with a persistent 64px header band.
- **Main Canvas:** Fluid grid adapting dynamically up to a 1600px ceiling with responsive 12-column subdivisions for telemetry cards and table containers.
- **Breakpoints:**
  - `sm` (640px): Full-screen stacked layouts, single-column forms, drawer-based filters.
  - `md` (768px): 2-column metrics grids, modal popovers.
  - `lg` (1024px): Sidebar reveals, persistent secondary panels, 3-column overview dashboards.
  - `xl` (1280px+): Full multi-column data views and synchronized split-pane trace logs.

## Elevation & Depth
Depth is established primarily through clean boundaries rather than heavy drop shadows:

- **Surface Partitioning:** Low-contrast 1px outlines (`border border-slate-200`) ground all cards, panels, and data grids against the Slate 50 backdrop.
- **Shadow Scale:**
  - **Flat Tier (Cards, Inset Panels):** Pure outline or micro-elevation using `box-shadow: 0 1px 2px 0 rgba(15, 23, 42, 0.05)` (`shadow-sm`).
  - **Floating Tier (Dropdowns, Tooltips, Action Popovers):** Raised elevation with `box-shadow: 0 4px 6px -1px rgba(15, 23, 42, 0.08), 0 2px 4px -2px rgba(15, 23, 42, 0.04)` combined with an explicit Slate 200 border.
  - **Overlay Tier (Modals, Slide-over Run Drawers):** High-level overlay with `box-shadow: 0 20px 25px -5px rgba(15, 23, 42, 0.12), 0 8px 10px -6px rgba(15, 23, 42, 0.06)` combined with a Slate 900/40 backdrop blur filter.

## Shapes
A disciplined, moderate corner radius hierarchy keeps interface elements orderly and architectural:

- **Inner Inputs, Buttons, & Table Badges:** Styled with `rounded-md` (0.375rem / 6px) to maintain a compact, precise operational aesthetic.
- **Cards, Panels, & Code Blocks:** Styled with `rounded-lg` (0.5rem / 8px) or `rounded-xl` (0.75rem / 12px) for primary layout surfaces.
- **Status Indicators & Micro Badges:** Badges use soft capsules (`rounded-full`) for high-contrast scanning of active/idle/error agent states.

## Components

### Buttons
- **Primary:** Background `bg-indigo-600` text white, hover `bg-indigo-700`, focus ring `ring-2 ring-indigo-500/20 ring-offset-1`.
- **Secondary / Neutral:** Background `bg-white` border `border-slate-200` text `text-slate-700`, hover `bg-slate-50 hover:text-slate-900 hover:border-slate-300`.
- **Destructive:** Background `bg-rose-500` text white, hover `bg-rose-600`, or secondary destructive `text-rose-600 bg-rose-50 hover:bg-rose-100`.

### Data Tables
- **Table Headers:** `bg-slate-50/75` text `text-slate-500` font medium, uppercase `text-[11px] tracking-wider` with bottom border `border-slate-200`.
- **Table Rows:** Background `bg-white`, alternating subtle hover state `hover:bg-slate-50/60`, horizontal cell border `border-b border-slate-100`.
- **Numeric/Code Cells:** Right-aligned or formatted using `font-mono text-xs text-slate-600`.

### Status Badges & Pills
- **Active / Provisioned:** `bg-emerald-50 text-emerald-700 border border-emerald-200/60` with optional pulse indicator dot `bg-emerald-500`.
- **Deploying / Throttled:** `bg-amber-50 text-amber-700 border border-amber-200/60`.
- **Terminated / Faulted:** `bg-rose-50 text-rose-700 border border-rose-200/60`.
- **Draft / Inactive:** `bg-slate-100 text-slate-600 border border-slate-200`.

### Input Fields & Controls
- **Inputs:** `bg-white border-slate-200 rounded-md text-sm text-slate-900 placeholder:text-slate-400 focus:border-indigo-600 focus:ring-1 focus:ring-indigo-600`.
- **Checkboxes & Radios:** `border-slate-300 text-indigo-600 rounded focus:ring-indigo-500 focus:ring-offset-0`.

### Cards & Container Panels
- White background (`bg-white`), wrapped in `border border-slate-200 shadow-sm rounded-xl`. Headers within cards feature distinct bottom borders (`border-b border-slate-100`) with padding `px-6 py-4`.

### Trace Log Viewer
- Dedicated terminal panel component using `bg-slate-900 text-slate-200 font-mono text-xs p-4 rounded-lg overflow-x-auto` with colored timestamp gutters (`text-slate-500`) and highlighted token parameters (`text-indigo-400` / `text-emerald-400`).