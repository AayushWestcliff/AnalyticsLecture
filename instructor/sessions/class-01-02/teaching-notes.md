# Classes 1–2 teaching notes (private)

Draft, 2026-10-12. Companion to the learner pages `docs/lessons/class-01.md` and `docs/lessons/class-02.md`. Do not link these notes from learner pages or copy them into `docs/`.

**Status:** draft for rehearsal (task L01). The Tableau click paths in the learner pages are written from general Tableau Desktop knowledge and have **not** been rehearsed on the course's installed Tableau Public version. D03's Tableau worksheet comparison is also still open, so treat every Tableau-displayed number below as "expected from the numerical reference", not as observed in Tableau.

## Dataset

| Item | Value |
|---|---|
| File | `data/prepared/superstore/retail-v1/order_lines.csv` |
| Contract | `superstore-retail-v1` |
| CSV SHA-256 | `434ba08abf665b617294b188e38c0d0b8a86d0b3386d41eff8a42c15bc708de2` |
| Scope | Order Date 2023-01-01 to 2025-12-31 (half-open interval to 2026-01-01) |
| Units | Source monetary units; currency not stated in source |
| Distribution | Not yet approved for learner download (`publication_approved=false`); rights and delivery route still to settle. Hand out only the CSV, never the whole prepared directory. |

## Reference values for these two classes

Source: `instructor/solutions/superstore/retail-v1/reference_answers.json`, key `primary_scope` unless stated. Values validated numerically only (`tableau_verified: false`).

| Check | Expected | Reference key |
|---|---|---|
| Rows (order lines) | 6,815 | `primary_scope.lines` |
| Distinct orders | 3,388 | `primary_scope.orders` |
| Distinct orders on returns list | 191 | `primary_scope.orders_listed_in_returns` |
| Sum of `returned_order_flag` over lines (the Class 2 debugging trap) | 511 | `debugging_diagnostics.sum_line_return_flags` |
| Segment distinct orders sum to company orders | Yes (partition) | `overlap_and_partition_checks.segment` |
| Category distinct orders summed | 4,779, i.e. 1,391 more than company orders | `overlap_and_partition_checks.category` |
| Ship dates in 2026 retained | 34 lines | see `planning/CLAUDE_TAKEOVER.md` |

Re-read the JSON before class; if the CSV hash ever changes, these values no longer apply.

## Class 1 facilitation

Minute budget from CURRICULUM.md: 15 diagnostic/decision; 20 demonstration; 30 guided setup/view; 5 break; 25 independent view; 15 challenge/debrief; 10 exit check.

- Open with the vague request; collect two or three learner questions and repair one live using the four-part table.
- Demonstration: pause before dragging Sales to ask what Tableau will do with a number (it aggregates to SUM).
- Expected type icons: IDs as text, dates as dates, sales/profit/quantity as numbers, flags as numbers. The D03 import smoke check observed Order ID as string and dates as dates.
- Part 4 quick check answer: the `(Count)` field counts rows, i.e. order lines (6,815), not orders.
- Challenge answer points: total Sales ignores profit, order count, average order value and segment size; a bigger bar does not show where an intervention would work; association is not a reason to invest.
- Access fallback: pair learners; they still submit the written question and grain sentence.

## Class 2 facilitation

Minute budget: 10 retrieval/decision; 20 demonstration; 30 guided preparation; 5 break; 30 independent segment/check; 15 debugging challenge; 10 exit check.

- Grain statement target: "one order line (one product within an order), identified by row_id."
- Rows vs orders demonstration: 6,815 vs 3,388.
- Segment partitions orders (each order has exactly one segment), so segment order counts add to 3,388. Category does not: an order can contain several categories, so category counts sum to 4,779.
- Debugging challenge answer: "6,815 orders" should be 3,388 distinct orders; "511 returned" counts lines of listed orders, the correct count is 191 distinct listed orders. And "returned" should be phrased "on the returns list", since absence does not prove no return.
- Hand-check order: choose a multi-line order live and compare a spreadsheet sum with Tableau's per-order SUM. Any order works; the point is the method.
- Discount: steer learners away from summing or averaging it; its base is undocumented.
- Customer conflict flags: mention only that a small ID issue exists and is handled later in customer analysis.

## Rehearsal checklist (to complete before teaching)

- [ ] Record the installed Tableau Public version (Help → About).
- [ ] Walk every click path in both learner pages and fix menu names.
- [ ] Confirm the `(Count)` field name and the Count (Distinct) right-click route.
- [ ] Confirm local Save As / reopen works in Public Edition on a learner-like machine.
- [ ] Confirm the 6,815 / 3,388 / 191 / 511 values appear in Tableau (closes part of D03).
- [ ] Time both classes with a novice and adjust the guided parts if they overrun.
