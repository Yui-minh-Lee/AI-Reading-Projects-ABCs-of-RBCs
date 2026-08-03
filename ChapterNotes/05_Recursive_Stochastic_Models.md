# Chapter 5 — Lecture Note

> Importance: ★★★★★  
> Suggested audit model: xhigh  
> Reading mode: careful  
> Estimated note reading time: 55-70 minutes  
> Source reliability: text OK; important figures embedded as source screenshots; formulas involving PDF symbols should still be checked against the original when used for coding

## 0. How to read this note

这一章是从确定性递归模型走向 RBC / DSGE 的关键过渡章。前面几章的核心对象是：给定初始资本和确定性环境，经济沿着一条最优路径演化。本章开始，经济不再只有一条确定路径，而是在每一期受到随机状态（state of nature）的影响。读这章时，不要把随机性理解成“模型突然变复杂了很多”，而应该抓住一个主线：**随机冲击进入递归模型后，本质上只是把随机状态也放进 state vector，并把未来 value function 用 probability-weighted expectation 来替代确定性的下一期 value function。**

换句话说，确定性 Bellman equation 中的“明天的价值”现在变成“明天各种可能状态下价值的期望”。如果随机状态是有限维的，比如技术只有好天气和坏天气两种状态，那么我们可以像第 4 章那样用 value function iteration，只是要为每一种技术状态分别迭代一条 value function 和一条 policy function。作者把这种依赖未来随机状态的 policy function 称为 plan，因为它不是一条单一路径，而是“如果明天发生状态 1 就怎样、发生状态 2 就怎样”的 contingent plan。

本章的第二个重点是 Markov chain。独立同分布冲击会产生随机波动，但通常不容易产生宏观时间序列中的 persistence。Markov chain 允许当前状态影响下一期状态的概率，因此可以让好状态或坏状态连续出现。但作者也提醒：用 Markov chain 可以把 persistence 做出来，却不等于解释了 persistence 的经济机制。

## 1. Opening: 本章的核心问题

前面的模型大多是 deterministic models：参数、函数形式和状态演化都确定，只要给出初始资本，经济的路径就被模型完全规定。但真实经济中的产出、消费、投资和资本积累显然不会沿着一条完全确定的路径前进。模型预测不能完全命中现实，原因可以有两类。

第一类原因是模型没有包括所有相关变量。比如 Robinson Crusoe 模型可以解释储蓄、劳动和资本如何影响产出，却没有把天气、健康状况、偶然得到一本农业书之类的因素放进模型。我们知道自己不可能把所有现实细节都建进去，于是可以把遗漏因素压缩成一个随机项，让“nature”在每一期决定某些参数或状态的取值。

第二类原因更深：世界本身也许就是随机的。作者没有在哲学上争论这一点，而是采取经济建模中的实用态度：无论随机性来自遗漏变量还是来自世界本身，把一部分无法建模的因素写成概率过程，往往能让模型生成的时间序列更接近数据。

因此，本章的核心问题是：**如何把随机冲击放进递归动态模型，并继续用 Bellman equation、value function、policy function / plan 和 simulation 来求解与理解模型？**

## 2. Main Lecture

### 2.1 概率空间：为什么要先讲 probability space

作者先用一点篇幅定义概率空间（probability space）。一个概率空间通常写成 $(\Omega, \mathcal{F}, P)$。其中 $\Omega$ 是所有可能状态的集合；$\mathcal{F}$ 是由这些状态构成的一些事件集合；$P$ 是给这些事件赋予概率的 probability measure。

如果状态是有限个，直觉很简单。假设技术只有两个可能值 $A_1$ 和 $A_2$，那么状态集合可以写成 $\Omega=\{A_1,A_2\}$。事件包括空集、只发生 $A_1$、只发生 $A_2$、以及一定发生 $A_1$ 或 $A_2$ 的全集。概率测度给空集赋值 0，给全集赋值 1，给 $A_1$ 赋值 $p_1$，给 $A_2$ 赋值 $p_2=1-p_1$。在有限状态并且底层事件相互独立时，我们通常可以直接说“状态 $A_1$ 的概率是 $p_1$，状态 $A_2$ 的概率是 $p_2$”，不用太纠结 $\mathcal{F}$ 的形式。

但当状态是连续变量时，事件集合就变得重要。假设技术 $A_t$ 可以取 $[0.9,1.2]$ 上任意值，并且服从 uniform distribution。此时“$A_t$ 恰好等于 1.15565”的概率是 0，但“$A_t$ 落在 $[0.97,1.03]$ 区间内”的概率可以是正的，例如区间长度 $0.06$ 除以总长度 $0.3$，得到 20%。这说明概率并不总是自然地定义在“单个点”上，而是定义在状态集合的子集，也就是事件上。

本章后面的模型主要使用有限个状态，所以技术上不复杂。但这个概率空间的铺垫很重要：在 stochastic Bellman equation 里，未来价值要对未来状态集合求 expectation，而 expectation 本质上就是用概率测度对不同状态加权。

### 2.2 一个简单的随机增长模型：随机性如何进入 Bellman equation

作者从一个最小化的 stochastic growth model 开始。经济和无限期 Robinson Crusoe 模型类似，但生产函数多了一个随机技术项：

$$
y_t=A_t f(k_t),
$$

其中 $f(k_t)$ 对资本递增且凹，劳动固定为 1。技术 $A_t$ 只有两个可能状态：

$$
A_t=\begin{cases}
A_1, & \text{with probability }p_1,\\
A_2, & \text{with probability }p_2,
\end{cases}
$$

并且 $p_1+p_2=1$，$A_1>A_2$。你可以把 $A_1$ 理解为好天气，$A_2$ 理解为坏天气。这个例子没有长期技术增长，只是同样资本下，不同自然状态会让产出高低不同。

资本积累方程是：

$$
k_{t+1}=A_t f(k_t)+(1-\delta)k_t-c_t.
$$

Robinson Crusoe 在 $t=0$ 最大化 expected discounted utility：

$$
E_0\sum_{t=0}^{\infty}\beta^t u(c_t).
$$

和确定性模型相比，最重要的变化是：未来的消费路径不可能在今天一次性写成一条确定序列。因为未来每一期的技术状态尚未实现，未来的最优消费取决于未来看到的技术状态。所以在随机模型中，计划不是“从今天到永远的一条路径”，而是一棵 decision tree：如果这一期是 $A_1$，选择某个 $k_{t+1}$；如果这一期是 $A_2$，选择另一个 $k_{t+1}$；下一期又根据新的状态继续分叉。

这就是为什么作者后来强调 plan。确定性模型中的 policy function 可以理解为 $k_{t+1}=h(k_t)$；随机模型中的 plan 则是 $k_{t+1}=h(k_t,A_t)$。资本状态和技术状态共同决定今天的最优选择。

### 2.3 随机 Bellman equation：期望项如何出现

这个简单模型的 Bellman equation 可以写成：

$$
V(k_t,A_t)=\max_{k_{t+1}}\left\{u\big(A_t f(k_t)+(1-\delta)k_t-k_{t+1}\big)+\beta E_t[V(k_{t+1},A_{t+1})]\right\}.
$$

> $E_t$ 是条件在 $t$ 期信息集下的期望；在 Markov 设定里，计算它时只需要对 $z_{t+1}$ 的条件分布积分/求和，因为 $V(k_{t+1},z_{t+1})$ 已经包含了 $t+1$ 以后所有未来随机性的最优期望价值。

如果 $A_{t+1}$ 只有 $A_1$ 和 $A_2$ 两种可能，并且每期独立同分布，那么 expectation 展开后就是：
$$
E_t[V(k_{t+1},A_{t+1})]
=p_1V(k_{t+1},A_1)+p_2V(k_{t+1},A_2).
$$

所以 Bellman equation 在状态 $A_1$ 下可以写为：

$$
V(k_t,A_1)=\max_{k_{t+1}}\{u(A_1f(k_t)+(1-\delta)k_t-k_{t+1})
+\beta[p_1V(k_{t+1},A_1)+p_2V(k_{t+1},A_2)]\},
$$

在状态 $A_2$ 下同理。注意这里不是只有一个 value function，而是对每个当前技术状态都有一个 value function。直觉上，今天处在高技术状态和低技术状态，当前可用资源不同，所以当前最大化得到的价值也不同。

如果把一般形式写出来，作者给出的结构是：

$$
V(x_t,z_t)=\max_{y_t}\{F(x_t,y_t,z_t)+\beta E_t[V(G(x_t,y_t,z_t),z_{t+1})]\},
$$

其中 $x_t$ 是非随机或内生 state variable，例如资本；$z_t$ 是随机 state variable，例如技术；$y_t$ 是 control variable，例如消费或下一期资本；$G(\cdot)$ 是状态转移方程。这个式子就是后面 RBC/DSGE 递归表示的基本雏形：**状态由内生状态和外生随机状态共同构成，控制变量由当前状态决定，未来价值对未来随机状态取期望。**

### 2.4 随机 Euler equation：今天的边际收益要和预期的明天边际收益比较

作者随后把随机模型推广到一般形式。设约束为：

$$
x_{t+1}=G(x_t,y_t,z_t),
$$

目标为：

$$
E_0\sum_{t=0}^{\infty}\beta^tF(x_t,y_t,z_t).
$$

在这种模型中，最优性条件仍然是“今天多留一点资源到明天”的边际成本等于预期边际收益。区别只在于，明天的边际收益不再确定，而是要对 $z_{t+1}$ 的可能值取条件期望。因此会得到 stochastic Euler equation。

这一步的经济直觉比代数更重要。确定性模型里，牺牲今天一点消费换来明天一点资本，明天的回报是确定的。随机模型里，明天的资本回报取决于明天技术状态。如果明天可能是高技术，也可能是低技术，那么今天多储蓄的价值就是这些状态下边际价值的 probability-weighted average。于是 Euler equation 中出现 expectation operator 是自然的：它不是额外假设，而是最优跨期权衡在不确定性下的形式。

### 2.5 维度灾难：为什么直接 value function iteration 很快变贵

在有限状态模型里，value function iteration 看起来只是从一条价值函数变成多条价值函数。但如果内生状态和外生状态很多，计算维度会快速上升。作者把这称为 the problem of dimensionality。

假设状态包括资本 $k_t$ 和技术 $z_t$。如果资本网格有 100 个点，技术状态有 2 个点，那么每次迭代需要计算 200 个状态点。如果再加入一个资产、一个货币状态、一个价格粘性状态，状态空间会呈乘法扩张。这就是动态规划中的 curse of dimensionality。第 5 章的小模型可以直接迭代 value function，但第 6 章 Hansen RBC 模型的技术冲击是连续 AR(1) 式过程，直接离散化后状态维度会迅速膨胀，所以后面章节会转向 log-linearization 和 linear quadratic methods。

### 2.6 具体数值例子：两种技术状态下的 value function 和 plan

作者用一个具体例子展示 value function iteration。效用为 $\ln c$，生产函数大致是 Cobb-Douglas：

$$
y_t=A_t k_t^{0.36},
$$

折旧率为 $\delta=0.1$，两个技术状态为 $A_1=1.75$ 和 $A_2=0.75$。在简单版本中，高技术状态出现概率为 $0.8$，低技术状态出现概率为 $0.2$，且每期独立。

迭代形式可以写成两条 Bellman equation：

$$
V_{j+1}(k_t,1.75)=\max_{k_{t+1}}\left\{\ln(1.75k_t^{0.36}+0.9k_t-k_{t+1})+\beta[0.8V_j(k_{t+1},1.75)+0.2V_j(k_{t+1},0.75)]\right\},
$$

$$
V_{j+1}(k_t,0.75)=\max_{k_{t+1}}\left\{\ln(0.75k_t^{0.36}+0.9k_t-k_{t+1})+\beta[0.8V_j(k_{t+1},1.75)+0.2V_j(k_{t+1},0.75)]\right\}.
$$

这两条式子的结构说明：当前技术状态影响当前资源约束，但由于下一期技术独立同分布，两个当前状态下的未来期望权重都是 $0.8$ 和 $0.2$。因此，高技术状态和低技术状态下的 value function 不同，policy function 也不同，但它们共同使用同一个未来状态分布。

作者迭代到 250 次后展示了 value functions 和 plans：

![Figure 5.1 — Iterations on the value function](../Figures/Ch05/figure_5_1_value_function_iterations.png)

Figure 5.1 的直观信息是：value function iteration 会逐渐收敛，每隔 50 次迭代画出的价值函数逐步向稳定形状靠近。状态 $A_t$ 越好，给定同样资本时可用资源越多，价值越高。

![Figure 5.2 — The plans](../Figures/Ch05/figure_5_2_policy_plans.png)

Figure 5.2 是本章最重要的图之一。它展示了两个 contingent plans：$H(k_t,1.75)$ 和 $H(k_t,0.75)$。在高技术状态下，给定同样的当前资本，下一期资本选择通常更高；在低技术状态下，可用资源少，最优储蓄少，下一期资本计划更低。这里的 policy function 已经不再只由 $k_t$ 决定，而是由 $(k_t,A_t)$ 决定。

### 2.7 Simulation：从 plan 到时间序列

一旦我们有了 plan，就可以模拟经济路径。模拟步骤很直接：给定初始资本 $k_0$；每期用随机数生成技术状态；根据当前 $(k_t,A_t)$ 查 plan 得到 $k_{t+1}$；重复这个过程。作者用 $k_0=1$ 开始模拟，用 $[0,1]$ 上均匀随机数决定状态：随机数小于等于 $0.8$ 时取高技术状态，否则取低技术状态。

![Figure 5.3 — A simulated time path](../Figures/Ch05/figure_5_3_simulated_path.png)

Figure 5.3 展示了资本路径。它不是平滑收敛到某个确定稳态，而是在随机冲击下上下波动。由于技术状态在每一期独立抽取，时间序列会波动，但不一定表现出强烈 persistence。也就是说，今天是高技术状态并不会提高明天仍为高技术状态的概率。

这一步很重要，因为 RBC/DSGE 的一个核心使用方式就是：先求出 policy rules，然后用外生冲击过程生成内生变量的 simulated time series，最后比较模型生成的 second moments、correlations、impulse responses 与真实数据是否接近。

### 2.8 Markov chain：给随机状态加入 persistence

独立同分布的技术冲击太“健忘”。现实宏观数据通常有 persistence：高产出时期往往持续几期，低产出时期也往往持续几期。为了让随机过程带有持续性，作者引入 Markov chain。

在 Markov chain 中，下一期状态的概率取决于当前状态，但不取决于更久远历史。若状态集合为 $\{A_1,A_2,\ldots,A_n\}$，transition matrix $P$ 的元素 $p_{ij}$ 表示：当前状态是 $i$ 时，下一期转移到状态 $j$ 的概率。

作者用的二状态例子是：

$$
P=\begin{pmatrix}
0.90 & 0.10\\
0.40 & 0.60
\end{pmatrix}.
$$

这表示：如果这一期是高技术 $A_1=1.75$，下一期仍然是高技术的概率是 90%；如果这一期是低技术 $A_2=0.75$，下一期仍然是低技术的概率是 60%。因此高状态和低状态都有一定 persistence，尤其高状态更容易延续。

这里要区分 conditional probabilities 和 unconditional probabilities。transition matrix 的每一行给的是条件概率：已知当前状态后，下一期状态如何分布。无条件概率则问：如果经济运行很久，不看初始状态，长期有多少比例时间处在 $A_1$ 或 $A_2$？

给定初始分布 $p_0$，第二期分布是 $p_0P$，第三期是 $p_0P^2$，第 $n+1$ 期是 $p_0P^n$。在作者的例子中，随着 $n\to\infty$，

$$
P^\infty=\begin{pmatrix}
0.80 & 0.20\\
0.80 & 0.20
\end{pmatrix}.
$$

这个极限矩阵的两行相同，说明无论初始状态是什么，长期分布都是 $[0.80,0.20]$。这和前面独立同分布模型的无条件概率一样，但 conditional probabilities 不同，所以动态路径不同。

### 2.9 Markov chain 下的 Bellman equation

一旦技术服从 Markov chain，Bellman equation 的主要变化是 expectation 要对当前状态条件化。一般形式变为：

$$
V_{j+1}(x_t,z_t)=\max_{y_t}\left\{F(x_t,y_t,z_t)+\beta E_t[V_j(G(x_t,y_t,z_t),z_{t+1})\mid z_t]\right\}.
$$

条件符号 $\mid z_t$ 表示：下一期状态分布取决于当前状态。如果当前是 $A_1$，未来价值的权重用 transition matrix 第一行；如果当前是 $A_2$，用第二行。

对本章的增长模型，Bellman equation 变成：

$$
V(k_t,A_1)=\max_{k_{t+1}}\{u(A_1f(k_t)+(1-\delta)k_t-k_{t+1})+\beta[p_{11}V(k_{t+1},A_1)+p_{12}V(k_{t+1},A_2)]\},
$$

$$
V(k_t,A_2)=\max_{k_{t+1}}\{u(A_2f(k_t)+(1-\delta)k_t-k_{t+1})+\beta[p_{21}V(k_{t+1},A_1)+p_{22}V(k_{t+1},A_2)]\}.
$$

和独立同分布版本相比，当前状态不仅影响当前产出，也影响未来状态分布。因此，即使两个模型有相同的长期无条件分布 $[0.8,0.2]$，它们的 policy functions 和模拟路径也不会完全一样。

![Figure 5.4 — The plans with Markov chains](../Figures/Ch05/figure_5_4_markov_plans.png)

Figure 5.4 显示 Markov chain 下的 plans。它们和 Figure 5.2 相似，因为无条件分布相同；但又不完全一样，因为条件分布不同。比如当前处在高技术状态时，下一期继续高技术的概率很高，所以高状态下的未来价值更乐观，这会影响储蓄选择。

![Figure 5.5 — A simulation with Markov chains](../Figures/Ch05/figure_5_5_markov_simulation.png)

Figure 5.5 和 Figure 5.3 使用同一组随机数生成过程，但由于 transition probabilities 依赖当前状态，路径显示出更强 persistence。高技术状态会连续出现，资本会有较长时间向高状态对应的水平移动；低技术状态也会持续一段时间，资本路径会持续下行或低位徘徊。

### 2.10 Markov chain 的优点与局限

Markov chain 的优点是显而易见的：它能让模型生成更像真实宏观数据的 persistence。后面的 RBC 模型常常会把 technology shock 写成高度持久的 AR(1) 过程，本质上也是为了让冲击具有持续性。

但作者强调了一个非常重要的局限：**用 Markov chain 写出 persistence，并不等于从经济机制上解释了 persistence。** 如果我们只是为了拟合时间序列，增加 Markov chain 的维度或调高自相关，确实可以让模型路径更持久。但如果研究问题是“为什么经济冲击会有持久效应”，Markov chain 只是把答案放进外生过程里，而不是从资本积累、劳动调整、投资时滞、价格粘性、金融摩擦等机制中推导出来。

这也是 RBC/DSGE 建模的一条主线：外生冲击过程可以帮助模型匹配数据，但真正有经济解释力的是模型内部传播机制（propagation mechanism）。第 6 章 Hansen 模型会继续面对这个问题：技术冲击给定后，模型能否通过劳动、投资、资本积累把冲击放大并延续？

### 2.11 Matlab code 在做什么

本章最后给出的 Matlab code 不是核心阅读重点，但有助于理解数值流程。主程序设置参数、建立资本网格、给两个初始 value functions，然后循环迭代。在每个资本网格点上，程序分别令当前技术为 $A_1$ 和 $A_2$，用 bounded minimization routine 找到使 Bellman 右侧最大化的 $k_{t+1}$。由于 Matlab 的求最小化函数使用 minimization，代码把 value function 取负来实现 maximization。

代码中的关键细节是 interpolation。因为最优 $k_{t+1}$ 不一定刚好落在资本网格点上，所以程序需要用线性插值从上一轮 value function 中读取 $V_j(k_{t+1},A_1)$ 和 $V_j(k_{t+1},A_2)$。这正是连续状态变量 value function iteration 的常见技术：状态空间离散化，但控制变量可以在网格之间选择，value function 用插值近似。

## 3. Compact Summary: What You Must Retain

- 随机递归模型的核心变化不是推翻 Bellman equation，而是把随机状态 $z_t$ 纳入 state vector，并把未来价值写成 conditional expectation。
- 在有限状态模型中，每个当前随机状态对应一条 value function 和一条 contingent policy function；作者把这种依赖状态的政策称为 plan。
- 简单 stochastic growth model 的 Bellman equation 中，未来价值项是 $p_1V(k_{t+1},A_1)+p_2V(k_{t+1},A_2)$；这就是概率加权的 continuation value。
- 随机 Euler equation 的经济含义是：今天储蓄的边际成本等于明天不同状态下边际收益的期望。
- Markov chain 让下一期状态概率取决于当前状态，因此可以生成 persistence；transition matrix 给的是 conditional probabilities。
- 长期无条件分布可以由 $p_0P^n$ 的极限得到；如果 $P^\infty$ 的各行相同，说明长期分布不依赖初始状态。
- 两个模型即使拥有相同的 unconditional distribution，也可能因为 conditional distribution 不同而有不同的 policy functions 和 simulated paths。
- Markov chain 能制造 persistence，但不一定解释 persistence；真正的经济解释要来自模型内部传播机制。

## 4. Figures, Tables, and Formulas to Check in the Original

本章重要图表已经作为截图放入 `Figures/Ch05/`，并在正文中嵌入：

- Figure 5.1：value function iteration 的收敛过程。
- Figure 5.2：两种技术状态下的 plans / policy functions。
- Figure 5.3：独立随机技术状态下的资本模拟路径。
- Figure 5.4：Markov chain 下的 plans。
- Figure 5.5：Markov chain 下的资本模拟路径，重点看 persistence。

需要重点核对的公式：

- 概率空间 $(\Omega,\mathcal{F},P)$ 的定义，尤其连续状态下“点概率为 0 但区间概率为正”的逻辑。
- 简单随机增长模型的 Bellman equation。
- 一般随机递归模型：
  $$V(x_t,z_t)=\max_{y_t}\{F(x_t,y_t,z_t)+\beta E_t[V(G(x_t,y_t,z_t),z_{t+1})]\}.$$
- Markov chain 条件期望版本：
  $$V_{j+1}(x_t,z_t)=\max_{y_t}\{F(x_t,y_t,z_t)+\beta E_t[V_j(G(x_t,y_t,z_t),z_{t+1})\mid z_t]\}.$$

> ⚠️【需要回原文看图】如果后续要复现 Matlab 代码或重新画图，请回原文核对资本网格、初始 value function、插值方法、迭代次数和图中坐标轴。截图足够理解主线，但不保证复现实验参数的每个细节都完整。

## 5. Questions and Answers

**Q1：随机模型里为什么不能像确定性模型一样在 $t=0$ 直接选择一整条消费路径？**  
因为未来技术状态尚未实现。未来每一期的最优消费取决于当期看到的状态，所以今天只能制定 contingent plan：不同状态发生时采取不同选择。

**Q2：为什么随机 Bellman equation 里要把 $A_t$ 或 $z_t$ 放进 state？**  
因为当前随机状态影响当前资源约束，也可能影响未来状态分布。最优选择必须知道当前资本和当前技术状态，所以 state vector 必须包含二者。

**Q3：独立同分布冲击和 Markov chain 冲击的区别是什么？**  
独立同分布冲击下，下一期状态概率不依赖当前状态；Markov chain 下，下一期状态概率取决于当前状态。后者能产生更强 persistence。

**Q4：transition matrix 的每一行怎么读？**  
第 $i$ 行表示当前状态为 $i$ 时，下一期转移到各个状态的条件概率。例如 $p_{12}$ 是当前为状态 1、下一期转到状态 2 的概率。

**Q5：为什么 Figure 5.2 和 Figure 5.4 的 plans 相似但不完全一样？**  
因为两个例子的长期无条件分布都是高技术 80%、低技术 20%，但 Markov chain 的条件分布不同。当前处在高状态时，未来更可能继续高状态，这会改变 continuation value 和储蓄选择。

**Q6：Markov chain 能不能解释经济周期的 persistence？**  
它能生成 persistence，但不一定解释 persistence。因为 persistence 是外生放进 transition probabilities 的；真正的经济解释需要说明为什么冲击会在资本、劳动、投资、价格或金融摩擦中被传播和放大。

**Q7：本章和第 6 章有什么关系？**  
本章教会你如何把随机状态放进递归模型；第 6 章会把这个思路用于 Hansen RBC 模型，并引入 log-linearization、calibration、variance matching 和 impulse response functions。
