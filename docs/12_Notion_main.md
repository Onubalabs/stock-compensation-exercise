# Stock compensation in Sherpas

## 0. Summary
- **The problem is not only where to enter stock compensation.** For the clients for whom it matters most, the diagnostic misses both their biggest risk and one of their largest sources of wealth.
- **The proposal:** identify all the employer stock a client owns, add their unvested RSUs, and link that exposure to their salary.
- **What the advisor gets:** the client's real wealth and income, the total exposure to the employer across accounts, a stress test, and a recommendation to diversify in stages.
- **What we leave out:** tax planning and event alerts, and modeling options and private-company equity. Options and private equity are asked about and flagged, never ignored.
- **Design principle:** every change must make the diagnosis **more honest, never more flattering**.

## 1. The problem

### A symptom, not the problem
The brief frames it as a capture gap: *"there is nowhere to put it."* That is true: there is no account type, income line, document category or employer question for it. But creating a place to enter it would not be enough: the diagnostic would still not understand it.

> **For the clients for whom it matters most, the diagnostic sees neither their biggest risk nor one of their largest sources of wealth.**

### Why it is hard: one object with four faces
| Face | Why |
|---|---|
| **Income** | Each vest is salary |
| **Asset** | The shares |
| **Expense** | Taxes at vest or exercise; ESPP contributions |
| **Risk** | Salary and savings depend on the same company |

It also changes over time: unvested shares aren't the client's yet, options expire, and selling has windows. The good news is that Sherpas' model already has the four dimensions (asset, liability, income, expense) and projects month by month. **The system doesn't need to be reinvented; it needs to learn a new object.**

### The driving case: John & Jane Doe
The demo household, plus one hypothesis: **John works at Acme** (publicly traded). He holds **$400K of Acme in his stock plan account and $100K in the joint brokerage**, and has **2,000 unvested RSUs (≈ $300K)** vesting quarterly through 2029. His salary is $195K.

Today the concentration check measures the **largest single position**. Neither Acme position is the largest on its own ($400K and $100K against VTI's $450K), so **the risk is invisible**. Together they are $500K, the largest exposure, and the same company pays John's salary.

## 2. Scope

> **We identify all the employer stock the client owns, add their unvested RSUs, and link that exposure to their salary.**

### What we include
| Item | What it does |
|---|---|
| **Employer stock already owned** (any origin) | "Who is your employer?", automatic detection and a total across accounts, and a reminder to add the stock plan account |
| **Unvested RSUs** (publicly traded employer) | Captured in the questionnaire; modeled as future income, taxed at vest. PSUs are captured as RSUs |
| **Income** | Salary and RSUs are kept apart |
| **Options and private-company equity** | Only their existence is asked; the diagnostic warns that they are not included |
| **Employer concentration** | The concentration check takes the larger of the largest position and the total employer exposure |
| **Link to the salary** | A stress test and a recommendation to diversify in stages. In the score, one rule only: concentration in the employer never scores better than the same concentration elsewhere |

**Why the type barely matters:** every type ends up as ordinary shares. Once the client owns them, what matters is that they are their employer's. Types only differ while they are future rights.

### The value
**For the advisor:**
1. **A correct diagnostic:** real wealth and income, with company stock and unvested RSUs.
2. **A risk that is invisible today:** the total exposure to the employer, not just the largest position.
3. **John is not Ana:** two clients with $500K in one company, but only John's salary depends on it. The stress test quantifies the triple hit: shares, salary and unvested RSUs.
4. **A prepared conversation:** a staged diversification plan, with figures and the company by name.
5. **A diagnostic they can trust:** what isn't modeled is flagged, not hidden.

**For Sherpas:** it reuses existing pieces: the ticker search, account entry, the concentration check, the "Concentrated stock risk" block and the "Trim concentration… in stages" recommendation. It completes the product instead of adding screens.

### Three options considered
The options are three **cumulative scopes**: each one includes the previous one.

| | 1 · Correct diagnostic | 2 · Concentration risk | 3 · Taxes and events |
|---|---|---|---|
| **Question** | What does my client really own and earn? | How much do they depend on one company? | What will happen, and what will it cost? |
| **Adds** | Stock compensation in every existing calculation | Total employer exposure, linked to the salary, in the score and the analysis | Vesting calendar, tax bill per event, advisor alerts |
| **For** | Fixes a wrong diagnostic; cheapest | Targets the main risk; reuses existing pieces; needs little data | Very actionable |
| **Against** | The main risk stays invisible, and the score could even **improve** as shares count as liquid assets | Touches more pieces | Needs data clients rarely know (calendars, strikes); no AMT in the engine |
| **Decision** | ✅ In | ✅ In | ❌ Out |

**Recommendation: scopes 1 + 2.** Scope 1 alone could make the diagnostic more flattering, and it offers no new analysis. Scope 3 is left out for cost, risk and the amount of data it needs, not for lack of value.

## 3. Functional design
We present it from what the advisor sees back to where the data comes from: **analysis → modeling → capture → types**. Codes match the amber labels in the prototype; the full acceptance criteria are in the **Specification**.

### 3.1 Analysis: what the advisor gets
Everything goes in the **existing diagnostic**, in existing components, with no new screens.

| # | Analysis | Where | With John |
|---|---|---|---|
| **A1** | **Total employer exposure** | Investment analysis › "Concentrated stock risk" | *"$500K of your investments (about 34% of them) is in Acme… and John's $195K salary depends on the same company."* |
| **A2** | **Employer stress test** | Next to the market scenarios | If Acme falls 40%: −$200K in shares, −$120K in unvested RSUs, $195K/yr of salary at risk |
| **A3** | **Path if nothing changes** | Retirement & Goals | Acme grows from $500K to ≈ $692K by 2029 as RSUs vest |
| **A4** | **Diversify in stages** | What we're recommending | Sell new shares as they vest, then trim in stages; the tax cost depends on how each share was acquired |
| **A5** | **Explanation in the score** | Score › View more › Investing, Liquidity | *"$500K of your investments are in Acme, which also pays your salary."* |
| **A6** | **Figures and warnings** | Net worth, Assets, Statements, Accounts & holdings | *"+ $300K unvested RSUs (not included)"*; an Acme row; RSU lines in Cash Flow; a warning when options or private equity aren't modeled |

### 3.2 Modeling: how existing calculations change
| # | Question | Decision | Why |
|---|---|---|---|
| **M2** | Do unvested RSUs count in net worth? | **No.** Shown apart; they enter as they vest | They aren't the client's yet and are lost if the client leaves |
| **M3** | What happens at vest? | Shares are **kept**, net of tax | It's what happens if the client does nothing; the recommendation proposes changing it |
| **M4** | At what price? | **Today's, held constant** | No speculation on the stock; consistent with a single-scenario model |
| **M5** | Liquidity and Protection? | Employer stock is **never an emergency reserve**; for Protection, vested stock counts like any investment | Losing the job and a drop in the stock can happen together |
| **M6** | Do RSUs count as savings? | **Neutral:** the savings rate excludes them | Counting them would inflate savings with concentrated savings |
| **M7** | What does the concentration check measure? | **The larger of** the largest position and the total employer exposure (summed across accounts and owners) | A household without employer stock scores exactly as today |

**Score:** we set criteria, not numbers. With equal exposure, the employer **never scores better** than another company; households without employer stock get **exactly the same score**; and the panel explains when the employer drives the result. Thresholds stay with Sherpas, who are calibrating the score in beta.

### 3.3 Capture: how it gets in
| Screen | New |
|---|---|
| **Documents** | **C1** "Stock plan statements" category |
| **Income** | **C2** "Salary and cash bonus only" help text · **C3** "Who is your employer?" (per person; publicly traded or private) · **C4** "Do you get company stock through work?" · **C5** unvested RSUs: units, end year, frequency · **C6** options or private equity: yes/no · **C7** reminders |
| **Investments** | **C8** "Stock plan account" type, pre-filled with the employer's stock · **C9** automatic "Your employer" tags and a total per employer · **C10** a consistency question if a stock plan account appears after "No" in C4 |

**Principles:** reuse existing patterns; ask only what the client knows (company, units, end year, frequency; no strikes or exact dates).

### 3.4 Types: what's in
| Type | How we treat it |
|---|---|
| **Shares already owned** (vested RSUs, ESPP purchases, exercised options, open-market) | ✅ Employer stock, whatever the origin |
| **Unvested RSUs / PSUs** | ✅ Modeled as future income |
| **Unexercised NSOs / ISOs** | ⚠️ Asked and flagged, not modeled |
| **Private-company equity** | ⚠️ Asked and flagged, not modeled |
| **Ongoing ESPP contributions** | ❌ Out: small, and shares within months |
| **RSA/83(b), SARs/phantom, carried interest, NQDC/409A** | ❌ Out: niche, or not equity |

**Criteria for future rights:** does it increase exposure to the employer? Can it be valued without inventing a price? Can the current engine model it without misleading?

## 4. What we leave out, and why
| Item | Why |
|---|---|
| **Score numbers** (penalty, thresholds, weights) | Sherpas' calibration; the score is in beta |
| **Tax cost of selling** by share origin | Needs the origin and date of each lot: tax planning |
| **Modeling NSOs** | Needs strike and expiry; exercising is a tax decision |
| **Modeling ISOs** | The engine doesn't compute AMT |
| **Private-company valuation** | No market price; we would have to invent one |
| **Ongoing ESPP contributions** | Small; within months they are shares we already detect |
| **Event calendar, withholding gap, advisor alerts** | Needs data clients rarely know; planning, not diagnosis |
| **Niche instruments** | RSA/83(b), SARs/phantom, carried interest, NQDC/409A |

**Out of the calculation, not off the radar:** whatever can change exposure a lot (options and private equity) is asked about and flagged. Leaving it out never makes the diagnostic more flattering.

## 5. Specification
Acceptance criteria (Given / When / Then), states, edge cases and open questions for Sherpas, in this subpage:

## 6. Prototype
A clickable reproduction of the questionnaire and the diagnostic with the proposal built in, on the John & Jane case. How to use it, and the case data behind it, in this subpage:

## 7. Route to market
Release notes and the advisor guide, in this subpage:

## 8. Hypotheses and validation plan
| # | Hypothesis | How to validate | If it's wrong |
|---|---|---|---|
| **H1** | Unvested RSUs are the most common type among advisors' clients with stock compensation | 5 advisor interviews; frequency of employer tickers in existing households | Prioritize the most common type (e.g. options in tech-heavy books) |
| **H2** | Clients know their units, end year and frequency, but not exact dates or strikes | Usability test of the questionnaire with 5 clients | Lean on the stock plan statement (C1) and on extraction |
| **H3** | Concentration in the employer worries advisors more than vest taxes | Advisor interviews: rank the two problems | Bring scope 3 (taxes and events) forward |
| **H4** | "Your paycheck and your savings depend on the same company" helps the client act | Observe 3–5 advisor conversations using the new analysis | Rework the A1/A2 messages |
| **H5** | The engine can model RSU vests and their tax month by month | Session with Sherpas' engine team (open questions in the Specification) | Simplify M3–M4 to an annual approximation |

**Advisor interview guide (excerpt):** How many of your clients have stock compensation, and of what type? Where do you track it today? What was the last decision you helped a client make about company stock? What makes that conversation hard?

## 9. Process
1. **Discovery:** I walked through the whole platform (questionnaire and diagnostic) and documented what I saw, separating facts from ideas and marking unknowns.
2. **Domain:** I learned stock compensation from scratch (types, vocabulary, taxes) and kept a glossary.
3. **Framing:** symptom vs. problem, three cumulative scopes, a recommendation, and a log of every decision, including discarded ones and why.
4. **Prototyping:** the questionnaire and the diagnostic, rebuilt as clickable HTML from what I observed, with the proposal highlighted and a driving case that runs from the questionnaire to the diagnostic. Every figure is labeled with its origin: calculated, assumption, or engine output.
5. **Independent audits:** a separate AI agent with only the necessary context audited coherence twice. It found real errors, including one introduced by an earlier fix; each finding was challenged before being applied.

**How I used AI:** Claude Code as a working partner. It explored the platform, drafted documents, built the prototypes and ran the audits. I challenged each proposal and made the decisions. The working documents are in a public repository, with the prototype published encrypted: https://github.com/Onubalabs/stock-compensation-exercise
