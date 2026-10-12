# Private retail source-audit hand check

Audited 2026-10-12. Internal numerical inspection evidence; not released lesson answers. Keep outside learner documentation and downloads. See the [independent source audit review](../../planning/SOURCE_AUDIT_REVIEW.md) for methods, count-level checks and limits.

Source: `data/raw/eu-superstore/2026-10-12/sample_-_superstore.xls`; SHA-256 `5045ed4fec49cae2cc0dfc5ab0d204ba09efa767fe00c996822499e8cc42fbbd`. Proposed scope: 2023-01-01 ≤ Order Date < 2026-01-01. Checked through direct xlrd worksheet iteration and `Decimal(str(cell_value))`; no pandas or Tableau execution. These are source monetary units, with currency and accounting semantics still unresolved.

## Proposed-scope control comparison

For readable comparison below, monetary inspection totals are rounded **only for this display** to two decimals; underlying Decimal comparisons were exact against the private controls. These are **source monetary units**, not approved USD/NPR amounts and not released lesson answers.

| Proposed 2023–2025 scope | Lines | Distinct orders | Reported Sales | Reported Profit |
| --- | --- | --- | --- | --- |
| Consumer | 3,586 | 1,738 | 835,747.86 | 90,101.17 |
| Corporate | 2,084 | 1,044 | 467,562.02 | 65,842.38 |
| Home Office | 1,145 | 606 | 277,656.95 | 40,426.92 |
| All segments, rounded after aggregation | 6,815 | 3,388 | 1,580,966.82 | 196,370.47 |

Displayed rounded Segment Sales sum to one cent more than the separately rounded overall total. This is a presentation-rounding effect, not a failed raw reconciliation; do not force a row-level rounding rule from this display.

### Small source fixture — audit only

Selected the first encountered two-line order in the proposed scope without a customer conflict: **US-2023-105417**, Consumer. Source coordinates below are Excel row numbers including the header; Row ID is the source's separate line identifier.

| Excel row | Row ID | Order ID | Sales via `Decimal(str(value))` | Profit via `Decimal(str(value))` |
| --- | --- | --- | --- | --- |
| 16 | 15 | US-2023-105417 | 76.72800000000001 | -53.70959999999999 |
| 17 | 16 | US-2023-105417 | 10.429999999999998 | -18.252500000000005 |

Transparent hand arithmetic using those source representations:

```text
Sales = 76.72800000000001 + 10.429999999999998
      = 87.158000000000008

Profit = -53.70959999999999 + -18.252500000000005
       = -71.962099999999995

Order ID set = {US-2023-105417}
Distinct orders = 1; source lines = 2
```

Final two-decimal display would be Sales 87.16 and Profit -71.96 in source monetary units. The negative source Profit is retained. No discount is applied a second time and no refund/COGS interpretation is invented. This fixture is an internal arithmetic/grain check, not a released assessment answer or a verified Tableau example.

