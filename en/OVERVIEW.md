# Docs

Creating/editing files in `docs/`: read [../AGENTS.md](../AGENTS.md) first.

Read in this order `api/` → `database/` → `infrastructure/` —
understand what the system does first, then look up data/infra details
as needed.

- `api/` — business flows by domain, following [000_templates/API_TEMPLATE.md](../000_templates/API_TEMPLATE.md), start at [api/000_OVERVIEW.md](api/000_OVERVIEW.md)
- `database/` — relationship diagram + schema changelog, following [000_templates/DATABASE_TEMPLATE.md](../000_templates/DATABASE_TEMPLATE.md)
- `infrastructure/` — infrastructure components, following [000_templates/INFRASTRUCTURE_TEMPLATE.md](../000_templates/INFRASTRUCTURE_TEMPLATE.md), start at [infrastructure/000_TOPOLOGY.md](infrastructure/000_TOPOLOGY.md)

Templates shared across every language live in [../000_templates/](../000_templates/)
(written in English). Creating a new file: copy the matching template,
keep the same sections and order.
