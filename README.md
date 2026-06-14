# Ticket Triage

Turns a flat ticketing export into a sorted, de-duplicated queue — separating the tickets where one customer opened several from the genuinely unique ones — then lets agents claim, assign, merge and resolve them without two people ever working the same customer in parallel.

**[Live demo](https://sebastianvalenza.github.io/ticket-triage/)** · runs instantly on synthetic data, or drop in your own ticketing export.

---

## The problem it solves

In a high-volume support queue the same customer often opens several tickets — different requests, same person. Left unsorted, two agents pick up the same player in parallel, the work gets duplicated, and the customer receives two inconsistent answers. The queue also hides who is overloaded and where repeat contacts concentrate. Triaging that by hand — scanning an export, eyeballing which rows share a customer, deciding who takes what — is slow, error-prone, and doesn't scale past a few dozen tickets.

Ticket Triage answers the question a queue actually poses — *who takes what, without collisions?* — by sorting the export into owned, de-duplicated work the moment it loads.

## What's inside

- **Triage** — the core view. A segmented control splits the queue into *Unique* (one ticket per customer) and *Duplicate groups* (one customer, several tickets), each quantified in the KPI strip. Every duplicate becomes a collapsible card holding the customer's whole thread sorted oldest-first; agents claim a single ticket, a whole group, or drag across several groups to claim them at once, and route work to any agent on the roster.
- **My queue** — everything claimed by the active agent, grouped by customer so duplicate threads stay together, with one-tick resolution per case.
- **Workload** — claimed, open and resolved tickets per agent across the roster, filterable by operation, surfacing who is overloaded and who has capacity.
- **Analysis** — where duplication concentrates: duplicate rate by market, volume by request type, and the distribution of how many tickets each customer opens.

A **duplicate group** is every ticket sharing the same customer within the same market. Consolidating a thread is non-destructive: the oldest ticket becomes the parent, the rest are linked as children rather than deleted, and the merge is fully reversible. The "I am" selector picks the active agent, simulating the multi-agent claim flow client-side.

## Use your own data

It ships with a deterministic synthetic dataset (900 tickets, 48 agents, 4 operations, 10 markets, 14-day window) so the live demo works with zero setup. The distribution is realistic — roughly 63% unique, 37% in duplicate groups — so the split reflects a real queue rather than an inflated demo. Claims, assignments, merges and resolutions persist per user; dark and light themes persist too, and a reset returns to the generated baseline. Nothing leaves the browser.

## Part of an operations ecosystem

Ticket Triage is one of five control surfaces for a single multi-hub operation, built to follow one decision down the whole chain — *from the shift being covered to the cash being collected*:

| Stage | Tool | The question it answers |
|---|---|---|
| Capacity | [Shift Planner](https://github.com/Sebastianvalenza/shift-planner) | Is the shift covered? |
| **Workflow** | **Ticket Triage** *(this tool)* | **Who takes what, without collisions?** |
| Productivity | [Performance Tracker](https://github.com/Sebastianvalenza/performance-tracker) | Is the team performing? |
| Revenue | [Revenue Cockpit](https://github.com/Sebastianvalenza/revenue-cockpit) | Are we going to make the number? |
| Cash | [AR Cockpit](https://github.com/Sebastianvalenza/ar-cockpit) | Did the money actually land? |

All five run on the same four hubs (Madrid 🇪🇸 · Berlin 🇩🇪 · Warsaw 🇵🇱 · Dublin 🇮🇪), the same ten markets, the same seed and the same visual system — one company seen from five functions. The hubs are the same operating centres throughout: the Berlin that books deals in Revenue Cockpit is the Berlin whose support floor this tool triages. The roster here is the same 48-agent population the Shift Planner staffs and the Performance Tracker scores — assign a ticket in this tool and you are routing it to the people those tools plan and measure. Same world, different layer of the business.

## Stack

Single-file `index.html` — no backend, no build step, no framework — deployable to GitHub Pages as-is. Vanilla JavaScript for the queue model and the de-duplication and claim logic, Chart.js for the duplication, volume and distribution visualizations, PapaParse for CSV parsing. Synthetic data is generated from a fixed seed (`mulberry32`) so the queue is identical on every load. State persists to local storage; dark and light themes, persisted locally. Fully client-side — no credentials, no data leaving the page.

## Notes

All data is synthetic. No real customers, tickets or company names appear anywhere in this repository. Names, markets and figures are randomly generated for demonstration.

---

*[linkedin.com/in/sebastianvalenza](https://linkedin.com/in/sebastianvalenza)*
