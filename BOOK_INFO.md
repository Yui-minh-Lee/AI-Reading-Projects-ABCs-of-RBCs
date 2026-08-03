# 书目信息与学习目标

## 基本信息

- 书名：*The ABCs of RBCs: An Introduction to Dynamic Macroeconomic Models*
- 作者：George McCandless
- 领域：宏观经济学、真实经济周期（RBC）、动态随机一般均衡模型（DSGE）、New Keynesian 模型
- 版本：Harvard University Press，2008
- 本地原书位置：`Sources/Full/The ABCs of RBCs  An Introduction to Dynamic Macroeconomic Models.pdf`
- 本地分章材料：`Sources/Chapters/`

原书和分章材料只用于个人学习，不纳入公开仓库。

## 我的学习目标

我希望系统掌握从 Solow 模型到 RBC / New Keynesian 动态宏观模型的建模主线，包括稳态求解、递归表示、随机化、log-linearization、数值求解和 impulse response analysis，并为后续代码复现与模型扩展打基础。

这个项目不是为了快速浏览一本通识书，而是要把教材转化为一套能够反复查阅的中文课程讲义。笔记需要回答的不只是“作者得出了什么结论”，还包括模型为什么这样设定、FOC 和稳态如何推导、线性化为什么这样变形，以及数值方法究竟在求什么。

## 讲义标准

- 以连贯的中文课堂讲解为主，不写成零散提纲。
- 保留重要英文术语，例如 representative agent、Bellman equation、value function、policy function、stationary state、log-linearization、calibration、impulse response function、cash-in-advance、Calvo pricing 和 Taylor rule。
- 正文是每章的主体，先讲经济含义，再进入代数推导，推导完成后再解释结果。
- 目标是保留原章约 80%—90% 的核心学习价值；第 4—8、10、12 章属于方法和建模重点，应更接近 85%—90%。
- 在不损害关键逻辑的前提下，争取把第一遍阅读时间缩短约 40%—60%。
- 不跳过非显然的推理步骤，也不反复解释已经清楚的术语。
- 原书出现较长 Matlab 代码时，默认解释代码解决的问题、对应的方程和数值逻辑，不整段照搬。

## 阅读参数

- 每天投入：45—60 分钟
- 每周频率：4—5 天
- 建议完成周期：6—8 周，可按实际情况调整
- 第一遍深度：第一部分仔细阅读；第二部分按研究兴趣选择 normal 或 careful
- 技术深度：研究生宏观 / 数量宏观入门到中阶
- 低优先级章节：第一遍可以略读第 2 章；扩展章节可按当前研究方向取舍

## 需要重点掌握的内容

- Solow 模型如何成为后续 RBC 模型的基础结构。
- 内生储蓄与代表性家庭的微观基础。
- 递归表示中的状态变量、控制变量、价值函数和政策函数。
- 随机动态规划、条件期望与 Markov chain。
- Hansen RBC 模型、可分与不可分劳动、log-linearization 和 Blanchard–Kahn 求解逻辑。
- 线性二次动态规划（LQ Dynamic Programming）与对数线性方法之间的关系。
- 货币扩展：cash-in-advance、money in utility 和 seigniorage。
- 名义刚性：交错定价、交错工资与 Calvo 类机制。
- 货币政策规则、金融市场和小型开放经济的闭合方式。

## 章节优先级

- 核心方法：第 1、3、4、5、6、7 章。
- 主要扩展：第 8、10、12、13 章。
- 第一遍可压缩：第 2 章；如果货币效用或工资刚性不是当前重点，第 9、11 章也可正常阅读或略读。

每章问答默认直接放在讲义末尾，不单独建立 Q&A 文件。涉及模拟结果、价值函数、政策函数、脉冲响应、稳态方程、矩阵系统和广义 Schur 条件时，应格外重视原文核对；如果 PDF 文本不足以可靠还原图表或公式，必须明确标记不确定性。
