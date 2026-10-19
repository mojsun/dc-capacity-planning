# Store Replenishment & DC Capacity Planning Model

**Forecasting store demand, converting it into distribution centre workload, and planning capacity relief before the winter and holiday peak.**

`KNIME` · `Power BI` · `Excel` · `MS Access` · `PowerPoint` · `Capacity Planning` · `Forecasting & Replenishment` · `Service Levels`

> **Status:** Business problem, data model and planning logic are complete. The KNIME workflow, Power BI dashboard and findings are being added in stages; see the [roadmap](#roadmap).

---

## Business problem

It's the end of September. A national retailer replenishes **20 stores** from **2 distribution centres (DCs)**, and the winter and holiday peak (weeks 46–52) is coming. Demand for winter, holiday and automotive products rises sharply, while DC capacity **drops** in holiday weeks and during planned maintenance.

The capacity planning team needs to answer, **weeks before the peak**:

1. **How much volume will each DC need to ship each week** from week 40 to week 52?
2. **Which weeks will exceed DC capacity**, and by how much?
3. **What is the risk to store service levels** (fill rate) if nothing changes?
4. **What capacity relief should we plan now:** pull volume into earlier weeks, rebalance between DCs, or add shifts?

## Planning approach

```
 Store sales     ──►  Demand       ──►  Replenishment   ──►  DC weekly    ──►  Capacity    ──►  Capacity relief
 history              forecast          requirement         workload          check            plan + service risk
 (2025 + 2026 YTD)    (by store, SKU,   (forecast units     (cases by DC      (utilization,    (pre-build, rebalance,
                       week)             → full cases)       and week)         over-capacity)   extra shifts)
```

| Step | Method | Planning question it answers |
|---|---|---|
| 1. Demand growth | 2026 weeks 1–39 ÷ 2025 weeks 1–39, by DC | Is demand growing, and is it growing equally in each region? |
| 2. Demand forecast | Seasonal-naïve: same week last year × DC growth factor | How much will each store sell, week by week, through the peak? |
| 3. Replenishment requirement | Forecast units converted to full cases (`ceil(units ÷ units per case)`) | What does each store need shipped each week? |
| 4. DC workload | Cases summed by DC and week | How much does each DC need to process and ship? |
| 5. Capacity check | Utilization = workload ÷ capacity; over-capacity cases | Which weeks are at risk, and by how much? |
| 6. Service risk | Estimated fill rate = min(1, capacity ÷ workload) | What happens to on-time, complete store deliveries if we do nothing? |
| 7. Capacity relief | Pre-build peak volume into earlier weeks with spare capacity; size any remaining gap | What should we do now, and what is left over that needs extra shifts or another DC? |

## Planned deliverables

| Deliverable | What it shows | Tool |
|---|---|---|
| **Capacity planning workflow** | Repeatable pipeline: data cleaning, forecast, replenishment, DC workload, capacity check | KNIME |
| **Capacity dashboard** | Weekly workload vs. capacity by DC, utilization, over-capacity weeks, fill-rate risk, before/after the relief plan | Power BI |
| **Weekly capacity summary** | One page for supply chain partners: trends, risks, recommended actions | PowerPoint |
| **Refresh SOP** | Step-by-step guide to update the plan each week with new sales data | Word / Markdown |

## Data

Synthetic data created for this project. All stores, products and figures are fictional.

| File | Contents |
|---|---|
| `weekly_store_sales.csv` | 54,600 rows: units sold by store, product and week (2025 W1–52, 2026 W1–39) |
| `stores.csv` | 20 stores in ON, QC, AB and BC, store size, and the DC serving each store |
| `products.csv` | 30 products across Winter, Holiday, Automotive, Outdoor and Home, with units per case |
| `distribution_centres.csv` | Eastern DC (ON/QC) and Western DC (AB/BC) |
| `dc_weekly_capacity.csv` | Weekly shipping capacity (cases) for weeks 40–52, including Thanksgiving, Christmas and planned maintenance reductions |

## Roadmap

- [x] Define the business problem and planning questions
- [x] Design the planning logic and KPIs
- [x] Prepare and document the data
- [ ] KNIME workflow: data cleaning → forecast → replenishment → DC workload → capacity check
- [ ] Validate workload results against an independent calculation
- [ ] Power BI dashboard
- [ ] Capacity relief scenario and service-level impact
- [ ] Weekly capacity summary and refresh SOP
- [ ] Key findings and recommendations (added to this README)

## Key findings

*To be added once the workflow and dashboard are complete.*

---

**Moji Shahi** · Master of Management Analytics candidate, Smith School of Business, Queen's University
[LinkedIn](https://www.linkedin.com/in/m-khorashahi) · [GitHub](https://github.com/mojsun)
