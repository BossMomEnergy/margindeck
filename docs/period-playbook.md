# Period playbook

The same steps every period (usually 4 weeks), split by who does them. The app's **Period checklist** tracks them for each client. When a period is finished, **Start next period** carries ending counts forward as beginning counts and clears that period's sales, invoices, hourly data, waste, transfers, P&L and readout. Recipes, ingredients, mappings and setup stay.

## IT specialist

1. **Confirm access** to the client's POS, purchasing and accounting systems: connector credentials, or permission to export.
2. **Schedule the exports or API pulls** for item sales, hourly sales & labor, invoice lines and the P&L, all on the same dates as the counts.
3. **Check the data landed complete.** Row counts and totals should match the POS sales summary and the invoice total for the period.

## Data entry assistant

1. **Import POS item sales and hourly sales & labor** (Data & mapping → Import CSV). See `templates/` for the expected columns.
2. **Import invoice lines.** Check units per pack on any new vendor items.
3. **Map new POS items to recipes and new vendor items to ingredients** until no open items are left. Modifiers ("add bacon") map to their own small recipe.
4. **Enter counts, waste and transfers** on the Count sheet, in each ingredient's count unit.
5. **Enter the P&L numbers** in Client setup: food sales, food COGS, total sales and total COGS.
6. **Work the data gaps list** (Opportunities → Review list).

## Consultant

1. **Review flagged ingredients and the ranked tickets** in Consumption and Opportunities. Recount before you call anything theft.
2. **Compare against the top 20%** in Benchmarks, using the client's segment.
3. **Draft and edit the client readout.**
4. **Agree on 30-day actions with the client.** Export the opportunities CSV for the meeting.

## Data rules that keep the numbers honest

- Counts, invoices, POS sales and the P&L must cover the **same dates**.
- Record **transfers** between outlets and to the bar, or costs land on the wrong P&L.
- Every vendor item maps to **one** ingredient, and every POS item to **one** recipe.
- The annualized values extrapolate one period to a full year, so say so when presenting them.
