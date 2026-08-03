# The ABCs of RBCs: An Introduction to Dynamic Macroeconomic Models Fast Reading Plan
## Goal
系统掌握从 Solow 模型到 RBC / New Keynesian 动态宏观模型的建模、稳态求解、递归表示、随机化、log-linearization、数值求解与 impulse response analysis 主线；用中文 lecture note 替代一读，并为后续代码复现和模型扩展打基础。
The goal is efficient first-pass understanding of dynamic macroeconomic model construction, not memorizing every algebraic line or Matlab command.
Default pace:

- 45-60 minutes per day
- 4-5 days per week
- Teacher-style chapter support: Chinese lecture note + concise Q&A inside each note
## Status Legend

- Not started
- Reading
- Lecture note drafted
- Q&A drafted
- Reviewed
## Reading Modes

- careful: read the chapter closely and create a full direct-reading lecture note with Q&A.
- normal: preserve the chapter's main argument and important logic, but compress supporting detail.
- skim: capture only the main contribution and keep the chapter available for reference.
## Chapter Priority Plan
| Item | Title | Source file | Printed pages | Priority | Reading mode | Est. AI-assisted time | Output needed | Status |
| --- | --- | --- | ---: | --- | --- | ---: | --- | --- |
| Intro | Introduction | `Sources/Chapters/00b_Introduction.pdf` | 1-4 | Medium | normal | 20 min | Short orientation note + concise Q&A | Not started |
| Ch01 | The Basic Solow Model | `Sources/Chapters/01_The_Basic_Solow_Model.pdf` | 7-18 | High | careful | 45-60 min | Lecture note + Q&A | Not started |
| Ch02 | Savings in an OLG Model | `Sources/Chapters/02_Savings_in_an_OLG_Model.pdf` | 19-32 | Medium | skim/normal | 35-45 min | Shorter lecture note + Q&A | Not started |
| Ch03 | Infinitely Lived Agents | `Sources/Chapters/03_Infinitely_Lived_Agents.pdf` | 33-49 | High | careful | 60 min | Lecture note + Q&A | Not started |
| Ch04 | Recursive Deterministic Models | `Sources/Chapters/04_Recursive_Deterministic_Models.pdf` | 50-68 | Very High | careful | 75-90 min | Full lecture note + Q&A | Reviewed |
| Ch05 | Recursive Stochastic Models | `Sources/Chapters/05_Recursive_Stochastic_Models.pdf` | 69-88 | Very High | careful | 75-90 min | Full lecture note + Q&A | Reviewed |
| Ch06 | Hansen’s RBC Model | `Sources/Chapters/06_Hansens_RBC_Model.pdf` | 89-145 | Very High | careful | 150-180 min | Full lecture note + Q&A; maybe split internally by section | Lecture note drafted |
| Ch07 | Linear Quadratic Dynamic Programming | `Sources/Chapters/07_Linear_Quadratic_Dynamic_Programming.pdf` | 146-182 | High | normal/careful | 90-120 min | Lecture note + Q&A | Lecture note drafted |
| Ch08 | Money: Cash in Advance | `Sources/Chapters/08_Money_Cash_in_Advance.pdf` | 183-235 | High | normal/careful | 130-160 min | Lecture note + Q&A | Lecture note drafted |
| Ch09 | Money in the Utility Function | `Sources/Chapters/09_Money_in_the_Utility_Function.pdf` | 236-257 | Medium | normal | 50-70 min | Lecture note + Q&A | Lecture note drafted |
| Ch10 | Staggered Pricing Model | `Sources/Chapters/10_Staggered_Pricing_Model.pdf` | 258-305 | High | normal/careful | 120-150 min | Lecture note + Q&A | Not started |
| Ch11 | Staggered Wage Setting | `Sources/Chapters/11_Staggered_Wage_Setting.pdf` | 306-328 | Medium | normal | 60-80 min | Lecture note + Q&A | Not started |
| Ch12 | Financial Markets and Monetary Policy | `Sources/Chapters/12_Financial_Markets_and_Monetary_Policy.pdf` | 329-369 | High | normal/careful | 110-140 min | Lecture note + Q&A | Not started |
| Ch13 | Small Open Economy Models | `Sources/Chapters/13_Small_Open_Economy_Models.pdf` | 370-410 | Medium/High | normal | 100-130 min | Lecture note + Q&A | Not started |

Total estimated AI-assisted first-pass time: roughly 18-23 hours if all chapters receive notes; roughly 10-13 hours if Chapter 2, 9, and 11 are compressed and Part Two is selective.

## Aggressive Plan

Use this only if speed matters more than retention. The main aim is to acquire the modeling skeleton and postpone most extensions.

| Session | Target | Mode | Time |
| --- | --- | --- | ---: |
| Day 1 | Introduction + Ch01 | normal/careful | 75-90 min |
| Day 2 | Ch03 | careful | 60-75 min |
| Day 3 | Ch04 | careful | 75-90 min |
| Day 4 | Ch05 | careful | 75-90 min |
| Day 5-6 | Ch06 sections 6.1-6.5 | careful | 3 hours total |
| Day 7 | Ch06 appendices + Ch07 overview | normal | 2 hours |
| Day 8 | Ch08 or Ch10 depending on interest | normal | 2 hours |
| Day 9 | Ch12 or Ch13 selected reading | normal | 2 hours |

## Comfortable Plan

This is the best plan if the goal is to actually learn the modeling technology.

| Week | Sessions | Target chapters | Focus |
| --- | --- | --- | --- |
| Week 1 | 4-5 | Intro, Ch01, skim Ch02 | Solow base model, why savings needs microfoundations, first contact with stochastic/log-linear thinking |
| Week 2 | 4-5 | Ch03, Ch04 | Infinitely lived agents, recursive deterministic dynamic programming |
| Week 3 | 4-5 | Ch05 | Stochastic recursive models, Markov chains, expectations inside Bellman equations |
| Week 4 | 4-5 | Ch06 first half | Hansen model structure, stationary state, log-linearization |
| Week 5 | 4-5 | Ch06 second half, Ch07 | Solution methods, Blanchard-Kahn, LQ dynamic programming |
| Week 6 | 4-5 | Ch08, Ch09 | Monetary RBC extensions: cash in advance and money in utility |
| Week 7 | 4-5 | Ch10, Ch11 | Nominal rigidity: staggered prices and wages |
| Week 8 | 4-5 | Ch12, Ch13 | Monetary policy, financial markets, small open economy |

Suggested daily split:

| Week | Day 1 | Day 2 | Day 3 | Day 4 | Day 5 |
| --- | --- | --- | --- | --- | --- |
| Week 1 | Intro | Ch01 §§1.1-1.3 | Ch01 §§1.4-1.6 | Ch02 skim | Review |
| Week 2 | Ch03 fixed labor | Ch03 variable labor/decentralization | Ch04 states/value function | Ch04 approximation | Review |
| Week 3 | Ch05 probability setup | Ch05 stochastic growth | Ch05 value function | Ch05 Markov chains | Review |
| Week 4 | Ch06 model setup | Ch06 log-linearization | Ch06 calibration | Ch06 variances | Review |
| Week 5 | Ch06 IRF/appendices | Ch06 Blanchard-Kahn | Ch07 LQ method | Ch07 stochastic shocks/IRF | Review |
| Week 6 | Ch08 model | Ch08 log-linear/LQ solution | Ch08 seigniorage | Ch09 | Review |
| Week 7 | Ch10 setup | Ch10 Phillips curve/log-linearization | Ch10 solution/IRF | Ch11 | Review |
| Week 8 | Ch12 working capital | Ch12 policy rules | Ch13 preliminary open economy | Ch13 closure/money | Final synthesis |

## Recommended Plan

Recommended: first treat Chapters 1, 3, 4, 5, 6, and 7 as the core sequence. Then choose Part Two based on your later project: monetary policy route = Chapters 8, 12; New Keynesian route = Chapters 8, 10, 11, 12; open-economy route = Chapter 13 after you understand Chapter 12.

Why this is the best default:

- The book is cumulative: later chapters reuse stationary states, FOCs, log-linear systems, calibration, and impulse response functions.
- Chapter 6 is the technical bottleneck; it should not be skimmed if the goal is to build or reproduce RBC/DSGE models.
- Chapter 2 is valuable but not necessary for the main representative-agent RBC sequence on first pass.
- Part Two is modular: once the solution workflow is clear, extensions can be read selectively.

Practical rule:

- High priority: complete lecture note + Q&A immediately after reading.
- Medium priority: create a shorter lecture note + concise Q&A.
- Low priority: skim unless it becomes important for another chapter.
