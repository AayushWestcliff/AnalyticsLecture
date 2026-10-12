# Lesson 4 teaching notes (private)

Draft, 2026-10-12. Companion to `docs/lessons/class-04.md` (trends, returns list, dashboard; task L03). Do not link from learner pages or copy into `docs/`.

**Status:** draft for rehearsal. The `LOOKUP` growth calculations, dashboard filter steps and field display names (`[Returned Order Flag]`, `[Order Id]`) are unexecuted in Tableau. The contract (`metric_contract.md` R11/R12) defines growth by calendar comparator. `LOOKUP` matches it **only** while all 36 months stay in the view, ordered by continuous Order Month; the learner page warns against filtering months. The separately contracted synthetic refund/cost exercise (task D02R) does not exist yet; the learner page only says it will come later.

## Reference values

Source: `instructor/solutions/superstore/retail-v1/reference_answers.json`, `primary_scope.monthly[*]` (`kpis`, `sales_growth_mom`, `sales_growth_yoy`), and `primary_scope.by_dimension.segment.*.kpis`. Validated numerically only (`tableau_verified: false`).

### Annual Sales (sum of monthly reference values, display rounding)

| Year | Sales |
|---|---|
| 2023 | ≈ 494,040 |
| 2024 | ≈ 472,993 |
| 2025 | ≈ 613,934 |

The annual sums are derived by the lead from the monthly reference values, not output directly by the validator.

### Seasonality and growth highlights

- Peaks every year in **September, November and December**; lows in **January and February**.
- Jan 2025 month-on-month: **−75.1%** (Dec 2024 → Jan 2025). Year-on-year for Jan 2025: **+2.0%**. This is the core of the debugging challenge.
- Other large month-on-month swings that are purely seasonal: Mar 2023 **+1,159.6%** (after a tiny February), Jan 2024 **−74.4%**.
- Dec 2025: month-on-month **+22.8%**, year-on-year **+29.1%**.
- MoM null only for Jan 2023; YoY null for all of 2023 (`status: unavailable_calendar_comparator`).

### Returns list by segment

| Segment | Orders on list | Share of orders |
|---|---|---|
| Consumer | 99 | 5.7% |
| Corporate | 61 | 5.8% |
| Home Office | 31 | 5.1% |
| All | 191 | 5.6% |

The shares are similar, so learners should not build a recommendation on returns differences between segments. Steer them to say so.

## Debugging challenge answers

1. Seasonal: January is always far below December (−74.4% in 2024, −75.1% in 2025). Year-on-year January 2025 is +2.0%, i.e. roughly flat.
2. `LOOKUP(…, -1)` uses the previous mark in the view. Filtering to 2025 removes December 2024, so January 2025 has no comparator and the IF guard returns null.
3. Example rewrite: "January sales were about 2% higher than January last year; the drop from December is the usual seasonal pattern."

## Expected recommendations

Accept any test with two different pieces of evidence, a limitation and a success measure. Examples: a Consumer-segment profitability test (lowest profit ratio, largest Sales, from Lesson 3) measured by year-on-year Sales and profit ratio for the same months; timing a promotion around the known September–December peak. Reject causal claims ("discounts caused…") and anything that subtracts returns from Sales.

## Rehearsal checklist

- [ ] Confirm continuous Order Month shows all 36 months, and the trend matches the monthly reference Sales.
- [ ] Confirm the MoM/YoY calculations with Compute Using → Order Month reproduce the reference growth values (spot-check Jan 2025, Mar 2023, Dec 2025), and nulls appear only where expected.
- [ ] Confirm filtering to 2025 blanks Jan 2025 MoM (the debugging scenario behaves as described).
- [ ] Confirm the returns-share calculation per segment matches the table above.
- [ ] Confirm "Apply to Worksheets → All Using This Data Source" works in Public Edition and the totals recompute.
- [ ] Time the dashboard build with a novice.
