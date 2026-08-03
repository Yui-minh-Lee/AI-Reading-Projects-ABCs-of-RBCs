# 《The ABCs of RBCs》阅读计划

## 总目标

系统掌握从 Solow 模型到 RBC / New Keynesian 动态宏观模型的建模主线，包括稳态求解、递归表示、随机化、log-linearization、数值求解与 impulse response analysis。第一遍阅读的重点是理解模型怎样搭起来、怎样求解，而不是记住每一行代数或 Matlab 命令。

默认节奏为每天 45—60 分钟、每周 4—5 天。AI 辅助产出采用“中文叙事讲义 + 章末精简问答”的形式。

## 状态说明

- 尚未开始：还没有形成讲义。
- 阅读中：正在处理原章或补充材料。
- 讲义初稿：已经形成可读版本，但还没有完成重点核对。
- 已复核：已经进行过一轮重点审校。

## 阅读方式

- **仔细阅读（careful）：**完整处理本章，保留主要推导、逻辑桥梁和问答。
- **正常阅读（normal）：**保留核心论证和重要推理，压缩次要材料。
- **略读（skim）：**只提取本章的主要贡献，供后续查阅。

## 分章计划与进度

| 章节 | 标题 | 优先级 | 阅读方式 | AI 辅助阅读时间 | 计划产出 | 当前状态 |
| --- | --- | --- | --- | ---: | --- | --- |
| 导论 | Introduction | 中 | normal | 20 分钟 | 导读与精简问答 | 尚未开始 |
| 第 1 章 | The Basic Solow Model | 高 | careful | 45—60 分钟 | 完整讲义与问答 | 尚未开始 |
| 第 2 章 | Savings in an OLG Model | 中 | skim / normal | 35—45 分钟 | 压缩讲义与问答 | 尚未开始 |
| 第 3 章 | Infinitely Lived Agents | 高 | careful | 60 分钟 | 完整讲义与问答 | 尚未开始 |
| 第 4 章 | Recursive Deterministic Models | 很高 | careful | 75—90 分钟 | 完整讲义与问答 | 已复核 |
| 第 5 章 | Recursive Stochastic Models | 很高 | careful | 75—90 分钟 | 完整讲义与问答 | 已复核 |
| 第 6 章 | Hansen’s RBC Model | 很高 | careful | 150—180 分钟 | 完整讲义、问答与附录 | 讲义初稿 |
| 第 7 章 | Linear Quadratic Dynamic Programming | 高 | normal / careful | 90—120 分钟 | 完整讲义与问答 | 讲义初稿 |
| 第 8 章 | Money: Cash in Advance | 高 | normal / careful | 130—160 分钟 | 完整讲义与问答 | 讲义初稿 |
| 第 9 章 | Money in the Utility Function | 中 | normal | 50—70 分钟 | 讲义与问答 | 讲义初稿 |
| 第 10 章 | Staggered Pricing Model | 高 | normal / careful | 120—150 分钟 | 完整讲义与问答 | 讲义初稿 |
| 第 11 章 | Staggered Wage Setting | 中 | normal | 60—80 分钟 | 讲义与问答 | 讲义初稿 |
| 第 12 章 | Financial Markets and Monetary Policy | 高 | normal / careful | 110—140 分钟 | 完整讲义与问答 | 讲义初稿 |
| 第 13 章 | Small Open Economy Models | 中高 | normal | 100—130 分钟 | 讲义与问答 | 讲义初稿 |

如果所有章节都形成讲义，预计第一遍 AI 辅助阅读需要约 18—23 小时；如果压缩第 2、9、11 章，并选择性阅读第二部分，预计约 10—13 小时。这是计划值，不是对实际效率提升的测量结果。

## 推荐顺序

第一遍先把第 1、3、4、5、6、7 章连成一条主线。它们依次解决基础增长模型、家庭最优化、递归表示、随机环境、标准 RBC 与数值求解问题。第 6 章是全书的技术瓶颈，如果目标是复现或扩展 RBC / DSGE 模型，不应略读。

掌握技术主线后，再根据后续方向选择第二部分：

- 货币与政策：第 8、12 章。
- New Keynesian：第 8、10、11、12 章。
- 开放经济：理解第 12 章后进入第 13 章。
- OLG：如果研究问题涉及代际结构，再回到第 2 章仔细处理。

## 八周参考安排

| 周次 | 主要内容 | 本周重点 |
| --- | --- | --- |
| 第 1 周 | 导论、第 1 章，略读第 2 章 | Solow 基础结构，以及为什么需要储蓄的微观基础 |
| 第 2 周 | 第 3、4 章 | 无限期家庭与确定性递归方法 |
| 第 3 周 | 第 5 章 | 随机递归模型、Markov chain 与条件期望 |
| 第 4 周 | 第 6 章上半 | Hansen 模型、稳态与 log-linearization |
| 第 5 周 | 第 6 章下半、第 7 章 | calibration、求解、IRF 与 LQ 动态规划 |
| 第 6 周 | 第 8、9 章 | cash-in-advance 与 money in utility |
| 第 7 周 | 第 10、11 章 | 交错价格、交错工资与名义刚性 |
| 第 8 周 | 第 12、13 章 | 政策规则、金融市场和开放经济 |

## 当前执行重点

1. 复核第 6 章，尤其是非线性均衡条件、稳态、线性系统与政策函数之间的衔接。
2. 复核第 7 章，并把 LQ 方法与第 6 章的 log-linear / Schur 求解联系起来。
3. 补齐第 1—3 章，完成从 Solow 到递归 RBC 的前置主线。
4. 在复核扩展章节时，优先检查公式、矩阵和图表引用；文本提取不可靠的部分必须回原书确认。
