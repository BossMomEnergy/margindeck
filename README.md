# Margin Desk

A consulting desk for restaurant food cost and labor. For each client it compares what the recipes say the kitchen should use with what the counts say it did use. It ranks the gaps as dollar opportunities and benchmarks the business against the top 20% of similar operators.

## What's in this repo

| Path | What it is |
|---|---|
| `app/index.html` | The Margin Desk app. One self-contained page with no build step. |
| `api/margin-desk-market-data.openapi.yaml` | Open API spec (OpenAPI 3.1) for distributor data, national commodity prices and GPO / national-account contract pricing. |
| `docs/period-playbook.md` | The repeatable period process, split by role. |
| `templates/*.csv` | Example CSVs for each import. Hand these to whoever pulls exports. |

## Running the app

- **Hosted (recommended for the team):** the published version lives on claude.ai and saves every client workspace on the server. The owner shares it from the page's Share menu.
- **Locally:** open `app/index.html` in a browser. It runs the same analysis and saves clients in that browser only. "Match with Claude" and the Claude-drafted readout need the hosted version.

The app opens on a demo tavern with sample numbers. **New client** creates a blank workspace.

## The analysis

- **Consumption:** actual use (beginning count + purchases − ending count − transfers out) against theoretical use (units sold × recipe quantity). The variance after logged waste is shown in units, % and $. Ingredients past the client's threshold are flagged.
- **Opportunities:** ranked, annualized tickets for usage overages, waste, underpriced plates, vendor price increases and overstaffed hours. A review list covers menu dogs, puzzles to promote, and data gaps.
- **Menu profitability:** menu engineering quadrants (stars, plowhorses, puzzles, dogs) and plate cost at the latest invoice price.
- **Food cost:** theoretical vs. actual vs. P&L, each against target.
- **Labor productivity:** sales per labor hour, labor % and prime cost, hour by hour.
- **Benchmarks:** six metrics against a typical operator and the top 20% for the client's segment.
- **Client readout:** a written summary and a CSV export of the opportunities.

> **Benchmarks are placeholders.** The typical and top-20% values in the app are starting estimates for each segment, not survey data. Replace them with figures from a benchmark source you license or trust before you show them to a client. They can be edited per client in the Benchmarks view.

## Import formats

Each import auto-matches column names. Odd headers can be matched by hand or with Claude.

| Import | Columns |
|---|---|
| POS item sales | menu item, qty sold, net sales |
| Hourly sales & labor | hour (0–23 or "3pm"), net sales, guests, labor hours, labor $ |
| Invoice lines | date, vendor, description, packs received, units per pack, cost per pack |
| Inventory counts | ingredient, beginning, ending, waste, transfers out |
| Recipe lines | recipe, menu price, ingredient, qty, unit |
| Ingredients | name, count unit, cost per unit, category |

Quantities are always in the ingredient's count unit. "Units per pack" converts a case into that unit (a 10# case of beef = 10 lb).

## Live data connections

The page can't call POS, purchasing or accounting APIs directly. Hosted pages block outside network calls, and client API keys must not live in a browser. Live sync needs a small server connector for each system that pulls on a schedule and writes into each client's workspace. Toast (standard API access is self-service for operators) and MarginEdge (API keys from its developer portal) are the easiest to wire first. `api/` defines the shape those connectors and the market-data service should expose.

## Roadmap

1. Connector service: Toast orders and menus, MarginEdge invoices, QuickBooks Online / Xero P&L.
2. Market data service implementing `api/margin-desk-market-data.openapi.yaml`, starting with public USDA AMS Market News and BLS series.
3. Member-authorized GPO and national-account contract loading, with compliance checks.
4. A licensed benchmark source to replace the placeholder benchmark values.
