# CRM Prototype

This repository contains a static prototype of the Sales Team CRM built with GitHub Pages. It uses July–August 2025 sales, timesheets, and seed-attributed orders to demonstrate key metrics for the Travel Agency sales team.

## Data sources
- **Sales transactions** (Raw Data 7/1/2025–8/31/2025): order-level revenue and unit counts.
- **Seed-attributed orders**: mapping of each order to the budtender who helped the customer.
- **Timesheets** (Jul 1–Aug 31 2025): summary of hours worked by each team member. Only the `Regular` column is used (OT and Double OT were NaN and ignored).

## Calculations
We matched `dutchie_order_id` from the seed attribution data with `TransId` in the sales transactions. Only first names present in both the seed data and the timesheets were considered. Reps that didn’t appear in the timesheets were excluded. For each rep we computed:

- **Revenue**: sum of `InvoiceTotal` across matched orders.
- **Units**: sum of `TotalItems`.
- **Average Ticket**: revenue divided by number of orders.
- **Share of Sales**: rep revenue divided by total revenue across all matched reps.
- **Hours Worked**: sum of the `Regular` hours for that first name in the timesheets.
- **Time-Weighted Efficiency (TWE)**: `(avg_ticket * share_of_sales_pct) / hours_worked`.

The overall KPIs (`totalRevenue` and `totalUnits`) are the sums across all matched reps.

## Using this prototype
The static dashboard at `index.html` reads metrics from `team_metrics.json`. To update metrics:
1. Create a new metrics file in the same JSON structure.
2. Replace `team_metrics.json` in the repository.
3. Commit and push; GitHub Pages will update automatically.

This prototype is intended for demonstration only. It does not fetch live data or call any APIs. Future iterations can integrate with your internal APIs for sales, inventory, and attribution data to automate the pipeline.
