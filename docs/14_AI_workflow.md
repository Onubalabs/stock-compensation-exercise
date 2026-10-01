# How we worked with AI

The exercise was done by Alejandro Moreno with **Claude Code** (Anthropic) as a working partner. AI did the exploring, drafting, building and checking; **every decision was Alejandro's**, after challenging the proposal.

## Working agreements
These were set at the start and written into the project instructions that Claude reads every session:
- **Reason step by step, together.** For every decision, Claude proposes options with a recommendation; Alejandro challenges it and decides. Nothing is written as final without his validation.
- **Facts and ideas are kept apart.** What was observed on the platform goes in one document, with the source of each fact. Interpretations and ideas go in another. Anything unknown is marked ❓ instead of inferred.
- **Every decision is logged** with its date and reason, including the ones that were later replaced (document 07, section 7).
- **Every term Alejandro asked about goes into a glossary** (document 06), explained from scratch, because he had no prior fintech experience.
- **Working documents in Spanish, deliverables in English.**

## Where AI was used
| Phase | What Claude did | What Alejandro did |
|---|---|---|
| **Discovery** | Walked through the questionnaire and the diagnostic in the browser and documented every screen, with sources and unknowns | Filled in the questionnaire, checked what Claude couldn't see, and set the rules on confidentiality |
| **Domain** | Explained stock compensation from zero (types, vocabulary, taxes) and built the glossary | Asked, challenged, and chose what mattered |
| **Framing** | Proposed readings of the brief, the problem and three scopes | Rejected weak options ("these are filler, not real alternatives") and chose the scope |
| **Design** | Drafted capture (C1–C10), modeling (M1–M7) and analysis (A1–A6) with options and trade-offs | Validated or changed each block; several of his challenges changed the design |
| **Prototyping** | Rebuilt the questionnaire and the diagnostic as clickable HTML from what was observed, on one driving case | Reviewed it screen by screen and asked for changes (e.g. one fixed case instead of live recalculation) |
| **Verification** | Ran automated checks in a headless browser: every screen, in both modes, with every figure compared against the case data | Decided which findings to fix |
| **Independent audit** | A **separate agent** (the *Validator*) audited the work with only the context it needed | Decided which findings to apply |
| **Deliverables** | Wrote the specification, the launch kit and the Notion page, and published it through the browser | Set the structure, the language and the order |

## The Validator: an independent check
An AI that audits its own work tends to confirm it. So the audits were done by a **second agent** with:
- **A different model** (Claude Fable 5.1).
- **Only the context it needs:** what to read, what not to read, how to run the prototype and how to report. None of our conclusions.
- **Read-only access:** it can't change anything.

Its definition is in `.claude/agents/validador.md`. It ran three audits (coherence, the specification, and confidentiality before publishing this repository). Each report was **challenged before being applied**, and every finding not applied has a stated reason (document 15).

## What AI got wrong, and how it was caught
- **A wrong percentage:** the stress test said Acme would be "13% of investable assets" after a 40% drop. Claude caught it while checking every figure against the case data; it is 23%.
- **A bug introduced by a fix:** an allocation shown as "119% / −19%". It came from a correction made in the previous round, and was caught by the Validator, not by the self-check.
- **A design inconsistency:** after reassigning an employer, the prototype moved John's RSUs to Jane. The Validator found it by testing a case outside the driving case.

The lesson that shaped the process: **AI is fast at producing and checking, but it needs a second, independent look and a human who decides.**

## Confidentiality guardrails
- Before this repository was published, the Validator audited it for confidentiality and found **two leaks that would have been published** (figures produced by Sherpas' engine for the demo household). They were removed, together with literal quotes and descriptions of platform defects.
- Nothing seen inside the platform is published in readable form: the platform inventory isn't included, and the prototype (which reproduces confidential screens) is published **encrypted**.
- Every export of the documents runs a filter that stops if any forbidden term or figure remains.
- Internal sources that were off-limits for the deliverable were never cited.
