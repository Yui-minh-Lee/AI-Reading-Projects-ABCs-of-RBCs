# Book Information

## Basic Information

- Title: The ABCs of RBCs: An Introduction to Dynamic Macroeconomic Models
- Author: George McCandless
- Field / Topic: 宏观经济学、Real Business Cycle (RBC)、动态随机一般均衡模型（DSGE）、New Keynesian 模型
- Edition / Year: Harvard University Press, 2008
- Source file location: `Sources/Full/The ABCs of RBCs  An Introduction to Dynamic Macroeconomic Models.pdf`
- Chapter source folder: `Sources/Chapters/`

## My Reading Goal

系统掌握从 Solow 模型到 RBC / New Keynesian 动态宏观模型的建模、稳态求解、递归表示、随机化、log-linearization、数值求解与 impulse response analysis 主线；用中文 lecture note 替代一读，并为后续代码复现和模型扩展打基础。

本项目的主要目标不是快速浏览一本通识书，而是把它转化为一套可以反复回看的中文课程讲义。读书笔记需要帮助读者理解每个模型为什么这样写、每一步稳态/一阶条件/线性化为什么这样变形、数值求解到底在解决什么问题。

## Desired Note Style

Default:

- Chinese narrative lecture note.
- Preserve important English terms, especially RBC, DSGE, representative agent, overlapping generations, Bellman equation, value function, policy function, stationary state, log-linearization, calibration, impulse response function, cash-in-advance, Calvo pricing, Taylor rule, small open economy.
- Main Lecture should be the largest section.
- Preserve 80-90% of core learning value. For Chapters 4-8, 10, 12, preserve closer to 85-90% because these are method/model-building chapters.
- Reduce first-pass reading time by 40-60% where feasible.
- Do not hide non-obvious reasoning.
- Explain technical terms selectively, not repeatedly.
- For mathematical derivations, explain the economic meaning before and after the algebra.
- When the source gives Matlab code, do not reproduce long code blocks by default; summarize what the code is solving and which equations it implements.

## Reading Parameters

- Reading time per day: default 45-60 minutes
- Days per week: default 4-5 days
- Target finish date: flexible; recommended first-pass project length 6-8 weeks
- First-pass depth: Part One careful; Part Two selective normal/careful depending on interest
- Desired technical depth: 研究生宏观/数量宏观入门到中阶：保留关键数学推导、FOC、Bellman equation、stationary state、log-linear system、calibration 与 Matlab/数值解法逻辑，但用老师式中文讲清主线。
- Whether low-priority chapters should be skim-only: yes, especially Chapter 2 on first pass and some extension chapters if the immediate goal is core RBC mechanics

## Special Instructions for This Book

- Concepts to pay special attention to:
  - Solow model as the base structure for later RBC models.
  - Endogenous saving and representative-agent foundations.
  - Recursive formulation: state, control, value function, policy function.
  - Stochastic dynamic programming and Markov chains.
  - Hansen's RBC model, divisible vs indivisible labor, log-linearization, and Blanchard-Kahn solution logic.
  - Linear Quadratic Dynamic Programming and its relationship to log-linear methods.
  - Monetary extensions: cash-in-advance, money-in-utility, seigniorage.
  - Nominal rigidity: staggered pricing/wage setting and Calvo-style mechanisms.
  - Monetary policy rules, financial markets, and small open economy closure.
- Chapters likely to be important:
  - Core methods: Chapters 1, 3, 4, 5, 6, 7.
  - Main extensions: Chapters 8, 10, 12, 13.
- Chapters likely to skim:
  - Chapter 2 can be skimmed on first pass if the immediate goal is standard representative-agent RBC modeling.
  - Chapter 9 and Chapter 11 can be normal/skim unless monetary utility or wage rigidity is central to the user's later project.
- Whether Q&A should be included inside each note: yes.
- Whether separate Q&A files are ever needed: only if explicitly requested.
- Figures, tables, or formulas that require special care:
  - All figures showing simulations, value functions, policy functions, impulse response functions, and log-linearized systems should be marked for original-check if not embedded.
  - Equations defining stationary states, first-order conditions, Bellman equations, matrix systems, and Blanchard-Kahn / generalized Schur solution conditions require especially careful treatment.
