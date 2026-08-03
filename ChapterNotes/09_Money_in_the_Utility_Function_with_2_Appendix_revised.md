# Chapter 9 — Lecture Note

> Importance: ★★★☆☆  
> Suggested audit model: high  
> Reading mode: normal  
> Estimated note reading time: 60-80 minutes  
> Source reliability: text OK; important figures/tables are embedded as source screenshots; dense log-linear matrix blocks should be checked against the original before coding

## 0. How to read this note

第 9 章继续讨论怎样把 money 放进 RBC / DSGE 模型。第 8 章的 cash-in-advance model 让 money 有用，是因为家庭必须用事先持有的 cash 购买消费品。第 9 章换了一种建模方式：money 直接进入 utility function。这个方法通常叫 money-in-the-utility-function model，简称 MIU model。

读这一章时，不要把它当成一个全新的 business cycle model。它真正做的事情是比较两种货币建模方式：

第一，cash-in-advance model 把 money 当成交易约束。money 不直接带来效用，但没有 money 就不能购买某些商品。

第二，money-in-the-utility-function model 把 real balances 当成一种提供服务的对象。持有更多真实余额可以减少交易成本、降低搜寻成本、提供流动性或保险，所以家庭从 real balances 本身得到 utility。

本章的关键结论很干净：在 baseline MIU model 中，money growth 对真实变量具有 stationary-state superneutrality，而且在 log-linear dynamics 中也不影响真实变量。只有当政府通过 seigniorage 购买真实商品，并且稳态中已经存在正的 seigniorage financing 时，货币/财政冲击才会对真实变量产生影响。

## 1. Opening: 本章的核心问题

第 8 章的 CIA model 有一个直观优点：它抓住了“交易要用 money”的事实。但它也有一个缺点：模型直接假设消费品必须用现金购买，这个交易约束本身没有被进一步推导出来。

第 9 章采用 Sidrauski 风格的做法：假设 household 持有 real balances 会带来服务流。这个服务可以被理解为减少交易时间、减少搜寻成本、帮助和陌生人交易，或者提供流动性保险。于是 real balances $m_t/P_t$ 直接进入当期效用函数。

本章要回答四个问题：

1. 如果 money 进入 utility function，家庭一阶条件和价格决定式会怎样变化？
2. 在 MIU model 的稳态中，money growth 是否影响 consumption、capital、hours 和 output？
3. 在 log-linear dynamics 中，money growth shock 是否影响真实变量？
4. 如果新发行货币不是 lump-sum transfer 给家庭，而是被政府用来购买真实商品，seigniorage 会不会打破 monetary neutrality？

## 2. Main Lecture

### 2.1 为什么把 money 放进 utility function？

把 money 放进 utility function 的基本想法是：money 本身不生产消费品，也不像资本一样提高未来产出，但它提供交易服务。如果家庭持有更多 real balances，就可能少花时间找交易对象、少处理 barter 的 double coincidence of wants 问题，也可能在不确定环境中拥有更多流动性缓冲。

因此，本章把 household 的 period utility 写成：

$$
u(c_t^i,m_t^i/P_t,1-h_t^i).
$$

在具体模型中，作者使用：

$$
u(c_t^i,m_t^i/P_t,1-h_t^i)
=\ln c_t^i + D\ln(m_t^i/P_t)+Bh_t^i.
$$

这里 $D>0$ 是 real balances 在 utility 中的权重。$B<0$ 来自 Hansen indivisible labor structure。由于工作会减少 leisure，劳动项对效用的影响为负。

这个设定的优点是简单：只要 real balances 进入 utility，家庭就愿意持有 money，即使经济中还有 capital 这种有回报资产。模型因此能给 money 一个正价值。

但这个设定也有代价。它没有真正解释“哪一种 money”进入 utility，也没有解释 money 在模型内部具体做了什么。尤其在一个代表性家庭、单一商品、完全对称的经济中，家庭之间其实没有真实交易需要发生；money 只是因为写进 utility function 才变得有用。所以 MIU model 更像一种 reduced-form approximation：它用一个简洁的效用项捕捉 money 的交易服务，而不是从更细的交易技术中推导 money demand。

### 2.2 Baseline MIU model：家庭问题与约束

经济中有质量为 1 的相同 households。每个家庭选择消费、货币持有、下一期资本和劳动：

$$
\{c_t^i,m_t^i,k_{t+1}^i,h_t^i\}_{t=0}^{\infty},
$$

最大化 expected discounted utility：

$$
E_0\sum_{t=0}^{\infty}\beta^t
u(c_t^i,m_t^i/P_t,1-h_t^i).
$$

家庭的预算约束为：

$$
c_t^i+k_{t+1}^i+\frac{m_t^i}{P_t}
=w_th_t^i+r_tk_t^i+(1-\delta)k_t^i
+\frac{m_{t-1}^i}{P_t}
+\frac{(g_t-1)M_{t-1}}{P_t}.
$$

这条约束和第 8 章 CIA model 的预算约束很像，但有一个关键差别：这里没有 cash-in-advance constraint。家庭不再被要求用期初 cash 购买消费品。money 的作用不是交易时序约束，而是效用函数中的 real balance service。

货币供给按 gross growth rate $g_t$ 增长：

$$
M_t=g_tM_{t-1}.
$$

新增货币 $(g_t-1)M_{t-1}$ 以 lump-sum transfer 方式给家庭。技术和货币增长过程分别为：

$$
\ln\lambda_t=\gamma\ln\lambda_{t-1}+\varepsilon_t^\lambda,
$$

$$
\ln g_t=(1-\pi)\ln\bar g+\pi\ln g_{t-1}+\varepsilon_t^g.
$$

企业端仍然是 Cobb-Douglas：

$$
Y_t=\lambda_tK_t^\theta H_t^{1-\theta}.
$$

竞争性 factor prices 给出：

$$
r_t=\theta\lambda_tK_t^{\theta-1}H_t^{1-\theta},
$$

$$
w_t=(1-\theta)\lambda_tK_t^\theta H_t^{-\theta}.
$$

### 2.3 FOCs：money demand 与 price level 为什么是 forward-looking？

家庭的一阶条件可以分成三类。

第一，money holding condition。多持有一单位 nominal money 的好处是：今天 real balances 增加，直接带来 utility；同时这单位 money 也可以带到未来，变成未来购买力。其一阶条件可以写成：

> 收益：1.现期效用；2.未来的预算式影子价格
> 损失：1.现期的预算式的影子价格；

$$
\frac{1}{c_t^i}
=\beta E_t\left[\frac{P_t}{c_{t+1}^iP_{t+1}}\right]
+D\frac{P_t}{m_t^i}.
$$

这条式子是 MIU model 的核心。左边是消费的边际效用；右边第一项是 money 留到明天的真实价值，第二项是 real balances 今天直接提供的边际效用。和 CIA model 不同，money demand 来自 utility，而不是来自必须用 cash 购买消费品。

> 这里是消掉了本期预算式的乘子之后的样子；
>
> - 左边是：一单位消费的效用 = 一单位消费对预算式的压力/损耗；
> - 右边是：一单位货币增持的效用（直接效用、下一期的预算式的影子价格） = 一单位货币增持给本期预算式的压力；
>
> （其实可以这么想，就是把货币的等式里面的乘子全部替换成用消费的边际效用表示）

第二，capital Euler equation：

$$
\frac{1}{c_t^i}
=\beta E_t\left[
\frac{1}{c_{t+1}^i}(r_{t+1}+1-\delta)
\right].
$$

这和前面 RBC 模型中的 Euler equation 一样。家庭在消费和资本积累之间权衡，资本的回报是租金加未折旧资本。

> 一样的，把资本的（收益=损耗）均衡等式列出来后，用消费的边际效用替换掉乘子；

第三，labor condition：

$$
\frac{1}{c_t^i}=-\frac{B}{w_t}.
$$

> 一样，用消费的边际效用替换掉劳动均衡式里面的乘子；

因为 $B<0$，这条式子可以整理成：
$$
w_t=-BC_t
$$

在 aggregate equilibrium 中使用。

作者进一步说明 price level 的 forward-looking 性质。在代表性家庭均衡中，money FOC 可以写成：

$$
\frac{1}{P_tC_t}
=\beta E_t\left[\frac{1}{P_{t+1}C_{t+1}}\right]
+\frac{D}{M_t}.
$$

反复向前替代后，可得当前价格水平与未来 money supply 路径有关：

$$
\frac{1}{P_t}
=DC_t\sum_{j=0}^{\infty}\beta^jE_t\left(\frac{1}{M_{t+j}}\right).
$$

> <u>这里可以回忆一下我们关于 “如何处理期望算符” 的办法，碰到带期望算符的不一定就需要通过假设一个政策函数来闭合，我们可以试着往后迭代几次，如果没有出现 “自己依赖自己” 的那种无限循环，那么其实就可以不用担心</u>。

如果用未来 money growth rates 展开，就是：
$$
\frac{1}{P_t}
=\frac{DC_t}{M_t}
\sum_{j=0}^{\infty}\beta^jE_t
\left[
\prod_{k=1}^j\frac{1}{g_{t+k}}
\right].
$$

不要被这个式子的形式吓住。它的经济含义很简单：price level 不是只由当期 money stock 决定，而是由当期消费、当期 money stock 和未来预期 money growth 共同决定。如果家庭预期未来 money growth 更高，未来 money 的购买力更低，今天的 price level 会提前调整。

### 2.4 Stationary state：MIU 下的 superneutrality

稳态中，real variables 常数，real balances $M/P$ 常数。如果 money supply 以 $\bar g$ 增长，price level 也必须以 $\bar g$ 增长，所以稳态 inflation rate 等于 steady money growth rate。

稳态资本回报由 capital Euler equation 决定：

$$
\bar r=\frac{1}{\beta}-(1-\delta).
$$

> 不同期之间的影子价格（不包含折现）应该是一样的，因此资本存储的收益（r + 1 - δ）乘上折现因子之后要保持不变，即等于 1，这样才能够维持资本这一项的 “收益 = 损耗” 的平衡；

稳态工资由 factor price conditions 决定：
$$
\bar w=(1-\theta)\left(\frac{\theta}{\bar r}\right)^{\theta/(1-\theta)}.
$$

> 稳态资本的均衡要求利率固定，因此劳动与资本的比例固定，因此工资一定固定；

稳态消费由 labor condition 决定：
$$
\bar C=-\frac{\bar w}{B}.
$$

> 一般这个稳态消费 c 都能通过两个等式来求解，一是消费的 FOC条件，二是商品市场均衡/家庭预算约束；
>
> 在前面我们解出了稳态 r、工资 w，这代表着劳动到约束式的乘子 w 是稳定的，再加上我们已经知道劳动的边际损耗是一个常数，以此此时预算式的影子价格就被钉住了，因此此时我们只需要利用消费 c 的一阶条件（边际收益 = 影子价格的损耗）即可解出稳态 c

这些式子都没有出现 $\bar g$。这就是本章最重要的结果：在 baseline MIU model 中，steady money growth 不影响 $\bar r,\bar w,\bar C$，进一步也不影响 $\bar K,\bar H,\bar Y$。

real balances 则由 money FOC 决定：

$$
\frac{M}{P}
=D\frac{\bar g\bar C}{\bar g-\beta}.
$$

> 解出约束式的影子价格之后，回到货币的 FOC 等式那里，直接展开成等比数列求和即可；

> **<u>价格的决定逻辑其实是这样的</u>**：货币有直接效用、同时也连接到约束式产生代价，那么稳态的时候会要求货币的边际效用 = 边际损失，但是注意到货币市场的出清要求持有货币量是一个固定值，这就导致货币的边际收益其实最终是固定的，我们不妨假设没有价格 p，那么这个边际收益不一定能够跟影子价格对得上（除非强制锚定影子价格就等于货币的边际收益）。如果存在多个这种“锚定类型”的变量（例如劳动 h），那么均衡就会陷入角点解，这其实不太好。
>
> 因此价格在这里面类似于一个弹簧，用来弥合固定的收益与错位的影子价格之间的间隙；

这条式子说明，money growth 越高，持有 money 的机会成本越高，稳态 real balances 越低。真实余额会调整，但真实产出、资本、劳动和消费不变。

作者把这种性质称为 superneutrality。普通 neutrality 通常指 money level 的一次性变化不影响真实变量；superneutrality 更强，指 money growth rate 的变化也不影响长期真实变量。

**<u>需要注意一个小问题。当 $\bar g=\beta$ 时，上式中的分母为 0，模型暗示 desired real balances 趋于无穷大。这和 Friedman rule 的直觉有关：如果 money 的 nominal return 通过 deflation 被调到接近无风险资产回报，持有 money 的机会成本消失，家庭想持有大量 real balances。但这里的无穷大结果也依赖于 separable log utility for real balances，是这个具体效用形式带来的特殊性</u>**。

> 因为资本的均衡条件等式，所以折现率 β 就被跟无风险利率强制连接在一起，当货币增速接近这个无风险利率时，大家就会想要持有无限多的实际货币；

![Table 9.1 — Stationary state values](../Figures/Ch09/table_9_1_stationary_state_values.png)

Table 9.1 给出标准校准下的稳态值。参数包括 $\beta=0.99,\delta=0.025,\theta=0.36,B=-2.5805$，并选择 $D=0.01$，使得在 $\bar g=1$ 时 real balances 与第 8 章 CIA model 的对应值一致。

### 2.5 Log-linear version：为什么 money growth shock 不影响真实变量？

接下来作者把模型 log-linearize。变量包括：

$$
\tilde K_t,\tilde M_t,\tilde P_t,\tilde r_t,\tilde w_t,\tilde C_t,\tilde Y_t,\tilde H_t,
$$

以及两个 shocks：

$$
\tilde\lambda_t,\tilde g_t.
$$

系统可以整理成前几章熟悉的 Uhlig-style form：

$$
0=Ax_t+Bx_{t-1}+Cy_t+Dz_t,
$$

$$
0=E_t(Fx_{t+1}+Gx_t+Hx_{t-1}+Jy_{t+1}+Ky_t+Lz_{t+1}+Mz_t),
$$

$$
z_{t+1}=Nz_t+\varepsilon_{t+1}.
$$

这里作者把：

$$
x_t=[\tilde K_{t+1},\tilde M_t,\tilde P_t]'
$$

称为 state variables，把：

$$
y_t=[\tilde r_t,\tilde w_t,\tilde C_t,\tilde Y_t,\tilde H_t]'
$$

称为 jump variables。

但有一个很重要的细节：$\tilde P_t$ 其实不是真正的 predetermined state。价格是 forward-looking variable，会根据 expected future money growth 立即调整。作者后面解出的 policy matrices 也显示，价格在真实变量方程中的系数为 0。

在 $\bar g=1$ 的校准下，解出来的 policy matrices 有两个经济含义。

第一，money growth shock 只影响 $\tilde M_t$ 和 $\tilde P_t$，不影响 real variables。也就是说，货币增长冲击会改变 nominal money 和 price level 的动态路径，但不会改变 consumption、output、capital、hours、wage、rental rate。

> 不光是稳态不会改变，就连 shock 都无法引起其任何变动。
>
> 原理其实不难想，因为当货币增速发生永久变化时，实际变量那一侧完全不需要变动，然后预算式的影子价格维持不变，因此货币的价值就单纯通过价格的变动（即乘子系数的变动）来进行调节，使之维持在与预算式的影子价格相匹配的水平上；

第二，money 和 prices 对 money growth shock 的反应并不完全同步。因为 price level 是 forward-looking，价格会提前反映未来 money growth 的预期；money stock 则按照 money growth process 逐步调整。

![Figure 9.1 — Response of money and prices to money growth shock](../Figures/Ch09/figure_9_1_money_prices_money_growth_shock.png)

Figure 9.1 展示一次 money growth shock 后 money 和 prices 的响应。两者最终都会上升到相近的新水平，但 prices 调整更快。由于 prices 短期内比 money stock 上升得更快，real balances $M/P$ 会下降。这是 MIU model 中货币冲击的主要效果：它改变 real balances 和价格路径，但不改变真实生产和劳动配置。



### **2.Appendix：状态变量、通用变量、政策函数与 jump variables

#### 1. 为什么要做变量分类？

变量分类的目的是回答：

$$
\boxed{
\text{站在时期 }t\text{ 的决策时点，哪些量已经给定，哪些量仍需由均衡系统求解？}
}
$$

因此，先把模型中的变量分成两大集合：

$$
\boxed{
\text{环境状态变量}
\qquad\text{与}\qquad
\text{通用变量}.
}
$$

“通用变量”是一个工作性称呼，指所有在<u>当期尚未确定</u>、必须由<u>完整均衡方程组</u>共同决定的内生变量。

---

#### 2. 第一类：环境状态变量

环境状态变量记为：

$$
s_t.
$$

其共同特征是：

> 在时期 \(t\) 的冲击已经实现、经济主体开始作当期决策时，其当前取值已经确定，不能再由本期的内生选择重新决定。

它们主要来自两个方向。

##### （1）过去继承下来的内生变量

例如：

$$
K_t,\qquad B_{t-1},\qquad m_{t-1}.
$$

这些变量由过去的选择决定。以资本为例：

$$
K_t=(1-\delta)K_{t-1}+I_{t-1}.
$$

进入时期 \(t\) 后，当前资本存量 \(K_t\) 已经确定。家庭只能通过本期投资决定 \(K_{t+1}\)，不能重新选择 \(K_t\)。

##### （2）当期已经实现的外生变量

例如：

$$
A_t,\qquad g_t,\qquad \tau_t,\qquad \varepsilon_t.
$$

它们在本期实现前可能不确定，但在时期 \(t\) 的决策发生时已经实现，因此同样属于家庭和企业面对的既定环境。

因此，可以统一写成：

$$
\boxed{
s_t=
\begin{bmatrix}
\text{继承的内生变量}\\
\text{当前已经实现的外生变量}
\end{bmatrix}.
}
$$

最终求解 DSGE 的目标，就是把当期尚未确定的变量表示成当前环境状态的函数。

---

#### 3. 第二类：通用变量

除环境状态变量以外，其余当期尚未确定的内生变量统一记为：

$$
v_t.
$$

这一集合可以包括：

- 家庭的消费、劳动、储蓄、投资和持币选择；
- 企业的投入、产出和定价决策；
- 市场工资、利率、商品价格和资产价格；
- 政府的内生政策变量；
- 各类约束对应的影子价格；
- 各种总量和相对价格。

例如：

$$
v_t=
\left(
C_t,H_t,K_{t+1},w_t,r_t,Y_t,P_t,\lambda_t,\ldots
\right).
$$

这些变量通常通过复杂的联立关系相互连接：

$$
\text{消费边际效用}
\longleftrightarrow
\text{预算影子价格}
\longleftrightarrow
\text{劳动条件}
\longleftrightarrow
\text{工资和生产}
\longleftrightarrow
\text{资本回报}.
$$

在复杂 DSGE 中，它们往往是同时确定、双向联系的，一般是不太可能把它们拆成若干具有单向决定关系的子集合；

---

#### 4. 为什么完整方程组仍然可能没有闭合？

把家庭 FOC、企业 FOC、预算约束、政府预算、市场出清和外生过程全部列出后，模型可以抽象写成：

$$
\boxed{
F\left(s_t,v_t,E_tv_{t+1}\right)=0.
}
$$

给定当前状态 \(s_t\) 后，当期通用变量 \(v_t\) 本应由这套均衡条件共同决定。

困难在于，一些当前变量依赖未来尚未确定的内生变量。

> 例如消费 Euler equation：
> $$
> u_C(C_t)
> =
> \beta E_t
> \left[
> u_C(C_{t+1})R_{t+1}
> \right].
> $$
> 时期 \(t\) 的消费依赖时期 \(t+1\) 的消费与回报；而时期 \(t+1\) 的消费又依赖时期 \(t+2\) 的变量，于是形成：
> $$
> C_t
> \longrightarrow
> E_tC_{t+1}
> \longrightarrow
> E_tC_{t+2}
> \longrightarrow\cdots
> $$
> 这样的无限前瞻递归。

因此，真正需要处理的是：**<u>经过所有可行的代换和联立以后，是否仍有某些独立变量形成 “自己依赖自己” 的无限循环</u>**？

需要注意的就是有些未来变量虽然出现在方程中，但可以继续利用其他关系表示为另外的未来变量和未来状态的函数，因此不构成新的**<u>独立递归方向</u>**。

> 例如，如果：
> $$
> H_t=h(C_t,K_t,A_t),
> $$
> 那么：
> $$
> H_{t+1}
> =
> h(C_{t+1},K_{t+1},A_{t+1}).
> $$
> 即使原方程中出现了 \(E_tH_{t+1}\)，它也可以被改写为未来消费和未来状态的函数，并不一定需要为劳动再独立设置一套政策函数。

所以，判断标准是“独立的自我前瞻循环”，而不是简单数有多少个带 \(t+1\) 或期望符号的变量。

---

#### 5. 政策函数如何关闭无限递归？

假设经过整理后，剩下的独立前瞻递归变量记为：

$$
j_t.
$$

为它们设置政策函数：

$$
\boxed{
j_t=J(s_t).
}
$$

这表示：给定当前环境状态，均衡中的这些变量应当取什么值。

下一期同一规律仍然成立：

$$
j_{t+1}=J(s_{t+1}).
$$

而下一期状态满足：

$$
s_{t+1}
=
T(s_t,v_t,\varepsilon_{t+1}).
$$

因此：

$$
E_tj_{t+1}
=
E_t
\left[
J\left(
T(s_t,v_t,\varepsilon_{t+1})
\right)
\right].
$$

把它代回原来的均衡方程，原来不断向未来延伸的递归就被政策函数闭合。

**<u>真正的政策函数必须满足自洽性</u>**：
$$
\boxed{
J=\mathcal T[J].
}
$$

也就是说，先假设经济以后都按照 \(J\) 运行，代回均衡方程后重新求出的当期 \(j_t\)，必须恰好等于 \(J(s_t)\)。

这就是动态模型求解的核心固定点问题。

---

#### 6. 并不是只有 \(j_t\) 才有政策函数

最终均衡解出来以后，所有通用变量都可以表示成状态变量的函数：

$$
v_t=V(s_t).
$$

例如：

$$
C_t=C(s_t),\qquad
H_t=H(s_t),\qquad
w_t=W(s_t),\qquad
P_t=P(s_t).
$$

因此，广义上所有内生变量最终都有政策函数或均衡函数。区别只在于：**<u>并不是每个变量都需要被独立猜测一个政策函数</u>**。

只需要对那些<u>自我前瞻循环</u>的变量设置政策函数。它们一旦求出，其余变量便可以通过原来的方程组恢复 / 得到政策函数。

---

#### 7. 三类变量与线性化系统

按照前面的分类，整个模型中的变量可以整理为三类：

$$
\boxed{
\begin{aligned}
s_t&：\text{环境状态变量；}\\
q_t&：\text{普通变量；}\\
j_t&：\text{形成独立无限前瞻递归的变量。}
\end{aligned}
}
$$

其中，$s_t$ 在时期 $t$ 的决策时点已经给定；$q_t$ 与 $j_t$ 都尚未确定，需要由完整均衡系统共同求解。

> 二者的区别在于：$q_t$ 不会留下独立的自我前瞻循环；而 $j_t$ 会形成 $j_t\longrightarrow E_tj_{t+1}\longrightarrow E_tj_{t+2} \longrightarrow\cdots$ 这样的无限递归。

如果像本章一样，不在非线性模型中提前消去工资、利率、产出、影子价格等中间变量，而是把全部均衡条件保留下来再统一一阶展开，线性化后的完整系统可以抽象写成两组方程。

- 第一组包含状态转移和前瞻动态关系：【**<u>仅包含 s 以及 j 的变量</u>**】
    $$
    0
    =
    A_sE_ts_{t+1}
    +B_ss_t
    +A_jE_tj_{t+1}
    +B_jj_t
    +A_qq_t
    +A_q^+E_tq_{t+1}.
    \tag{1}
    $$
    
- 第二组把普通变量与当前状态、当前前瞻变量连接起来：【**<u>在得到 j 的政策函数之后，进一步确定 q 类型变量</u>**】
    $$
    0
    =
    C_ss_t+C_jj_t+C_qq_t.
    \tag{2}
    $$

> 普遍的做法是可以这样的，因为在线性化之后，一般而言都是可以进行消元、然后把 q 变量全部消除，再得到一个纯粹只有 s 、j 变量的方程组，这部分就能够作为 Schur method 的操作起始点；

> 【<u>如何消元</u>】
>
> 一阶展开以后，普通变量之间的关系成为线性联立方程组。只要方程数量足够、相应系数矩阵具有满秩，就可以由（2）整体解出：
> $$
> C_qq_t
> =
> -C_ss_t-C_jj_t,
> $$
>
> 从而得到：
>
> $$
> \boxed{
> q_t
> =
> -C_q^{-1}C_ss_t
> -C_q^{-1}C_jj_t.
> }
> $$
>
> 简写为：
>
> $$
> \boxed{
> q_t=Q_ss_t+Q_jj_t.
> }
> \tag{3}
> $$
>
> 另外：
> $$
> \boxed{
> E_tq_{t+1}
> =
> Q_sE_ts_{t+1}
> +
> Q_jE_tj_{t+1}.
> }
> \tag{4}
> $$
>
> 这说明，<u>**普通变量即使出现在未来期，也不会自动形成新的独立前瞻方向**</u>。只要它能够由未来状态和未来 $j_{t+1}$ 表示，就可以继续代换。

> 普通变量能够被消去所需要的条件，是相关线性方程对 $q_t$ 具有足够的独立秩：
>
> $$
> \operatorname{rank}(C_q)=\dim(q_t).
> $$
>
> 满足这一条件时，普通变量可以被统一表示成 $s_t$ 和 $j_t$ 的函数。若不满秩，说明当前分类或方程体系仍未闭合：可能存在遗漏的状态方向、遗漏的前瞻方向、冗余方程、缺失的均衡条件，或者尚未处理的名义归一化问题。

把（3）和（4）代回动态方程（1），普通变量 $q_t$ 与 $E_tq_{t+1}$ 就从核心系统中消失。

整理后得到：

$$
\boxed{
\widetilde A_sE_ts_{t+1}
+
\widetilde B_ss_t
+
\widetilde A_jE_tj_{t+1}
+
\widetilde B_jj_t
=0.
}
\tag{5}
$$

> 也可以把（5）整理成：
>
> $$
> \begin{bmatrix}
> s_{t+1}\\
> E_tj_{t+1}
> \end{bmatrix}
> =
> M
> \begin{bmatrix}
> s_t\\
> j_t
> \end{bmatrix},
> \tag{6}
> $$
>

这一步把完整线性方程组约化成只包含：
$$
s_t,\qquad E_ts_{t+1},\qquad j_t,\qquad E_tj_{t+1}
$$

> $s_{t+1}$ 跟 q 变量一样，也不会涉及无限递归，因此最终也能够转化为 st 与 jt 的函数；

真正进入 Schur/QZ 分解的，是经过完整方程组约化以后剩余的：

$$
\boxed{
\text{环境状态方向 s}
\qquad\text{与}\qquad
\text{独立无限前瞻递归变量 j}.
}
$$

---

#### 8. Schur/QZ 如何确定第 3 类变量的政策函数？

在时期 $t$，环境状态 $s_t$ 已经给定，$j_t$ 的当前取值仍然可以调整。任意选择 $j_t$，通常会使初始向量

$$
\begin{bmatrix}
s_t\\
j_t
\end{bmatrix}
$$

同时包含稳定方向和爆炸方向。

Schur/QZ 分解把系统中的动态方向分成：

$$
\text{稳定方向}
\qquad\text{与}\qquad
\text{爆炸方向}.
$$

给定 $s_t$ 后，需要选择 $j_t$，使整个初始向量位于稳定不变子空间上，从而消除爆炸分量。由此得到：

$$
\boxed{
j_t=Fs_t.
}
\tag{8}
$$

这就是第 3 类变量的线性政策函数。

前面识别出的“独立自我前瞻递归变量”，正是 Schur/BK 条件中需要通过当期取值选择稳定路径的 jump variables。它们的当前值没有被过去锁定，可以根据未来均衡与稳定性要求立即调整。

> 在我们这个例子中价格水平也可以属于这一类。它虽然不是家庭的 control variable，却满足这个依赖关系：
> $$
> P_t
> \longrightarrow
> E_tP_{t+1}
> \longrightarrow
> E_tP_{t+2}
> \longrightarrow\cdots
> $$
> 这样的独立前瞻递归，并且没有被上一期价格机械决定。在这种模型中，价格就是 jump variable。

---

#### 9. 代回原方程组，恢复普通变量的政策函数

Schur/QZ 给出：

$$
j_t=Fs_t.
$$

前面已经得到：

$$
q_t=Q_ss_t+Q_jj_t.
$$

把第 3 类变量的政策函数代入：

$$
q_t
=
Q_ss_t+Q_jFs_t,
$$

于是：

$$
\boxed{
q_t=(Q_s+Q_jF)s_t.
}
\tag{9}
$$

记：

$$
G=Q_s+Q_jF,
$$

就得到：

$$
\boxed{
q_t=Gs_t.
}
\tag{10}
$$

整个模型最终被写成：

$$
\boxed{
\begin{aligned}
j_t&=Fs_t,\\
q_t&=Gs_t,\\
s_{t+1}&=T_s s_t+T_\varepsilon\varepsilon_{t+1}.
\end{aligned}
}
$$

求解过程由此完全闭合：

$$
\boxed{
\text{完整均衡方程组}
\longrightarrow
\text{一阶线性化}
\longrightarrow
\text{消去普通变量}
\longrightarrow
\text{Schur/QZ 求 }j_t=Fs_t
\longrightarrow
\text{代回求 }q_t=Gs_t.
}
$$

书中所谓“不提前消元”，指的是在非线性模型和建模阶段保留工资、利率、产出、影子价格等变量，统一写出并线性化全部方程。进入线性求解阶段以后，这些普通变量仍然会通过线性代数被显式消去，或者由求解器在 generalized Schur/QZ 过程中隐式约化。

> 先消元再一阶近似、先一阶近似再消元，其实结果是一样的（但就从一阶近似的角度来说，二者精确度是一样的，不会产生遗漏）

整套逻辑可以压缩为：

$$
\boxed{
\begin{aligned}
&1.\ \text{环境状态变量在时期 }t\text{ 已经给定；}\\
&2.\ \text{普通变量与无限前瞻递归变量由完整均衡系统共同决定；}\\
&3.\ \text{一阶线性化后，普通变量可以通过线性联立方程统一消去；}\\
&4.\ \text{约化系统只保留状态方向和独立无限前瞻递归方向；}\\
&5.\ \text{Schur/QZ 选择第 3 类变量，使系统落在稳定不变子空间；}\\
&6.\ \text{第 3 类政策函数求出后，代回原方程恢复所有普通变量。}
\end{aligned}
}
$$

### 2.6 Technology shock：真实侧和 CIA model 相同

Figure 9.2 展示 MIU model 对一次 technology shock 的真实变量响应。

![Figure 9.2 — Responses to a .01 impulse in technology](../Figures/Ch09/figure_9_2_technology_impulse_responses.png)

这个图的重点不是每条线的微小差异，而是一个对照结论：这些真实变量响应和第 8 章 Cooley-Hansen cash-in-advance model 中的技术冲击响应相同。原因是，在 baseline MIU model 中，money sector 没有改变 real side 的资源约束、生产函数、capital Euler equation 和 labor condition 的核心结构。

技术冲击提高生产率，导致 output、investment、capital、consumption 和 hours 按 RBC 机制响应；price level 则根据 money demand 和 real balances 条件调整。但真实侧的 dynamics 仍然由 technology、capital accumulation 和 labor choice 驱动，而不是由 money growth shock 驱动。

这就是本章所谓 dynamic superneutrality：不只是稳态中 money growth 不影响真实变量，在 log-linear dynamics 中，money growth shock 也不推动真实变量波动。

### 2.7 Seigniorage：从 lump-sum transfer 到政府购买

> 最简单的直觉：
>
> 1. 资本 k 连接前后预算式的影子价格；因为 “<u>均衡时影子价格是一样的</u>”（$λ_{t}=λ_{t+1}$），所以利率是被折现率锁定的，因此劳动、资本的比例是不变的，因此工资 w 也不变；
>
> 2. 工资 w 不变就锁定了劳动对预算式的影子价格的锚定效应，因此影子价格始终就是不变的；
>
> 3. 现在我们来看消费 c，消费的收益只有当期边际效用的增加，损失只有当期预算式的影子价格，因此影子价格不变，那么消费数量就是不变的，消费 c 也被锁死了；
>
> 4. 现在我们来看政府购买，如果政府的实际购买增加了，那么总产出就会增加，这代表着劳动与资本投入的增加；
>
> 5. g = (φ-1)/φ \* M/P，现在我们就分析实际货币会怎么变；
>
> 6. 这里需要用到货币的均衡等式：λ/p\_{t+1} + D/m\_t = λ/p\_t，变形得到：M/p = (φ\*D) / (φ-β)\*λ ，代入就能够知道：
>
>     $g\approx (\frac{φ-1}{φ\\})·\frac{φ·D}{(φ-β)λ}$，因此当货币增速 φ 增加的时候，g 也会慢慢增加，因此总产出是增加的；

前面 baseline model 假设新发行 money 以 lump-sum transfer 给家庭。第 9.4 节改变这一点：政府通过发行 money 购买真实商品。也就是说，money creation 现在用于 financing government expenditure。这就是 seigniorage。

政府预算约束为：

$$
g_t=\hat g_t\bar g=\frac{M_t-M_{t-1}}{P_t}.
$$

这里 $g_t$ 不再表示 money growth rate，而表示由 seigniorage financed 的 real government consumption。作者也提醒这个符号有点容易混淆。为了区分，货币供给增长因子写成：

$$
M_t=\phi_tM_{t-1}.
$$

于是：

$$
g_t
=\frac{\phi_t-1}{\phi_t}\frac{M_t}{P_t}.
$$

这个版本和 baseline MIU model 的区别有两个。

第一，家庭不再收到 lump-sum money transfer。家庭预算约束变成：

$$
c_t^i+k_{t+1}^i+\frac{m_t^i}{P_t}
=w_th_t^i+r_tk_t^i+(1-\delta)k_t^i+\frac{m_{t-1}^i}{P_t}.
$$

第二，政府购买真实商品，因而进入 aggregate resource constraint。稳态 feasibility constraint 变成：

$$
\bar C+\bar g+\delta\bar K=\bar Y.
$$

这一步是 seigniorage 打破 neutrality 的关键。baseline MIU 中新钱只是转移给家庭，aggregate resource constraint 不变；seigniorage 版本中新钱被政府用来购买真实 goods，所以私人 consumption、government purchases、investment replacement 都要从 output 中分配。

### 2.8 Seigniorage steady states：为什么消费不变，但资本和劳动上升？

在 seigniorage 版本的稳态中，政府预算约束为：

$$
\bar g=\left(1-\frac{1}{\bar\phi}\right)\frac{M}{P}.
$$

money FOC 给出：

$$
\frac{M}{P}
=D\frac{\bar\phi\bar C}{\bar\phi-\beta}.
$$

所以 seigniorage revenue 可以写成：

$$
\bar g
=\frac{(\bar\phi-1)D\bar C}{\bar\phi-\beta}.
$$

这就是 Bailey curve 的来源：提高 money growth / inflation 会提高 inflation tax rate，但也会降低 real balances tax base。两种力量相互作用，使 seigniorage 和 inflation 的关系不是简单线性。

![Figure 9.3 — Real seigniorage](../Figures/Ch09/figure_9_3_real_seigniorage.png)

Figure 9.3 显示标准校准下的 real seigniorage curve。在本章的参数范围内，seigniorage 随 inflation 上升而增加，但逐渐变平，说明税基收缩开始抵消税率上升。

稳态中一个看似反直觉的结论是：consumption 不随 seigniorage steady state 改变。原因是 $\bar r$ 由 Euler equation 决定，$\bar w$ 由 factor prices 决定，$\bar C=-\bar w/B$ 又由 labor condition 决定。这三者都没有直接使用 money growth。

那么更高 seigniorage 如何被 finance？答案是：通过更高 output。由于 consumption 不变，而政府要购买更多 goods，经济必须有更高 capital 和 hours 来生产更多 output，同时还要替换更高 capital stock 带来的 depreciation。

![Table 9.2 — Stationary states for different inflation rates](../Figures/Ch09/table_9_2_stationary_states_inflation_rates.png)

Table 9.2 展示这个机制。随着 inflation 从 0% 提高到 400%，rental、wages、consumption 基本不变；real balances 大幅下降；output、capital、hours worked 小幅上升；seigniorage 上升但趋于平缓。

### 2.9 Seigniorage dynamics：什么时候 money 不再中性？

> 什么时候不再中性？我们可以这么考虑：
>
> 1. 货币增发意味着家庭必须持有更多的货币，那么这就需要考虑货币的均衡等式条件，不妨老样子假设所有变量都不发生改变，那么由于效用函数的特性，货币数量增加到一定程度后，边际效用是降低的，因此需要通过增加 “增持一单位货币” 的未来的收益、降低 “增持一单位货币” 对本期预算式的loss；
> 2. 一般我们先不考虑直接降低影子价格，尤其这里还是工资不变、影子价格因此被劳动锁定而不能改变的局面。
> 3. 那么我们就能考虑货币对于预算式的影响力的乘子了（在预算式里面，一单位货币变动都要乘一个价格的导数才能转换到对预算式本身的直接影响），两个乘子分别是 β/p\_{t+1} 以及 1/p\_t，（考虑到稳态时，实际货币/实际价格应该是稳定的，不可能一直维持一个单调增/单调减的情况），我们可以考虑同时放大 pt 以及 p\_{t+1}，这样就会让这两边的差距缩小，能够让降低后的货币边际效用依然能够补上之后维持收益 = 损失的平衡。
> 4. 从这里我们可以看到，如果我们真得想通过货币来改变 c、h、k 的比例，那么我们就要从劳动的边际损失这边下功夫，不能够让某个变量 “锚定” 影子价格；
> 5. 同时由于资本这一项沟通前后两期预算式的作用，如果不改变 k 的连通结构，利率 r 就一定是被锁死的，如果生产函数依然是 cb 型，那么工资 w 一定被锁死，k/h 比例不可能改变；

Seigniorage 版本也可以 log-linearize。相对于 baseline MIU model，主要变化是 household budget constraint、money growth rule 和 government budget constraint。

作者重点比较两个稳态。

第一，如果 $\bar\phi=1$，稳态中没有 seigniorage financing。此时对 seigniorage shock 的响应除了 money 和 prices 之外是 flat 的。换句话说，在 no-seigniorage steady state 附近，经济仍然表现出 dynamic neutrality。

第二，如果 $\bar\phi=1.19$，稳态中有正的 seigniorage financing。此时政府本来就通过 money creation 购买 goods，所以 seigniorage shock 会改变 government purchases，进而进入 resource constraint，真实变量会有反应。

> 注意这里我们需要区分 “比较静态” 与 “动态分析”
>
> 1. 对于前者，我们主要是对比其不同的稳态之间的状况，在这个对比中，因为利率、工资都被锁死，因此货币增速是不改变这些变量；
>
> 2. 对于后者，也就是下面 figure 9.4 所显式的，它研究的是在旧稳态中如果发生变化，那么经济中各变量如何迁移到新稳态，因此 w、r 都会在中途发生变化。例如货币变化后，在新一期的基础上，我们拿到手上的变量并不是处在均衡状态的。
>
>     例如政府在 t 期的初期突然大量增发货币，这就会导致总产量不足，推动劳动力投入增加，但是此时资本存量还是老样子，因此这就会导致比例错配，w、r 发生波动；
>
>     【本质上就是慢变量，例如资本，没办法直接一步走到均衡，因此 jump variable 还得陪着慢变量一步步演化；数学上就是说，我们不能把均衡方程组的下标 t 擦掉，得慢慢看它演化】

![Figure 9.4 — Response to seigniorage shock](../Figures/Ch09/figure_9_4_seigniorage_shock_response.png)

Figure 9.4 展示 $\bar\phi=1.19$ 时一次 seigniorage shock 对真实变量的响应。注意纵轴尺度是 $10^{-5}$，所以真实变量反应很小。但它不是零。hours、rental rate、output、wage 和 consumption 都出现响应，并逐步回到稳态。这说明：货币冲击是否中性，取决于它是否通过政府购买进入真实资源配置。

作者还考察了在 positive seigniorage steady state 下，technology shock 对 money 和 prices 的影响。

![Figure 9.5 — Responses of money and prices to a technology shock with seigniorage](../Figures/Ch09/figure_9_5_money_prices_technology_shock_seigniorage.png)

Figure 9.5 显示，技术冲击发生后，money 和 prices 都下降到一个新水平，但 $M/P$ 的 ratio 最终回到稳态值。直觉是：正的技术冲击提高生产能力并压低相对价格；由于政府购买支出通过 seigniorage finance，较低价格意味着政府不需要发行同样多 money 来购买给定真实支出。prices 下降得比 money 更快，但长期二者的相对变化使 real balances 回到稳态比例。

### 2.10 Reprise：第 9 章在全书中的位置

本章给了第二种货币建模技术：MIU。它比 CIA model 更简单，也更容易放进代表性家庭优化问题中。只要 real balances 进入 utility，money demand 就自然出现。

但 MIU model 的解释力也更弱。它把 money 的交易服务直接塞进 utility，而没有解释背后的交易技术。因此它适合快速生成 money demand 和 price dynamics，却不是最深层的 monetary microfoundation。

在 baseline MIU model 中，money growth 对真实变量具有强 neutrality：稳态中不影响 real variables，log-linear dynamics 中 money growth shock 也不影响 real variables。加入 seigniorage 后，结论更微妙：如果稳态中没有 seigniorage financing，冲击仍然中性；如果稳态中已经有 positive seigniorage，money-financed government purchases 会进入 resource constraint，从而让货币/财政冲击影响真实变量。

## 3. Compact Summary: What You Must Retain

本章最重要的内容可以压缩成七点。

第一，MIU model 把 real balances 直接放进 utility function，用来近似 money 提供的交易服务、流动性服务或保险服务。

第二，baseline MIU model 没有 cash-in-advance constraint。money demand 来自 real balances 的边际效用，而不是来自消费必须用现金购买。

第三，money FOC 让 price level 具有 forward-looking 性质：当前 price level 取决于当前 money stock、current consumption 和 expected future money growth。

第四，在 baseline MIU steady state 中，steady money growth 不影响 consumption、capital、hours、output、wages 和 rental rate，只影响 real balances。这就是 stationary-state superneutrality。

第五，在 log-linear baseline MIU model 中，money growth shock 只影响 money 和 prices，不影响真实变量；prices 调整快于 money，所以 real balances 短期下降。

第六，technology shock 的真实变量响应和第 8 章 CIA model 相同，因为 baseline MIU 的 money sector 没有改变 real side 的核心资源配置。

第七，seigniorage 会改变 neutrality 结论。若政府用新发行 money 购买真实商品，并且稳态中有 positive seigniorage financing，则 seigniorage shocks 会通过 government purchases 和 resource constraint 影响真实变量。

## 4. Figures, Tables, and Formulas to Check in the Original

本章重要图表已经作为截图放入 `Figures/Ch09/`，并在正文中嵌入：

- Table 9.1：baseline MIU model 的 stationary state values。
- Figure 9.1：money growth shock 下 money 和 prices 的响应。
- Figure 9.2：technology shock 下真实变量响应，与 CIA model 对照。
- Figure 9.3：real seigniorage 与 gross stationary inflation rate 的关系。
- Table 9.2：不同 inflation rates 下的 seigniorage steady states。
- Figure 9.4：positive seigniorage steady state 下真实变量对 seigniorage shock 的响应。
- Figure 9.5：positive seigniorage steady state 下 money 和 prices 对 technology shock 的响应。

最需要回原文核对的公式包括：

$$
\frac{M}{P}=D\frac{\bar g\bar C}{\bar g-\beta},
$$

baseline MIU 的 price-level forward-looking expression：

$$
\frac{1}{P_t}
=DC_t\sum_{j=0}^{\infty}\beta^jE_t\left(\frac{1}{M_{t+j}}\right),
$$

以及 seigniorage steady state：

$$
\bar g
=\frac{(\bar\phi-1)D\bar C}{\bar\phi-\beta}.
$$

> ⚠️【需要回原文看图】这里涉及重要图表/表格/公式，PDF 文本提取可能不足以完整保留信息。建议回到原文核对。

如果要复现本章 Matlab code 或矩阵求解，需要回原文核对 log-linear system 中 $x_t,y_t,z_t$ 的变量顺序，以及 baseline MIU 和 seigniorage model 中 $A,B,C,D,F,G,H,J,K,L,M,N$ 矩阵的每个元素。

## 5. Questions and Answers

**Q1：MIU model 和 CIA model 的核心差别是什么？**

CIA model 让 money 有用，是因为消费品必须用事先持有的 cash 购买；MIU model 让 money 有用，是因为 real balances 直接进入 utility function。前者强调交易约束，后者强调 money 提供的服务流。

**Q2：为什么 MIU model 中 money 有价值？**

因为 household 从 real balances $m_t/P_t$ 中得到 utility。即使 capital 有回报，家庭也愿意持有 money，因为 money 本身提供交易便利、流动性或保险服务。这个服务不是模型推导出来的，而是用 utility term 近似表达。

**Q3：为什么 price level 是 forward-looking？**

money FOC 把今天持有 money 的价值和未来 money 的购买力联系起来。反复向前替代后，当前 price level 取决于 expected future money growth。如果未来 money growth 预期上升，价格会提前反应。

**Q4：什么是 superneutrality？**

在本章语境中，superneutrality 指 money growth rate 的变化不影响长期真实变量。baseline MIU model 中，$\bar g$ 改变 real balances，但不改变 consumption、capital、hours、output、wage 和 rental rate。

**Q5：为什么 $\bar g=\beta$ 时 real balances 会趋于无穷大？**

因为稳态 real balances 满足 $M/P=D\bar g\bar C/(\bar g-\beta)$。当 $\bar g$ 接近 $\beta$ 时，持有 money 的机会成本接近消失，log real balances utility 使 household 想持有非常大的 real balances。这个极端结果依赖本章使用的 separable log specification。

**Q6：money growth shock 为什么不影响真实变量？**

在 baseline MIU log-linear solution 中，money growth shock 只进入 money 和 price dynamics。真实侧的 Euler equation、labor condition、production function 和 resource constraint 没有把 money growth shock 转化为 real allocation 的变化。因此真实变量不响应。

**Q7：seigniorage 为什么可能打破 neutrality？**

因为 seigniorage 不是单纯把新钱转移给家庭，而是政府用新发行 money 购买真实商品。这样 government purchases 进入 aggregate resource constraint。若稳态中已有 positive seigniorage financing，seigniorage shocks 会改变真实资源分配。

**Q8：Figure 9.4 的响应为什么很小但仍重要？**

图 9.4 的纵轴是 $10^{-5}$，说明真实变量对 seigniorage shock 的响应很小。但它不是零。这正是本节的要点：positive seigniorage steady state 下，货币/财政冲击可以通过 government expenditure channel 影响真实变量，哪怕定量幅度很有限。
