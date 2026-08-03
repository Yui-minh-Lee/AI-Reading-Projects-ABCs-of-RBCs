# Chapter 11 — Lecture Note

> Importance: ★★★★☆  
> Suggested audit model: high  
> Reading mode: careful  
> Estimated note reading time: 65-85 minutes  
> Source reliability: text OK; major figures/tables embedded as source screenshots; matrix blocks should be checked against the original before coding

## 0. How to read this note

第 11 章把第 10 章的 staggered pricing 思路搬到 labor market。第 10 章中，差异化的是 intermediate goods，拥有 market power 的是 intermediate goods firms；第 11 章中，差异化的是 labor types，拥有 market power 的是 households / workers。家庭提供不同类型劳动，劳动打包厂商（labor bundler）把这些差异化劳动合成为最终生产部门使用的 effective labor。

读这一章时建议把它和第 10 章并排看：

- 第 10 章：final goods firm 打包 differentiated goods，intermediate firms 设置 sticky prices。
- 第 11 章：labor bundler 打包 differentiated labor，households 设置 sticky nominal wages。

本章最重要的结论是：staggered wage setting 也能让 money growth shocks 对真实变量产生 persistent effects，而且它避免了第 10 章 staggered pricing model 中 positive technology shock 下某些真实变量短期大幅负响应的奇怪现象。

## 1. Opening: 本章的核心问题

价格粘性不是让货币政策产生真实效应的唯一方式。现实中，工资也常常调整缓慢：合同、谈判、制度安排、心理锚定、工资刚性都会让 nominal wages 难以连续快速变化。第 11 章问的是：如果把 Calvo friction 放在 wage setting 上，而不是 price setting 上，会得到怎样的动态宏观模型？

本章要回答四个问题：

1. 怎样把 heterogeneous labor types 放进代表性家庭框架？
2. 为什么 staggered wage setting 需要一个 insurance arrangement？
3. household 的最优工资方程如何导出 wage Phillips curve 式的关系？
4. sticky wages 下，technology shock 和 money growth shock 的 IRF 与前面模型有什么不同？

## 2. Main Lecture

### 2.1 Labor bundler：把 differentiated labor 合成为 effective labor

本章假设每个 household 提供一种差异化劳动 $h_t^i$。最终生产部门不直接使用每一种劳动，而是使用 labor bundler 合成的 effective labor：

$$
H_t=
\left[
\int_0^1(h_t^i)^{\frac{\psi_w-1}{\psi_w}}di
\right]^{\frac{\psi_w}{\psi_w-1}}.
$$

这里 $\psi_w$ 是不同劳动类型之间的 elasticity of substitution。$\psi_w$ 越大，各类劳动越容易替代【<u>$\psi_w$ 越大，里面呢越接近线性函数，线性函数下如果各要素成本稍有变化，那么替代幅度将会非常大</u>】，单个 worker 的 wage-setting power 越弱；$\psi_w$ 越小，劳动类型越特殊，worker 的 market power 越强。

劳动打包厂商是 perfectly competitive，所以 aggregate nominal wage index 为：

$$
W_t=
\left[
\int_0^1W_t(i)^{1-\psi_w}di
\right]^{\frac{1}{1-\psi_w}}.
$$

对每种劳动的需求为：

$$
h_t^i=H_t\left(\frac{W_t}{W_t(i)}\right)^{\psi_w}.
$$

这和第 10 章的中间品需求完全平行。第 10 章是：

$$
Y_t(k)=Y_t\left(\frac{P_t}{P_t(k)}\right)^\psi.
$$

本章只是把 product price 换成 wage，把 intermediate firm 换成 household。

### 2.2 Calvo wage setting 与 insurance arrangement

每一期有 $1-\rho_w$ 的 households 可以重新选择工资，其余 $\rho_w$ 的 households 不能优化工资，baseline 情形下保持上一期 nominal wage：

$$
W_t(i)=W_{t-1}(i).
$$

也可以设定其他 rule of thumb，例如按 steady inflation 或 lagged inflation 调整工资，但本章主体先使用 fixed nominal wage rule。

这里有一个第 10 章没有的麻烦：<u>**如果不同 household 的工资不同，它们的劳动收入就不同；如果劳动收入不同，它们的储蓄、资本持有、消费和边际效用都会不同；如果边际效用不同，那么获得调工资机会的 household 不会选择同一个工资。这会让模型变成一个复杂的异质性家庭问题**</u>。

为了避免这个问题，作者引入 labor income insurance arrangement。直觉上，在 household 知道自己本期是否能调工资之前，先进入一个保险市场。保险使所有家庭在均衡中拥有相同 consumption 和 marginal utility of consumption。这样，即使不同家庭的 nominal wage 不同，经过保险支付之后，它们的当期消费相同，模型仍能保持代表性结构。

这个保险安排在 aggregate level 会消失，因为总 premiums 和 payouts 加总为零。但它在模型内部非常重要：它让所有能优化工资的 households 在同一时期选择同一个 $W_t^*$。

### 2.3 Household problem：工资选择为什么包含未来劳动需求？

家庭效用为：

$$
E_t\sum_{j=0}^{\infty}\beta^j
\left[
\ln c_{t+j}^i+A\ln(1-h_{t+j}^i)
\right].
$$

本章仍有 cash-in-advance constraint：

$$
P_tc_t^i=m_{t-1}^i+(g_t-1)M_{t-1},
$$

以及 budget constraint：

$$
k_{t+1}^i+\frac{m_t^i}{P_t}
=\frac{W_t(i)}{P_t}h_t^i+r_tk_t^i+(1-\delta)k_t^i+b_t^i.
$$

其中 $b_t^i$ 是保险支付或保费。

当 household 在 $t$ 期可以选择工资时，它知道这个工资未来第 $j$ 期仍然有效的概率是 $\rho_w^j$。因此，它选择 $W_t^*$ 时最大化：

$$
E_t\sum_{j=0}^{\infty}(\beta\rho_w)^j
\left[
\ln c_{t+j}^i+A\ln(1-h_{t+j}^i)
\right],
$$

> 一个重要的数学依赖：
>
> $E_t[...]=E\Big[E_t[...|p=1]·P(p=1)+E_t[...|p=0]·P(p=0)\Big]$ 
>
> 而求导只能对前面 p=1 的这部分进行，因此我们写成上面这个形式的前提是：$E_t[...|p=1]=E_t[...]$ 

subject to future constraints and labor demand：
$$
h_{t+j}^i
=H_{t+j}
\left(\frac{W_{t+j}}{W_t^*}\right)^{\psi_w}.
$$

这个式子解释了为什么 wage setting 是 forward-looking：今天设定的工资可能在未来很多期继续有效，而未来的 aggregate wage、labor demand、prices 和 consumption 都会影响这个工资是否合适。

### 2.4 非工资 FOCs：价格出现 $t+2$ 的技术问题

对 consumption、money、capital 求一阶条件，可以整理为：

$$
\vartheta_t^1=-\frac{1}{P_tc_t^i},
$$

$$
\vartheta_t^2
=-\beta E_t\frac{P_t}{P_{t+1}c_{t+1}^i},
$$

以及：

$$
E_t\frac{P_t}{P_{t+1}c_{t+1}^i}
=
\beta E_t
\left[
\frac{P_{t+1}}{P_{t+2}c_{t+2}^i}
(r_{t+1}+1-\delta)
\right].
$$

这个条件让价格形成具有 forward-looking component，因为它同时涉及 $P_t,P_{t+1},P_{t+2}$。但我们前面使用的求解方法通常处理 $t-1,t,t+1$ 的系统，$t+2$ 会造成技术麻烦。

作者强调，**<u>不能简单把这条式子整体往前挪一期，因为原式是两个条件期望之间的关系</u>**；强行改成带 $P_{t-1}$ 的 backward-looking 形式会改变模型动态，甚至导致 explosive behavior。

后面 log-linearization 时，作者用 CIA constraint 和 money growth process 把 $P_{t+2}c_{t+2}$ 替换掉，从而把系统重新写成只含 $t$ 和 $t+1$ 的形式。

### 2.5 最优工资方程：sticky wage 的核心

对 $W_t^*$ 求一阶条件，经过代入乘子后，可以得到 wage-setting rule：

$$
W_t^*(i)
=
\frac{\psi_w}{\psi_w-1}
\frac{A}{\beta}
\frac{
E_t\sum_{j=0}^{\infty}(\beta\rho_w)^j
\frac{h_{t+j}^i}{1-h_{t+j}^i}
}{
E_t\sum_{j=0}^{\infty}(\beta\rho_w)^j
\frac{h_{t+j}^i}{P_{t+1+j}c_{t+1+j}^i}
}.
$$

不要被形式吓到。它的经济含义类似第 10 章：

- 第 10 章的 intermediate firm 设定 price，面对未来 marginal cost；
- 第 11 章的 household 设定 wage，面对未来 labor disutility 和 consumption marginal utility。

$\psi_w/(\psi_w-1)$ 是 wage markup。household 因为提供 differentiated labor 而有 market power，可以把 wage 设置在边际替代率之上。

### 2.6 Rest of the model：生产部门仍然竞争

本章生产部门没有第 10 章那样的 sticky prices。企业使用 aggregate production function：

$$
Y_t=\lambda_tK_t^\theta H_t^{1-\theta}.
$$

竞争性要素价格为：

$$
\frac{W_t}{P_t}
=(1-\theta)\frac{Y_t}{H_t},
$$

$$
r_t=\theta\frac{Y_t}{K_t}.
$$

aggregate budget constraint 为：

$$
K_{t+1}+\frac{M_t}{P_t}
=\frac{W_t}{P_t}H_t+r_tK_t+(1-\delta)K_t.
$$

由于劳动打包厂商零利润：

$$
W_tH_t=\int_0^1W_t(i)h_t^i\,di.
$$

保险市场在 aggregate level 也消失，因为总保险支付为零。

### 2.7 Stationary state：工资 markup 如何改变稳态？

稳态中，所有 real variables 常数，货币增长和技术冲击为 1，nominal wages 和 prices 不变。Calvo wage aggregation 给出：

$$
\bar W^*=\bar W,
\qquad
\bar h^*=\bar H.
$$

资本 Euler equation 给出：

$$
\bar r=\frac{1}{\beta}-1+\delta.
$$

CIA constraint 给出：

$$
\frac{M}{P}=\bar C.
$$

wage-setting equation 给出 real wage：

$$
\frac{W}{P}
=
\frac{\psi_w}{\psi_w-1}
\frac{A\bar C}{\beta(1-\bar H)}.
$$

> - 注意 1：这里 AC 不是指平均成本，A 是稳态技术、$\bar{C}$ 是稳态消费；
>
> - 注意 2：这里是求稳态方程，而不是一阶线性化；

> #### 具体推导
>
> 先从本书的最优工资方程出发：
> $$
> W_t^*
> =
> \frac{\psi_w}{\psi_w-1}
> \frac{A}{\beta}
> \frac{
> E_t\sum_{j=0}^{\infty}(\beta\rho_w)^j
> \dfrac{h_{t+j}^*}{1-h_{t+j}^*}
> }{
> E_t\sum_{j=0}^{\infty}(\beta\rho_w)^j
> \dfrac{h_{t+j}^*}{P_{t+1+j}C_{t+1+j}}
> }.
> $$
> 在稳态中：
> $$
> W_t^*=\bar W,\qquad
> h_{t+j}^*=\bar H,\qquad
> P_{t+1+j}=\bar P,\qquad
> C_{t+1+j}=\bar C.
> $$
> 因此分子变成：
> $$
> \sum_{j=0}^{\infty}(\beta\rho_w)^j
> \frac{\bar H}{1-\bar H},
> $$
> 分母变成：
> $$
> \sum_{j=0}^{\infty}(\beta\rho_w)^j
> \frac{\bar H}{\bar P\bar C}.
> $$
> 两边共同的几何级数：
> $$
> \sum_{j=0}^{\infty}(\beta\rho_w)^j
> $$
> 相消，$\bar H$ 也相消，于是比值为：
> $$
> \frac{\dfrac{\bar H}{1-\bar H}}
> {\dfrac{\bar H}{\bar P\bar C}}
> =
> \frac{\bar P\bar C}{1-\bar H}.
> $$
> 所以：
> $$
> \bar W
> =
> \frac{\psi_w}{\psi_w-1}
> \frac{A}{\beta}
> \frac{\bar P\bar C}{1-\bar H}.
> $$
> 两边除以 $\bar P$：
> $$
> \boxed{
> \frac{\bar W}{\bar P}
> =
> \frac{\psi_w}{\psi_w-1}
> \frac{A\bar C}{\beta(1-\bar H)}.
> }
> $$

这里的重点是 wage markup：由于 labor type 差异化，家庭设置的 wage 高于竞争性边际替代率。

生产端给出：

$$
\bar Y=\bar K^\theta\bar H^{1-\theta},
$$

$$
\frac{W}{P}=(1-\theta)\frac{\bar Y}{\bar H},
$$

$$
\bar r=\theta\frac{\bar Y}{\bar K}.
$$

使用 baseline 参数 $\beta=.99,\delta=.025,\theta=.36,A=1.72,\rho_w=.7,\psi_w=21$，作者得到：

![Table 11.1 — Stationary state values for staggered wage economy](../Figures/Ch11/table_11_1_stationary_state_values.png)

注意这里的 $\psi_w=21$ 意味着 wage markup 约为 $21/20=1.05$，也就是 5% 左右。

### 2.8 Log-linearization：工资方程如何变成递归形式？

本章最复杂的 log-linearization 是 wage-setting equation。最终可以得到：

$$
\tilde W_t^*
=(1-\beta\rho_w)
E_t\sum_{j=0}^{\infty}(\beta\rho_w)^j
\left[
\tilde P_{t+1+j}
+\tilde C_{t+1+j}
+\frac{\bar H}{1-\bar H}\tilde h_{t+j}^i
\right].
$$

> #### 一阶线性化的技巧
>
> $\frac{1}{A+B·dk}\approx \frac{1}{A}·(1-\frac{B}{A}dk)$ （一阶近似意义下）
>
> 主要是因为一阶近似下可以直接进行展开，完全不用担心展开次数不够而丢精度。

> - 分子
>
>     $\frac{h_t}{1-h_t\\}=\frac{h·(1+\tilde{h}_t)}{1-h-h·\tilde{h}_t}=\frac{h}{1-h}(1+\tilde{h}_t)(1+\frac{h}{1-h}\tilde{h})$ 
>
>     （全部化成这种因子连乘形式）
>
> - 分母
>
>     （同样化为因子连乘形式）
>
>     然后前面的系数（$\frac{h}{1-h\\},\frac{h}{PC}$ 都会被提出来然后被稳态的 $W^*$ 消掉）

这与第 10 章的 $\tilde P_t^*$ 方程结构完全平行：当前最优工资取决于未来一串变量的 expected weighted average。

aggregate wage evolution 是：

$$
\tilde W_t=(1-\rho_w)\tilde W_t^*+\rho_w\tilde W_{t-1}.
$$

> 这里面是对数线性化之后的形式，原本的工资迭代是应该是：所以：
> $$
> \boxed{
> W_t^{\,1-\psi_w}
> =
> (1-\rho_w)(W_t^*)^{\,1-\psi_w}
> +
> \rho_w W_{t-1}^{\,1-\psi_w}.
> }
> $$
> （推导是根据劳动聚合商的 FOC + 无盈利条件）
>
> 笔记中在稳态附近的一阶近似，写成：
> $$
> \widetilde W_t
> =
> (1-\rho_w)\widetilde W_t^*
> +
> \rho_w\widetilde W_{t-1},
> $$

把二者结合，再使用 quasi-differencing operator：
$$
1-\beta\rho_wL^{-1},
$$

> 意思就是说 $W^*_t$ 有一个递归形式，因此可以通过这个递归形式消去 $W^*_t$，因此首先把它单独放一边：
>
> $\bar{W}_t-\rho_w\bar{W}_{t-1}=(1-\rho_w)\bar{W}^*$
>
> 然后利用这个递归形式作差，消去右边的 $\bar{W}^*$，就可以得到下面的 (11.1) 式；

可以消去无限期未来和，得到：
$$
(1+\beta\rho_w^2)\tilde W_t
-\rho_w\tilde W_{t-1}
-\beta\rho_wE_t\tilde W_{t+1}
=
(1-\rho_w)(1-\beta\rho_w)
E_t
\left[
\tilde P_{t+1}
+\tilde C_{t+1}
+\frac{\bar H}{1-\bar H}\tilde h_t^*
\right].
\tag{11.1}
$$

还要把 individual labor $\tilde h_t^*$ 消掉。由 labor demand 和 wage aggregation：

$$
\tilde h_t^*
=\tilde H_t+\psi_w\tilde W_t-\psi_w\tilde W_t^*,
$$

$$
\tilde W_t=(1-\rho_w)\tilde W_t^*+\rho_w\tilde W_{t-1},
$$

可将 $\tilde h_t^*$ 表示为 aggregate variables 和 wage variables。最终工资方程只包含 aggregate wage、prices、consumption 和 hours。

### 2.9 处理 $t+2$ 期价格：用 CIA 和 money law 消去

前面 capital/money FOC 中有：

$$
E_t
\frac{P_t}{P_{t+1}C_{t+1}}
=
\beta E_t
\left[
\frac{P_{t+1}}{P_{t+2}C_{t+2}}
(r_{t+1}+1-\delta)
\right].
$$

为了避免 $P_{t+2}$，作者使用 CIA：

$$
P_{t+2}C_{t+2}=g_{t+2}M_{t+1}.
$$

于是原式可以改写成只含 $P_{t+1},g_{t+2},M_{t+1}$ 的形式。log-linearization 后得到：

$$
E_t[\tilde P_t-\tilde P_{t+1}-\tilde C_{t+1}]
=
E_t[
\tilde P_{t+1}-\tilde g_{t+2}
-\tilde M_{t+1}
+\beta\bar r\tilde r_{t+1}
].
\tag{11.2}
$$

再用 money growth process：

$$
\tilde g_{t+2}=\pi\tilde g_{t+1}+\varepsilon^g_{t+2},
$$

> ## 并非总能消掉高阶领先变量
>
> 这里是利用了外生的变量的迭代过程，这种消除未来变量的方法并不一定总是能够做到。
>
> 要把 $t+2$ 变量降成 $t+1$，通常需要模型中存在某条额外关系，使这个两期领先对象能够写成：
> $$
> X_{t+2}
> =
> F(\text{截至 }t+1\text{ 的变量},\varepsilon_{t+2}),
> $$
> 而且未来 inovation 需要满足可处理的条件期望（我们能知道其取值），例如：
> $$
> E_t\varepsilon_{t+2}=0.
> $$

并利用 $E_t\varepsilon^g_{t+2}=0$，可以把它写成：
$$
E_t[\tilde P_t-\tilde P_{t+1}-\tilde C_{t+1}]
=
E_t[
\tilde P_{t+1}
-\pi\tilde g_{t+1}
-\tilde M_{t+1}
+\beta\bar r\tilde r_{t+1}
].
$$

这一步的直觉非常重要：期望算子没有被“神奇地消掉”，而是利用外生过程的条件期望，把未来两期的 money growth 用未来一期状态变量的条件期望表示出来。

### 2.10 Solving the model：为什么 wage 是 state variable？

log-linear system 中，作者选择：

$$
x_t=[\tilde K_{t+1},\tilde M_t,\tilde P_t,\tilde W_t]',
$$

$$
y_t=[\tilde r_t,\tilde C_t,\tilde Y_t,\tilde H_t]',
$$

$$
z_t=[\tilde\lambda_t,\tilde g_t]'.
$$

wage $\tilde W_t$ 必须放进 state vector，因为 wage equation 中同时出现 $\tilde W_{t-1},\tilde W_t,E_t\tilde W_{t+1}$。past wage 是当前均衡的一部分。

系统仍然写成：

$$
0=A x_t+B x_{t-1}+C y_t+D z_t,
$$

$$
0=E_t[
F x_{t+1}+Gx_t+Hx_{t-1}
+J y_{t+1}+K y_t+L z_{t+1}+Mz_t
],
$$

$$
z_{t+1}=Nz_t+\varepsilon_{t+1}.
$$

解仍然是：

$$
x_{t+1}=Px_t+Qz_t,
\qquad
y_t=Rx_t+Sz_t.
$$

作者给出一个有意思的观察：虽然一开始把 prices $\tilde P_t$ 放进 state vector，但解出来的 $P,R$ 矩阵中 price column 为零。这意味着 price 实际上不是一个真正有用的 state variable。也就是说，求解算法会在某种程度上“拒绝”没有状态信息价值的变量：你把它放进 state，它的相关系数会被解成零。

> ⚠️【需要回原文看图】本章矩阵块排版密集，笔记不建议直接转录矩阵用于 coding。若要复现，回原文核对 $x_t,y_t,z_t$ 的变量顺序与矩阵元素。

### 2.11 Simulation moments and IRFs：sticky wages 的经济含义

作者选择 money growth shock 的标准差，使 output relative standard error 等于 1.76%。

![Table 11.2 — Standard errors and correlations](../Figures/Ch11/table_11_2_standard_errors_correlations.png)

Table 11.2 显示，staggered wage model 能生成较高的 hours-output correlation 和 investment-output correlation；prices 和 wages 也有较明显波动。

先看 technology shock：

![Figure 11.1 — Technology shock response](../Figures/Ch11/figure_11_1_technology_shock_response.png)

Figure 11.1 中，多数变量对 technology shock 的反应类似 Cooley-Hansen model，但更 persistent。价格和消费与前面模型有些差别，但整体没有第 10 章 staggered pricing model 那种非常怪异的短期大幅反向响应。

再看 money growth shock：

![Figure 11.2 — Money growth shock response](../Figures/Ch11/figure_11_2_money_growth_shock_response.png)

Figure 11.2 是本章最重要的图。money growth shock 使真实变量出现明显、持久的响应，而且响应形状有点像 technology shock。机制是：prices 初期比 nominal wages 上升更快，所以 real wage $W/P$ 短期下降，企业愿意雇佣更多劳动，hours 和 output 上升。之后 nominal wages 逐渐调整，real wage 可能超过稳态，真实变量回落。

作者还专门比较 real wage response：

![Figure 11.3 — Real wage comparison](../Figures/Ch11/figure_11_3_real_wage_comparison.png)

Figure 11.3 比较 Cooley-Hansen model 和 staggered wage model 中 real wage 对 technology shock 的反应。二者相似，但 staggered wage model 的反应略大、持续更久。

### 2.12 Reprise：为什么 sticky wages 是有吸引力的替代机制？

**<u>第 10 章的 staggered pricing 能让 monetary shocks 产生真实影响，但也会在 technology shock 下制造一些短期不太自然的动态。第 11 章的 staggered wage setting 提供了一个替代方案：它同样能让 monetary policy shocks 影响真实变量，并且方向更接近数据，同时避免第 10 章中某些短期异常</u>**。

实践中，central-bank DSGE 和 New Keynesian 模型通常同时包含 sticky prices 和 sticky wages。二者不是互斥关系，而是互补机制：价格刚性影响商品市场的调整，工资刚性影响劳动市场的调整。第 10 和第 11 章合在一起，基本把 New Keynesian nominal rigidities 的核心技术搭起来了。



### 2.Appendix 一般确认机制的方法

> #### 1.第一层：沿结构方程检查符号和时序
>
> 这是最基本的方法。
>
> 先提出一条链：
> $$
> \varepsilon_t^g
> \rightarrow P_t-W_t
> \rightarrow W_t/P_t
> \rightarrow H_t
> \rightarrow Y_t.
> $$
> 然后逐条检查：
>
> 1. 模型中是否真的存在对应方程；
> 2. 方程的局部导数是否符合这个符号；
> 3. IRF 中上游变量是否先于或至少同时于下游变量变化；
> 4. 是否存在明显相反的力量。
>
> 例如本章：
> $$
> \frac{\partial H_t}{\partial (W_t/P_t)}<0,
> \qquad
> \frac{\partial Y_t}{\partial H_t}>0.
> $$
> 加上 IRF 中实际工资下降、劳动和产出上升，至少证明这条机制与均衡结果一致。
>
> 但这只能说明：
> $$
> \boxed{\text{该机制是成立且方向一致的。}}
> $$
> 还不能证明：
> $$
> \boxed{\text{全部响应都由它造成。}}
> $$
>
> #### 2.第二层：关闭渠道做反事实实验
>
> 这是 DSGE 中最常用、也最有说服力的方法。
>
> 例如要检验“工资粘性渠道”，可以比较：
>
> ##### 基准模型
>
> $$
> \rho_w=0.7.
> $$
>
> 工资调整迟缓。
>
> ##### 反事实模型
>
> $$
> \rho_w=0.
> $$
>
> 所有家庭每期都能重新设定工资，工资完全灵活。
>
> 然后对两个模型施加完全相同的货币增长冲击，比较：
> $$
> IRF_Y^{\text{sticky wage}}
> \quad\text{与}\quad
> IRF_Y^{\text{flexible wage}}.
> $$
> 若工资完全灵活后：
>
> - 名义工资迅速跟随价格；
> - 实际工资不再明显下降；
> - hours 和 output 的真实响应大幅减弱或消失；
>
> 那么就有较强依据说：
> $$
> \boxed{\text{原来的真实效应主要来自工资粘性渠道。}}
> $$
> 这通常被称为：
>
> - channel shutdown；
> - counterfactual decomposition；
> - friction-off experiment；
> - model comparison。
>
> 这是你以后分析自己的 DSGE 模型时最实用的方法。
>
> #### 3.关闭渠道实验的局限
>
> 不过也不能把两组 IRF 的差机械地称为“该渠道的贡献”。
>
> 因为把：
> $$
> \rho_w=0.7
> $$
> 改成：
> $$
> \rho_w=0
> $$
> 以后，整个一般均衡都会重新求解：
>
> - 家庭工资决策改变；
> - 预期改变；
> - 消费和投资政策函数改变；
> - 其他变量的反馈也改变。
>
> 因此两组结果之差表示：
> $$
> \boxed{\text{包含全部一般均衡反馈在内的工资粘性净作用。}}
> $$
> 它不是一个“其他变量完全不动，只单独拿掉工资渠道”的偏导数。
>
> 但在宏观结构模型中，这通常正是我们想要的反事实。
>
> #### 4.第三层：参数敏感性
>
> 还可以逐渐降低工资粘性：
> $$
> \rho_w=0.9,\ 0.7,\ 0.5,\ 0.2,\ 0.
> $$
> 观察随着工资越来越灵活：
>
> - 实际工资下降是否越来越小；
> - 劳动和产出响应是否单调减弱；
> - 持续性是否下降。
>
> 如果响应随着 $\rho_w$ 系统性变化，这比只比较两个极端模型更有说服力。
>
> 例如如果：
> $$
> \rho_w\uparrow
> \quad\Rightarrow\quad
> W_t\text{ 调整更慢}
> \quad\Rightarrow\quad
> W_t/P_t\text{ 下跌更深}
> \quad\Rightarrow\quad
> H_t,Y_t\text{ 响应更大},
> $$
> 那么工资粘性机制就得到了比较完整的验证。
>
> #### 5.多个渠道同时存在时
>
> 更复杂的模型可能同时存在：
>
> - sticky prices；
> - sticky wages；
> - investment adjustment costs；
> - habit formation；
> - financial accelerator；
> - working-capital channel。
>
> 这时可以构造一组嵌套模型：
> $$
> \begin{array}{ll}
> \text{模型 A：}&\text{所有摩擦都开启},\\
> \text{模型 B：}&\text{关闭工资粘性},\\
> \text{模型 C：}&\text{关闭价格粘性},\\
> \text{模型 D：}&\text{关闭投资调整成本},\\
> \text{模型 E：}&\text{关闭金融摩擦}.
> \end{array}
> $$
> 比较 IRF 的变化，可以判断每个摩擦对：
>
> - 当期响应；
> - 峰值；
> - 累积响应；
> - 持续性；
>
> 分别有什么作用。
>
> 需要注意，渠道之间往往存在交互，因此：
> $$
> \text{工资渠道贡献}
> +
> \text{价格渠道贡献}
> $$
> 未必正好等于总效应。关闭顺序不同，结果也可能不同。若一定要做可加总的数量分解，可以使用 Shapley-style decomposition，对不同关闭顺序取平均，但多数普通 DSGE 分析不必走到这一步。

> #### 6.你拿到一个模型后的实际分析流程
>
> 建议按照下面的顺序判断机制：
>
> ##### 第一步：看冲击直接进入哪条方程
>
> 本章货币冲击进入 money growth process 和 CIA 体系。
>
> ##### 第二步：找最先受到影响的价格或约束
>
> 这里是价格水平和名义工资的相对调整速度。
>
> ##### 第三步：利用预定变量缩小当期可能性
>
> 冲击当期 $K_t$ 已定、$\lambda_t$ 未变，所以劳动 FOC 可以清楚地解释 $H_t$ 的变化。
>
> ##### 第四步：沿方程追踪
>
> $$
> P_t-W_t
> \rightarrow W_t/P_t
> \rightarrow H_t
> \rightarrow Y_t.
> $$
>
> ##### 第五步：检查 IRF 符号与时序
>
> 价格是否真的快于工资，实际工资是否下降，劳动和产出是否同步上升。
>
> ##### 第六步：关闭渠道重新求解
>
> 令 $\rho_w=0$，检查真实响应是否消失或显著缩小。





## 3. Compact Summary: What You Must Retain

第一，第 11 章把 Calvo friction 从 price setting 移到 wage setting。差异化劳动通过 labor bundler 合成为 effective labor，households 因此有 wage-setting power。

第二，staggered wage setting 需要 insurance arrangement，否则不同工资会导致不同收入、储蓄、资本和消费，模型会变成复杂异质性家庭问题。

第三，最优工资 $W_t^*$ 是 forward-looking 的，因为今天设定的工资未来可能持续有效，家庭必须考虑未来 labor demand、prices、consumption 和 labor disutility。

第四，工资方程 log-linear 后包含无限期预期和，作者用 quasi-differencing 把它压缩成递归 wage equation。

第五，capital/money FOC 中出现 $P_{t+2}C_{t+2}$，作者用 CIA constraint 和 money growth process 把它改写成只含 $t,t+1$ 变量的期望关系。

第六，wage 必须作为 state variable，因为当前均衡依赖 past wage；price 虽然被放入 state，但解显示它不是真正有信息价值的 state。

第七，sticky wages 能让 money growth shocks 对真实变量产生持久影响，而且不像第 10 章 baseline staggered pricing 那样产生特别怪异的 technology-shock 短期响应。

## 4. Figures, Tables, and Formulas to Check in the Original

本章重要图表已经作为截图放入 `Figures/Ch11/`，并在正文嵌入：

- Table 11.1：staggered wage economy 的 stationary state values。
- Table 11.2：simulation standard errors and correlations。
- Figure 11.1：technology shock 的 IRF。
- Figure 11.2：money growth shock 的 IRF。
- Figure 11.3：Cooley-Hansen 与 staggered wage model 的 real wage response 比较。

最需要回原文核对的公式包括：

$$
h_t^i=H_t\left(\frac{W_t}{W_t(i)}\right)^{\psi_w},
$$

wage-setting rule：

$$
W_t^*(i)
=
\frac{\psi_w}{\psi_w-1}
\frac{A}{\beta}
\frac{
E_t\sum_{j=0}^{\infty}(\beta\rho_w)^j
\frac{h_{t+j}^i}{1-h_{t+j}^i}
}{
E_t\sum_{j=0}^{\infty}(\beta\rho_w)^j
\frac{h_{t+j}^i}{P_{t+1+j}c_{t+1+j}^i}
},
$$

以及 quasi-differenced wage equation：

$$
(1+\beta\rho_w^2)\tilde W_t
-\rho_w\tilde W_{t-1}
-\beta\rho_wE_t\tilde W_{t+1}
=
(1-\rho_w)(1-\beta\rho_w)
E_t
\left[
\tilde P_{t+1}
+\tilde C_{t+1}
+\frac{\bar H}{1-\bar H}\tilde h_t^*
\right].
$$

> ⚠️【需要回原文看图】本章矩阵块和 wage equation 推导较密，PDF 文本提取可能不足以完整保留排版。如果要 coding，请回原文核对变量顺序和矩阵元素。

## 5. Questions and Answers

**Q1：第 11 章和第 10 章的结构平行在哪里？**

第 10 章是 final goods firm 打包 differentiated goods，intermediate firms 设置 sticky prices；第 11 章是 labor bundler 打包 differentiated labor，households 设置 sticky wages。两者都用 CES aggregator、Calvo rule 和 quasi-differencing。

**Q2：为什么需要 labor income insurance？**

没有保险时，不同工资会带来不同劳动收入，进一步导致不同消费、储蓄、资本和边际效用。这样获得调工资机会的 households 不会选择同一个工资，代表性结构会崩掉。保险让所有家庭消费和边际效用相同，从而保留 tractability。

**Q3：为什么 household 有 wage-setting power？**

因为每个 household 提供的是 differentiated labor type。劳动打包厂商对每种劳动有向下倾斜的需求曲线，household 提高自己的 wage 会减少劳动需求，但不会使需求归零，所以 household 能设置 wage markup。

**Q4：为什么最优工资是 forward-looking？**

因为今天设定的工资未来可能继续有效。household 设工资时必须考虑未来每一期这个工资仍有效时的劳动需求、劳动厌恶、价格和消费边际效用。

**Q5：本章如何处理 FOC 中的 $P_{t+2}$？**

作者用 CIA constraint 把 $P_{t+2}C_{t+2}$ 替换为 $g_{t+2}M_{t+1}$，再用 money growth process 的条件期望把 $g_{t+2}$ 改写成 $\pi g_{t+1}$ 加上期望为零的冲击项。

**Q6：为什么 wage 是 state variable？**

因为 Calvo wage equation 同时包含 lagged wage、current wage 和 expected future wage。过去工资会影响当前 aggregate wage index，因此它是当前经济状态的一部分。

**Q7：为什么 price 被放进 state 后又“没用”？**

解出来的 policy matrices 中，price column 为零，说明 $P_t$ 不提供预测未来状态和当前 jump variables 的额外信息。求解算法相当于告诉我们：你可以把它放进去，但它不是真正的 state。

**Q8：sticky wage model 的主要优势是什么？**

它能让 money growth shock 对真实变量产生显著且持久的影响，同时避免 baseline staggered pricing model 在 technology shock 下出现的一些短期异常动态。因此它是 New Keynesian 模型中很常见的 nominal rigidity 机制。
