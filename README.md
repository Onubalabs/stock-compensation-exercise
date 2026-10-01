# Stock compensation · Product Builder exercise

Alejandro Moreno's answer to the exercise *"How would you integrate stock compensation into the platform?"*.

**Start with the Notion page:** it is the main deliverable, with the problem, the scope, the functional design, the specification, the launch kit and the process. This repository is the annex: the prototype and the working documents that show **how** we got there.

## Prototype
**[Open the prototype](https://onubalabs.github.io/stock-compensation-exercise/prototype/index.html)**: a clickable reproduction of the questionnaire and the diagnostic with the proposal built in.
- It reproduces confidential screens, so it is **encrypted**. The password is on the Notion page.
- How to use it: [Prototype guide](docs/13_Prototype_EN.md).

## What to read
| Document | What it shows | Language |
|---|---|---|
| [Specification](docs/10_Specification.md) | 45 acceptance criteria, states, edge cases and open questions | English |
| [Launch kit](docs/11_Launch_kit.md) | Release notes and the advisor guide | English |
| [Notion page source](docs/12_Notion_main.md) · [Prototype page](docs/13_Prototype_EN.md) | The same content as Notion | English |
| [How we worked with AI](docs/14_AI_workflow.md) | Working agreements, where AI was used, what it got wrong | English |
| [Independent audits](docs/15_Audits.md) · [The Validator agent](.claude/agents/validador.md) | Two audits by a separate AI agent, and how each finding was challenged | English · Spanish |
| [Work in progress](docs/07_Trabajo_en_curso.md) | **The working document:** problem, scope, functional design and the log of every decision, including the ones replaced and why | Spanish |
| [Driving case](docs/08_Caso_conductor.md) | Every input of the prototype, where it comes from, the assumptions, the derived figures and what can't be recalculated | Spanish |
| [Prototype guide (working version)](docs/09_Guia_del_prototipo.md) · [Glossary](docs/06_Glosario.md) · [Domain training](docs/04_Formacion_stock_compensation.md) | How the domain was learned from scratch | Spanish |

## What is not included, and why
Sherpas asked that everything seen inside the platform stay confidential. So this repository **does not include** the inventory of the observed platform, the screenshots, or the prototype's source code; the prototype is published encrypted. The working documents were cleaned on export: references to the internal inventory were removed, and the outputs of Sherpas' engine for the demo household are not shown.

## Notation
- Paths like `prototipo/` or `caso.js` in the working documents refer to the private working copy; the published prototype is in `prototype/`, encrypted.
- **C1–C10** capture, **M1–M7** modeling, **A1–A6** analysis: the same codes in the documents and in the prototype.
- **❓** unknown: not observed, or depends on Sherpas' engine.
- **[HC]**: the Help Center article on the score, included in the exercise brief.
