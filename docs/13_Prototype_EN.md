# Prototype

## What it is
Two Sherpas screens with the proposal built in, on an example case: **John & Jane Doe**. John works at Acme, holds **$500K of Acme stock** and has **2,000 unvested RSUs**.
- **Part 1, the questionnaire:** where stock compensation is captured.
- **Part 2, the diagnostic:** what the advisor sees as a result.

**How to open it:** [open the prototype](https://onubalabs.github.io/stock-compensation-exercise/prototype/index.html) and enter the password given on the Notion page. It is encrypted because it reproduces confidential screens. Works best on a desktop browser.

## Suggested walkthrough (5 minutes)
| Step | Where | What to look at |
|---|---|---|
| 1 | Questionnaire → **3 · Income** | The employer of each person, "Do you get company stock through work?" and the RSU row with its value |
| 2 | Questionnaire → **4 · Investments** | The "Stock plan account", the Acme holdings tagged "Your employer", and the summary: **$500K across 2 accounts** |
| 3 | Questionnaire → **Envío** (submit) | The link to Part 2 |
| 4 | Diagnostic → **Financial health** | Net worth with the RSUs kept apart, the Acme path if nothing changes and, in the score's **View more**, the **Investing** area |
| 5 | Diagnostic → **Investment analysis** and **Statements** | Total exposure to Acme, the recommendation to diversify, a 40% drop in Acme, and the RSUs in the balance sheet and cash flow |

## The buttons
- **Datos de entrada** (input data): the case data that produces the diagnostic.
- **Hoy / Propuesta** (today / proposal): compares the current platform with the proposal.
- **Notas** (notes): shows or hides the explanations.

## How to read it
- **Amber highlight = new.** Each item has a code: C = capture, A = analysis.
- **Amber notes** explain each new item; **grey text** describes what already exists.
- **Next to each diagnostic figure**, an icon shows its origin: ↻ calculated by us · S an assumption · ❓ output of Sherpas' engine, shown with the demo value · ✎ demo text with figures adapted to the case.
- **Hover any icon or button** to see what it means.

## What it doesn't do
- **The diagnostic is not recalculated.** It always shows the result of the case, even if you change the questionnaire.
- **Only the sections with changes can be edited:** Documents, Income and Investments (amber tabs).
- **It is not the real interface:** it reproduces what we observed; companies and prices are fictional. The prototype notes are in Spanish.

## The case behind the diagnostic
**The household (from the demo):** John (40) and Jane (38), three children. Salaries of $195K and $120K, and $24K a year of rental income. Checking $150K; a joint brokerage with VTI $450K and AGG $250K; 401(k)s of $80K and $60K. A $600K home with a $125K mortgage, a $350K rental property, cars, a card balance and a student loan.

**Stock compensation (our hypothesis):**
- John works at **Acme** ($150); Jane at Bluerock Pharma, with no stock compensation.
- **$500K of Acme stock:** $400K in a stock plan account and $100K in the brokerage.
- **2,000 unvested RSUs** (≈ $300K), vesting quarterly through 2029.
- No options or private-company equity.

**Calculation assumptions:** Acme at a constant $150 · ≈ 154 RSUs per quarter, Dec 2026 – Dec 2029 · tax at vest ≈ 36% (illustrative) · stress test: a 40% drop.

**Result:** net worth **$2.37M** (with the RSUs kept apart) · total investments **$1.49M**: Acme 34%, VTI 30%.

**What we can't recalculate:** the score and its areas, projections, the retirement gap, taxes, the Investment analysis and the narrative texts come from Sherpas' engine. They show the demo values, marked ❓. Each one is an open question for Sherpas (see the Specification).
