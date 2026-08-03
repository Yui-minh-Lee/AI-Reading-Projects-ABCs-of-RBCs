# The ABCs of RBCs: An Introduction to Dynamic Macroeconomic Models Reading Dashboard

## Current status

- Current chapter: Ch06 — Hansen's RBC Model
- Current focus: Ch04 and Ch05 have been read and reviewed; next step is the Hansen RBC model, especially stationary state, log-linearization, calibration, second moments, and impulse responses.
- Last updated: 2026-06-18

## Reading goal

系统掌握从 Solow 模型到 RBC / New Keynesian 动态宏观模型的建模、稳态求解、递归表示、随机化、log-linearization、数值求解与 impulse response analysis 主线；用中文 lecture note 替代一读，并为后续代码复现和模型扩展打基础。

## Main files

- [[BOOK_INFO]]: project metadata, reading goal, conventions, chapter priority assumptions.
- [[Plan]]: chapter-by-chapter reading plan and suggested schedules.
- `Sources/Full/`: full original PDF.
- `Sources/Chapters/`: generated chapter-level source PDFs.
- `ChapterNotes/`: final Chinese narrative lecture notes, to be generated chapter by chapter.
- `Q&A/`: optional separate Q&A files, normally not used because Q&A should be embedded in chapter notes.
- `Reviews/`: initialization report, later weekly reviews and cross-chapter syntheses.
- `Figures/`: optional source screenshots or self-drawn figures, only when explicitly requested.

## Core concept map

```text
Solow growth model
  -> endogenous saving: OLG and infinitely lived agents
  -> recursive representation: states, controls, Bellman equation
  -> stochastic recursive models: expectation and Markov chains
  -> Hansen RBC model: labor, technology shock, calibration, log-linearization
  -> solution methods: Blanchard-Kahn / generalized Schur and LQ dynamic programming
  -> extensions:
       money: cash-in-advance / money in utility / seigniorage
       nominal rigidity: staggered prices and wages
       monetary policy and finance: working capital, Taylor rule, Friedman rule
       open economy: foreign asset, closure, exchange rate dynamics
```

## Suggested reading strategy

Start with the Introduction and Chapter 1 to understand what problem the book is solving. Then treat Chapters 3-7 as the technical core. Chapter 2 is useful background but can be skimmed on first pass. After Chapter 7, choose Part Two chapters according to interest: monetary models begin at Chapter 8, nominal rigidity at Chapters 10-11, policy rules at Chapter 12, and open-economy modeling at Chapter 13.

## Next actions

1. Read/review `ChapterNotes/06_Hansens_RBC_Model.md` carefully; this is the main bottleneck for building baseline RBC/DSGE models.
2. Pay special attention to the transition from nonlinear equilibrium conditions to the log-linear system and policy matrices.
3. After Ch06, review `ChapterNotes/07_Linear_Quadratic_Dynamic_Programming.md` as an alternative solution language.
4. For the VAT research direction, keep Ch06 as the baseline modeling template and add tax wedges only after the baseline mechanism is clear.
