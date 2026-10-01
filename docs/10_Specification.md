# Stock compensation · Functional specification

> **Examples** use the driving case, John & Jane Doe. John works at Acme (publicly traded, $150), holds **$500K of Acme stock across 2 accounts** ($400K in a stock plan account, $100K in the joint brokerage) and has **2,000 unvested RSUs**. Jane works at Bluerock Pharma and has no stock compensation. Full data: *Caso conductor* (document 08). The Case figures can be checked in the prototype; criteria about the score engine, the advisor view or cases outside the Case cannot.
>
> Codes C1–C10 (capture) and A1–A6 (analysis) match the amber labels in the prototype; M1–M7 (modeling) match the design document. This document says **what** the product does, not how it is built.

## 0. Scope

**In scope:**
- **Employer stock the client already owns**, whatever its origin (vested RSUs, ESPP purchases, exercised options, open-market purchases): it is detected, summed across accounts and owners, and treated as concentration linked to the salary.
- **Unvested RSUs of a publicly traded employer** (PSUs captured as RSUs): modeled as future income, taxed at vest.
- **Unexercised options and private-company equity:** only their existence is asked, and the diagnostic warns that they are not included.

**Out of scope:** score thresholds and weights, the tax cost of selling, modeling NSOs, ISOs (no AMT in the engine), private-company valuation, ongoing ESPP contributions, an event calendar and advisor alerts for vests, the withholding gap, and niche or non-equity instruments (RSA/83(b), SARs/phantom stock, carried interest, NQDC/409A). Reasons in *What we leave out*.

**Who edits:** the client answers in the questionnaire; the advisor sees and edits these fields like any other data (*Data & Assumptions*).

---

## 1. Capture (questionnaire)

### C1 · Document category "Stock plan statements"
- **AC-C1-1.** *Given* the Documents step, *then* a ninth category "Stock plan statements" is shown, with the subtitle *"Vesting schedule or statement from your company's stock plan"* and the same Add / counter behavior as the existing eight.
- **AC-C1-2.** *Given* a file uploaded there, *then* it is listed under that category and available to the advisor. It does **not** fill C5 automatically (no extraction is specified).

### C2 · Employment income help text
- **AC-C2-1.** *Given* the Income step, *then* the help text under the employment income reads *"Gross annual, before taxes. Salary and cash bonus only — don't include company stock."*

### C3 · Employer
- **AC-C3-1.** *Given* the Income step, *then* "Who is your employer?" appears **once per person with employment income** (client, plus the co-client if there is one).
- **AC-C3-2.** *When* the person types, *then* a search shows publicly traded companies with ticker, name and current price (e.g. *ACME · Acme Corp. · $150.00*).
- **AC-C3-3.** *When* the company is not publicly traded, *then* the person can add it as *"Add '<name>' as a private company"*. An employer is either publicly traded or private, never both.
- **AC-C3-4.** The employer is optional. Without one, C4 can still be answered and the Income reminder (AC-C7-1) is shown; C5, C6, the Investments reminder (AC-C7-2) and detection (C9) need an employer.

### C4 · Filter question
- **AC-C4-1.** *Given* the Income step, *then* the household is asked *"Do you get company stock through work?"* (with a co-client: *"Do you or Jane get…"*), with the help text *"For example RSUs, stock options or an employee stock purchase plan (ESPP)."*
- **AC-C4-2.** *When* the answer is Yes, *then* C5 (if any employer is publicly traded), C6 and C7 are shown. *When* it is No, *then* they are hidden.
- **AC-C4-3.** C4 does **not** affect detection: employer stock is tagged in Investments (C9) whatever the answer.

### C5 · Unvested RSUs
- **AC-C5-1.** *Given* C4 = Yes and at least one publicly traded employer, *then* a block *"RSUs not yet vested"* shows one row per grant: **Units · Vesting ends (year) · Frequency** (Monthly, Quarterly, Semi-annual, Annual), plus **Owner** when there is a co-client. *"+ Add grant"* adds rows; each row can be deleted.
- **AC-C5-2.** *When* units are entered, *then* the row shows the value at today's price of the owner's employer: *2,000 units → "≈ $300,000 at today's price (ACME $150.00)"*.
- **AC-C5-3.** *Given* the owner's employer is private, *then* no RSU row can be created for that person (see C6).
- **AC-C5-4.** PSUs are entered here, with their target number of units.

### C6 · Options and private-company equity
- **AC-C6-1.** *Given* C4 = Yes and a publicly traded employer, *then* the household is asked *"Do you also have unexercised stock options, or equity in a private company you work or worked for?"* *When* the answer is Yes, *then* the message *"We'll flag these to your advisor. They're not included in the analysis yet."* is shown. A business the client owns does not go here: it goes under the existing "Business" income chip.
- **AC-C6-2.** *Given* C4 = Yes and a private employer, *then* there is no RSU block for that person and the message *"<Employer> is a private company, so your RSUs or options there can't be valued yet. We'll flag them to your advisor; they're not included in the analysis."* is shown.

### C7 · Reminders
- **AC-C7-1.** *Given* C4 = Yes, *then* Income shows *"Shares you already own (vested RSUs, ESPP purchases, exercised options) go in Investments. Add your stock plan account there."*
- **AC-C7-2.** *Given* C4 = Yes, *then* Investments starts with *"Don't forget your stock plan account at <employer>."*, naming the employer of **whoever has RSUs in C5**, or every employer if nobody does. The banner adds *"Vested RSUs and ESPP purchases usually sit there."* *Case: "…at Acme Corp."* (Jane is not named).

### C8 · Account type "Stock plan account"
- **AC-C8-1.** *Given* the account Type list, *then* "Stock plan account" appears under **Brokerage (Taxable)**.
- **AC-C8-2.** *When* it is selected, *then* the first holding is pre-filled with the stock of the account owner's employer (or the first publicly traded employer), and the client only enters the balance. *Case: ACME, $400,000.* If the account already has a holding, nothing is overwritten. If there is no publicly traded employer, nothing is pre-filled.

### C9 · Employer stock detection and summary
- **AC-C9-1.** *Given* a publicly traded employer, *when* any holding in any account (however it was added) has the employer's ticker, *then* it is tagged *"Your employer"* (*"Jane's employer"* for the co-client's; *"Employer of both"* if they share it).
- **AC-C9-2.** *When* the client removes a tag (✕), *then* that holding no longer counts as employer stock (it still counts as an ordinary holding).
- **AC-C9-3.** *Given* tagged holdings, *then* the end of the account list shows one summary per employer: *"Acme Corp (your employer): $500,000 across 2 accounts"* (*"Jane's employer"* or *"employer of both"* when it applies), followed by the account names (*Acme stock plan · Brokerage*). This is the figure the diagnostic uses.

### C10 · Consistency question
- **AC-C10-1.** *Given* C4 = No, *when* an account is set to "Stock plan account", *then* the account shows *"You said you don't get company stock through work. Is this account from <employer>?"* with two buttons.
- **AC-C10-2.** *When* the client answers *"Yes, update my answer"*, *then* C4 becomes Yes. *When* they answer *"No, it's from a former employer"*, *then* the account is marked as from a former employer: its stock counts as concentration but **not** as employer exposure (no salary link). Neither option blocks the questionnaire.

---

## 2. Modeling and score

### M1 · The four dimensions
| Item | Asset | Income | Expense |
|---|---|---|---|
| Employer stock owned | Holding, flagged as employer stock | — | — |
| Unvested RSUs | **Not** in net worth (M2) | Salary at each vest (M4) | Tax at each vest (federal, state, FICA) |
| After each vest | Becomes employer stock, net of tax (M3) | — | — |

### M2–M7 · Rules
- **AC-M2-1.** Unvested RSUs are **not** added to net worth or assets. *Case: net worth $2,365,000*; the $300,000 of unvested RSUs is shown separately.
- **AC-M3-1.** At each vest, the vested value **minus its tax** is added to the employer stock position (the client is assumed to keep the shares).
- **AC-M4-1.** Future vests are valued at **today's price, held constant**.
- **AC-M4-2.** The client gives only units, end year and frequency, so the units are split **equally across the remaining vest dates**, from the next period through the end year. The exact dates are an assumption to validate (they are on the plan statement, C1). *Case: 13 quarterly vests, Dec 2026 – Dec 2029, of ≈ 154 units = $92,400 a year.*
- **AC-M5-1.** **Liquidity:** employer stock never counts as an emergency reserve. *Case: the reserve is still the $150K in cash.*
- **AC-M5-2.** **Protection:** vested employer stock counts like any other investment; unvested RSUs never count.
- **AC-M6-1.** **Savings rate:** RSUs are excluded from both the income base and the savings; the base is otherwise unchanged. *Case: the rate is the same as without RSUs.*
- **AC-M6-2.** **Statements (Cash Flow):** *RSU vesting* appears under Earned income, *Taxes on RSU vesting* under Taxes, and *Retained as company stock* under Savings. The free cash flow does not change, and the score's savings rate still excludes these lines (AC-M6-1). *Case: +$92,400 inflow; free cash flow unchanged.*
- **AC-M7-1.** The concentration check uses **the larger of** (a) the largest single position, as today, and (b) the **total employer exposure**: vested employer stock summed across accounts and owners (if both partners share the employer, both are added). Unvested RSUs are excluded. *Case: max(VTI 30%, Acme 34%) = Acme.*
- **AC-M7-2.** The base for percentages is total investments **including cash**, the same base the check appears to use today (inferred from the Demo: VTI 45% = $450K / $990K). *Case: $500K / $1.49M = 34%.*

### Score (criteria only; Sherpas sets the thresholds)
- **AC-S-1. Comparison.** *Given* two households identical except that in A the concentrated company is the employer and in B it is not, *then* A's concentration score is **lower than or equal to** B's.
- **AC-S-2. No side effects.** *Given* a household with no employer stock, *then* its score is **exactly the same as today**.
- **AC-S-3. Explainable.** *When* the employer drives the concentration check, *then* the score's View more panel says so. *Case: "$500K of your investments are in Acme, which also pays your salary."*

---

## 3. Analysis (diagnostic)

All analyses appear in the existing diagnostic shared with the client, inside existing components. They appear only when there is employer exposure or unvested RSUs.

- **AC-A1-1. Total employer exposure.** *Given* employer exposure, *then* Investment analysis › *What your portfolio should be doing* includes a block *"Concentrated stock risk — <Employer>, your employer"* with the total, the share of investments, the split by account, the unvested RSUs and the salary at stake. *Case: "$500K of your investments (about 34% of them) is in Acme: $400K in your stock plan and $100K in your brokerage. Another $300K in RSUs is still vesting through 2029, and John's $195K salary depends on the same company."*
- **AC-A2-1. Employer stress test.** *Then* next to the market scenarios, *"If <Employer>'s stock falls 40%"* shows three figures: the loss on vested stock, the loss on unvested RSUs, and the salary at risk. *Case: −$200K (Acme becomes 23% of investments), −$120K, $195K/yr.* The 40% drop is fixed and labeled illustrative.
- **AC-A3-1. Path if nothing changes.** *Given* unvested RSUs, *then* Retirement & Goals shows the employer stock at the end of each year until the last vest (constant price, net of tax). *Case: ≈ $515K · $574K · $633K · $692K.*
- **AC-A4-1. Recommendation.** *Then* *What we're recommending* includes *"Diversify <Employer> as it vests, then trim in stages"*: sell new shares as they vest and reduce the position in stages toward Sherpas' *well-controlled range*, warning that the tax cost depends on how each share was acquired. No target percentage of our own.
- **AC-A5-1. Score explanation.** *Then* the score's View more panel explains the employer in **Investing** (AC-S-3) and, in **Liquidity**, that employer stock is not counted as a reserve.
- **AC-A6-1. Figures.** *Then* the employer exposure and the unvested RSUs appear, kept apart from net worth, in: the Net worth card (*"+ $300K unvested RSUs (not included)"*), the Assets card (an *"Acme · your employer $500,000"* row), Savings & Expenses (RSU flow), the Emergency fund note, *Accounts & holdings* (*"Stock plan account"* type and *"Your employer"* tags) and Statements (Balance: *"RSUs not yet vested"*; Cash Flow: AC-M6-2).
- **AC-A6-2. Not-modeled warning.** *Given* C4 = Yes and either C6 = Yes or a private employer, *then* every diagnostic tab starts with *"Not included in this analysis: you told us you have stock options or equity in a private company. They can't be valued yet, so your real exposure to a single company may be higher than shown here."*

---

## 4. States

| State | Questionnaire | Diagnostic |
|---|---|---|
| **No employer** | C3 empty; C4 can be answered; no detection | Same as today |
| **Publicly traded employer, C4 = No, no employer stock** | C5–C7 hidden | Same as today (AC-S-2) |
| **Publicly traded employer, C4 = No, employer stock held** | Holdings tagged (C9) and summary shown | Employer exposure in M7 and A1, A2, A4–A6; no RSUs, so no A3 |
| **Publicly traded employer, C4 = Yes** (the Case) | C5, C6, C7 shown; C9 summary | Full A1–A6 |
| **Private employer, C4 = Yes** | No C5; private-company message (AC-C6-2) | Warning (AC-A6-2); no exposure computed for that employer |
| **C6 = Yes** | Message *"We'll flag these…"* | Warning (AC-A6-2) |
| **With co-client** | C3 and C5 Owner per person; tags *"Jane's employer"* | Exposure summed across owners |
| **Stock plan account with C4 = No** | C10 question | Depends on the answer (AC-C10-2) |

## 5. Edge cases

| Case | Expected behavior |
|---|---|
| **Both partners work for the same company** | Tag *"Employer of both"*; their exposures are summed (M7); A2 shows both salaries at risk |
| **Former employee of a publicly traded company** | Without C10, the shares count as an ordinary holding (largest-position check). With C10 → *"former employer"*: concentration, but no salary link |
| **Company stock fund inside a 401(k) without a ticker** | **Not detected** (no ticker to match). Known limitation: the client cannot tag it manually in this scope |
| **Grant ending this year** | Remaining units vest within this year; the A3 path has a single point |
| **Grant with 0 units** | Shown as *"≈ $0"* in C5 and ignored in modeling |
| **Employer changed after entering RSUs** | The RSUs are revalued at the new employer's price; if it is private, they become "not valued" (AC-C6-2) |
| **Client removes the "Your employer" tag** | AC-C9-2 |
| **Employer stock below the largest position** | Still drives the check if its total across accounts is larger (M7). *Case: $400K and $100K are each below VTI's $450K; together, $500K* |

## 6. Open questions for Sherpas
1. **Concentration check:** which thresholds does it use, and how should "employer never scores better" (AC-S-1) be calibrated?
2. **Engine:** can it model a non-cash income that becomes an asset (RSU vests) month by month?
3. **Taxes:** can the tax engine compute the ordinary-income tax of a vest (federal, state, FICA)?
4. **Protection:** which assets count as *liquid assets* in the life-cover check?
5. **Income per person:** with a co-client, is employment income captured per person? (We saw a single field without a co-client; the diagnostic splits John and Jane.)
6. **Company stock funds inside 401(k)s:** is there any identifier we could use to detect them?
7. **Vest dates:** is an equal split of units across periods (AC-M4-2) good enough, or should the vest dates come from the plan statement?
