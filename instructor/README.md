# Instructor resources

This directory contains private teaching guidance and solutions. It is outside the learner-facing `docs/` source and must not be added to the MkDocs navigation or copied into the learner site. Learner pages must not link here. A local directory boundary does not make a repository private: before sharing a repository or archive, explicitly review who can access instructor files.

**Current phase:** foundation and first retail development validation. Private numerical references now exist for the exact prepared retail CSV; full lesson answer packs, reference Tableau workbooks and classroom-ready lessons remain to produce. The pilot outline is maintained in `planning/PILOT_LESSON.md`; it is an internal design, not a lesson to teach directly.

`source-audit/catalog-2026-10-12-controls.json` now contains private numerical controls from the four-file inspection. They refer to the exact raw-source manifest and proposed scopes, not a prepared course release. The independent audit review includes a small hand-check fixture. Neither is a validated teaching answer pack: source-specific contracts, prepared releases and Tableau comparisons remain to produce. Do not copy these controls into learner starter resources.

`source-audit/retail-contract-fixtures.json` adds small, explicitly synthetic D01 cases with expected results for metric/population edge conditions. The read-only retail contract checker consumes them. They are partial hand fixtures rather than a complete prepared-table schema, a full simulation generator or actual source records. Detailed source arithmetic remains in `source-audit/retail-hand-check.md`. Prepared-release answers and teaching examples will require their own version-bound validation.

`solutions/superstore/retail-v1/` contains D02 private exceptions, D03 `reference_answers.json` and `numerical_validation.json`. The independent validator compares every saved typed value against a separate source read and produces whole/eligible/excluded bridges, Segment/Region/Category/month metrics and calendar growth references. Numerical checks passed; Tableau worksheet/filter/grand-total/zero-case and local save/reopen checks remain incomplete. This is development evidence, not an approved teaching answer pack. See `planning/CLAUDE_TAKEOVER.md` and `data/README.md` for exact commands/version/limits. Keep these files outside learner materials and public archives.

## Future solution pack structure

For each produced lesson, create a directory named for the curriculum session and case, with these components:

| Component | Required content |
| --- | --- |
| Teaching notes | Stakeholder decision, outcomes, prerequisites, timings, demonstration prompts, mixed-experience support, access fallback and common recovery paths |
| Dataset manifest | Exact released filenames, version, checksum, provenance/rights, grain, keys, scope, preparation rules and metric contract |
| Answer manifest | Independently computed totals and filtered answers; units, rounding, tolerance, denominator and null/zero behavior; links to the exact release used |
| Worked solution | Verified Tableau steps and original workbook/screenshots, with calculations, filters and interpretation explained |
| Exercise guidance | Expected evidence, rubric mapping, partial-credit criteria, acceptable recommendation variants and further questions |
| Debugging key | Intentional error, diagnostic mechanism, correction, validation and why the mistake changes the business conclusion |
| Python verification | Optional companion outputs using the same release and contracts; recorded execution environment and actual checks |
| Verification record | Commands actually run, tool/version, date, outputs, Tableau comparisons, timing rehearsal, known limits and reviewer |

These are production requirements, not claims that the components exist. Keep learner starter materials free of completed assessed answers, hidden solution sheets and unintended hints. A checkpoint workbook is a learner resource only after a separate content review.

## Answer and teaching quality

1. Freeze the released data before computing solutions. Never validate against a similar, regenerated or silently modified file.
2. Define the population, date window, units, filters, denominator, missingness and zero behavior alongside each answer. State whether retail sales include refunds and whether costs include overheads.
3. Independently compute the values, then compare with Tableau, including filtered and grand-total views. Do not accept a plausible chart as verification. Record the rounding contract and comparison tolerance.
4. Explain weighted rates, overlapping populations and relationship cardinality when they affect the answer. Numerical correctness alone does not demonstrate an appropriate business recommendation.
5. Treat open-ended recommendations with a rubric: evidence, analytical validity, business relevance, uncertainty and an actionable next check. Multiple recommendations can be defensible.
6. Use actual commands and observed outcomes in verification records. Label UI steps, calculations or notebook outputs unverified until they have been checked; a documentation build does not validate them.
7. Rehearse the teaching plan, including recovery for beginners and access problems. Python remains optional initially and must not become a hidden prerequisite.

## Publication and sharing check

- Build only from `docs/`; inspect generated output for private links and answers.
- Publish only reviewed synthetic/public data. Tableau Public uploads are public, even when profile visibility is reduced.
- Review exported Tableau workbooks for data, hidden sheets, solution calculations and metadata before distributing starter files.
- Share answer packs through the agreed instructor channel; learner feedback and any later release of worked answers should be a deliberate teaching decision.
- Run the documented documentation checks and inspect `git diff --check` and `git status --short` when integrating changes. Do not deploy or publish as a verification step.
