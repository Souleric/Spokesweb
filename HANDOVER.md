# Handover — Spokesweb Accounting App

## What Is This
A self-contained HTML prototype of a Malaysian cloud accounting web app for BETA Social Sdn Bhd, built to visually match Bukku.my's interface. It covers the core accounting workflows — quotations, invoices, expenses, tax management, and financial reports — in a single `.html` file with no backend, no build tools, and no framework. It is a working interactive demo, not a static mockup.

## Where Things Stand
As of 26 March 2026, the app has a fully styled dashboard, a complete Quotations list and detail view (BSQ-0274), and a functional Tax Rates settings page with CRUD and localStorage persistence. The UI has been restyled from an original teal/orange Spokesweb theme to match Bukku.my's navy/blue/cyan palette. The core navigation structure mirrors Bukku's sidebar with expandable groups.

## The Decisions That Matter

**1. Match Bukku.my exactly, not approximately**
Eric chose to replicate Bukku.my's UI closely — not just be "inspired by" it. Colors, spacing, component patterns (filter bars, pagination, breadcrumb headers, sticky bottom bars) all follow Bukku's actual product screenshots. When in doubt, look at a Bukku.my screenshot before deciding how to style something.

**2. Single HTML file is intentional**
Everything — CSS, JS, HTML — lives in `spokesweb-accounting.html`. This is not laziness; it makes the prototype maximally portable (open in any browser, share as one file, no setup). Do not split it into components or suggest a framework unless Eric asks.

**3. CSS variable names are misleading — read carefully**
The original Spokesweb theme used `--teal` and `--orange`. These variable names were kept when the palette was swapped to Bukku's blue/cyan. So `--teal` is now `#4183D7` (blue), `--teal-dark` is `#1C2B3A` (navy sidebar), and `--orange` is `#1DBED8` (cyan). This is confusing but correct. Do not rename them.

**4. The navSub duplicate function bug**
Early in the project, a tax page init hook was added by declaring a second `function navSub()`, which caused JavaScript hoisting to make the original `navSub` call itself infinitely, crashing the entire script silently. The fix was to put all page-specific init hooks inside the single `navSub()` function. Never introduce a second declaration of any function.

**5. Layout scrolling requires bounded height**
The app uses a flex layout: `body → .sidebar + .main → .topbar + .content`. For `.content { overflow-y: auto }` to scroll, `body` must have `height: 100vh` (not `min-height: 100vh`). If scrolling ever breaks, check this first.

## How To Pick This Up

1. Open `spokesweb-accounting.html` in a browser — it runs immediately, no setup
2. Read `CLAUDE.md` in this folder for technical conventions
3. Read `~/.claude/CLAUDE.md` to understand how Eric likes to work
4. The sidebar nav maps to page `div`s with IDs like `pg-dashboard`, `pg-quotations`, `pg-tax`
5. Tax data persists in `localStorage` under key `sw_taxes`
6. To add a new page: add a nav item calling `navSub('newpage', this)`, add `<div class="page" id="pg-newpage">`, add an entry to `pgConfig`

## Open Questions / Known Issues
- Sale Orders, Delivery Orders, Credit Notes, Payments, Refunds pages are nav stubs — no content yet
- The Invoices page exists but uses the old layout style (pre-Bukku restyle) — needs updating to match Quotations layout
- The `SV8` tax code in the Quotation Items table is hardcoded — ideally it should pull from the `localStorage` tax list dynamically
- No print / PDF export functionality yet
- QuickShare via Email button on Quotation detail is visual only — no actual email sending

## Session Log

### 2026-03-26
First full session on this project. Restyled the entire app from Spokesweb teal/orange palette to Bukku.my navy/blue/cyan palette, changed fonts from DM Sans/DM Serif to Inter, rebuilt KPI cards as fully-colored blue panels, restructured sidebar to Bukku's expandable nav pattern, added the Quotations list page (exact Bukku layout with all 11 rows from BSQ-0264 to BSQ-0274), added the Quotation detail view (BSQ-0274) with all 8 tabs and sticky bottom bar, added Tax Rates settings page with full CRUD, fixed body scrolling (height vs min-height), fixed sidebar scrolling, and debugged a silent infinite recursion crash caused by a duplicate `navSub` function declaration. Also created the `/wrap` slash command for end-of-session memory updates.
