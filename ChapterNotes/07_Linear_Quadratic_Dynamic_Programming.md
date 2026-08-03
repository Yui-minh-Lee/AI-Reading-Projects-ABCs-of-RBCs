# Chapter 7 — Lecture Note

> Importance: ★★★★★  
> Suggested audit model: xhigh  
> Reading mode: careful  
> Estimated note reading time: 100-130 minutes  
> Source reliability: text OK; major tables and figures embedded as source screenshots; long matrix formulas should be checked against the original before coding

## 0. How to read this note

这一章可以看成第 6 章的“第二种求解语言”。第 6 章的主线是：先写出 Hansen RBC model 的 FOCs，再把 FOCs 和约束条件 log-linearize，最后求解线性动态系统。第 7 章换了一个入口：不从一阶条件出发，而是直接把动态规划问题的目标函数近似成 quadratic objective，并把约束写成 linear law of motion，然后使用 linear-quadratic dynamic programming 求出 policy function。

读这一章时，不要把它理解为一个全新的经济模型。它的经济对象仍然是 Hansen-style RBC model，真正的新内容是求解技术。你需要把注意力放在三个问题上。

第一，为什么需要二阶近似，而不是一阶近似？因为一阶近似的目标函数是线性的，最大化问题通常会给出角点解或缺乏稳定的边际权衡；动态宏观模型真正需要的是“偏离稳态时边际收益和边际成本如何变化”，这至少需要二阶曲率。

第二，为什么 linear-quadratic 方法可以把非线性模型变成一个可递归求解的问题？关键是：quadratic return + linear transition 会让 value function 仍然是 quadratic 的，于是 Bellman equation 可以化成一个矩阵二次方程，也就是 Riccati equation。

第三，为什么本章还要重新讨论 Hansen 的 indivisible labor model？因为这样可以把第 6 章的 log-linearization 解法和第 7 章的 LQ 解法放在同一个经济模型上比较。你会看到，两种近似方法给出的 impulse responses 很接近，但并不完全相同。

## 1. Opening: 本章的核心问题

第 6 章已经展示了一个标准 RBC 模型的完整求解：找到 stationary state，围绕稳态 log-linearize FOCs，然后求出状态变量和控制变量的线性响应。这个方法很自然，因为经济学家通常习惯从 FOCs 出发。

第 7 章提出另一种方法：**不要先线性化 FOCs，而是先把 planner problem 本身近似成一个 linear-quadratic problem。** 也就是说，把效用函数和生产约束组合后的目标函数在稳态附近做二阶 Taylor approximation，把状态转移方程写成线性形式，然后求一个线性 policy rule。

所以本章的核心问题是：

1. 怎样把一个非线性动态规划问题改写成 quadratic objective + linear transition？
2. 怎样通过 Riccati equation 求出线性政策函数？
3. 这种 LQ 解法与第 6 章的 log-linearization 解法相比，有什么相同与不同？

## 2. Main Lecture

### 2.1 从一般 LQ 问题开始：quadratic objective + linear transition

本章的标准问题可以写成：

$$
\max_{\{y_t\}_{t=0}^{\infty}} \sum_{t=0}^{\infty}\beta^t\left(x_t'Rx_t+y_t'Qy_t+2y_t'Wx_t\right)
$$

subject to

$$
x_{t+1}=Ax_t+By_t.
$$

这里 $x_t$ 是 state vector，$y_t$ 是 control vector。矩阵 $R,Q,W$ 描述当期 payoff 的二次型结构，矩阵 $A,B$ 描述状态如何随控制变量演化。

这个形式的好处是非常强的：如果当期收益是 quadratic，状态转移是 linear，那么 value function 可以猜成 quadratic：

$$
V(x_t)=x_t'Px_t.
$$

> #### 为什么在确定性 LQ 问题中，值函数一定是二次的？
>
> 这里最好区分两个对象：
>
> 1. 给定初始状态和初始控制以后，沿候选路径得到的总收益；
> 2. 对初始控制进行最优化以后得到的 value function。
>
> 确定性 LQ 问题中，每期收益是二次型：
>
> $$
> r(x_t,y_t)
> =
> x_t'Rx_t+y_t'Qy_t+2y_t'Wx_t,
> $$
>
> 状态转移和 Euler/FOC 系统都是线性的。因此，在给定初始状态 $x_0$ 和初始控制 $y_0$ 后，后续所有候选变量都可以写成 $(x_0,y_0)$ 的线性函数：
>
> $$
> \begin{bmatrix}
> x_t\\
> y_t
> \end{bmatrix}
> =
> M_t
> \begin{bmatrix}
> x_0\\
> y_0
> \end{bmatrix}.
> $$
>
> 把这些线性路径代入每期二次收益，再做无限期折现求和，得到的候选总收益一定是关于 $(x_0,y_0)$ 的二次函数：
>
> $$
> J(x_0,y_0)
> =
> \begin{bmatrix}
> x_0\\
> y_0
> \end{bmatrix}'
> H
> \begin{bmatrix}
> x_0\\
> y_0
> \end{bmatrix}.
> $$
>
> 但 value function 不是 $V(y_0)$。状态 $x_0$ 是历史给定的，控制 $y_0$ 才是要选择的，因此：
>
> $$
> V(x_0)=\max_{y_0}J(x_0,y_0).
> $$
>
> 最大化一个关于 $(x_0,y_0)$ 的凹二次函数，其一阶条件必然给出线性控制：
>
> $$
> y_0=Fx_0.
> $$
>
> 再把最优控制代回候选总收益：
>
> $$
> V(x_0)
> =
> J(x_0,Fx_0)
> =
> x_0'Px_0.
> $$
>
> 因而确定性情形的完整逻辑是：
>
> $$
> \boxed{
> \text{线性候选动态}
> \Rightarrow
> J(x_0,y_0)\text{ 为二次型}
> \Rightarrow
> y_0^*=Fx_0
> \Rightarrow
> V(x_0)=x_0'Px_0
> }
> $$
>
> 这说明“值函数是二次型”并不是凭空猜测，而是由**线性动态与二次目标**共同决定的。

代入 Bellman equation：
$$
x_t'Px_t=\max_{y_t}\left\{x_t'Rx_t+y_t'Qy_t+2y_t'Wx_t+\beta(Ax_t+By_t)'P(Ax_t+By_t)\right\}.
$$

对 $y_t$ 求一阶条件，可得：
$$
(Q+\beta B'PB)y_t=-(W+\beta B'PA)x_t.
$$

因此政策函数是线性的：

$$
y_t=Fx_t,
$$

其中

$$
F=-(Q+\beta B'PB)^{-1}(W+\beta B'PA).
$$

剩下的问题就是求 $P$。把最优 $y_t=Fx_t$ 代回 Bellman equation，可以得到 Riccati equation：

$$
P=R+\beta A'PA-(\beta A'PB+W')(Q+\beta B'PB)^{-1}(\beta B'PA+W).
$$

> **<u>为什么是代入？</u>** —— 一般而言对于递归问题，我们都是 FOC+包络定理，但是实际上我们搞错逻辑了。
>
> 包络定理本质上依然是从 bellman 方程导出的，因此如果满足 bellman 方程，那么就一定满足包络定理。而一般情况下我们求 FOC 之后，得到的是值函数的导数 V'，这东西没法代进 bellman 方程，因此我们采用另外的手段给原 bellman 方程“降级”（即包络定理），同样得到一个 V' 的方程即可完成对接，然后理想情况下消去 V' 、得到原函数 V 即可。

实际计算时通常从一个初始矩阵 $P_0$ 出发，反复迭代右边，直到 $P$ 收敛。收敛后再用上面的公式计算 $F$。

这就是本章技术主线的骨架。它看起来像纯粹的矩阵代数，但背后的经济含义很简单：**如果模型在稳态附近可以被近似成“二次损失 / 二次收益 + 线性运动”，那么最优决策就是状态变量的线性函数。**

### 2.2 为什么必须做二阶 Taylor approximation？

假设原模型的当期效用或 return function 是 $f(z_t)$，其中 $z_t$ 可能包含资本、劳动、消费、技术等变量。围绕稳态 $\bar z$ 做 Taylor approximation：

$$
f(z_t)\approx f(\bar z)+D f(\bar z)(z_t-\bar z)+\frac{1}{2}(z_t-\bar z)'D^2f(\bar z)(z_t-\bar z).
$$

如果只保留一阶项，目标函数会变成线性的。线性目标没有曲率，不能描述“偏离稳态越远，边际代价越高”这一类动态宏观模型中非常关键的机制。保留二阶项以后，模型才会有稳定的边际替代关系，才能产生内点的 linear feedback rule。

不过二阶 Taylor expansion 有一个小麻烦：它包含常数项和线性项，而标准 LQ 形式通常写成纯二次型 $z_t'Mz_t$。Kydland and Prescott 的技巧是把常数 1 加入状态向量。例如定义：

$$
z_t=\begin{bmatrix}1\\x_t\\y_t\end{bmatrix}.
$$

这样一来，原来 Taylor expansion 中的常数项、线性项和二次项都可以统一写成：

$$
z_t'Mz_t.
$$

直观地说，加入第一维的常数 1，是为了让“线性项”也能被二次型吸收。比如 $a x_t$ 可以写成 $2\cdot(1)\cdot (a/2)x_t$，于是它成为矩阵 $M$ 中常数维和 $x$ 维之间的交叉项。

### 2.3 一个确定性 RBC 例子：把 Hansen 模型改写成 LQ 问题

本章先从一个没有随机冲击的 Hansen-style model 开始。planner 最大化：

$$
\sum_{t=0}^{\infty}\beta^t u(c_t,h_t),
$$

其中

$$
u(c_t,h_t)=\ln c_t+A\ln(1-h_t),
$$

资源约束为：

$$
c_t=f(k_t,h_t)+(1-\delta)k_t-k_{t+1}.
$$

把消费代回效用函数后，当期效用可以写成 $k_t,k_{t+1},h_t$ 的函数：

$$
u\left(f(k_t,h_t)+(1-\delta)k_t-k_{t+1},h_t\right).
$$

于是状态变量是 $k_t$，控制变量是 $k_{t+1}$ 和 $h_t$。为了吸收 Taylor expansion 中的常数项和线性项，定义：

$$
z_t=\begin{bmatrix}1\\ k_t\\ k_{t+1}\\ h_t\end{bmatrix}.
$$

本章接着围绕 stationary state 对这个非线性 return function 做二阶 Taylor approximation，并把它写成 $z_t'Mz_t$。书中给出了一组较长的矩阵元素表达式，它们本质上都是在稳态处计算的一阶导数和二阶导数。阅读时不需要死记这些矩阵元素，但要理解它们的来源：**矩阵 $M$ 不是凭空设定的，而是原始效用函数和生产函数在稳态附近的二阶近似。**

在校准参数

$$
\beta=0.99,\quad \delta=0.025,\quad \theta=0.36,\quad A=1.72
$$

下，模型的稳态大致为：

$$
h=0.3335,\quad k=12.6695,\quad y=1.2353,\quad c=0.9186.
$$

经过 Riccati iteration 后，书中得到的 policy function 可以写成：

$$
\begin{bmatrix}k_{t+1}\\h_t\end{bmatrix}
=
\begin{bmatrix}
0.5869 & 0.9537\\
0.4146 & -0.0064
\end{bmatrix}
\begin{bmatrix}1\\k_t\end{bmatrix}.
$$

这组数字的经济含义很直接。资本越高，下一期资本也越高，因为资本具有持久性；同时劳动供给对资本状态的系数略为负，意味着当资本高于稳态时，家庭倾向于用较少劳动配合较高资本存量。这个方向不是单独由偏好决定的，而是资本积累、边际产品和闲暇效用共同作用的结果。

> #### Clarification：为什么这里没有把 $c_t$ 放进二次型？
>
> 一般 LQ 方法的思路是：对目标函数 / return function 做二阶 Taylor approximation，对约束或状态转移方程做一阶 Taylor approximation，最后得到 quadratic objective + linear transition。
>
> 但 2.3 这个 RBC 例子有一个特殊便利：资源约束可以先精确写成
>
> $$
> c_t=f(k_t,h_t)+(1-\delta)k_t-k_{t+1}.
> $$
>
> 因此我们可以先把 $c_t$ 代入效用函数，把当期 return 改写成：
>
> $$
> u\left(f(k_t,h_t)+(1-\delta)k_t-k_{t+1},h_t\right).
> $$
>
> 这样 $c_t$ 已经不是独立变量，而是由 $k_t,k_{t+1},h_t$ 决定，所以二次型里的向量只需要包含 $1,k_t,k_{t+1},h_t$，不需要再单独包含 $c_t$。
>
> 这并不是说资源约束的影响被忽略了。恰恰相反，生产函数和资源约束对消费的影响已经全部进入这个复合 return function 里。接下来做二阶近似时，近似的是这个复合函数本身。
>
> 另外，由于本例直接把 $k_{t+1}$ 当作 control variable，状态转移就是“下一期状态等于本期选择的 $k_{t+1}$”，本身已经是线性的 identity。因此这里看起来像是“省掉了约束方程的一阶近似”，更准确地说，是先用资源约束精确消元，再对消元后的 return function 做二阶近似。

### 2.4 加入随机冲击

接下来本章把线性状态转移改成：

$$
x_{t+1}=Ax_t+By_t+C\varepsilon_{t+1},
$$

其中 $E\varepsilon_{t+1}=0$。如果冲击只进入状态转移，而且目标函数仍然是 quadratic，那么 value function 变成：

$$
V(x_t)=x_t'Px_t+d.
$$

> #### Clarification 1：随机 LQ 中为什么仍然可以写 $V(x)=x'Px+d$？
>
> 这不是“先随便猜一个方便计算的函数形式”。真正的理由是：
>
> $$
> \boxed{
> \text{quadratic return}
> +
> \text{linear transition}
> +
> \text{additive zero-mean shock}
> }
> $$
>
> 会使“二次型加常数”这一函数家族在 Bellman 算子下保持封闭。
>
> 最清楚的证明是先看有限期问题。令终端价值：
>
> $$
> V_T(x_T)=0.
> $$
>
> 假设下一期价值函数为：
>
> $$
> V_{t+1}(x)=x'P_{t+1}x+d_{t+1}.
> $$
>
> 因为状态转移是：
>
> $$
> x_{t+1}=Ax_t+By_t+C\varepsilon_{t+1},
> $$
>
> 所以把它代入 $E_t[V_{t+1}(x_{t+1})]$ 后，仍然得到关于 $(x_t,y_t)$ 的二次函数，再加上一个由冲击方差产生的常数。零均值冲击使状态—冲击交叉项消失，而冲击平方项不依赖当前控制。
>
> 因此，Bellman equation 右侧仍是“二次函数加常数”。最大化这个二次函数时，一阶条件给出线性政策：
>
> $$
> y_t=F_tx_t.
> $$
>
> 再代回后，本期价值函数仍为：
>
> $$
> V_t(x_t)=x_t'P_tx_t+d_t.
> $$
>
> 于是：
>
> $$
> \boxed{
> V_{t+1}\text{ 是二次型加常数}
> \Longrightarrow
> V_t\text{ 也是二次型加常数}
> }
> $$
>
> 由有限期向后归纳，再令终点不断后移，在适当稳定性条件下就得到无穷期形式：
>
> $$
> \boxed{V(x)=x'Px+d.}
> $$
>
> ---
>
> 
>

> #### Clarification2：值函数里的 d 是什么东西？
>
> 这里多出来的 $d$ 不是消费，而是一个常数项。它来自随机冲击的方差。下面把这个结论具体展开。可以把下一期状态写成：
>
> $$
> x_{t+1}=m_t+C\varepsilon_{t+1},
> \quad
> m_t\equiv Ax_t+By_t.
> $$
>
> 如果 value function 的二次项是 $x'Px$，那么 continuation value 里会出现：
>
> $$
> E_t[V(x_{t+1})]
> =
> E_t[x_{t+1}'Px_{t+1}+d].
> $$
>
> 代入 $x_{t+1}=m_t+C\varepsilon_{t+1}$：
>
> $$
> E_t[V(x_{t+1})]
> =
> E_t[(m_t+C\varepsilon_{t+1})'P(m_t+C\varepsilon_{t+1})]+d.
> $$
>
> 展开二次型：
>
> $$
> (m_t+C\varepsilon)'P(m_t+C\varepsilon)
> =
> m_t'Pm_t
> +2m_t'PC\varepsilon
> +\varepsilon'C'PC\varepsilon.
> $$
>
> 取条件期望。因为 $E_t\varepsilon_{t+1}=0$，中间的交叉项消失：
>
> $$
> E_t[2m_t'PC\varepsilon_{t+1}]=0.
> $$
>
> 剩下：
>
> $$
> E_t[V(x_{t+1})]
> =
> m_t'Pm_t
> +E_t[\varepsilon_{t+1}'C'PC\varepsilon_{t+1}]
> +d.
> $$
>
> 其中
>
> $$
> E_t[\varepsilon_{t+1}'C'PC\varepsilon_{t+1}]
> $$
>
> 只和冲击的方差有关，不依赖 $x_t$ 或 $y_t$。如果记 $\Sigma=E[\varepsilon_{t+1}\varepsilon_{t+1}']$，这个常数可以写成：
>
> $$
> \operatorname{tr}(C'PC\Sigma).
> $$
>
> 因此随机冲击会给 value function 加上一个常数项 $d$。Bellman equation 中这个常数满足类似：
>
> $$
> d=\beta d+\beta\operatorname{tr}(C'PC\Sigma),
> $$
>
> 所以：
>
> $$
> d=\frac{\beta}{1-\beta}\operatorname{tr}(C'PC\Sigma).
> $$
>

但这个 $d$ 不依赖当期控制变量 $y_t$，冲击方差项也不依赖 $y_t$，所以对 $y_t$ 求一阶条件时它们都会消失。于是 $P$ 和 $F$ 与没有随机冲击时相同，冲击只改变 value function 的常数项，以及模拟出来的方差、协方差和样本路径。【<u>换句话来说，加入随机性之后，值函数只是多了一个与control variable yt 无关的常数项，因此不会改变最优政策函数的形式</u>】

这一点非常重要。很多初学者会以为“加入随机冲击以后，政策函数一定会改变”。在一般非线性模型里，这个直觉可能成立；但在本章这种 LQ + additive shock + risk does not affect marginal conditions 的结构下，随机冲击通过常数项进入 value function，不改变最优线性反馈矩阵。

加入技术冲击后，技术过程写成：

$$
\lambda_{t+1}=(1-\gamma)+\gamma\lambda_t+\varepsilon_{t+1}.
$$

状态向量变为：

$$
x_t=\begin{bmatrix}1\\k_t\\\lambda_t\end{bmatrix},
$$

控制变量仍然是：

$$
y_t=\begin{bmatrix}k_{t+1}\\h_t\end{bmatrix}.
$$

在 $\gamma=0.95$ 的校准下，书中得到的 policy function 为：

$$
\begin{bmatrix}k_{t+1}\\h_t\end{bmatrix}
=
\begin{bmatrix}
-0.8470 & 0.9537 & 1.4340\\
0.1789 & -0.0064 & 0.2357
\end{bmatrix}
\begin{bmatrix}1\\k_t\\\lambda_t\end{bmatrix}.
$$

技术水平越高，下一期资本和当期劳动都上升。前者对应投资增加，后者对应正技术冲击提高劳动边际产品，从而提高劳动供给。

把政策函数代回状态转移，可以得到闭环 law of motion：

$$
\begin{bmatrix}1\\k_{t+1}\\\lambda_{t+1}\end{bmatrix}
=
\begin{bmatrix}
1&0&0\\
-0.8470&0.9537&1.4340\\
0.05&0&0.95
\end{bmatrix}
\begin{bmatrix}1\\k_t\\\lambda_t\end{bmatrix}
+
\begin{bmatrix}0\\0\\1\end{bmatrix}\varepsilon_{t+1}.
$$

这个闭环系统是后面计算 variance、correlation 和 impulse response 的基础。

> #### 另一个（非递归）思路：为什么值函数是二次的？
>
> 随机 RBC 的 Euler equation（非递归形式下） 为：
>
> $$
> U'(c_t)
> =
> \beta E_t\left[
> U'(c_{t+1})
> \left(
> f_k(k_{t+1},\lambda_{t+1})+1-\delta
> \right)
> \right].
> $$
>
> 对 Euler equation 和资源约束在稳态附近做一阶近似后，会得到类似：
>
> $$
> \hat c_t
> =
> aE_t\hat c_{t+1}
> +
> b\hat k_{t+1}
> +
> dE_t\hat\lambda_{t+1},
> $$
>
> 以及：
>
> $$
> \hat k_{t+1}
> =
> \phi_k\hat k_t
> +
> \phi_\lambda\hat\lambda_t
> -
> \phi_c\hat c_t.
> $$
>
> 与确定性模型不同，第一条方程仍含有内生预期 $E_t\hat c_{t+1}$。因此，它不是一条给定 $\hat c_t$ 后就能直接向前迭代的确定性递推方程。
>
> 真正需要寻找的是自洽的消费政策函数：
>
> $$
> \hat c_t=g(\hat k_t,\hat\lambda_t).
> $$
>
> 在线性化模型中【**<u>注意：这里我们先验地假设 g 函数是线性的</u>**】，我们用待定系数法在线性函数家族中寻找它：（即将该政策函数代入原 FOC or 资源约束方程，来求解 q 必须满足的条件，筛选出逻辑自洽的 q）
>
> $$
> \boxed{
> \hat c_t
> =
> p\hat k_t+q\hat\lambda_t
> }
> $$
>
> 这里不是随便指定政策，而是先规定候选函数家族，再利用模型方程求出 $p,q$。
>
> 下一期同一政策仍然成立：
>
> $$
> \hat c_{t+1}
> =
> p\hat k_{t+1}
> +
> q\hat\lambda_{t+1}.
> $$
>
> 因而：
>
> $$
> E_t\hat c_{t+1}
> =
> pE_t\hat k_{t+1}
> +
> qE_t\hat\lambda_{t+1}.
> $$
>
> 由于 $k_{t+1}$ 已在 $t$ 期决定：
>
> $$
> E_t\hat k_{t+1}=\hat k_{t+1}.
> $$
>
> 若技术过程为：
>
> $$
> \hat\lambda_{t+1}
> =
> \rho\hat\lambda_t+\varepsilon_{t+1},
> \qquad
> E_t\varepsilon_{t+1}=0,
> $$
>
> 则：
>
> $$
> E_t\hat\lambda_{t+1}=\rho\hat\lambda_t.
> $$
>
> 所以：
>
> $$
> \boxed{
> E_t\hat c_{t+1}
> =
> p\hat k_{t+1}
> +
> q\rho\hat\lambda_t
> }
> $$
>
> 这样，原本无法直接计算的未来消费期望就被写成当前已知变量与待定系数的函数。
>
> 再把：
>
> $$
> \hat c_t=p\hat k_t+q\hat\lambda_t
> $$
>
> 代入资源约束，就能把 $\hat k_{t+1}$ 也写成当前状态的线性函数。随后将这些表达式全部代回 Euler equation，并比较 $\hat k_t$ 与 $\hat\lambda_t$ 的系数，就得到决定 $p,q$ 的代数方程。
>
> 这些方程可能产生多个候选根，因此还需要利用凹性、二阶条件、TVC 或等价的 Schur/BK 稳定性条件，选择使闭环动态稳定的政策根。【<u>这里主要是因为你把 g 函数代进去之后，求得的 g 需要满足的条件可能不能完全确定 g 应该是什么形式，可能会存在非确定性的部分，类似于确定性 RBC 里面的“初值问题”一样。因此如果要完全确定 g，可能还需要借助 TVC 等条件</u>】
>
> 最终得到线性政策：
>
> $$
> \hat c_t=p\hat k_t+q\hat\lambda_t,
> $$
>
> 以及线性闭环状态转移：
>
> $$
> x_{t+1}=Gx_t+C\varepsilon_{t+1}.
> $$
>
> 把这条线性最优政策代回每期二次收益后，每期收益变成状态的二次型：
>
> $$
> r(x_t,Fx_t)=x_t'Hx_t.
> $$
>
> 因此：
>
> $$
> V(x_t)
> =
> E_t\sum_{j=0}^{\infty}
> \beta^j x_{t+j}'Hx_{t+j}.
> $$
>
> 未来状态是当前状态与未来冲击的线性组合。展开二次型并取条件期望后：
>
> - 当前状态部分形成 $x_t'Px_t$；
> - 状态与未来冲击的交叉项因零均值而消失；
> - 冲击平方项只贡献与当前状态无关的常数。
>
> 因而仍然得到：
>
> $$
> \boxed{V(x_t)=x_t'Px_t+d.}
> $$
>
> 
>
> #### Summary：两条路线的关系
>
> $$
> \boxed{
> \begin{aligned}
> \text{Bellman--Riccati 路线：}\quad
> &V\text{ 二次}
> \Rightarrow
> g\text{ 线性};\\[4pt]
> \text{Euler--待定系数路线：}\quad
> &g\text{ 线性}
> \Rightarrow
> V\text{ 二次}.
> \end{aligned}
> }
> $$
>
> 在 LQ 结构、内点解、凹性与稳定性条件成立时，两条路线描述的是同一个最优解。第七章正文采用 Bellman–Riccati 路线；沿用你的非递归思路时，则相当于先在线性化模型中寻找稳定的线性政策函数，再由它推出二次价值函数。
>
> 因而，最准确的表述不是“第七章毫无依据地直接假定 $g$ 线性”，而是：**LQ 问题中的二次价值函数与线性政策函数构成相互闭合的结构：(1).递归方法从二次价值函数推出线性政策；(2).非递归方法从线性 Euler 系统中求出线性政策，再推出二次价值函数。**

> #### Some last comment ！！！
>
> - 关于 “为什么 V 是二次形式 / 最优政策是一次形式”
>
>     目前最好的、不涉及高级知识的证明是从有限期的问题中得出结论，然后利用归纳法推演到无穷期的情况。有限期的优点在于，可以处理 $E_t[c_{t+1}]$ ，主要就是通过从最后一期 T 开始，先算出 T 期的最优政策函数，然后再算 T-1 期、再算 T-2...，这样就可以不用 “先验地假设一个政策函数，然后再代入求解”，因为这样倒着计算，我们就已经先把未来的政策函数算好了，因此就能直接计算出这个期望  $E_t[c_{t+1}]$  到底是多少；
>
>     - 在无限期的问题中，先假设政策函数 & 先假设价值函数，他俩本质上的目的都是一样的，就是为了解决 “ct 取决于 E[c\_{t+1}]” 的无穷无尽的递归性的结构，面对递归性结构只能通过率先假设存在一个结构，然后再去验证这个结构需要满足的性质来进行求解；因此我们通过从有限期的问题开始，能够很好地规避掉这一点；
>
>     上面这个所谓的 “另一个（非递归）思路：为什么值函数是二次的？” 其实并没有完成证明（因为可以看到推导过程中加了一步“假设政策函数 g 是线性的”），而要想真正地直接从无限维问题中直接推导出 “V 是二次 / 政策函数是一次”，需要一些更加高级的知识。
>
> - 目前的结论：
>
>     1. 如果你提前知道 V 是二次函数的样子，那么政策函数一定是线性的；
>
>     2. 如果你假设政策函数是线性的，那么一定能推导出二次函数样子的值函数；

### 2.5 用 LQ 解法重新评估 basic model

有了线性 law of motion，就可以模拟模型变量并计算 second moments。本章先给出 basic model 的模拟结果。

![Table 7.1 — Simulation statistics for the basic model](../Figures/Ch07/table_7_1_simulation_stats.png)

> #### Clarification：这个表是怎样算的？
>
> 整个流程可以分成以下几个连续步骤。
>
> **第一步：校准结构参数和冲击过程。**
>
> 先给定偏好、技术和资本积累参数，例如：
>
> $$
>\beta,\quad \delta,\quad \theta,\quad \gamma,
> $$
> 
> 并校准技术冲击的方差：
>
> $$
>\operatorname{Var}(\varepsilon_t)=\sigma_\varepsilon^2.
> $$
> 
> 技术过程例如写成：
>
> $$
>\lambda_{t+1}
> =
> (1-\gamma)+\gamma\lambda_t+\varepsilon_{t+1}.
> $$
> 
> 其中，$\gamma$ 决定冲击的持久性，$\sigma_\varepsilon^2$ 决定冲击规模。完成这些参数设定以后，Riccati equation 给出最优政策矩阵。
>
> **第二步：把最优政策代回状态转移，得到闭环系统。**
>
> 假设状态向量为：
>
> $$
>s_t=
> \begin{bmatrix}
> 1\\
> k_t\\
> \lambda_t
> \end{bmatrix},
> $$
> 
> 控制向量为：
>
> $$
>u_t=
> \begin{bmatrix}
> k_{t+1}\\
> h_t
> \end{bmatrix}.
> $$
> 
> 最优政策写成：（<u>设好政策函数、代入 Euler 方程、消掉 Et[c\_{t+1}] 之后，就能够得到 ct 关于 kt 以及随机变量的一个函数，这个函数就是这个，控制变量被表示成为状态变量的函数 / 其实也就是政策函数嘛</u>）
>
> $$
>u_t=Fs_t.
> $$
> 
> 把它代回原来的状态转移方程，可以得到：（<u>这里就变成纯状态变量的递推了，就没有控制变量了</u>）
>
> $$
>\boxed{
> s_{t+1}=Gs_t+C\varepsilon_{t+1}
> }
> $$
> 
> 其中 $G$ 是闭环状态转移矩阵。继续递推可得：
>
> $$
>s_t
> =
> G^ts_0
> +
> \sum_{j=1}^{t}G^{t-j}C\varepsilon_j.
> $$
> 
> 因此，任意时点的状态都是初始状态和历次冲击的线性组合。
>
> **第三步：把所有宏观变量写成状态的线性函数。**
>
> 求出政策以后，消费、投资、劳动和产出都可以写成状态的线性函数：
>
> $$
>c_t=H_cs_t,\qquad
> i_t=H_is_t,\qquad
> h_t=H_hs_t,\qquad
> y_t=H_ys_t.
> $$
> 
> 将它们堆叠起来：
>
> $$
>v_t=
> \begin{bmatrix}
> y_t\\
> c_t\\
> i_t\\
> h_t\\
> k_t
> \end{bmatrix}
> =
> Hs_t.
> $$
> 
> 所以，模型中的所有变量最终都由同一个闭环状态系统驱动。
>
> **第四步：计算长期平稳分布下的 second moments。**
>
> 这里有两种等价的实现方法。
>
> 第一种是模拟法（<u>直接采样一条模拟路径，然后算样本方差</u>）。给定初始状态 $s_0$，从已校准的冲击分布中反复抽取：
>
> $$
>\varepsilon_1,\varepsilon_2,\ldots,\varepsilon_T,
> $$
> 
> 再利用：
>
> $$
>s_{t+1}=Gs_t+C\varepsilon_{t+1}
> $$
> 
> 生成一条足够长的时间序列。然后由模拟得到的 $y_t,c_t,i_t,h_t,k_t$ 计算样本标准差、样本相关系数和样本自相关系数。书中所说的 simulation statistics，主要就是这条路线。
>
> 第二种是解析法（<u>算出解析形态之后，使用公式直接计算</u>）。若闭环系统稳定，则当 $t\to\infty$ 时，初始状态的影响：
>
> $$
>G^ts_0
> $$
> 
> 会逐渐消失，系统进入由持续随机冲击维持的平稳分布。去掉常数维以后，记状态偏离为 $\tilde s_t$：
>
> $$
>\tilde s_{t+1}
> =
> G\tilde s_t+C\varepsilon_{t+1}.
> $$
> 
> 令状态的无条件协方差矩阵为：
>
> $$
>\Sigma_s
> =
> E[\tilde s_t\tilde s_t'].
> $$
> 
> 它满足离散 Lyapunov equation：
>
> $$
>\boxed{
> \Sigma_s
> =
> G\Sigma_sG'
> +
> C\Sigma_\varepsilon C'
> }
> $$
> 
> 其中：
>
> $$
>\Sigma_\varepsilon
> =
> E[\varepsilon_t\varepsilon_t'].
> $$
> 
> 解出 $\Sigma_s$ 后，因为：
>
> $$
>v_t=H\tilde s_t,
> $$
> 
> 所有宏观变量的协方差矩阵就是：
>
> $$
>\boxed{
> \Sigma_v
> =
> H\Sigma_sH'
> }
> $$
> 
> 模拟法是从一条很长的随机样本路径估计这些 moments；解析法则直接由闭环矩阵和冲击方差计算理论 moments。在线性模型中，两种方法在样本足够长时应当相互接近。
>
> **第五步：从协方差矩阵中提取需要报告的统计量。**
>
> 首先是每个变量的标准差：
>
> $$
>\sigma_x
> =
> \sqrt{\operatorname{Var}(x_t)}.
> $$
> 
> 其次是相对标准差。例如把产出的波动设为 $100\%$，消费的相对波动为：
>
> $$
>\boxed{
> \frac{\sigma_c}{\sigma_y}\times100\%
> }
> $$
> 
> 投资和劳动的相对波动分别为：
>
> $$
>\frac{\sigma_i}{\sigma_y}\times100\%,
> \qquad
> \frac{\sigma_h}{\sigma_y}\times100\%.
> $$
> 
> 这些比率回答的是：某变量的波动幅度是产出波动的多少倍。
>
> 再次是变量与产出的相关系数：
>
> $$
>\boxed{
> \operatorname{Corr}(x_t,y_t)
> =
> \frac{\operatorname{Cov}(x_t,y_t)}
> {\sigma_x\sigma_y}
> }
> $$
> 
> 它回答的是该变量是否与产出同方向波动。相关系数为正，表示顺周期；为负，表示逆周期。
>
> 有些表格还会报告自相关系数：
>
> $$
>\operatorname{Corr}(x_t,x_{t-1}),
> $$
> 
> 用来衡量变量的持续性。
>
> 因此，从政策函数到表 7.1 的完整逻辑是：
>
> $$
>\boxed{
> \begin{aligned}
> &\text{校准参数和冲击方差}\\
> &\Rightarrow \text{求出最优政策 }u_t=Fs_t\\
> &\Rightarrow \text{构造闭环系统 }s_{t+1}=Gs_t+C\varepsilon_{t+1}\\
> &\Rightarrow \text{把 }y_t,c_t,i_t,h_t,k_t\text{ 写成状态的线性函数}\\
> &\Rightarrow
> \begin{cases}
> \text{模拟长时间序列并计算样本 moments},\\
> \text{或解 Lyapunov equation 得到理论 moments}
> \end{cases}\\
> &\Rightarrow \text{报告标准差、相对标准差、相关系数和自相关系数。}
> \end{aligned}
> }
> $$
> 
> 这里 $t\to\infty$ 的含义不是要求 $y_t,c_t$ 等变量收敛到某个固定数值，而是让初始条件的影响消失，使随机系统进入平稳分布，再研究这个平稳分布下的波动特征。
>
> 在实际 RBC 文献中，即使理论 moments 可以解析求出，也经常使用模拟法，因为这样可以生成与真实数据相同长度的样本，并对模拟数据使用与真实数据相同的滤波方法，例如 HP filter。

表 7.1 的读法与第 6 章类似：先看各变量的标准差，再看它们与 output 的相关性。basic model 可以生成顺周期的 consumption、investment、hours 和 technology，但 hours 的波动明显偏低。这一问题在第 6 章已经出现过：连续可调劳动模型通常让劳动反应过于平滑，无法匹配真实经济中劳动时长相对产出的高波动。

### 2.6 Indivisible labor：为什么要再次引入 Hansen 的劳动彩票？

为了改善 hours worked 的波动，本章再次引入 Hansen 的 indivisible labor。个体不能选择任意劳动时间，而是在“工作固定时长 $h_0$”和“不工作”之间选择。通过 lottery 与 insurance，代表性家庭的效用可以写成：

$$
E\sum_{t=0}^{\infty}\beta^t\left[\ln c_t+\alpha_t A\ln(1-h_0)\right],
$$

其中 $\alpha_t$ 是工作概率，也等于 aggregate employment rate。

> #### 如何理解 at？
>
> indivisible labor 的核心在于不能够选择劳动市场，要么完全不劳动，要么就固定劳动 h0 个小时。那么这个时候，对于代表性家庭而言，他们的决策变量变成啥了呢？其实就是 at，但是不应该理解为参与“工作的概率”，这样容易产生误解：“家庭怎么能够决定这个概率呢？”，实际上 at 就是家庭中参与劳动的人数，不过一般我们认为一个家庭只有一单位劳动力，因此 at=0.5 就代表一半的家庭成员参与了劳动。

> #### 为什么 indivisible labor 能够增加波动？
>
> 不妨假设 h0 = 0.5（代表一半的时间用来工作），那么：
>
> - 劳动时间可调整：$\frac{\partial{loss}}{\part{h_0}\\}=A·\frac{1}{0.5}\approx 2A$
>
> - 不可变劳动时间：$\frac{\part loss}{\part a\\}=Aln(0.5)\approx 0.69A$
>
>     但是注意到要统一单位，我们看的波动不是 a，而是劳动时间，即 N = a·h0，因此:
>
>     $\frac{\part loss}{\part N\\}\approx \frac{(\part loss/\part a)·(da)}{dN}=\frac{(\part loss/\part a)·(da)}{da·h_0}=\frac{0.69A}{0.5}\approx 1.38A$
>
>     所以可以看到，在这里劳动的边际损失没有很大，因此劳动自身变动的 “阻尼” 较小，所以会导致劳动时间的波动幅度加大；

生产函数变成：
$$
y_t=\lambda_t k_t^\theta(\alpha_t h_0)^{1-\theta}.
$$

在 LQ 形式下，状态变量仍然包含 $1,k_t,\lambda_t$，控制变量则变成 $k_{t+1}$ 和 $\alpha_t$。劳动选择的非线性被转移到生产函数和 Taylor approximation 中；效用中的劳动 disutility 对 $\alpha_t$ 是线性的。

这一结构的经济含义是：总劳动的调整更多来自 employment margin，而不是每个个体连续微调工作时长。这样 aggregate hours 对技术冲击更敏感，模型生成的 hours volatility 会更接近美国数据。

先看美国数据中的 second moments：

![Table 7.2 — US data statistics](../Figures/Ch07/table_7_2_us_data_stats.png)

再看模型对比：

![Table 7.3 — Model standard errors: basic model vs indivisible labor](../Figures/Ch07/table_7_3_model_standard_errors.png)

表 7.3 的核心信息非常清楚：basic model 中 hours 的相对标准差只有 output 的约 38%，而 indivisible labor model 把它提高到约 61%，与表 7.2 的美国数据更加接近。investment 的相对波动也更接近数据。换句话说，indivisible labor 并不是一个装饰性设定，它直接改善了 RBC 模型最重要的 second-moment fit。

### 2.7 Impulse response functions：从一次技术冲击看动态机制

本章接着用 impulse response function 检验模型如何响应一次技术冲击。设定是在第 2 期给技术过程一个 1% 的冲击，然后观察 output、consumption、investment、hours、capital 和 technology 的动态路径。

> <u>我们在 RBC 中折腾这么久主要就是为了得到各变量的递推方程系统，然后通过第一期的初始变量，推演出后续所有的变动，比如我们可以把变量一开始设置在均衡位置，然后假设某个时间点发生冲击（即设置好冲击序列 {εt}），然后通过递推公式来计算出后续的所有变量的路径，这其实就是 IRF</u>。这一章节的 IRF 就是这么画出来的。

图 7.1 用 levels 展示这些变量的响应：

![Figure 7.1 — Impulse responses in levels](../Figures/Ch07/figure_7_1_irf_levels.png)

因为资本存量的 level 远大于其他变量，直接画 levels 时资本曲线会支配视觉尺度。因此图 7.2 改用 log deviations，便于比较不同变量的相对响应：

![Figure 7.2 — LQ impulse responses in log deviations](../Figures/Ch07/figure_7_2_lq_irf.png)

图 7.2 的经济机制与第 6 章基本一致。正技术冲击提高劳动边际产品，使 hours、output 和 investment 当期上升。消费也上升，但通常比 investment 平滑。资本因为投资增加而逐步积累，并在冲击消退后缓慢回落。技术冲击本身因为 $\gamma=0.95$ 具有很强 persistence，所以整个经济响应也带有明显持久性。

图 7.3 直接比较本章 LQ 解法与第 6 章 log-linearization 解法得到的 impulse responses：

![Figure 7.3 — Comparing LQ and log-linear solution methods](../Figures/Ch07/figure_7_3_solution_comparison.png)

两条路径非常接近，但不是完全重合。原因在于两种方法近似的对象不同：第 6 章近似的是一阶条件和约束；第 7 章近似的是 objective function 与状态转移结构。两者都在稳态附近有效，但保留的信息不同，因此数值结果会有细微差异。

### 2.8 VAR 与 empirical impulse responses

本章还短暂介绍了 vector autoregressions。这部分并不是要用 VAR 替代 RBC 模型，而是在回答一个更靠后的问题：

> 前面已经从 RBC 模型求出了各变量的 law of motion 和 theoretical impulse responses，那么应当怎样把这些理论动态与真实数据中的动态进行比较？

#### VAR 也可以理解成一个递推系统

以 VAR(1) 为例：

$$
y_t=Ay_{t-1}+u_t,
$$

其中 $y_t$ 是一组宏观变量，$A$ 从数据中估计，$u_t$ 是当期不可由过去信息预测的 innovation。给定初值 $y_0$ 和冲击序列以后，整个系统可以逐期递推：

$$
\begin{aligned}
y_1&=Ay_0+u_1,\\
y_2&=A^2y_0+Au_1+u_2,\\
&\ \vdots
\end{aligned}
$$

VAR($p$) 需要最近 $p$ 期的初始值，但可以通过 companion form 改写为一个更大的 VAR(1)。所以从动态系统的角度看，估计后的 VAR 和求解后的 RBC 确实具有相似的形式：

$$
\boxed{
\text{下一期变量}
=
\text{过去变量的线性函数}
+
\text{当期冲击}.
}
$$

不过二者的系数来源不同。求解后的 RBC 可以写成：

$$
x_{t+1}=Gx_t+C\varepsilon_{t+1},
$$

其中 $G$ 来自偏好、技术、约束和最优化；而 VAR 的系数矩阵来自对数据的统计估计。因此，RBC 给出的是模型预测的理论动态，VAR 提取的是数据中的经验动态。

#### 从递推系统到 impulse response

impulse response 的直观定义正是：

1. 先给定一条没有额外冲击的基准路径；
2. 在某一期对某个冲击施加一次单位变化；
3. 此后把新增冲击重新设为零，并利用递推方程向后模拟；
4. 用冲击路径减去基准路径。

> <u>我们在 RBC 中折腾这么久主要就是为了得到各变量的递推方程系统，然后通过第一期的初始变量，推演出后续所有的变动，比如我们可以把变量一开始设置在均衡位置，然后假设某个时间点发生冲击，然后模拟后续变动，这其实就是 IRF</u>。

例如，在 VAR(1) 中令第 0 期出现一次冲击 $e_j$，以后不再出现新冲击，则：

$$
\begin{aligned}
IRF(0)&=e_j,\\
IRF(1)&=Ae_j,\\
IRF(2)&=A^2e_j,\\
&\ \vdots
\end{aligned}
$$

这与 RBC 中“让经济从稳态出发，在某一期施加一次技术冲击，然后利用闭环 law of motion 模拟后续变量”的操作是同一个动态思想。在线性系统中，IRF 更一般地等于“有冲击路径”和“无冲击路径”之差，并不一定要求初始状态恰好位于稳态；从稳态出发只是最容易解释。

#### 为什么书中把 VAR 转换成 MA representation？

VAR 是一个适合估计和递推的表示：

$$
y_t=A(L)y_{t-1}+u_t.
$$

将其写成 moving-average representation 后：

$$
y_t=C(L)u_t
=
C_0u_t+C_1u_{t-1}+C_2u_{t-2}+\cdots.
$$

矩阵 $C_j$ 直接表示一单位 innovation 在 $j$ 期以后对各变量的影响。因此，$C_j$ 的相应列就是第 $j$ 期的 impulse response。VAR 与 MA 并非两个不同的经济模型：前者按变量的滞后值递推，后者把同一个动态系统改写成历史冲击的累积结果。

#### 理论 IRF 与 empirical IRF

RBC 模型中的 $\varepsilon_t$ 通常被模型直接定义为某种 structural shock，例如 technology shock。模型求解后，可以计算：

$$
\text{technology shock}
\longrightarrow
\{y_t,c_t,i_t,h_t,k_t,\ldots\}
$$

的理论响应。

VAR 则可以从真实数据中估计变量受到 innovation 后的经验响应。于是可以比较：

$$
\boxed{
\text{RBC theoretical IRF}
\quad\text{与}\quad
\text{VAR empirical IRF}.
}
$$

如果模型声称技术冲击是商业周期的重要来源，那么模型产生的 output、consumption、investment 和 hours 等变量的响应方向、相对幅度及持久性，应当与数据中估计出的响应大体一致。相较于只比较标准差和相关系数，IRF 比较对模型提出了更严格的动态要求。

#### 识别问题：VAR residual 不自动等于经济学冲击

这里存在一个重要困难。reduced-form VAR 中的 $u_t$ 首先只是预测误差，并不自动等于具有清晰经济含义的 technology shock、monetary shock 等结构冲击。不同方程的 residual 还可能在当期相互相关。

因此，要把 VAR innovation 解释为某一种 structural shock，通常需要额外的 identification assumptions，例如变量排序、短期限制、长期限制、符号限制或外部工具变量。书中特别指出，现实中的“技术冲击”是什么、大小如何以及如何从数据中识别，本身就很困难。如果无法找到与模型冲击相对应的现实冲击，理论 IRF 与 empirical IRF 便不能被简单地直接比较。

> ##### <u>RBC 的 IRF 不好直接跟 VAR 的 IRF 比较</u>
>
> 这里会产生问题，就是 RBC 的 IRF 不好直接跟 VAR 的 IRF 比较，因为 VAR 的冲击识别可能不一定很好，识别出来的冲击并不一定就能够在经济含义上一一对应到 RBC 中设置的各个冲击变量，因此比如 RBC 拿 λ1 的冲击来分析、VAR 拿分离出的第一个独立冲击，两个冲击可能根本就不是同一个东西，导致 “鸡同鸭讲”，因此我们说两者不好直接比较。

#### Sims 提出的另一种比较方式

乍看之下，我们似乎可以直接比较：

$$
\text{RBC 模型算出来的 IRF}
\quad\text{与}\quad
\text{现实数据中的 VAR IRF}.
$$

但这两者未必是同一种口径下的对象。

在 RBC 模型里，研究者自己规定了什么叫 technology shock。例如，技术过程中的创新 $\varepsilon_t$ 就被直接定义为“纯技术冲击”。因为模型的全部结构和参数都是已知的，我们可以直接计算这个冲击对所有变量的真实模型响应。

现实 VAR 则没有这种“上帝视角”。VAR 首先只能得到一组无法由过去信息预测的 residual。这些 residual 可能混合了技术、货币、财政、偏好等多种冲击。研究者必须再加入变量排序、长期限制、符号限制等 identification assumptions，才能从中分离出一个被称为“技术冲击”的对象。

问题在于：

> VAR 根据某套识别假设分离出来的“技术冲击”，不一定恰好等于 RBC 模型中事先定义的那个纯技术冲击。

此外，模型 IRF 通常是根据已知模型矩阵直接计算的 population response；现实 VAR IRF 却会受到有限样本、变量遗漏、滞后阶数、数据去趋势方法以及估计误差的影响。因此，直接比较有点像让一边提交“模型的标准答案”，另一边提交“从有限现实数据中估计出来的答案”，两边经历的处理过程并不相同。

Sims 提出的办法可以通俗地理解为：

> 既然现实数据必须经过 VAR 才能得到 IRF，那就让 RBC 模型生成的数据也经过完全相同的 VAR 程序，然后再比较。

具体做法是：

1. 用校准后的 RBC 模型生成与现实样本长度相近的模拟数据；
2. 对模拟数据采用与现实数据相同的变量选择、去趋势方法和滞后阶数；
3. 使用相同的 VAR specification 和 shock identification 方法；
4. 分别计算模拟数据 VAR 与现实数据 VAR 的 IRF；
5. 比较这两组经过相同程序得到的 IRF。

因此最后比较的是：

$$
\boxed{
\text{RBC 模拟数据经过 VAR 得到的 IRF}
\quad\text{与}\quad
\text{现实数据经过 VAR 得到的 IRF}.
}
$$

这相当于让模型数据和现实数据“参加同一场考试”。即使 VAR 的识别方法不能完美恢复真正的结构冲击，有限样本和 VAR specification 也会造成误差，至少这些处理会同时施加在两边，比较口径更加一致。

不过，这种方法并没有自动解决冲击识别问题。它只是控制了计量程序不同所造成的差异。如果两组 IRF 最后仍不一致，原因可能来自 RBC 模型本身，也可能来自所采用的 VAR 识别方法；解释结果时仍需谨慎。

因此，本节的核心作用可以概括为：

$$
\boxed{
\text{RBC 求解给出理论递推系统和理论 IRF；}
\quad
\text{VAR 从数据中提取经验递推关系和 empirical IRF；}
\quad
\text{IRF 是检验二者动态一致性的一座桥梁。}
}
$$

### 2.9 Alternative technology process：冲击过程本身也会影响动态响应

本章后面还讨论了技术过程的替代设定。这里最重要的不是某个具体公式，而是一个建模原则：**外生冲击过程的 persistence 和形式会直接影响模型动态。**

如果技术冲击高度持久，家庭会把它理解为较长期的生产率改善，于是投资和资本积累反应更强。如果技术冲击很快消失，最优反应会更偏向短期劳动和消费调整，资本响应相对较弱。因此，RBC 模型中的 impulse response 不仅来自偏好、技术和资本积累，也高度依赖外生 shock process 的设定。

## 3. Compact Summary: What You Must Retain

本章最重要的内容可以压缩成五句话。

第一，linear-quadratic dynamic programming 是第 6 章 log-linearization 的替代求解方法；它不是换了一个经济模型，而是换了一个近似和求解入口。

第二，LQ 方法需要 quadratic objective 和 linear transition。二阶 Taylor approximation 负责提供 quadratic objective，把常数 1 加入状态向量则可以把常数项和线性项一起写进二次型。

第三，在 LQ 问题中，value function 也是 quadratic，政策函数是 linear feedback rule：

$$
y_t=Fx_t.
$$

核心计算对象是 Riccati equation。

第四，当随机冲击以 additive form 进入线性状态转移，并且不直接改变目标函数曲率时，shock variance 只改变 value function 的常数项，不改变 policy matrix $F$。

第五，LQ 方法复制了第 6 章的主要经济结论：basic model 的 hours volatility 偏低，indivisible labor 能显著改善 hours 和 investment 的相对波动；LQ 与 log-linear 解法的 impulse responses 很接近，但不完全相同。

## 4. Figures, Tables, and Formulas to Check in the Original

本章最应该对照原文检查的是以下内容。

> ⚠️【需要回原文看图】这里涉及重要图表/表格/公式，PDF 文本提取可能不足以完整保留信息。建议回到原文核对。

**Figure 7.1** 展示一次技术冲击下各变量的 level response。它的主要作用是提醒我们：直接画 level 时，资本存量因为量级较大，会压缩其他变量的视觉变化。

**Figure 7.2** 展示 LQ 解法下的 log-deviation impulse responses。这是理解本章经济机制的核心图。

**Figure 7.3** 比较 LQ 解法和第 6 章 log-linear 解法。它说明两种近似在稳态附近给出相近结论，但数值上不必完全一致。

**Table 7.1** 给出 basic model 的 simulated standard errors 和 correlations。重点看 hours volatility 偏低。

**Table 7.2** 给出美国数据的对照 moments。它是判断模型 fit 的 benchmark。

**Table 7.3** 比较 basic model 和 indivisible labor model。重点看 indivisible labor 如何改善 hours 和 investment 的相对标准差。

**Riccati equation** 是本章的技术核心：

$$
P=R+\beta A'PA-(\beta A'PB+W')(Q+\beta B'PB)^{-1}(\beta B'PA+W).
$$

如果要复现本章 Matlab code，必须逐项检查矩阵维度、变量排序和 $M,R,Q,W,A,B,C$ 的定义。最容易出错的地方不是经济直觉，而是矩阵中变量顺序不一致。

## 5. Questions and Answers

**Q1：为什么第 7 章不继续沿用第 6 章的 log-linearization？**

因为作者想展示另一种常用的动态宏观求解方法。log-linearization 是近似 FOCs；LQ 方法是近似原始优化问题。两者都能得到线性 policy rule，但近似对象不同。

**Q2：为什么一阶 Taylor approximation 不够？**

一阶近似只给出线性目标函数，缺乏曲率。没有曲率，就很难产生稳定的内点最优决策。二阶近似保留了边际收益和边际成本随状态变化而变化的信息，所以才能形成有意义的 feedback rule。

**Q3：为什么要把常数 1 放进 state vector？**

因为二阶 Taylor expansion 中包含常数项和线性项。把 1 放进向量以后，常数项可以写成 $1\cdot 1$，线性项可以写成 $1\cdot x$ 的交叉项。这样整个近似目标函数都可以统一写成 $z'Mz$。

**Q4：随机冲击为什么不改变 policy function？**

在本章设定下，冲击是 additive shock，且均值为 0。它进入 value function 时只增加一个与当期控制无关的常数项。既然一阶条件不受这个常数项影响，最优政策矩阵 $F$ 就不变。冲击会影响模拟方差和样本路径，但不改变线性反馈规则。

**Q5：LQ 方法和 log-linearization 方法哪一个更“正确”？**

不能简单说谁更正确。它们都是稳态附近的近似方法。log-linearization 更贴近经济学家从 FOCs 出发的习惯；LQ 方法更贴近控制理论和动态规划。只要模型在稳态附近波动不大，两者通常会给出相似结论。

**Q6：为什么 indivisible labor 能改善模型表现？**

因为它把劳动调整从 intensive margin 转向 extensive margin。个体不是连续改变工作时长，而是在工作与不工作之间通过 lottery 调整就业概率。这样 aggregate hours 对冲击更敏感，hours volatility 更接近美国数据。

**Q7：这一章最值得带走的技术能力是什么？**

你需要掌握一套转换思路：先找稳态，再围绕稳态二阶近似目标函数，把问题写成 LQ 形式，求 Riccati equation，得到 linear feedback rule，最后模拟 second moments 和 impulse responses。这套流程是后面很多 DSGE 近似解法的重要基础。
