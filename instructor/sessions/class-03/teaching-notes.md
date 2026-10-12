# Lesson 3 teaching notes (private)

Draft, 2026-10-12. Companion to `docs/lessons/class-03.md` (segment KPI comparison, task L02). Do not link from learner pages or copy into `docs/`.

**Status:** draft for rehearsal. The calculated fields follow the frozen candidates in `data/metadata/superstore/retail-v1/metric_contract.md` but have **not** been executed in Tableau. The learner page uses Tableau's tidied field names (`[Sales]`, `[Order Id]`, `[Profit]`). Confirm the actual display names on the installed version, because the CSV headers are lowercase (`sales`, `order_id`). Values below come from the numerically validated reference (`tableau_verified: false`).

## Dataset

Same as Lessons 1–2: `data/prepared/superstore/retail-v1/order_lines.csv`, SHA-256 `434ba08a…08de2`, orders placed 2023-01-01 to 2025-12-31, source monetary units.

## Reference values (display rounding; full precision in JSON)

Source: `instructor/solutions/superstore/retail-v1/reference_answers.json`, `primary_scope.by_dimension.segment.<name>.kpis` and `primary_scope.overall`.

| Segment | Lines | Orders | Sales | Profit | AOV | Profit ratio |
|---|---|---|---|---|---|---|
| Consumer | 3,586 | 1,738 | 835,747.86 | 90,101.17 | 480.87 | 10.8% |
| Corporate | 2,084 | 1,044 | 467,562.02 | 65,842.38 | 447.86 | 14.1% |
| Home Office | 1,145 | 606 | 277,656.95 | 40,426.92 | 458.18 | 14.6% |
| **All** | **6,815** | **3,388** | **1,580,966.82** | **196,370.47** | **466.64** | **12.4%** |

Segment orders sum to 3,388 (segment partitions orders). Display-rounded segment values may not add exactly to the separately rounded total; compare at full precision.

### Region filter (Part 5A)

`primary_scope.by_dimension.region` — overall by region: Central 771 orders, Sales 355,317.07, AOV 460.85, ratio 9.1%; East 979 / 475,261.13 / 485.46 / 12.8%; South 549 / 268,816.05 / 489.65 / 14.1%; West 1,089 / 481,572.58 / 442.22 / 13.6%. Region × Segment cross values are **not** in the reference JSON; compute them with the validator approach before using them as answers.

### Category (Part 5B)

`primary_scope.by_dimension.category`, AOV label "Selected-line Sales per participating order": Furniture 1,235 orders, ratio 3.1%; Office Supplies 2,516, ratio 17.6%; Technology 1,028, ratio 16.9%. Category orders sum to 4,779, which is 1,391 more than 3,388 (`overlap_and_partition_checks.category`).

### Debugging challenge (Part 6)

Derived by lead from the reference values above (Decimal arithmetic on the JSON strings, not a separate validator output):

- Simple mean of the three segment profit ratios: **13.14%** vs correct overall **12.42%**. Consumer has the most Sales and the lowest ratio, so the unweighted mean overstates the overall ratio.
- Sales ÷ rows = **231.98** vs correct AOV **466.64**. Rows are order lines, so it understates order value by roughly half.
- Answer to Q4: Consumer has the most influence because it carries about 53% of Sales.

## Expected discussion

- Consumer is the largest by Sales and Orders and has the highest AOV, but the lowest profit ratio. Corporate and Home Office have higher ratios on smaller Sales. Several recommendations are defensible: e.g. investigate Consumer because its large Sales base with the lowest ratio has the largest profit at stake. Reward reasoning with two different measures, a limitation and a next check, not one "right" segment.
- Limitations to accept: Profit definition unknown; no cost or refund detail; returns list is membership only; fictitious sample; association not causation (discount and product mix differ by segment).
- Good next checks: Consumer profit ratio by Category and Sub-Category; discount distribution by segment (descriptive only, Discount base undocumented); monthly trend (Lesson 4).
- Blank AOV or ratio: appears only with an empty filter selection; it means "not available", not zero.

## Rehearsal checklist

- [ ] Confirm field display names and fix formulas on the learner page if needed.
- [ ] Confirm "Show Column Grand Totals" recomputes AOV and ratio from totals (not summed or averaged) for these calculated fields.
- [ ] Reproduce the segment table and compare with the values above at full precision where Tableau allows (records part of D03).
- [ ] Confirm an empty selection shows blanks for AOV and ratio.
- [ ] Time the guided and independent parts with a novice.
