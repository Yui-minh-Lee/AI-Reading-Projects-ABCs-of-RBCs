# The ABCs of RBCs — AI-Assisted Reading Project

This repository is an AI-assisted direct-reading lecture-note project for George McCandless's *The ABCs of RBCs: An Introduction to Dynamic Macroeconomic Models*.

The goal is to turn the book into Chinese narrative lecture notes that preserve the main economic logic, model-building steps, and key mathematical derivations while reducing first-pass reading friction. It also serves as a portfolio example of a structured human-AI reading workflow: source-grounded chapter processing, reusable prompts, narrative technical notes, visual checks, and iterative review.

> Copyright note: the original book, chapter PDFs, and extracted book figures are intentionally excluded from this public repository. The repository contains original study notes and workflow files only.

## Current status

- Book metadata and project-specific agent instructions are in place.
- The source PDFs and extracted book figures are kept locally and excluded by `.gitignore`.
- Lecture notes cover recursive methods, the RBC model, monetary models, nominal rigidities, monetary policy, and small open economy models.
- Ch04 and Ch05 have been read and reviewed.
- Additional technical notes cover calibration, Schur methods, transversality conditions, and stochastic RBC log-linearization.

## Repository structure

- `AGENTS.md`: customized instructions that define the AI reading-teacher workflow.
- `BOOK_INFO.md`: metadata, reading objective, technical depth, and conventions.
- `Home.md`: lightweight reading dashboard.
- `Plan.md`: reading schedule and chapter status.
- `Sources/`: local source PDFs (not included in the public repository).
- `ChapterNotes/`: Chinese narrative lecture notes and technical supplements.
- `Reviews/`: initialization report, review notes, and cross-chapter synthesis.
- `Figures/`: local visual references extracted from the source (not included in the public repository).
- `Prompts/`: reusable prompts for generation, review, and clarification.

## Example agent instruction

```text
请参照 AGENTS.md 的规则，处理 Sources/Chapters/01_The_Basic_Solow_Model.pdf，生成 ChapterNotes/01_The_Basic_Solow_Model.md。注意这一章是后续 RBC 模型的起点，请保留核心公式推导，并用中文讲清楚 log-linearization 的直觉。
```

For the technical core, the recommended reading order is:

1. `01_The_Basic_Solow_Model.pdf`
2. `03_Infinitely_Lived_Agents.pdf`
3. `04_Recursive_Deterministic_Models.pdf` — reviewed
4. `05_Recursive_Stochastic_Models.pdf` — reviewed
5. `06_Hansens_RBC_Model.pdf`
6. `07_Linear_Quadratic_Dynamic_Programming.pdf`

Chapter 2 can be skimmed first unless overlapping generations models are important for the immediate goal.
