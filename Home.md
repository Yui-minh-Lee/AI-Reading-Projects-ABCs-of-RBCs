# 《The ABCs of RBCs》阅读看板

## 当前进度

- 已完成讲义：第 4—13 章
- 已重点复核：第 4、5 章
- 技术专题：calibration、Schur 方法、横截条件（TVC）、随机 RBC 的 log-linearization、动态宏观数学知识路线图
- 后续重点：继续复核第 6 章 Hansen RBC 模型，并补齐第 1—3 章
- 最近更新：2026-08-03

## 阅读目标

系统掌握从 Solow 模型到 RBC / New Keynesian 动态宏观模型的建模主线，包括稳态求解、递归表示、随机化、log-linearization、数值求解和 impulse response analysis。中文讲义用于降低第一遍阅读门槛，之后再回到原书与代码处理重点问题。

## 主要入口

- [`README.md`](README.md)：项目介绍，以及 AI 在整个阅读流程中的作用。
- [`BOOK_INFO.md`](BOOK_INFO.md)：书目信息、阅读目标和讲义标准。
- [`Plan.md`](Plan.md)：分章优先级、建议顺序和当前状态。
- [`ChapterNotes/`](ChapterNotes/)：已经形成的分章讲义与技术专题。
- [`Prompts/`](Prompts/)：生成、审校和澄清讲义时使用的 Prompt。
- [`Reviews/`](Reviews/)：初始化记录与阶段性复盘。

`Sources/` 与 `Figures/` 只保留在本地，不进入公开仓库。

## 知识主线

```text
Solow 增长模型
  → 储蓄内生化：OLG 与无限期生存家庭
  → 递归表示：状态、控制、Bellman equation
  → 随机递归模型：条件期望与 Markov chain
  → Hansen RBC：劳动、技术冲击、calibration、log-linearization
  → 求解方法：Blanchard–Kahn / generalized Schur 与 LQ 动态规划
  → 模型扩展：
       货币：cash-in-advance / money in utility / seigniorage
       名义刚性：交错价格与交错工资
       货币政策和金融：营运资金、Taylor rule、Friedman rule
       开放经济：国外资产、闭合条件、汇率动态
```

## 建议阅读顺序

先通过第 1 章掌握 Solow 模型的基础结构，再把第 3—7 章作为技术主线。第 2 章提供 OLG 背景，第一遍可以略读。掌握第 7 章后，第二部分可以按兴趣选择：第 8 章进入货币模型，第 10—11 章处理名义刚性，第 12 章讨论金融市场与政策规则，第 13 章扩展到开放经济。

## 下一步

1. 仔细复核 `ChapterNotes/06_Hansens_RBC_Model.md`，重点检查稳态、log-linearization、calibration、二阶矩和 impulse response。
2. 对照原书检查从非线性均衡条件到线性系统与政策矩阵的过渡。
3. 复核 `ChapterNotes/07_Linear_Quadratic_Dynamic_Programming.md`，理解另一套求解语言。
4. 补齐第 1—3 章，使 Solow、OLG、无限期家庭与后续 RBC 主线完整衔接。
