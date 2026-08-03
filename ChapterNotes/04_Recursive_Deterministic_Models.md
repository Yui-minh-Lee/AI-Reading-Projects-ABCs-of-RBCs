# Chapter 4 — Lecture Note

> Importance: ★★★★★  
> Suggested audit model: xhigh  
> Reading mode: careful  
> Estimated note reading time: 80-105 minutes  
> Source reliability: text OK; important figures embedded as source screenshots; formulas involving envelope theorem and numerical iteration should be checked against the original before coding

## 0. How to read this note

这一章是全书最重要的方法章之一。前三章主要用 sequence problem 和 variational methods 来求稳态；第 4 章开始换成 recursive methods，也就是后面 RBC / DSGE 模型真正通用的语言。

读这一章时，不要只把 Bellman equation 当成一个新公式。它真正改变的是建模视角：经济主体不再一次性选择从现在到无限未来的整条序列，而是在每一期观察 state variables，然后按照 policy function 选择 control variables。这个转化会让无限维优化问题变成一个递归的一期问题。

本章要带走三件事：

第一，区分 state variables 和 control variables。状态变量是已经由过去或外生过程决定的变量，控制变量是本期可以选择的变量。

第二，理解 value function 和 Bellman equation。value function 把“从当前状态出发、未来最优行为带来的总效用”压缩成一个函数。

第三，理解 value function iteration。很多情况下 value function 没有解析形式，但可以从一个初始猜测出发反复迭代，同时得到 value function 和 policy function 的数值近似。

## 1. Opening: 本章的核心问题

无限期宏观模型看起来很难，因为 household 或 planner 要选择无限多期的消费、投资、资本、劳动路径。第 3 章用 variational method 处理这种问题，核心是从整条路径的最优性条件中得到 Euler equation 和 stationary state。

第 4 章提出另一种方式：如果每一期的偏好、技术、折现因子和约束形式都一样，那么经济主体在每一期面对的是“同一个问题”，只是初始条件不同。比如今天继承的资本 $k_t$ 不同，会改变今天最优消费和储蓄，但优化问题的结构没有变。

这就是 recursive deterministic model 的核心：**同一个优化问题反复出现，当前状态总结过去，policy function 决定当前选择。**

本章要回答的问题是：

1. 什么是 state variables，什么是 control variables？
2. 为什么无限期 sequence problem 可以写成 Bellman equation？
3. Bellman equation 的一阶条件如何重新得到 Euler equation？
4. 为什么 control variable 的选择会影响求解便利程度？
5. 当 value function 不知道解析形式时，怎样用数值迭代近似它？

## 2. Main Lecture

### 2.1 State variables 和 control variables：递归模型的第一步

递归建模的第一步，是把变量分成状态变量（state variables）和控制变量（control variables）。

状态变量是在本期决策之前已经给定的变量。它们可能由过去的选择决定，也可能由自然状态决定。在增长模型中，最典型的状态变量是资本存量 $k_t$。今天的资本来自过去的投资，今天不能重新选择它，只能接受它。

如果模型有 stochastic technology，那么技术状态也可以是 state variable，因为本期决策时 household 或 firm 已经观察到当前技术水平。若模型有 habit formation，过去消费 $c_{t-1}$ 也会成为 state variable，因为当前效用可能取决于 $c_t-\xi c_{t-1}$，而 $c_{t-1}$ 已经由历史决定。

控制变量是本期可以主动选择的变量。比如 Robinson Crusoe model 中，Crusoe 可以选择 consumption $c_t$，也可以等价地选择下一期资本 $k_{t+1}$. 选择 $c_t$ 后，预算约束会决定 investment 和 $k_{t+1}$；选择 $k_{t+1}$ 后，预算约束会决定 $c_t$。

这说明 control variable 的选择有一定自由度。经济内容可以相同，但求解便利程度可能不同。第 4 章后面会专门展示：选择 $k_{t+1}$ 作为 control variable，通常比选择 $c_t$ 更方便，因为它可以让 envelope theorem 的表达式简化。

### 2.2 Robinson Crusoe model：从 sequence problem 到 recursive problem

考虑最简单的 Robinson Crusoe economy。固定劳动供给，生产函数为：

$$
y_t=f(k_t).
$$

资源约束和资本积累可以合并成：

$$
c_t=f(k_t)+(1-\delta)k_t-k_{t+1}.
$$

如果用 sequence problem 写，Crusoe 从 $t$ 期开始选择整条未来资本路径：

$$
V(k_t)
=
\max_{\{k_s\}_{s=t+1}^{\infty}}
\sum_{i=0}^{\infty}
\beta^i
u(f(k_{t+i})-k_{t+i+1}+(1-\delta)k_{t+i}).
$$

这里 $V(k_t)$ 是 value function。它的含义是：给定当前资本 $k_t$，如果从现在开始一直最优决策，能够得到的最大 discounted lifetime utility。

为什么 $V$ 是 $k_t$ 的函数？因为在这个简单模型里，当前资本是唯一的状态变量。只要知道 $k_t$，所有未来可行选择和最优路径都由同一个优化问题决定。若当前资本更高，当前资源更多，未来选择集合也不同，所以最大价值也不同。

关键递归思想是：从 $t+1$ 期看，$k_{t+1}$ 又会成为下一期的状态变量。而从 $t+1$ 期开始的“剩余最大效用”正是 $V(k_{t+1})$。因此，原来的无限期问题可以拆成：

1. 今天选择 $k_{t+1}$，决定今天消费和当期效用；
2. 明天开始的全部最优未来，用 $\beta V(k_{t+1})$ 表示。

于是得到 Bellman equation：

$$
V(k_t)
=
\max_{k_{t+1}}
\left\{
u(f(k_t)-k_{t+1}+(1-\delta)k_t)
+\beta V(k_{t+1})
\right\}.
$$

这就是第 4 章的核心公式。它把无限维选择问题变成了一个一维选择问题：给定 $k_t$，只选择 $k_{t+1}$。

不过这个简化不是免费的。现在问题中出现了未知的 $V(k_{t+1})$。如果 value function 已知，求最优 $k_{t+1}$ 会很容易；但 value function 本身正是我们要解的对象。所以 Bellman equation 是一个 functional equation，未知数不是一个数字，而是一个函数。

### 2.3 Bellman equation 的 FOC 与 envelope theorem

对 Bellman equation 中的 control $k_{t+1}$ 求一阶条件：

$$
0
=
-u'(c_t)+\beta V'(k_{t+1}).
$$

这条式子的含义很直接：多留一单位资本到明天，会减少今天消费，边际成本是 $u'(c_t)$；收益是明天状态资本提高后带来的未来价值，折现后是 $\beta V'(k_{t+1})$。

但是这里又出现了未知对象 $V'(k_{t+1})$。这时需要 envelope theorem。

Bellman equation 为：

$$
V(k_t)
=
\max_{k_{t+1}}
\{u(c_t)+\beta V(k_{t+1})\}.
$$

在最优选择下，对当前状态 $k_t$ 求偏导时，不需要再考虑最优 $k_{t+1}$ 对 $k_t$ 的间接变化。直觉是：在最优点上，control 的边际变化已经满足一阶条件，所以通过 control 变化带来的间接项为零。于是：

$$
V'(k_t)
=
u'(c_t)[f'(k_t)+(1-\delta)].
$$

把这条式子向前一期开，即：

$$
V'(k_{t+1})
=
u'(c_{t+1})[f'(k_{t+1})+(1-\delta)].
$$

再代回一阶条件：

$$
u'(c_t)
=
\beta u'(c_{t+1})
[f'(k_{t+1})+(1-\delta)].
$$

这就是熟悉的 Euler equation。递归方法和第 3 章 variational method 给出的跨期最优条件是一致的。

在 stationary state 中，$c_t=c_{t+1}$，于是：

$$
f'(\bar k)
=
\frac{1}{\beta}-(1-\delta).
$$

经济含义仍然是：稳态下资本边际产出等于由贴现因子隐含的净利率加折旧率。

### 2.4 一般形式：Bellman equation、policy function 与 functional equation

作者接着把 Robinson Crusoe 例子推广到一般形式。设：

$$
x_t
$$

为 state vector，

$$
y_t
$$

为 control vector。当期收益或效用为：

$$
F(x_t,y_t),
$$

状态转移为：

$$
x_{t+1}=G(x_t,y_t).
$$

那么 value function 可以写为：

$$
V(x_t)
=
\max_{y_t}
\left\{
F(x_t,y_t)+\beta V(G(x_t,y_t))
\right\}.
$$

这个式子是后面所有 RBC/DSGE recursive representation 的模板。当前状态 $x_t$ 总结过去；控制变量 $y_t$ 由当前状态决定；状态转移 $G$ 把今天的状态和选择带到明天；未来价值通过 $V$ 表示。

最优选择 $y_t$ 可以写成 state 的函数：

$$
y_t=H(x_t).
$$

这个 $H$ 叫 policy function。它告诉我们：给定任何当前状态，模型中的 agent 会如何选择 control variables。

当 policy function 已经找到时，Bellman equation 可以写成：

$$
V(x_t)
=
F(x_t,H(x_t))
+\beta V(G(x_t,H(x_t))).
$$

这里已经不再写 max，因为最优化已经被 $H(x_t)$ 内含了。

对一般 Bellman equation 求一阶条件，会得到：

$$
0
=
F_y(x_t,y_t)
+\beta V'(G(x_t,y_t))G_y(x_t,y_t).
$$

它和简单模型中的 FOC 是同一个结构：当前控制的边际收益/成本，加上它通过明天状态影响未来价值的边际效应，必须为零。

Envelope condition 一般写成：

$$
V'(x_t)
=
F_x(x_t,y_t)
+\beta V'(G(x_t,y_t))G_x(x_t,y_t).
$$

如果模型写得巧妙，让：

$$
G_x(x_t,y_t)=0,
$$

那么 envelope condition 会简化为：

$$
V'(x_t)=F_x(x_t,y_t).
$$

这就是作者强调 control variable 选择的原因。经济模型相同，但变量定义会决定求解是否干净。

### 2.5 为什么选择 $k_{t+1}$ 比选择 $c_t$ 方便？

回到固定劳动的 Robinson Crusoe model。若选择下一期资本 $k_{t+1}$ 作为 control，那么：

$$
x_t=k_t,\quad y_t=k_{t+1}.
$$

状态转移非常简单：

$$
x_{t+1}=G(x_t,y_t)=y_t=k_{t+1}.
$$

因此：

$$
G_x(x_t,y_t)=0.
$$

这让 envelope theorem 简化，$V'(k_t)$ 可以直接用当期已知函数表达出来。

如果改用消费 $c_t$ 作为 control，那么：

$$
x_t=k_t,\quad y_t=c_t,
$$

状态转移变成：

$$
k_{t+1}=G(x_t,y_t)
=
f(k_t)+(1-\delta)k_t-c_t.
$$

此时：

$$
G_x(x_t,y_t)=f'(k_t)+(1-\delta)\neq 0.
$$

Envelope condition 中仍然含有 $V'(G(x_t,y_t))$，也就是未来 value function 的导数。这样并没有真正消除未知对象。

这不是说用 $c_t$ 做控制变量是错的；经济问题完全相同。但用 $k_{t+1}$ 做 control variable 通常更方便，因为它把更多内容放进当期 return function，让状态转移对当前状态的偏导简化。

这一点对 DSGE 建模很有用：变量选取不是纯粹记号问题。好的状态和控制变量定义，可以让 FOC、envelope condition、数值求解和代码实现简单很多。

### 2.6 Value function iteration：当解析解不可得时怎么做

许多模型无法解析求出 value function。作者因此介绍 value function iteration，也就是 successive approximations。

设初始猜测为：

$$
V_0(x_t).
$$

最简单的选择是常数 0。然后用 Bellman operator 更新：

$$
V_1(x_t)
=
\max_{y_t}
\{F(x_t,y_t)+\beta V_0(G(x_t,y_t))\}.
$$

再用 $V_1$ 更新：

$$
V_2(x_t)
=
\max_{y_t}
\{F(x_t,y_t)+\beta V_1(G(x_t,y_t))\}.
$$

不断重复，得到一列函数：

$$
V_0,V_1,V_2,\ldots
$$

在常见经济问题满足一定条件时，这列函数会收敛到真正的 value function $V$。

为什么这个方法会收敛？直觉是 discounting。初始猜测 $V_0$ 对 $V_1$ 的影响乘以 $\beta$；对 $V_2$ 的影响进一步乘以 $\beta^2$；随着迭代次数增加，初始猜测的影响逐渐消失。剩下的是反复最大化真实当期 return function 后累积起来的最优价值。

更重要的是，value function iteration 不只给出 value function。每次在每个状态点上做最大化时，都会得到最优 control。随着 $V_j$ 收敛，这些最优 control 也会收敛到 policy function：

$$
y_t=H(x_t).
$$

所以同一套数值过程同时产出 value function 和 policy function。

### 2.7 固定劳动例子：value function 和 policy function 的数值近似

作者用固定劳动的简单增长模型展示数值迭代。生产函数为：

$$
f(k_t)=k_t^\theta,
$$

效用函数为：

$$
u(c_t)=\ln c_t.
$$

Bellman equation 为：

$$
V(k_t)
=
\max_{k_{t+1}}
\left\{
\ln(k_t^\theta-k_{t+1}+(1-\delta)k_t)
+\beta V(k_{t+1})
\right\}.
$$

作者使用：

$$
\delta=0.1,\quad \theta=0.36,\quad \beta=0.98.
$$

稳态资本由：

$$
.36\bar k^{-0.64}
=
\frac{1}{0.98}-(1-0.1)
$$

给出，得到：

$$
\bar k=5.537.
$$

初始 value function 设为：

$$
V_0(k)=0.
$$

经过迭代，value function 从一条水平线逐渐向真实 value function 靠近。

![Figure 4.1 — Value function, first three approximations](../Figures/Ch04/figure_4_1_value_function_first_three_approximations.png)

Figure 4.1 展示前三次近似。由于未来价值一开始被设成 0，第一轮只看当期效用；第二、三轮开始逐步把更长未来纳入。线条向上移动，说明模型逐步认识到“资本不仅给今天产出，也给未来选择带来价值”。

![Figure 4.2 — Approximating the value function](../Figures/Ch04/figure_4_2_approximating_value_function.png)

Figure 4.2 展示更长迭代过程。由于 $\beta=0.98$ 接近 1，未来很重要，收敛比较慢。图中每隔 48 次迭代画一条线，到 240 次时已经很接近最终 value function。线条之间的距离逐渐变小，说明 value function iteration 正在收敛。

![Figure 4.3 — The policy function after 240 iterations](../Figures/Ch04/figure_4_3_policy_function_after_240_iterations.png)

Figure 4.3 是对应的 policy function：

$$
k_{t+1}=H(k_t).
$$

图中 45 度线表示 $k_{t+1}=k_t$。policy function 与 45 度线的交点就是 stationary state。若当前资本低于稳态，policy function 通常位于 45 度线上方，表示 $k_{t+1}>k_t$，资本会积累；若高于稳态，则资本积累放缓或下降。这个图把动态路径的方向直接可视化了。

### 2.8 加入 variable labor：两个 controls 与两个 policy functions

作者最后展示递归方法也能处理可变劳动的 Robinson Crusoe model。现在 household / planner 最大化：

$$
\sum_{i=0}^{\infty}\beta^i u(c_{t+i},h_{t+i}),
$$

约束为：

$$
k_{t+1}=(1-\delta)k_t+i_t,
$$

$$
y_t=f(k_t,h_t)\geq c_t+i_t,
$$

$$
h_t\leq 1.
$$

把消费消去后，Bellman equation 写成：

$$
V(k_t)
=
\max_{h_t,k_{t+1}}
\left\{
u(f(k_t,h_t)+(1-\delta)k_t-k_{t+1},h_t)
+\beta V(k_{t+1})
\right\}.
$$

现在状态变量仍然只有 $k_t$，但控制变量有两个：

$$
h_t,\quad k_{t+1}.
$$

因此会有两个 policy functions：

$$
k_{t+1}=H^k(k_t),
$$

$$
h_t=H^h(k_t).
$$

对 $h_t$ 的一阶条件表达 labor-leisure tradeoff。增加劳动提高产出和消费，但也降低 leisure。用边际效用写就是：

$$
\frac{u_h(c_t,h_t)}{u_c(c_t,h_t)}
=
-f_h(k_t,h_t).
$$

右边是劳动边际产品的负值，左边是劳动给效用带来的边际损失相对于消费边际效用的比率。这条式子说：最优劳动选择要让劳动带来的消费收益等于 leisure 损失。

对 $k_{t+1}$ 的一阶条件结合 envelope theorem，会得到 familiar Euler equation：

$$
\frac{u_c(c_t,h_t)}{u_c(c_{t+1},h_{t+1})}
=
\beta [f_k(k_{t+1},h_{t+1})+(1-\delta)].
$$

它和第 3 章 variable labor model 得到的条件一致。这说明递归方法不是改变经济内容，而是改变问题表达和求解方式。

作者的数值例子使用：

$$
\delta=0.1,\quad \theta=0.36,\quad \beta=0.98,\quad A=0.5,
$$

效用函数为：

$$
u(c_t,h_t)=\ln(c_t)+A\ln(1-h_t),
$$

生产函数为：

$$
f(k_t,h_t)=k_t^\theta h_t^{1-\theta}.
$$

![Figure 4.4 — Approximating the pair of value functions](../Figures/Ch04/figure_4_4_variable_labor_value_functions.png)

Figure 4.4 展示 variable labor 模型中 value function 的迭代收敛。形状和固定劳动例子类似，但由于劳动也可调整，给定同样资本时经济还有额外 margin 来提高当前效用和未来资本配置。

![Figure 4.5 — The two policy functions after 240 iterations](../Figures/Ch04/figure_4_5_variable_labor_policy_functions.png)

Figure 4.5 展示两个 policy functions。上升的曲线是：

$$
k_{t+1}=H^k(k_t),
$$

较低且略微下降的曲线是：

$$
h_t=H^h(k_t).
$$

图中 $H^k(k_t)$ 和 45 度线的交点给出资本稳态。劳动 policy function 略向下，说明沿着均衡路径，当资本较高时，最优劳动供给会下降。直觉是：资本更多时，同样劳动能生产更多产出，household 可以用更多资本替代部分劳动，从而享受更多 leisure。

### 2.9 Matlab code 在做什么

本章末尾的 Matlab code 是第一个很明确的 value function iteration 程序模板。它的逻辑如下。

首先设定资本网格，例如 $k=0.06,0.12,\ldots,6$。然后设定参数 $\beta,\delta,\theta$，并把初始 value function 设为一列 0。

接着进入迭代循环。对每一个当前资本网格点 $k_t$，程序使用数值优化器寻找使 Bellman 右侧最大的 $k_{t+1}$。由于 Matlab 的 `fminbnd` 是求最小值，代码把目标函数取负，从而把 maximization 改写成 minimization。

一个重要细节是 interpolation。最优 $k_{t+1}$ 不一定刚好落在资本网格点上，所以程序用线性插值从上一轮 value function 中读取 $V_j(k_{t+1})$。这就是连续状态变量数值动态规划中的常见处理：状态空间用网格近似，value function 用插值近似。

> 网格化之后，求这个 argmax 有不同的求法：
>
> 1. 遍历法：在网格中遍历，找到最大的那个；
> 2. 插值法：用线性插值在网格中找最好的；
> 3. 解析法：如果模型足够光滑、凹性好，可以对 Bellman RHS 求一阶条件，然后用 root-finding 解 argmax
>
> 总之：
>
> - 都是压缩映射：不论这个 max 是通过什么方式求/是何种 max，这都是压缩映射；
>
>     > 需要注意：max 不会破坏压缩性，这是基于：“只要插值/近似评估未来值的步骤不放大 sup norm 距离”，那么折现因子 $\beta$ 会保证该数值 Bellman operator 仍是压缩映射。有些插值可能会破坏这个关系，因此不一定总是成立的；（**高阶插值如果有负权重或 overshooting，可能不是 sup norm non-expansive**）
>
> - 收敛点不保证：虽然都是压缩映射，但是不同 max 方式下，收敛点是不相同的，比如用遍历法求 argmax，即使完全收敛之后，每个网格上的取值也不一定等于真正的值函数的取值；

代码还加入了避免负消费的惩罚。如果给定 $k_t$ 和候选 $k_{t+1}$ 导致消费小于等于 0，程序返回一个很差的 value，让优化器避开不可行选择。

这段代码虽然简单，但已经包含了后面计算 RBC / DSGE 模型的基本数值思想：设网格、猜 value function、逐状态最大化、插值、更新 value function、保存 policy function。

## 3. Compact Summary: What You Must Retain

本章最重要的内容可以压缩成七点。

- Recursive methods 适用于每期问题结构相同、只是 state variables 不同的无限期模型。当前状态总结过去，policy function 决定当前选择。
- State variables 是本期决策前已经给定的变量；control variables 是本期可以选择的变量。变量选择不改变经济内容，但会影响求解便利程度。
- Value function $V(x_t)$ 表示从当前状态出发、未来一直最优选择所能得到的最大 discounted value。
- Bellman equation 把无限期 sequence problem 改写成当前 return 加 discounted future value 的一期递归问题。
- Envelope theorem 让我们不用显式知道整个 value function，也能得到 $V'(x_t)$ 的表达，并重新推出 Euler equation。
- Value function iteration 从一个初始猜测出发反复应用 Bellman operator，在常见条件下收敛到真正的 value function，同时得到 policy function。
- 在 variable labor 模型中，同一个状态 $k_t$ 可以对应多个 controls，因此会有多个 policy functions，例如 $H^k(k_t)$ 和 $H^h(k_t)$。

## 4. Figures, Tables, and Formulas to Check in the Original

本章重要图表已经作为截图放入 `Figures/Ch04/`，并在正文中嵌入：

- Figure 4.1：value function 的前三次近似。
- Figure 4.2：value function iteration 到 240 次的收敛过程。
- Figure 4.3：固定劳动模型的 policy function $k_{t+1}=H(k_t)$。
- Figure 4.4：variable labor 模型中的 value function iteration。
- Figure 4.5：variable labor 模型中的两个 policy functions。

最需要回原文核对的公式包括：

$$
V(k_t)
=
\max_{k_{t+1}}
\{u(f(k_t)-k_{t+1}+(1-\delta)k_t)+\beta V(k_{t+1})\},
$$

一般 Bellman equation：

$$
V(x_t)
=
\max_{y_t}
\{F(x_t,y_t)+\beta V(G(x_t,y_t))\},
$$

一般 FOC：

$$
0=F_y(x_t,y_t)+\beta V'(G(x_t,y_t))G_y(x_t,y_t),
$$

以及 envelope condition：

$$
V'(x_t)
=
F_x(x_t,y_t)
+\beta V'(G(x_t,y_t))G_x(x_t,y_t).
$$

> ⚠️【需要回原文看图】这里涉及重要图表/表格/公式，PDF 文本提取可能不足以完整保留信息。建议回到原文核对。

如果要复现 Matlab code，应回原文核对资本网格、`fminbnd` 搜索区间、插值方式、不可行消费惩罚项和每隔多少次迭代画图。

## 5. Questions and Answers

**Q1：为什么 recursive method 能把无限期问题写成一期问题？**

因为每一期问题的结构相同，未来从 $t+1$ 期开始面对的仍然是同一个优化问题，只是初始状态变成了 $x_{t+1}$。所以未来全部最优价值可以用同一个 value function $V(x_{t+1})$ 表示。

**Q2：value function 和 policy function 有什么区别？**

Value function 告诉我们“给定当前状态，最大可得价值是多少”；policy function 告诉我们“给定当前状态，应该选择什么 control”。前者是价值，后者是行为规则。

**Q3：为什么选择 $k_{t+1}$ 做 control variable 会比较方便？**

因为在简单增长模型中，若令 $y_t=k_{t+1}$，状态转移可写成 $x_{t+1}=G(x_t,y_t)=y_t$，所以 $G_x=0$。这会让 envelope condition 简化，避免未来 value function 导数反复嵌套。

**Q4：Bellman equation 的 FOC 为什么还不够？**

FOC 中通常含有 $V'(x_{t+1})$，而 value function 本身未知。需要 envelope theorem 或数值迭代来处理这个未知导数。

**Q5：value function iteration 为什么会逐步忘掉初始猜测？**

因为初始猜测对未来价值的影响不断乘以 $\beta^j$。只要 $0<\beta<1$，迭代越多，初始猜测的权重越小，真实当期 return 的反复最大化逐渐主导结果。

**Q6：Figure 4.3 中 policy function 和 45 度线的交点代表什么？**

交点满足 $k_{t+1}=k_t$，所以它是 stationary state capital。如果当前资本低于交点，policy function 位于 45 度线上方，资本会增加；如果高于交点，资本会向稳态回落。

**Q7：加入 variable labor 后有什么新东西？**

状态变量仍可只有资本 $k_t$，但 controls 变成 $h_t$ 和 $k_{t+1}$。因此模型会同时产生资本政策函数 $H^k(k_t)$ 和劳动政策函数 $H^h(k_t)$，并且 FOC 同时包含劳动-闲暇权衡和跨期储蓄权衡。
