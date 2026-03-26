# Spokesweb Accounting App — Project Context

## Project Overview
A single-file HTML prototype of a Malaysian cloud accounting web app, styled to closely match Bukku.my's UI. Built for BETA Social Sdn Bhd. The app demonstrates a full accounting dashboard including quotations, invoices, expenses, tax management, and financial reports — all in one self-contained HTML file with no build tools or dependencies beyond Google Fonts.

## Tech Stack
- **Single file:** `spokesweb-accounting.html` — all HTML, CSS, JS in one file
- **Fonts:** Inter (UI), DM Mono (numbers) via Google Fonts
- **Persistence:** `localStorage` for tax rates
- **No frameworks, no build tools, no external JS**

## Key Decisions Made
- **Bukku.my color palette** — Eric explicitly chose to match Bukku.my's style. Colors: navy sidebar `#1C2B3A`, blue metric cards (`#4D96DA` → `#1D3F8C`), cyan accent `#1DBED8` for section headings and active states, lime green `#9DC820` for charts. Do NOT revert to teal/orange Spokesweb colors.
- **KPI cards are fully colored blue** — not white with a colored stripe. This was a deliberate redesign from the original teal design.
- **Single HTML file** — deliberately no framework. Don't suggest splitting into components or adding a bundler.
- **Inter font replaces DM Sans/DM Serif** — all headings use Inter semibold, not a serif font.
- **Tax rates stored in localStorage** — intentional lightweight persistence. Pre-seeded with SV8, SV6, GST0, NOTAX.
- **navSub override pattern is BANNED** — caused infinite recursion bug. All page-specific hooks must be inlined into the single `navSub()` function.

## Current Status
### Done
- Dashboard page with KPI cards (Bukku blue style), revenue chart, SST summary, cash flow, top expenses, receivables aging, recent transactions
- Sidebar: Bukku-style expandable nav (Sales, Purchases, Bank, Stock, Reports, Accounting, Control Panel)
- Quotations list page (BSQ-0274 to BSQ-0264, exact Bukku layout: filter bar, pagination, action icons, Ready badges)
- Quotation detail view (BSQ-0274): all 8 tabs, Billing & Shipping, General Info, Items with totals, Payment Terms, Additional Info, Attachments, Controls, History, sticky bottom bar
- Tax Rates settings page (Control Panel → Tax Rates): full CRUD, modal with validation, localStorage persistence
- Scrolling fixed: `body { height: 100vh }` and sidebar `overflow-y: auto`

### In Progress / Next
- Other Sales sub-pages (Sale Orders, Delivery Orders, Credit Notes, Payments, Refunds) — stubs only
- Invoices page exists but has old styling (pre-Bukku restyle)

## Important Files
- `spokesweb-accounting.html` — the entire app, ~2400 lines

## Conventions
- CSS variables named with old `--teal-*` names but remapped to blue values — do not rename them, it will break too many rules
- `--orange` variable is now cyan `#1DBED8` (accent color) — not actually orange
- Page IDs follow pattern `pg-{name}` (e.g. `pg-quotations`, `pg-quotation-view`, `pg-tax`)
- Nav uses `nav()` for top-level items, `navSub()` for sub-items
- Modals: `.modal-bg` + `.modal`, opened with `openModal('id')`, closed with `closeModal('id')`

## Do Not Touch
- The CSS variable names (`--teal`, `--orange`) — they're remapped intentionally, renaming breaks the cascade
- The `navSub()` function structure — do not add a second declaration
- The `localStorage` tax persistence — don't replace with in-memory only
