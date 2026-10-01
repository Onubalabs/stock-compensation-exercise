# Stock compensation · Launch kit

Two pieces for launch day: the **release notes** (what's new) and the **advisor guide** (how to use it with clients). Examples use the John & Jane Doe case.

---

## Part 1 · Release notes

### Sherpas now understands stock compensation

Many of your clients are paid partly in company stock. Until now, the Financial Health diagnostic saw those shares as just another holding, and did not see unvested RSUs at all. The biggest risk for these clients was invisible: **their savings and their salary depend on the same company.**

**What's new**
- **The questionnaire asks who each client works for** and lets them add unvested RSUs (units, end year, frequency) and a new "Stock plan account" type.
- **Employer stock is detected automatically** in every account and added up. *John holds $400K of Acme in his stock plan and $100K in his brokerage: neither looks big alone, but together they are his largest exposure, at $500K.*
- **The score's concentration check now sees the total employer exposure**, not just the largest single position. Clients without employer stock score exactly as before.
- **New analysis for you and your client:** total employer exposure, a stress test if the employer's stock falls 40%, the path of the position if nothing changes, and a recommendation to diversify in stages.
- **Unvested RSUs are shown, but kept out of net worth:** they are not the client's yet.

**Not included yet**
- Stock options and private-company equity are **flagged, not valued**: the diagnostic warns that real exposure may be higher.
- Tax planning: the tax cost of selling, the withholding gap, ISO/AMT and vesting-event alerts.
- Company stock held as a fund inside a 401(k) without a ticker is not detected.

---

## Part 2 · Advisor guide

### When you'll see it
Only for clients who hold their employer's stock or have unvested RSUs. Nothing changes for everyone else.

### How to read it
| Where | What it tells you |
|---|---|
| **Investment analysis › Concentrated stock risk** (A1) | Total exposure to the employer, split by account, plus unvested RSUs and the salary at stake. Start here |
| **Investment analysis › If the stock falls 40%** (A2) | What the client could lose at once: shares, unvested RSUs and income. Illustrative, not a forecast |
| **Retirement & Goals › Exposure if nothing changes** (A3) | How the position grows as RSUs vest if the client keeps every share |
| **What we're recommending › Diversify as it vests** (A4) | The suggested path: sell new shares as they vest, then trim in stages |
| **Score › View more › Investing and Liquidity** (A5) | Why the employer weighs on the score, and why the shares don't count as an emergency reserve |
| **Net worth, Assets, Statements** (A6) | Employer stock shown as its own line; unvested RSUs shown apart from net worth |

### Three messages for the client conversation
1. **"Your largest investment is your employer."** *"About a third of your investments, $500K, is in Acme, across two accounts. Each account looks reasonable on its own; together, it's your largest single bet."*
2. **"Your paycheck and your savings are tied to the same company."** *"If Acme had a bad year, you could lose part of your shares, part of your unvested RSUs and possibly your job at the same time. That's why we look at it differently from any other stock."*
3. **"A plan, not a fire sale."** *"We're not suggesting you sell everything. Start by selling new shares as they vest so the position stops growing, then reduce it in stages, with an eye on taxes."*

### FAQ
**Why aren't unvested RSUs in my client's net worth?**
They aren't the client's yet: they are lost if the client leaves the company. We show them separately and add them as they vest.

**Why does the employer's stock count differently from other stocks?**
Because the client's salary depends on the same company. With the same amount invested, being concentrated in your employer never scores better than being concentrated in another company.

**My client has stock options or works for a startup. What happens?**
The client answers that they have them, and the diagnostic warns that they are not included and that real exposure may be higher. Review them with the client directly.

**Are the tax figures exact?**
Taxes at vest are estimated by the planning engine, like any other income. The tax cost of selling depends on how each share was acquired and is not calculated: check it before recommending a sale.

**The client's employer or holdings look wrong. Can I fix them?**
Yes. You can edit the employer, the RSUs and the tagged holdings like any other client data. Clients can also remove the "Your employer" tag from a holding that isn't really employer stock.
