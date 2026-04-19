---
description: Pie chart of spending by category. Writes spending-pie.png (or falls back to ASCII if no plotting library).
---

You have access to BankBridge MCP tools. The user wants a visualization of their spending composition.

`$ARGUMENTS` optionally specifies a window (e.g. "march", "last 30 days", "2026-q1"). Default: last 30 days.

Steps:
1. Call `get_spending_summary` with `group_by: "category"` for the resolved window.
2. Keep the top 7 categories by spend; bucket the rest into "Other".
3. Render a pie chart via matplotlib (if available) or a fallback ASCII donut.

Matplotlib version:
- Sort wedges by size; use a muted palette (no neon).
- Label each wedge with category name + percentage.
- Title: "Spending by category — <window>"
- Save as `spending-pie.png` in the current working directory.
- Confirm the file was written.

ASCII fallback (if matplotlib not available):
```
     FOOD_AND_DRINK ███████████████████  34%  $ X
   TRANSPORTATION  ███████████          19%  $ X
RENT_AND_UTILITIES ████████              14%  $ X
   ENTERTAINMENT  ███████               12%  $ X
         GROCERIES ██████                10%  $ X
        GENERAL_MERCH ████                7%  $ X
            HEALTH ██                     3%  $ X
             Other █                      1%  $ X
```

Keep the bar glyph consistent. Widths proportional to percentage, rounded down.

Relay any `warnings` above the chart.
