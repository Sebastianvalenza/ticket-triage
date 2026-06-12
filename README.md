# Ticket Triage (Demo below)

A client-side triage tool that turns a flat ticketing export into a sorted, de-duplicated queue — separating tickets where the same customer opened several from genuinely unique ones, then letting agents claim, assign, merge and resolve them without two people ever working the same customer.

Third tool in a four-part operations ecosystem, alongside the [VIP Performance Tracker](https://github.com/Sebastianvalenza/vip-performance-tracker) and [Shift Planner](https://github.com/Sebastianvalenza/shift-planner). All three share one synthetic roster and seed, so an agent is the same person across every tool.

## The Problem

In a high-volume support queue the same customer often opens multiple tickets — different requests, same person. Left unsorted, two agents pick up the same player in parallel, the work gets duplicated, and the customer receives two inconsistent answers. The queue also hides who is overloaded and where repeat contacts concentrate. Triaging that by hand — scanning an export, eyeballing which rows share a customer, deciding who takes what — is slow, error-prone, and doesn't scale past a few dozen tickets.

## The Solution

Ticket Triage ingests the ticket export and renders it as an interactive triage queue with four views:

* **Triage** — the core view. A segmented control splits the queue into *Unique* (one ticket per customer) and *Duplicate groups* (one customer, several tickets), each quantified in the KPI strip. Every duplicate becomes a collapsible card holding the customer's whole thread sorted oldest-first; agents claim a single ticket, a whole group, or drag across several groups to claim them at once, and route work to any agent on the roster.
* **My queue** — everything claimed by the active agent, grouped by customer so duplicate threads stay together, with one-tick resolution per case.
* **Workload** — claimed, open and resolved tickets per agent across the roster, filterable by operation, surfacing who is overloaded and who has capacity.
* **Analysis** — where duplication concentrates: duplicate rate by market, volume by request type, and the distribution of how many tickets each customer opens.

A **duplicate group** is every ticket sharing the same customer within the same market. Consolidating a thread is non-destructive: the oldest ticket becomes the parent, the rest are linked as children rather than deleted, and the merge is fully reversible. The "I am" selector picks the active agent, simulating the multi-agent claim flow client-side.

It ships with a deterministic synthetic dataset (900 tickets, 48 agents, 4 operations, 10 markets, 14-day window) so the live demo works with zero setup. The distribution is realistic in ticket volume — roughly 63% unique, 37% in duplicate groups — so the split reflects a real queue rather than an inflated demo. Claims, assignments, merges and resolutions persist per user; dark/light themes persist too, and a reset returns to the generated baseline.

## Stack

* Vanilla HTML + CSS + JavaScript — single file, no build step, no framework
* Chart.js for the duplication, volume and distribution visualizations
* Deterministic seeded PRNG (`mulberry32`) for reproducible synthetic data — the same roster and seed as the other two ecosystem tools
* State persisted to `localStorage`; no real, proprietary or customer data anywhere
* Fully static — runs on GitHub Pages with no backend, no credentials, no data leaving the browser

## Demo

Live: https://sebastianvalenza.github.io/ticket-triage/

## Impact

Turns a flat ticket export into a sorted, owned, de-duplicated queue — making the split between unique and duplicate work immediate, preventing claim collisions by design, and surfacing repeat-contact hotspots on their own. The difference between a queue you fight and a queue you steer.
