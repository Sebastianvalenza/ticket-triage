# Ticket Triage

**Live demo → [sebastianvalenza.github.io/ticket-triage](https://sebastianvalenza.github.io/ticket-triage/)**

A client-side triage tool that separates **duplicate tickets** (the same player opening several tickets) from **unique ones**, then lets agents claim, assign, merge and resolve them — without two people ever working the same customer.

Third tool in a four-part operations ecosystem, alongside the [VIP Performance Tracker](https://github.com/Sebastianvalenza/vip-performance-tracker) and [Shift Planner](https://github.com/Sebastianvalenza/shift-planner). All three share one synthetic roster and seed, so an agent is the same person across every tool.

---

## The problem

In a high-volume support queue, the same customer often opens multiple tickets — different requests, same person. Left unsorted, two agents pick up the same player in parallel, work gets duplicated, and the customer gets two inconsistent answers. The queue also hides who is overloaded and where repeat contacts concentrate.

Triaging that by hand — scanning an export, eyeballing which rows share a player, deciding who takes what — is slow and error-prone, and it doesn't scale past a few dozen tickets.

## What it does

- **Splits the queue in one view.** A segmented control flips between *Unique* (one ticket per player) and *Duplicate groups* (one player, several tickets). The KPI strip quantifies both at a glance.
- **Groups duplicates by player.** Every player with more than one ticket in the same market becomes a collapsible card holding their whole thread, sorted oldest-first.
- **Claim — single or in bulk.** Claim one ticket, a whole group, or drag across several groups to claim them all for yourself. Claimed work moves to *My queue*.
- **Assign to anyone.** A team lead can route a group or a single ticket to a specific agent from the roster.
- **Merge, non-destructively.** Consolidate a duplicate thread under its oldest ticket as the parent; the rest are linked as children, never deleted, and the merge is fully reversible.
- **Resolve and track.** Tick cases done; *Workload* shows claimed/open/done per agent (filterable by operation), *Analysis* shows where duplication concentrates by market, request type and group size.

## Impact

Turns a flat ticket export into a sorted, owned, de-duplicated queue. The split between unique and duplicate work is immediate, claim collisions are prevented by design, and repeat-contact hotspots surface on their own — the difference between a queue you fight and a queue you steer.

---

## Stack

- **Single-file `index.html`** — no build step, no framework, no backend. Open it or deploy it to GitHub Pages as-is.
- **Vanilla JS + CSS.** Chart.js (via cdnjs) for the Analysis charts; everything else is hand-rolled.
- **Deterministic synthetic data.** A `mulberry32` seed generates 900 tickets across 48 agents, 4 operations and 10 markets — the same roster and seed as the other two ecosystem tools. No real, proprietary or customer data anywhere.
- **State persists to `localStorage`** (claims, assignments, merges, resolutions); a reset returns to the generated baseline.
- **Dark / light themes** on a shared token set, responsive down to mobile.

## Data model

A **duplicate group** is every ticket sharing the same `player_id` within the same `market`. The "I am" selector picks the active agent, simulating the multi-agent claim flow client-side (real multi-user state would need a backend). The distribution is realistic in ticket volume — ~63% of tickets are unique, ~37% sit in duplicate groups — so the split reflects a real queue rather than an inflated demo.

## Run locally

```bash
git clone https://github.com/Sebastianvalenza/ticket-triage.git
cd ticket-triage
# open index.html in any browser — that's it
```

## License

MIT — see [LICENSE](LICENSE).
