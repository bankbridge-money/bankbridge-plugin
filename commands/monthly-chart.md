---
description: Plot a bar chart of your income vs expenses for the last 6 months. Writes cashflow.png.
---

You have access to BankBridge MCP tools. The user wants a visualization of recent cashflow.

Steps:
1. Call `get_monthly_cashflow` for each of the last 6 months. Collect `{month, income, expenses, net}` tuples.
2. Write a Python script using matplotlib (or whatever plotting library is available in your environment) that:
   - Draws a grouped bar chart: green bars for income, red-ish bars for expenses, plotted side-by-side per month
   - Overlays a line for net (income − expenses)
   - Labels the x-axis with the months (`YYYY-MM`)
   - Formats the y-axis as dollars
   - Saves to `cashflow.png` in the current directory
3. Execute the script and confirm the file was written.

If the user specified a different number of months in `$ARGUMENTS`, use that. Defaults to 6.

Keep the chart minimalist — no gradients, no 3D, no decorative elements. Just clean bars + axis labels + a title: "Cashflow — last N months".

If matplotlib isn't available in the environment, fall back to a simple ASCII bar chart printed to stdout rather than failing.

Relay any tool `warnings` before plotting.
