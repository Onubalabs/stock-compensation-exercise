# Independent audits

Three audits by the *Validator*, a separate AI agent with only the context it needs (see document 14). Each finding was **challenged before being applied**.

## Audit 1 · Coherence: case data ↔ prototype
**Scope:** the driving case (document 08), the data file, the input-data panel, and the questionnaire and the diagnostic in both modes (*Today* and *Proposal*).

**Result:** 13 findings; **12 applied, 1 rejected**.

| # | Finding | Decision |
|---|---|---|
| 1 | Brokerage allocation shown as "119% / −19%" | ✅ **A bug introduced by the previous fix.** Now 69% / 31% |
| 2 | Cash Flow totals that change with RSUs had no "calculated" mark | ✅ Marked |
| 3 | Some derived totals (Taxable, Assets) had no mark | ✅ Marked |
| 4 | Recommended insurance ranges had no "engine output" mark | ✅ Marked |
| 5 | Housing costs: $47,850, not $48,000 | ✅ Fixed in the case |
| 6 | Diagnostic date earlier than the case date | ✅ The case uses the demo's date |
| 7 | "$1.2M sits in brokerage" next to a table that splits brokerage and the stock plan | ✅ "sits in taxable accounts" |
| 8 | Cash flow diagram: inflows include RSUs, outflows didn't | ✅ RSU node added |
| 9 | "34% of investable assets" used a different base than the card labeled "investable assets" | ✅ **The most valuable finding:** an evaluator could compute 37%. New texts now say "of your investments" |
| 10 | A note in *Today* mode mentioned RSU lines that weren't shown | ✅ Shown only in *Proposal* |
| 11 | Add the college assumption to the input-data panel | ❌ **Rejected:** it only derives the children's ages and never appears in the diagnostic; the panel had just been simplified |
| 12 | Fund names differed between the two parts | ✅ Aligned with the demo |
| 13 | One question's wording differed between design and prototype | ✅ Aligned |

## Audit 2 · Specification ↔ design ↔ prototype
**Scope:** the specification (document 10) against the design decisions (document 07) and the prototype, run in a headless browser with states outside the driving case.

**Result:** 19 findings; **all applied**.

**Three were prototype bugs, not specification errors:**
- An account marked as "from a former employer" still counted as employer exposure.
- Changing John's employer to a private company **moved his RSUs to Jane** and valued them at her employer's price.
- With both partners at the same company, the summary read "your employer · jane's employer" (now "employer of both").

**One text was changed to match the score rule:** the score panel said the employer's stock *"weighs more"*, but the rule is that it *"never scores better"* (≤). The new text speaks of risk, which is true, without promising how Sherpas will calibrate the score: *"That makes it riskier than the same amount in another company."*

**The rest made the specification sharper:**
- Criteria that were false or ambiguous were corrected (a missing employer, when the not-modeled warning appears, where RSU lines go in Cash Flow).
- A new criterion and an open question: vest dates are an assumption, not a rule.
- Missing pieces from the design were added (out-of-scope instruments, the "Business" chip, advisor edits).
- US English throughout.

**New behaviors** the specification had fixed without a prior decision (e.g. the employer is optional, both salaries at risk when partners share the employer) were listed separately for Alejandro to accept. All were accepted.

## Audit 3 · Confidentiality before publishing
**Scope:** this repository, before making it public, compared against the internal inventory of the platform (not published).

**Result:** 13 findings; **12 applied, 1 kept by decision**.
- **Two blocking leaks:** a table with figures that Sherpas' engine produced for the demo household (scenario losses, balances, a literal quote), and a cash-flow figure computed by the engine. Both removed.
- **Also removed:** short literal quotes from the demo diagnostic, an engine parameter and the name of a data provider, descriptions of platform defects, and internal file paths in the Validator's definition.
- **Fixed:** references to files that only exist in the private working copy, a hard-coded decision count that had gone stale, and the claim that the repository would never be public (decision 27).
- **Kept by decision:** the detailed (fictional) demo household data in the driving case, already summarized on the Notion page.
- **Not in the report, but triggered by it:** the prototype password was replaced by a strong random one, since a weak password makes the encryption pointless.

## What we learned
- **Self-checks miss what the author doesn't think to test.** The Validator tested cases outside the driving case and found three bugs.
- **Fixes need re-checking.** The worst finding of audit 1 was introduced by the previous round of fixes.
- **Cleaning by rules isn't enough.** The export filter passed, and the Validator still found two leaks the rules didn't cover.
- **Not every finding is worth applying.** Each one was weighed against its cost and against decisions already made.
