# Chapter 12 — Lecture Note

> Importance: ★★★★★  
> Suggested audit model: xhigh  
> Reading mode: careful  
> Estimated note reading time: 95–125 minutes  
> Source reliability: text OK；关键图表均已嵌入原文截图；矩阵块与变量顺序在 coding 前仍应回原文核对

## 0. How to read this note

第 12 章第一次在本书中明确加入金融中介（financial intermediary），并把货币政策、企业流动资金和生产决策连成一条完整链条。此前第 8 章中，新发行货币直接转移给家庭，货币增长主要通过 cash-in-advance constraint 改变家庭持币与消费选择；本章则让新货币进入银行体系，银行再把资金借给企业支付当期工资。结果会发生根本变化：同样是货币扩张，进入家庭可能像一种通胀税，进入金融体系却可能降低企业的 working-capital cost，从而提高劳动、资本和产出。

阅读本章时，应始终抓住两个层次。第一层是模型结构：家庭把期初货币分成消费现金与银行存款，银行把存款和央行注入资金贷给企业，企业必须借钱支付工资。第二层是政策含义：货币从哪里进入经济，决定了它首先改变谁的约束和哪一个相对价格。后半章进一步把随机货币增长改成明确的 monetary policy rule，比较 Taylor rule 与 Friedman constant-money-growth rule。

## 1. Opening: 本章的核心问题

货币模型常被简化为“货币增长改变价格水平”。但在一般均衡中，新增货币不会凭空进入所有人的账户；它必须通过某个具体入口进入经济。若政府直接把钱转给家庭，首先改变的是家庭的 cash-in-advance constraint。若央行把钱注入金融中介，首先改变的则是银行可贷资金和企业融资成本。两个入口即使最终创造相同数量的货币，也可能产生完全不同的真实效应。

第 12 章因此提出三个核心问题。第一，企业必须借入 working capital 才能支付工资时，借款利率如何进入劳动需求与边际成本？第二，央行把新货币交给金融中介以后，为什么可能提高而不是降低产出与福利？第三，当央行不再机械地制造随机货币增长，而是承诺遵循 Taylor rule 或 Friedman rule 时，模型动态会如何变化？

本章的价值不只在于多加入一个“银行部门”，而在于展示一个更一般的方法：要理解货币政策渠道，不能只看货币总量，必须明确资金流向、交易时点和哪个约束最先被放松。

## 2. Main Lecture

### 2.1 Working capital：企业为什么必须先借钱才能生产

本章考虑一个由家庭、企业和金融中介组成的经济。企业在期初雇佣劳动并生产，但产品要到期末出售以后才能取得销售收入。因此企业在支付工资与取得收入之间存在时间错配。模型用一条简单但强的设定表示这种错配：企业必须向金融中介借入足够资金，先支付全部工资账单，期末出售产品后再偿还贷款。

贷款在同一期内发放和偿还，而且当期的技术冲击和货币冲击在贷款发生前已经被观察到，因此贷款没有违约风险。这里的金融摩擦不是 default risk 或 agency cost，而是一种 production-side cash-in-advance constraint：企业不是因为资产负债表太弱而支付风险溢价，而是因为工资必须预先融资，所以借款利率直接进入使用劳动的有效成本。

交易时点如下：

```text
期初家庭持有上期结转货币
        ↓
家庭把货币分成消费现金和银行存款
        ↓
央行向金融中介注入或抽走货币
        ↓
金融中介把全部可贷资金贷给企业
        ↓
企业用贷款支付工资并进行生产
        ↓
产品出售，企业偿还本息
        ↓
家庭取得工资、资本收入和存款本息，用于期末资产配置
```

本章采用的时间结构还包含一个重要限制：当期工资收入不能用于当期消费，只能用于当期末积累资本或货币。因此，家庭在期初必须用上一期结转的货币支付本期消费。作者也指出，其他 working-capital 或 limited-participation 模型可以采用不同时间结构，例如允许当期工资支付当期消费，或者要求家庭在货币冲击实现之前就决定银行存款。时点变化会改变模型动态，所以它不是无关紧要的技术细节。

### 2.2 家庭：消费现金与银行存款之间的配置

家庭最大化预期效用：

$$
E_t\sum_{s=0}^{\infty}\beta^s
\left[\ln c_{t+s}^i+B h_{t+s}^i\right].
$$

本章延续 Hansen 的 indivisible labor 设定。若家庭被抽中工作，它提供固定劳动量 $h_0$；$h_t^i/h_0$ 可以理解为被抽中工作的概率。参数

$$
B=\frac{\ln(1-h_0)}{h_0}<0
$$

表示劳动对效用的负贡献。劳动收入保险仍然存在，使家庭无论是否实际被抽中工作都获得相同的劳动收入，从而保持代表性家庭结构。

家庭的 cash-in-advance constraint 是：

$$
P_t c_t^i\le m_{t-1}^i-N_t^i,
$$

其中 $m_{t-1}^i$ 是家庭从上一期带入本期的名义货币，$N_t^i$ 是本期借给金融中介的名义存款。这个式子揭示了家庭面临的基本取舍：同一笔期初货币既可以用于购买消费，也可以存入银行获得利息。存得越多，当期可以用于消费的现金越少。

家庭的期末预算约束为：

$$
\frac{m_t^i}{P_t}+k_{t+1}^i
=
w_t h_t^i+r_tk_t^i+(1-\delta)k_t^i
+\frac{r_t^nN_t^i}{P_t}.
$$

这里 $r_t^n$ 是银行支付给家庭存款的 gross return。存款在期初以货币形式交给银行，期末以货币本息返还；由于同一期内价格不变，这个利率既可以说是 nominal rate，也可以说是 real within-period rate。**<u>它不需要再除以一期通胀，因为贷款和偿还没有跨越两个价格时期</u>**。

家庭最重要的三个一阶条件可以写为：【c、k、h、N、m；可以用 CIA 消掉 N，然后用 h 的 FOC 消掉影子价格（所以在等式左边才会有这么多 1/w）】
$$
\frac{B}{w_t}
=-\beta E_t\frac{P_t}{P_{t+1}C_{t+1}},
\tag{12.1}
$$

$$
\frac1{w_t}
=\beta E_t\frac{r_{t+1}+1-\delta}{w_{t+1}},
\tag{12.2}
$$

以及

$$
r_t^n
=-\frac{w_t}{BC_t}
=
\frac1{\beta P_tC_tE_t[1/(P_{t+1}C_{t+1})]}.
\tag{12.3}
$$

第一条把劳动的边际效用损失与未来消费边际效用联系起来；第二条是资本 Euler equation（<u>对资本 k\_{t+1} 求 FOC 然后用劳动的条件替换掉影子价格</u>）；第三条决定家庭愿意牺牲当期消费现金、把货币存入银行所要求的回报（<u>(12.3)式的第一个等号来自于对消费 c 求 FOC，然后用工资消掉影子价格</u>；<u>(12.3)的第二个等式来自于对 mt 求 FOC 然后消去影子价格</u>）。

> （12.1）并不是一个独立的 FOC 条件，它来自于（12.3），将（12.3）倒过来之后就是（12.1）的形式了；

聚合以后，家庭 CIA 约束和流量预算为：

$$
P_tC_t=M_{t-1}-N_t,
\tag{12.4}
$$

$$
\frac{M_t}{P_t}+K_{t+1}
=w_tH_t+r_tK_t+(1-\delta)K_t+
\frac{r_t^nN_t}{P_t}.
\tag{12.5}
$$

式（12.4）非常值得记住：家庭期初真实货币余额被明确分成了两部分，一部分购买消费，另一部分成为银行存款。金融市场因此不是额外创造家庭资源，而是在同一笔货币内部改变用途。

### 2.3 企业：借款利率为什么进入劳动需求

代表性企业使用 Cobb-Douglas 技术：

$$
Y_t=\lambda_tK_t^\theta H_t^{1-\theta}.
$$

企业购买资本服务时直接支付租金 $r_tK_t$，但工资账单必须由银行贷款融资。若企业借入 $P_tw_tH_t$ 的名义资金，并支付 gross borrowing rate $r_t^f$，则以产品计价的劳动总成本为：

$$
r_t^f w_tH_t.
$$

企业零利润条件写成：

$$
Y_t=r_t^f w_tH_t+r_tK_t.
$$

劳动和资本的一阶条件为：

$$
r_t^f w_t
=(1-\theta)\lambda_tK_t^\theta H_t^{-\theta},
\tag{12.6}
$$

$$
r_t
=\theta\lambda_tK_t^{\theta-1}H_t^{1-\theta}.
\tag{12.7}
$$

> 这里面的 $r^f_t$、$r^n_t$ 都是包含了本金的，即形如 (1+r...) 这种；

与普通竞争性 RBC 模型相比，资本条件没有变化；劳动条件却把实际工资 $w_t$ 乘上了融资因子 $r_t^f$。因此企业真正比较的是劳动边际产出与“工资加融资成本”：
$$
\text{effective labor cost}=r_t^f w_t.
$$

这就是本章全部货币传导机制的生产端入口。只要货币政策能够降低 $r_t^f$，即使实际工资没有下降，企业使用劳动的有效成本也会降低，劳动需求和产出就会上升。

### 2.4 金融中介：存款、央行注资与企业贷款如何闭合

金融中介完全竞争、没有运营成本，也不承担风险。它的资金来源有两项：家庭存款 $N_t$，以及央行本期新增货币 $(g_t-1)M_{t-1}$。全部资金都贷给企业支付工资，因此信用市场清算条件是：

$$
N_t+(g_t-1)M_{t-1}=P_tw_tH_t.
\tag{12.8}
$$

银行零利润条件为：

$$
r_t^f\left[N_t+(g_t-1)M_{t-1}\right]
=r_t^nN_t.
\tag{12.9}
$$

> #### 【信贷市场出清条件】
>
> 这里 （12.8）、（12.9）其实是信贷市场的量价关系使得市场出清所需要满足的条件；
>
> - 一般而言市场出清条件是不用显式指出的，例如劳动力市场，因为它们共用同一个量价字母（w、L；注意，这里厂商支付给家庭的依然是 w 而不是 $r^fw$）
>
> - 但是这里信贷市场并不是使用了统一的量价字母，因此需要显式写出市场出清条件。

银行对家庭存款支付利息，但央行注入的新增货币不需要支付利息。于是当央行增加注资时，银行总可贷资金增加，而需要支付市场存款回报的资金占比下降。零利润条件允许企业借款利率 $r_t^f$ 低于家庭存款利率 $r_t^n$。

这不是银行获得垄断利润形成的利差。银行利润仍然为零；利差来自央行提供了一部分“无息资金”。从企业角度，它表现为融资补贴；从家庭角度，存款回报仍由其跨期选择决定。

货币总量遵循：

$$
M_t=g_tM_{t-1},
$$

> #### 【货币市场出清条件】
>
> 1. 一般来说我们解 DSGE 都是把各个 agent 的最优化行为解出来，这样就相当于是把各个内生变量写作所有市场的价格的函数，这样系统内就只剩下 n 个市场的价格是未确定的；
>
> 2. 然后在列出 n-1 个市场出清条件，这样系统内部就只剩下最后一个自由度；
> 3. 一般消除这个自由度需要额外添加一个条件，古典中常用 MV=Py、NK 中常用央行的 Taylor 规则；
> 4. 在这个模型中货币 M 是外生的，通过家庭的 FOC，将 m 表达为所有市场价格的函数，然后再令 m=M（在本模型中他俩用同一个字母，相当于隐式表达了市场出清），这样就相当于额外增加了一个条件，确定了最后一个自由度。
> 5. 如果要引入央行规则，那么 M 外生这个条件就需要改掉，改成让央行来控制 M。
>
> 【关键点在于，货币市场没有价格，因此它天生就是用来填补多余的自由度的】

并假定货币增长率服从：
$$
\ln g_t=\pi_g\ln g_{t-1}+\varepsilon_t^g.
\tag{12.10}
$$

至此，家庭、企业、银行和货币政策构成了完整一般均衡系统。

### 2.5 本章的核心机制：货币注入位置为什么改变结果

把式（12.8）和（12.9）放在一起，就能看清本章与第 8 章的根本区别。

在第 8 章的 Cooley-Hansen CIA model 中，新货币直接转给家庭。更高的货币增长降低了家庭持有上期货币的实际回报，表现为 inflation tax。家庭减少劳动和生产，稳态消费、产出与福利下降。

本章的新货币则直接进入金融中介。它首先增加可贷资金：

$$
(g_t-1)M_{t-1}\uparrow
\quad\Rightarrow\quad
\text{loanable funds}\uparrow.
$$

因为这部分资金不需要向家庭支付存款利息，企业贷款利率下降：

$$
r_t^f\downarrow.
$$

由企业劳动需求条件：

$$
r_t^f w_t=(1-\theta)\lambda_tK_t^\theta H_t^{-\theta},
$$

融资成本下降提高劳动需求，进而提高就业和产出。更多劳动又提高资本边际产出，资本逐步积累，直到资本回报重新满足家庭 Euler condition。

因此本章给出的因果链是：

```text
央行向银行注入货币
        ↓
银行无息可贷资金增加
        ↓
企业 working-capital borrowing rate 下降
        ↓
劳动的有效成本 rᶠw 下降
        ↓
劳动需求、就业与产出上升
        ↓
资本边际产出提高，资本逐渐积累
```

这条机制并不是从 IRF 中事后挑出几条同向曲线，而是由金融市场清算、银行零利润和企业劳动 FOC 三条结构方程共同给出的。作者进一步把本章结果与第 8 章进行模型对照，相当于改变货币入口的反事实实验，因此“注入位置”是本章最可信的机制识别。

### 2.6 Stationary state：更高通胀为什么反而提高本模型的产出

在稳态中，实际变量不变，名义货币和价格以同一速度增长，因此：

$$
\bar\pi=\bar g.
$$

资本 Euler equation 给出：

$$
\bar r=\frac1\beta-1+\delta.
\tag{12.11}
$$

家庭存款回报为：

$$
\bar r^n=\frac{\bar g}{\beta}.
\tag{12.12}
$$

当 $\bar g=1$ 时，银行没有持续的货币注入，企业贷款全部来自家庭存款，因此：

$$
\bar r^f=\bar r^n=\frac1\beta.
$$

但当 $\bar g>1$ 时，银行持续获得无息新增货币。随着趋势货币增长上升，家庭要求的存款回报 $\bar r^n$ 上升，而企业支付的借款回报 $\bar r^f$ 反而下降，二者之间出现越来越大的政策性 wedge。

家庭条件还给出：

$$
\bar C=-\frac{\bar w\beta}{\bar gB}.
\tag{12.13}
$$

剩余稳态方程由企业 FOC、银行零利润、信贷市场清算、CIA 和家庭预算约束共同构成。作者用标准参数

$$
\beta=.99,\qquad \delta=.025,\qquad \theta=.36,
\qquad B=-2.5805
$$

数值求解不同货币增长率下的稳态。

![Table 12.1 — Stationary states for working capital model](../Figures/Ch12/table_12_1_stationary_states_working_capital.png)

Table 12.1 显示，在本模型中，趋势货币增长越高：

- 企业借款利率 $\bar r^f$ 越低；
- 家庭存款回报 $\bar r^n$ 越高；
- household deposits $\bar N/\bar P$ 下降，但银行获得的央行资金更多；
- 总可贷资金上升；
- 劳动、资本、产出、消费和稳态福利上升。

这个结论并不是一般的“通胀有利于增长”。它严格依赖本章的制度设定：新增货币全部无偿进入银行，并降低企业工资融资成本。若货币直接转给家庭、银行需要为央行资金付息，或者企业只有部分工资需要融资，数量结果都可能改变。

### 2.7 Stationary-state Phillips/Fisher curve

在 indivisible labor 模型中，每个就业家庭提供固定 $h_0$，所以：

$$
\frac{\bar H}{h_0}
$$

是就业家庭比例，而

$$
1-\frac{\bar H}{h_0}
$$

可以解释为失业率。由于更高趋势货币增长降低企业融资成本并提高劳动需求，本模型在稳态中生成一条通胀与失业负相关的曲线。

![Figure 12.1 — Stationary state Phillips curve](../Figures/Ch12/figure_12_1_stationary_state_phillips_curve.png)

**<u>作者称其为 stationary-state Phillips curve，也指出从历史归属上说更接近 Fisher curve。需要注意，这不是现代 New Keynesian Phillips Curve：它不是价格粘性导致的短期通胀—产出权衡，而是趋势货币增长通过 working-capital subsidy 改变稳态就业的结果</u>**。

### 2.8 Log-linearization：哪些方程承载了动态机制

本章把非线性系统在稳态附近 log-linearize。最有解释力的核心方程包括：

$$
0=\widetilde w_t+\widetilde P_t
-E_t\widetilde P_{t+1}-E_t\widetilde C_{t+1},
$$

$$
0=\widetilde w_t-E_t\widetilde w_{t+1}
+\beta\bar rE_t\widetilde r_{t+1},
$$

$$
0=\widetilde r_t^n-\widetilde w_t+\widetilde C_t,
$$

以及企业劳动需求：

$$
0=\widetilde w_t+\widetilde r_t^f
-\widetilde\lambda_t-\theta\widetilde K_t
+\theta\widetilde H_t.
\tag{12.14}
$$

式（12.14）直接说明，当技术和当期资本给定时，企业贷款利率下降会提高劳动：

$$
\widetilde r_t^f\downarrow
\quad\Rightarrow\quad
\widetilde H_t\uparrow.
$$

作者把状态、跳跃变量和外生冲击组织为：

$$
x_t=[\widetilde K_{t+1},\widetilde M_t,\widetilde P_t]',
$$

$$
y_t=[\widetilde r_t,\widetilde w_t,\widetilde Y_t,
\widetilde C_t,\widetilde H_t,\widetilde N_t,
\widetilde r_t^n,\widetilde r_t^f]',
$$

$$
z_t=[\widetilde\lambda_t,\widetilde g_t]'.
$$

系统继续写成第 6 章的 Uhlig 形式，并求出：

$$
x_{t+1}=Px_t+Qz_t,
\qquad
y_t=Rx_t+Sz_t.
$$

> ⚠️【需要回原文看图】本章的 A–N 矩阵块和政策矩阵排版非常密集。笔记保留变量分组和经济含义，但不建议直接依据笔记转录矩阵进行 coding；实现前应回原文逐项核对变量顺序、稳态权重和系数。

### 2.9 基准经济的二阶矩与冲击响应

作者分别校准技术冲击和货币增长冲击，使模型产出标准差接近 1.76%。Table 12.2 报告标准差与产出相关性。

![Table 12.2 — Standard errors and correlations for working capital model](../Figures/Ch12/table_12_2_standard_errors_correlations_working_capital.png)

技术冲击的真实变量 IRF 如下：

![Figure 12.2 — Response of real variables to a technology shock](../Figures/Ch12/figure_12_2_real_variables_technology_shock.png)

正向技术冲击提高产出、消费、资本和工资，整体形状与第 6 章 Hansen indivisible-labor model 相似。多数动态较快衰减，较长的持续性主要来自技术过程本身较高的 AR coefficient。价格下降，家庭初期增加银行存款；随着经济回归稳态，存款随后回落。

货币增长冲击的真实变量 IRF 是本章第一部分最重要的结果：

![Figure 12.3 — Response of real variables to a money growth shock](../Figures/Ch12/figure_12_3_real_variables_money_growth_shock.png)

冲击发生时，企业借款利率下降，劳动和产出明显上升。消费反而下降，是因为货币冲击虽然通过银行端补贴生产，但家庭仍必须在消费现金和存款之间配置期初货币，且一般均衡中的工资、利率和资本积累同时调整。因此不能把“产出上升”直接等同于“家庭当期消费上升”。

技术冲击与货币冲击下的名义变量分别如下：

![Figure 12.4 — Response of nominal variables to a technology shock](../Figures/Ch12/figure_12_4_nominal_variables_technology_shock.png)

![Figure 12.5 — Response of nominal variables to a money growth shock](../Figures/Ch12/figure_12_5_nominal_variables_money_growth_shock.png)

货币增长冲击使 money stock、price level 和 nominal deposits 最终趋向同一个新的长期水平。货币存量最先跳升，价格与存款较慢追赶。由于这些名义水平含有 unit root，它们的对数水平不会回到原稳态，而是 cointegrated 地收敛到共同的新水平。

### 2.10 高趋势通胀：稳态改变会怎样影响动态

作者进一步考虑年通胀约 100%、季度 gross money growth $\bar g=1.19$ 的经济。此时模型的稳态和 log-linear coefficients 都改变，因此同样大小的冲击不再产生与零通胀稳态相同的响应。

![Table 12.3 — Standard errors and correlations under high stationary-state inflation](../Figures/Ch12/table_12_3_high_inflation_moments.png)

高通胀稳态下，多数变量的标准差更高，尤其是投资与价格。作者再用比较图把零通胀经济的响应放在横轴、100% 通胀经济的响应放在纵轴；45 度线表示两者响应相同。

![Figure 12.6 — Real responses to technology shock: 0% versus 100% inflation](../Figures/Ch12/figure_12_6_real_technology_comparison_0_vs_100_inflation.png)

![Figure 12.7 — Nominal responses to technology shock: 0% versus 100% inflation](../Figures/Ch12/figure_12_7_nominal_technology_comparison_0_vs_100_inflation.png)

![Figure 12.8 — Real responses to money shock: 0% versus 100% inflation](../Figures/Ch12/figure_12_8_real_money_comparison_0_vs_100_inflation.png)

![Figure 12.9 — Nominal responses to money shock: 0% versus 100% inflation](../Figures/Ch12/figure_12_9_nominal_money_comparison_0_vs_100_inflation.png)

总体上，同样大小的技术或货币增长冲击在高趋势通胀经济中引起的真实响应较弱；价格调整更快，而银行存款调整更慢。这里的重要方法论是：IRF 不只取决于冲击和方程形式，也取决于围绕哪个稳态进行近似。改变趋势通胀会同时改变稳态比率和线性化系数，因此不能只把高通胀理解成在原 IRF 上机械添加一个常数。

### 2.11 从随机货币增长转向明确的中央银行规则

前面的 monetary policy 只是一个外生随机货币增长过程，并不真正像“政策规则”。本章第二部分假设央行能够可信地承诺遵循规则，并比较两种著名政策：Taylor interest-rate rule 与 Friedman constant-money-growth rule。

为了给两种规则提供共同的 monetary disturbance，作者把随机货币转移重新放到家庭端。可以把它理解为财政部门向家庭进行 lump-sum money transfer：

$$
P_tC_t=g_t^fM_{t-1}-N_t,
$$

其中 $g_t^f$ 是 fiscal money transfer shock。中央银行则通过向金融中介注资或征收货币税来执行政策，记其对应的货币增长成分为 $g_t^M$。

金融中介的资金约束和零利润条件变成：
$$
N_t+(g_t^M-1)M_{t-1}=P_tw_tH_t,
\tag{12.15}
$$

$$
r_t^nN_t=r_t^fP_tw_tH_t.
\tag{12.16}
$$

给定家庭存款、工资账单和目标企业借款利率，央行必须选择：

$$
g_t^M
=1+\frac{(r_t^n-r_t^f)N_t}{r_t^fM_{t-1}}.
\tag{12.17}
$$

这条式子给出了本章中“央行如何实现目标利率”的具体资产负债表机制：央行不是凭口头宣布利率，而是调整注入金融系统的货币，使银行零利润条件恰好支持目标贷款利率。

> #### 【这里是在干什么】
>
> 首先为了插入Friedman rule & Taylor rule，我们需要修改货币政策的方程，也就是说不能用原来的：
> $$
> M_t=g_tM_{t-1}
> $$
> $$
> \ln g_t=\pi_g\ln g_{t-1}+\varepsilon_t^g.
> $$
>
> 这个货币增长规则方程。
>
> 那么应该怎么修改呢：
>
> - Taylor rule
>
>     $r^f = \bar r^f+a_y(Y-\bar Y)+a_π(π-\bar π)$
>
>     但是在我们这个体系内部直接这样引入不是最方便的方式，Taylor 规则的本质是让利率 $r^f$ 处于特定位置水平，因此在我们这个框架内只需要 “调整向银行注资的数量 $g^M_t$，使得利率水平 $r^f$ 位于特定水平”；
>
>     所以在上文中，央行的 Taylor 规则被设置为 $g_t^M=1+\frac{(r_t^n-r_t^f)N_t}{r_t^fM_{t-1}\\}$ 
>     
>     - 需要注意的是，这里泰勒规则依然是满足上面的表达式，只不过我们通过产出、通胀缺口计算得到 $r^f$ 之后，然后我们再通过这个公式换算到 $g^M_t$，也就是说需要增加这么多的货币才能够达到我们想要的利率水平。
>     
> - Fridman rule
>
>     这个是为了保持货币增速维持在一个稳定水平，原来的货币增速规则其实是可以的，我们只需要去掉 $ε_t^g$ 即可，但是这样就太单调了，并且如果采用两个规则，那么原来框架内的货币冲击就没有了。
>
>     因此作者重新把货币冲击放到家庭的 CIA 约束里面。
>
>     - 所以说，新增 $g_t^f$ 只是为了再做一组实验：
>         $$
>         \text{家庭突然收到一笔外生货币转移时，两种央行规则如何反应。}
>         $$
>
>     - 由于家庭中增加了一个货币冲击，因此弗里德曼规则不能够仅是让 $ε^g_t=0$，而且同时需要平衡家庭那边多余出来的冲击。
>

### 2.12 Taylor rule

作者采用的 Taylor rule 为：

$$
r_t^f
=a(Y_t-\bar Y)+b(\pi_t-\bar\pi)+\bar r^f.
\tag{12.18}
$$

央行在产出高于目标或通胀高于目标时提高企业 working-capital borrowing rate。**<u>需要注意，本模型中的 $r_t^f$ 是同一期内发放和偿还的贷款回报，不承受跨期通胀，因此更接近 real within-period rate，而不是标准 Taylor rule 中的一期 nominal policy rate。作者因此使用 $a=.5,b=.5$，而不是 Taylor 原始建议中针对 nominal rate 的 $b=1.5$</u>**。

总货币存量由家庭端财政转移和央行银行端操作共同决定：

$$
M_t=(g_t^f+g_t^M-1)M_{t-1}.
$$

稳态通胀目标与目标利率之间的关系画在 Figure 12.10 中：

![Figure 12.10 — Stationary-state inflation target and associated interest rate](../Figures/Ch12/figure_12_10_inflation_target_interest_rate.png)

![Table 12.4 — Stationary-state values for Taylor-rule economy](../Figures/Ch12/table_12_4_taylor_rule_stationary_state.png)

这里的稳态本质上仍是 working-capital model 的稳态，只是央行选择的政策目标必须与银行市场、家庭存款回报和目标通胀相容。

### 2.13 Friedman rule：保持货币增长恒定

作者所说的 Friedman rule 是 constant money-growth rule。央行设定固定目标 $\bar g^M$，并完全抵消家庭端的财政货币冲击：

$$
g_t^M-\bar g^M=-(g_t^f-1).
\tag{12.19}
$$

因此无论财政部门本期向家庭多发或少发多少货币，中央银行都在金融系统中反向操作，使总货币增长保持不变。

这里有一个重要的一般均衡含义：两种货币操作的总量可以相互抵消，但渠道不能相互抵消。正向家庭转移会放松家庭 CIA、同时形成通胀税效应；央行为保持总量不变而从金融系统抽走货币，会减少企业 working-capital funds、提高融资成本。恒定货币增长规则下，一个家庭端冲击实际上同时伴随一项银行端反向操作。

### 2.14 Taylor rule 与 Friedman rule 的 IRF 比较

技术冲击下的真实变量比较：

![Figure 12.11 — Real variables after technology shock: Taylor versus Friedman](../Figures/Ch12/figure_12_11_real_technology_taylor_vs_friedman.png)

两种规则下真实变量的响应总体相似。Taylor rule 会根据产出和通胀变化调整融资利率，因此产出、工资与资本回报的响应略有差异，但技术本身仍是主要驱动力。

名义变量的差异更大：

![Figure 12.12 — Nominal variables after technology shock: Taylor versus Friedman](../Figures/Ch12/figure_12_12_nominal_technology_taylor_vs_friedman.png)

constant-money-growth rule 迫使货币量回到既定路径，价格和存款最终回归；**<u>Taylor rule 为满足利率规则会内生调整货币供给，因此 nominal money、price level 和 deposits 可以收敛到新的水平。</u>**

> - 稳态是 “实际变量” 的稳态，因此名义变量上的冲击可能确实不会消失。

家庭端 monetary/fiscal shock 下的真实变量比较为：

![Figure 12.13 — Real variables after monetary shock: Taylor versus Friedman](../Figures/Ch12/figure_12_13_real_monetary_taylor_vs_friedman.png)

在 Friedman rule 下，央行必须完全抵消家庭转移，因此金融体系遭遇等量反向抽资，企业融资成本渠道更强，劳动和产出下降更明显。Taylor rule 只根据产出和通胀反馈调整利率，反应相对温和，因此真实变量跌幅较小。

名义变量与通胀比较为：

![Figure 12.14 — Nominal variables after monetary shock: Taylor versus Friedman](../Figures/Ch12/figure_12_14_nominal_monetary_taylor_vs_friedman.png)

![Figure 12.15 — Inflation after monetary shock: Taylor versus Friedman](../Figures/Ch12/figure_12_15_inflation_monetary_taylor_vs_friedman.png)

constant-money rule 下，初期通胀较低，随后出现通缩以把价格水平拉回原路径；Taylor rule 下，初期通胀更高，但随后逐步回落。两种规则的通胀方差并没有极端差异，却通过不同的利率与金融注入路径产生不同的真实调整。

### 2.15 本章模型能说明什么，不能说明什么

本章成功说明了三件事。第一，working-capital requirement 可以让利率直接进入企业边际成本。第二，货币注入位置是货币非中性的关键组成部分。第三，明确的 policy rule 必须配合一个实现工具；在这里，央行通过金融中介资产负债表调整企业借款利率。

但它还不是完整的现代金融 DSGE。贷款无风险，银行没有资本约束和运营成本，企业没有净值、违约或 external finance premium；全部工资账单都由一期贷款融资，也可能过强。Taylor-rule coefficients 的最优选择、规则的 determinacy 和福利评价都没有系统解决。

作者在 Exercise 12.1 中要求把本章金融中介与第 11 章 staggered wages 结合，这一点非常重要：工资粘性决定名义工资如何调整，working capital 决定既定工资如何通过融资成本进入企业劳动需求。两者结合后，货币政策同时作用于 nominal wage rigidity 与 financing-cost channel。

## 3. Compact Summary: What You Must Retain

- 本章把企业工资账单设为必须由一期 working-capital loan 预先融资，因此企业劳动成本从 $w_t$ 变为 $r_t^fw_t$。
- 家庭把期初货币分成消费现金与银行存款；银行把家庭存款和央行注入资金全部贷给企业支付工资。
- 央行注入银行的资金不需要支付家庭存款利息，因此能够降低企业借款利率，即使银行仍然零利润。
- 货币直接进入家庭时可能表现为 inflation tax；进入金融系统时则可能降低融资成本、提高劳动、资本、产出与福利。货币入口决定渠道。
- 高趋势货币增长改变的不只是通胀水平，也改变稳态利差、稳态比率和 log-linear coefficients，因此会改变冲击响应。
- Taylor rule 通过调整金融系统注资实现目标企业贷款利率；Friedman rule 则完全抵消家庭端货币冲击，使总货币增长恒定。
- 规则之间的差异不只是货币总量路径，还在于家庭端与银行端操作对消费约束和企业融资成本产生不同作用。
- 本章金融结构仍很简化：没有违约、净值、银行资本或 agency costs，不能直接替代完整的 financial accelerator model。

## 4. Figures, Tables, and Formulas to Check in the Original

本章重要图表均已作为原文截图嵌入 `Figures/Ch12/`：

- Table 12.1：不同趋势通胀下 working-capital economy 的稳态。
- Figure 12.1：稳态通胀与失业率之间的 Fisher/Phillips curve。
- Table 12.2：基准 working-capital model 的标准差与产出相关性。
- Figures 12.2–12.5：技术冲击与货币增长冲击下的真实、名义 IRF。
- Table 12.3 与 Figures 12.6–12.9：高趋势通胀经济及与零通胀经济的比较。
- Figure 12.10 与 Table 12.4：Taylor-rule economy 的目标通胀、贷款利率与稳态值。
- Figures 12.11–12.15：Taylor rule 与 Friedman rule 的技术、货币冲击比较。

最需要掌握的结构方程是：

$$
r_t^fw_t=(1-\theta)\lambda_tK_t^\theta H_t^{-\theta},
$$

$$
N_t+(g_t-1)M_{t-1}=P_tw_tH_t,
$$

$$
r_t^f[N_t+(g_t-1)M_{t-1}]=r_t^nN_t,
$$

以及政策实施式：

$$
g_t^M
=1+\frac{(r_t^n-r_t^f)N_t}{r_t^fM_{t-1}}.
$$

> ⚠️【需要回原文看图】A–N 系数矩阵、P/Q/R/S 数值矩阵以及高通胀稳态下的矩阵变化排版密集。理解模型不必记忆这些矩阵，但若要复现代码，必须回原文核对。

## 5. Questions and Answers

**Q1：working capital friction 的实质是什么？**  
它是企业端的现金先行约束。企业在出售产品取得收入以前必须先支付工资，所以需要一期贷款；借款利率因此乘在工资上，直接进入劳动边际成本。

**Q2：为什么家庭存款利率和企业借款利率可以不同，而银行仍然零利润？**  
因为银行除了家庭存款，还获得央行无息注入资金。企业贷款收益要覆盖家庭存款本息，但不必为央行资金付息，于是企业贷款利率可以低于家庭存款回报。

**Q3：为什么本章更高通胀会提高稳态产出，而第 8 章相反？**  
第 8 章新货币直接进入家庭，首先降低持币实际回报；本章新货币进入银行，首先增加可贷资金并降低企业工资融资成本。结论来自不同注入位置，不是“通胀本身”具有固定正负效应。

**Q4：为什么货币增长冲击下消费可能下降，而产出上升？**  
产出上升主要来自企业融资成本下降和劳动需求扩张；消费同时受家庭 CIA、存款选择、工资和跨期配置影响。一般均衡中产出增加不意味着当期消费必然增加。

**Q5：本章的 stationary-state Phillips curve 与 New Keynesian Phillips Curve 相同吗？**  
不同。本章是趋势货币增长通过银行融资补贴改变稳态就业；NKPC 则通常描述价格或工资粘性下通胀与实际边际成本的短期动态关系。

**Q6：Taylor rule 在模型中如何真正“设定利率”？**  
央行根据产出与通胀计算目标企业贷款利率，再调整对金融中介的货币注入，使银行资金约束和零利润条件支持该利率。

**Q7：Friedman rule 为什么会对企业产生额外收缩效应？**  
家庭端正向货币转移若要被完全抵消，央行必须从金融中介抽走等量货币。这样总货币增长不变，但企业可贷 working capital 减少、融资成本上升。

**Q8：本章与完整 BGG 金融加速器的差别是什么？**  
本章没有企业净值、违约概率、外部融资溢价或银行资本；借款利率变化来自央行注入资金的构成，而不是借款人资产负债表风险。因此它是 working-capital channel，不是完整的 financial accelerator。
