# AgentHub Admin

A desktop-first internal administration prototype for AgentHub, a platform for
renting preconfigured AI agents with reusable skills.

## Preview

Open `index.html` in a browser, or serve the repository with Python:

```sh
python3 -m http.server 3000
```

Then visit `http://localhost:3000`. Internet access is required for the
Tailwind v3 Play CDN. There are no package dependencies or build steps.

## Included

- Dashboard with September 2026 financial and operational metrics and an
  explicitly labeled weekly activity placeholder.
- User Management, Agent Management, Skills, Agent Rentals, and Error Log.
- Record details, itemized contracts, complete execution traces, editable
  system prompts, and independently expandable agent skills.
- Guarded deletion, error acknowledgment, accessible dialogs and dropdowns,
  and light/dark themes.
- Persistent navigation at 1440px, 1024px, and 768px; tables scroll locally.

The implementation is a single semantic HTML document with Tailwind CDN
utilities, embedded SVG icons, and vanilla JavaScript. It follows
[SPECS.md](./SPECS.md), including its authoritative synthetic fixture.

## Prototype behavior

All changes are held in memory and reset on reload, including theme, prompts,
deletions, and error resolutions. No backend, authentication, real billing,
agent execution, or persistent storage is connected.

Try these flows:

1. Open **Agent Management**, expand an agent's skills, and select
   **Configure** from its three-dot menu. Edit and save its system prompt.
2. Open **Agent Rentals** and select **View Details** to see a contract's
   individual skill prices, discounts, and total.
3. Open **Error Log** to inspect a complete trace or mark an open record
   resolved. This does not change the agent's health.
4. Open **User Management** and delete Emma Dubois, the unlinked invited
   user. Linked records are protected with visible relationship explanations.
5. Toggle dark mode, navigate between sections, and reload to restore the
   original light-theme fixture.
