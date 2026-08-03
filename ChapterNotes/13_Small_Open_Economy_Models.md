# Chapter 13 — Lecture Note

> Importance: ★★★★☆  
> Suggested audit model: high  
> Reading mode: normal  
> Estimated note reading time: 90–120 minutes  
> Source reliability: text OK；关键图表均已嵌入原文截图；负稳态外债的“对数偏离”与密集矩阵块在 coding 前需特别核对

## 0. How to read this note

第 13 章不是简单地在封闭经济模型后面加一条“净出口恒等式”。它真正处理的是开放经济 DSGE 中一个很基础、也很容易被忽略的技术问题：一旦家庭既可以持有国内资本，又可以持有国外无风险债券，而两种资产在一阶线性模型中提供相同预期回报，模型就无法决定财富究竟应配置到哪种资产。更严重的是，净外国资产没有唯一稳态，经济可能沿资产方向随机游走或爆炸，使围绕某个固定稳态做的 log-linear approximation 失去意义。

本章的逻辑分为四步。第一，建立没有货币的 preliminary small open economy，展示“相同回报的两种资产”如何造成稳态不唯一和投资组合不确定。第二，加入 capital adjustment costs，说明它虽然能区分资本与债券的短期回报，却仍没有真正闭合模型。第三，让外国利率随一国净外国资产变化，用 debt-elastic interest-rate premium 生成唯一稳态和均值回复。第四，在已经闭合的模型中加入国内货币、外国价格、汇率和净出口，研究国内技术、货币与外国价格冲击。

阅读时应把重点放在“为什么需要 closure”以及“closure 改变了哪一条动态方程”，而不是记住每一个 P/Q/R/S 矩阵元素。

## 1. Opening: 本章的核心问题

在封闭经济中，家庭储蓄最终只能转化为国内资本。资本积累由家庭 Euler equation、企业资本边际产出和资源约束共同决定。开放经济加入外国债券以后，家庭可以把储蓄分成国内资本与国外资产。直觉上，这似乎只是增加了一个消费平滑工具；但在线性、无风险的模型里，国内资本和外国债券若具有相同预期回报，家庭对两者没有严格偏好。

于是出现两个问题：

第一，**portfolio indeterminacy**。模型只能决定总财富，却不能决定其中多少是国内资本、多少是外国债券。

第二，**stationary-state indeterminacy**。不同的初始净外国资产位置都可以对应一个稳态；没有一条力量把债券持有拉回某个唯一水平。

而本书采用的求解方法依赖一个明确稳态：先求稳态，再围绕它做一阶近似。如果净外国资产能够持续漂移，局部线性化迟早会离开其有效邻域。因此，“闭合开放经济”不是为了让方程数量看起来相等，而是为了恢复唯一、局部稳定的长期锚。

## 2. Main Lecture

### 2.1 Preliminary model：家庭多了一种国外资产

模型首先考虑没有货币的 small open economy，因此暂时没有汇率。经济中只有一种商品，国内家庭可以持有两类资产：国内实物资本 $k_{t+1}$，以及一期外国无风险债券 $b_t$。本国规模很小，不能影响世界利率，所以把外国 real net interest rate $r^f$ 当作外生常数。

家庭最大化：

$$
E_t\sum_{s=0}^{\infty}\beta^s
\left[\ln c_{t+s}+Bh_{t+s}\right],
$$

其中仍采用 Hansen 的 indivisible labor 与劳动收入保险。家庭预算约束为：

$$
b_t+k_{t+1}+c_t
=w_th_t+r_tk_t+(1-\delta)k_t
+(1+r^f)b_{t-1}+\xi_t.
\tag{13.1}
$$

$b_t>0$ 表示持有外国资产，$b_t<0$ 表示对外负债。因为模型表面上允许家庭不断从国外借新债还旧债，需要额外施加 no-Ponzi/transversality condition：

$$
\lim_{t\to\infty}
\frac{b_t}{(1+r^f)^t}=0.
\tag{13.2}
$$

它排除债务永久按不低于利率的速度滚动，而不要求每一期外国债务都为零。

家庭一阶条件为：

$$
B=-\frac{w_t}{c_t},
\tag{13.3}
$$

$$
\frac1{\beta c_t}
=E_t\frac{1+r^f}{c_{t+1}},
\tag{13.4}
$$

$$
\frac1\beta
=E_t\left[
\frac{c_t}{c_{t+1}}
(r_{t+1}+1-\delta)
\right].
\tag{13.5}
$$

式（13.4）是外国债券 Euler equation，式（13.5）是国内资本 Euler equation。两者共同要求家庭在边际上比较国内资本和外国债券的回报。

### 2.2 企业与要素价格

国内企业仍然完全竞争，技术为：

$$
Y_t=\lambda_tK_t^\theta H_t^{1-\theta}.
$$

因此：

$$
r_t=\theta\lambda_tK_t^{\theta-1}H_t^{1-\theta},
\tag{13.6}
$$

$$
w_t=(1-\theta)\lambda_tK_t^\theta H_t^{-\theta}.
\tag{13.7}
$$

所有家庭相同，所以个体资产和劳动在均衡中聚合为 $B_t,K_t,H_t$。

### 2.3 为什么外国利率必须等于时间偏好决定的回报

稳态消费要求 $C_t=C_{t+1}=\bar C$。把它代入外国债券 Euler equation：

$$
\frac1\beta=1+r^f.
\tag{13.8}
$$

若世界利率高于 $1/\beta-1$，家庭想把消费不断推迟并积累外国资产；若低于该值，家庭倾向持续借债提前消费。只有当：

$$
r^f=\frac1\beta-1
$$

时，常数消费稳态才可能存在。

资本 Euler equation同时给出：

$$
\bar r=\frac1\beta-1+\delta.
\tag{13.9}
$$

因此国内资本净回报与国外债券回报相同。这是资产套利的正常结果，但也正是模型困难的来源。

### 2.4 稳态为什么不是唯一的

稳态预算约束为：

$$
\bar C
=\bar w\bar H+(\bar r-\delta)\bar K+r^f\bar B.
\tag{13.10}
$$

劳动条件、资本 Euler equation和企业 FOC 能够确定 $\bar C,\bar w,\bar r$，但 $\bar B$ 没有被唯一决定。给定任意可行的净外国资产 $\bar B$，资源约束都可以通过调整国内资本、劳动和产出来满足。

换言之，模型不是没有稳态，而是有一整族稳态：

$$
\bar B
\quad\longrightarrow\quad
(\bar K,\bar H,\bar Y).
$$

一个净外国资产更多的国家可以依靠更多外国利息收入，以较少劳动和国内资本维持相同消费；一个负债更多的国家必须生产更多、工作更多，才能支付国外利息。

由于 indivisible labor 对总劳动设置了上限，模型仍然存在最大可持续外债，但这个可行性边界并不等于唯一稳态。只要债务位于边界以内，仍有无穷多个长期位置。

### 2.5 动态模型中的资产配置不确定

对外国债券 Euler equation 做 log-linearization，并使用 $1+r^f=1/\beta$，得到：

$$
\widetilde C_t=E_t\widetilde C_{t+1}.
\tag{13.11}
$$

预期消费近似随机游走。资本 Euler equation则要求国内资本回报与同一消费路径相容。

问题在于，家庭今天增加一单位储蓄时，可以增加 $K_{t+1}$，也可以增加 $B_t$；两者提供相同预期回报。预算约束只约束它们的总和，没有另一条独立条件决定资产组合。因此模型无法分别求出：

$$
\widetilde K_{t+1}
\quad\text{和}\quad
\widetilde B_t.
$$

这不是变量或方程计数失误，而是经济内容上的 indifference：两种无风险资产在一阶模型中完全替代。

### 2.6 加入 capital adjustment costs：解决了一半问题

常见做法是在资本积累中加入调整成本：

$$
\frac\kappa2(k_{t+1}-k_t)^2.
\tag{13.12}
$$

家庭预算变为：

$$
b_t+k_{t+1}
+\frac\kappa2(k_{t+1}-k_t)^2+c_t
=
w_th_t+r_tk_t+(1-\delta)k_t+(1+r^f)b_{t-1}.
\tag{13.13}
$$

调整资本现在需要支付成本，而买卖外国债券不需要，因此资本回报条件与债券回报条件不再完全相同。资本 Euler equation包含：

$$
\beta\kappa\bar K E_t\widetilde K_{t+2}
-(1+\beta)\kappa\bar K\widetilde K_{t+1}
+\kappa\bar K\widetilde K_t.
$$

这使模型能够先求资本动态，再利用预算约束求外国债券动态。

需要注意，调整成本在稳态为零，因为 $K_{t+1}=K_t$；而且它是纯二次项，所以在资源约束的一阶近似中也消失。它虽然不直接消耗一阶资源，却通过资本 FOC 的一阶导数改变动态选择。

### 2.7 为什么 adjustment costs 仍没有真正闭合开放经济

作者尝试寻找：

$$
\widetilde K_{t+1}
=P_{11}\widetilde K_t+Q_1\widetilde\lambda_t,
$$

$$
\widetilde B_t
=P_{21}\widetilde K_t+P_{22}\widetilde B_{t-1}
+Q_2\widetilde\lambda_t.
$$

资本方程给出两个候选根：

$$
P_{11}=1
\qquad\text{或}\qquad
P_{11}=\frac1\beta.
$$

第二个根大于 1，意味着资本爆炸，因此被稳定性条件排除；保留下来的却是：

$$
P_{11}=1,
$$

即资本包含 unit root。外国债券动态则给出：

$$
P_{22}=1+r^f=\frac1\beta>1.
$$

这意味着债券方向是爆炸的，而且政策函数还依赖初始外国债券持有。模型虽然在代数上能写出资本和债券政策函数，却会不断离开最初选择的稳态。既然一阶近似只在稳态邻域内可靠，这种解无法作为可信的局部动态模型。

因此 capital adjustment costs 的作用是：

- 它区分了资本和外国债券的短期调整；
- 但它没有决定长期净外国资产锚；
- 也没有把资产状态拉回唯一稳态。

这就是为什么开放经济文献还需要额外的 closure device。

### 2.8 “Closing the open economy”的准确含义

所谓闭合开放经济，是引入一条经济力量，使模型具有唯一净外国资产稳态，并让偏离该稳态的资产路径具有均值回复。闭合不是让经济停止贸易，也不是强制净出口为零；它只是消除资产方向上的长期漂移。

本章采用一种简单的 country-risk/debt-elastic interest-rate specification：

$$
r_t^f=r^*-aB_t,
\qquad a>0.
\tag{13.14}
$$

按照本章符号，$B_t>0$ 是净外国资产，$B_t<0$ 是外债。因此：

- 若国家增加外债，$B_t$ 更负，$r_t^f$ 上升；
- 若国家积累更多国外资产，$B_t$ 更正，获得的外国回报下降。

这种设定可理解为 country risk：债务越高，国外债权人要求的回报越高。对净储蓄国，它也意味着随着对外资产增加，边际国外资产收益下降。

单个家庭规模为零，把 aggregate $B_t$ 和由此决定的 $r_t^f$ 视为给定，所以家庭优化时没有内化自己对 country premium 的影响。利率函数作为 aggregate equilibrium condition 进入模型，而不是成为单个家庭债券选择的额外导数项。

### 2.9 唯一稳态如何产生

稳态债券 Euler equation要求：

$$
\frac1\beta=1+r^*-a\bar B.
$$

因此：

$$
\boxed{
\bar B=\frac{r^*+1-1/\beta}{a}
}.
\tag{13.15}
$$

净外国资产不再任意，而是恰好调整到使本国面对的外国利率等于国内时间偏好所要求的回报。

当 $a=.01,r^*=.03$ 时，本国是净外国资产持有者：

![Table 13.1 — Stationary state for a net foreign saver](../Figures/Ch13/table_13_1_stationary_state_net_saver.png)

当 $a=.01,r^*=0$ 时，本国是净借款者：

![Table 13.2 — Stationary state for a net foreign borrower](../Figures/Ch13/table_13_2_stationary_state_net_borrower.png)

两种稳态中的消费、工资和资本回报相同，但债务国需要更高的资本、就业和产出，用额外生产支付国外利息。

### 2.10 动态闭合的关键：净外国资产开始影响消费增长

利率函数加入后，债券 Euler equation 的一阶近似变成：

$$
0
=
\widetilde C_t-E_t\widetilde C_{t+1}
-\beta a\bar B\widetilde B_t.
\tag{13.16}
$$

与原来的随机游走条件：

$$
\widetilde C_t=E_t\widetilde C_{t+1}
$$

相比，多出了一项 $\widetilde B_t$。这就是 closure 真正改变模型的地方。

当一国的净外国资产偏离稳态时，它面对的国外利率随之改变，家庭最优消费增长也改变。这个反馈迫使资产位置逐渐回到稳态。作者因此可以把状态、跳跃变量与技术冲击写成：

$$
x_t=[\widetilde K_{t+1},\widetilde B_t]',
$$

$$
y_t=[\widetilde C_t,\widetilde r_t,
\widetilde w_t,\widetilde H_t]',
$$

$$
z_t=[\widetilde\lambda_t]'.
$$

模型重新获得标准 policy functions：

$$
x_{t+1}=Px_t+Qz_t,
\qquad
y_t=Rx_t+Sz_t.
$$

### 2.11 技术冲击：外国资产如何充当 shock absorber

净储蓄国在正向技术冲击后同时增加国内资本与国外资产：

![Figure 13.1 — Technology shock in a net foreign saver](../Figures/Ch13/figure_13_1_technology_irf_net_saver.png)

生产率暂时提高后，家庭不必把全部新增资源立即用于国内消费或资本，可以把一部分存到国外。国外资产因此上升，消费路径更平滑。

净借款国的图形中，标记为 $\widetilde B_t$ 的曲线下降：

![Figure 13.2 — Technology shock in a net foreign borrower](../Figures/Ch13/figure_13_2_technology_irf_net_borrower.png)

这里必须谨慎解释符号。稳态 $\bar B<0$，正向技术冲击使实际 $B_t$ 变得“没那么负”，即国家减少外债、提高净外国资产。作者用 $\widetilde B_t=\log(B_t/\bar B)$ 描述该比例，因此图中的下降对应债务绝对值下降，而不是国家借得更多。

> 💡 Clarification  
> 对负的稳态外债，严格的 $\ln B_t-\ln\bar B$ 并没有定义。原文通过 $\ln(B_t/\bar B)$ 在 $B_t$ 与 $\bar B$ 同号时解释比例变化。实际 coding 时更稳妥的做法是使用 level deviation $B_t-\bar B$、按正量缩放的偏离，或改用正定义的 debt variable $D_t=-B_t$；不要机械地对负数取对数。

无论一国初始是净储蓄者还是净借款者，正向技术冲击都提高其净外国资产：储蓄国增加国外储蓄，借款国偿还部分外债。

作者把开放经济与第 6 章封闭 Hansen economy 并排比较：

![Figure 13.3 — Closed versus open economy after technology shock](../Figures/Ch13/figure_13_3_closed_vs_open_technology_shock.png)

开放经济中，多数国内变量的峰值更小、调整更平缓，因为外国资产吸收了一部分冲击。消费能够在冲击初期更快上升，随后路径更平滑；国内资本和产出不必承受全部储蓄调整。外国资产因此像 shock absorber，但代价是经济暴露于外国利率、价格和资本流动冲击。

### 2.12 加入货币、外国价格与汇率

前面的模型没有货币，所以也没有 exchange rate。第 13.4 节在已经闭合的开放经济中加入：

- 国内货币与 domestic CIA constraint；
- 外国货币计价的债券；
- 外国价格水平 $P_t^*$；
- 名义汇率 $e_t$；
- 净出口 $X_t$；
- 国内货币增长、国内技术和外国价格三类冲击。

汇率定义为每单位外国货币需要多少国内货币。模型采用 purchasing power parity：

$$
e_t=\frac{P_t}{P_t^*}.
\tag{13.17}
$$

这是一种非常简化的汇率决定方式，不包含 sticky prices、home bias 或 incomplete pass-through。

### 2.13 国际收支与外国利率

外国债券用外国货币计价。国际资产变化与净出口满足 balance-of-payments condition：

$$
B_t-(1+r_{t-1}^f)B_{t-1}=P_t^*X_t.
\tag{13.18}
$$

如果本期净出口为正，国家积累更多外国资产；如果贸易逆差，就必须减少外国资产或增加外债。

外国利率取决于按外国商品计价的净外国资产：

$$
r_t^f
=r^*-a\frac{B_t}{P_t^*}.
\tag{13.19}
$$

外国价格本身服从外生随机过程。由于 $B_t$ 是名义外国债券，除以 $P_t^*$ 才得到 real foreign-asset position。

### 2.14 家庭、企业与资源约束

家庭仍受国内 CIA constraint：

$$
P_tC_t=M_{t-1}+(g_t-1)M_{t-1}=g_tM_{t-1}.
\tag{13.20}
$$

家庭预算包含国内货币、国内资本、以汇率换算的外国债券及其收益，并保留 capital adjustment costs。

企业生产结构仍是：

$$
Y_t=\lambda_tK_t^\theta H_t^{1-\theta}.
$$

开放经济资源约束为：

$$
Y_t
=C_t+K_{t+1}-(1-\delta)K_t+X_t.
\tag{13.21}
$$

这里 $X_t>0$ 表示部分国内产出没有被本国消费或投资，而是用于净出口并积累国外资产。

### 2.15 带货币开放经济的稳态

稳态资本回报和外国回报仍满足：

$$
\bar r=\frac1\beta-1+\delta,
$$

$$
\bar r^f=\frac1\beta-1.
$$

因此 closure condition 再次给出：

$$
\bar B=\frac{r^*+1-1/\beta}{a}.
$$

国际收支稳态要求：

$$
\bar X=-\bar r^f\bar B.
\tag{13.22}
$$

净储蓄国通过国外利息收入可以维持贸易逆差，所以 $\bar B>0$ 时 $\bar X<0$；净债务国需要贸易顺差支付利息，所以 $\bar B<0$ 时 $\bar X>0$。

CIA 与家庭劳动条件给出：

$$
\bar C=\frac{\beta\bar w}{-B\bar\pi},
\qquad
\bar\pi=\bar g.
\tag{13.23}
$$

更高趋势货币增长在这里具有第 8 章家庭转移型 CIA model 的性质：稳态消费和产出下降。净外国资产位置不改变稳态消费，却会改变国内资本、劳动、产出与净出口，因为债务国必须生产更多来偿还国外利息。

![Table 13.3 — Stationary states for the open economy with money](../Figures/Ch13/table_13_3_open_economy_money_stationary_states.png)

Table 13.3 同时比较净储蓄国/净债务国以及零通胀/高通胀稳态，清楚展示了这两个维度的作用：趋势通胀压低消费与生产；外债则提高为偿债所需的资本、就业、产出和贸易顺差。

### 2.16 为什么模型再次出现 $t+2$，又如何降回 $t+1$

带货币的外国债券 Euler equation和资本 Euler equation含有：

$$
E_t\widetilde P_{t+2}
+E_t\widetilde C_{t+2}.
$$

本书的求解方法只允许一期领先变量，因此需要利用模型中另一条恒等关系降阶。CIA 的 log-linear form 是：

$$
\widetilde P_t+\widetilde C_t=\widetilde M_t,
\tag{13.24}
$$

货币运动方程为：

$$
\widetilde M_t=\widetilde g_t+\widetilde M_{t-1}.
\tag{13.25}
$$

因此：

$$
E_t(\widetilde P_{t+2}+\widetilde C_{t+2})
=E_t\widetilde M_{t+2}
=E_t\widetilde g_{t+2}+E_t\widetilde M_{t+1}.
$$

若货币增长服从 AR(1)：

$$
\widetilde g_{t+2}
=\gamma_g\widetilde g_{t+1}+\varepsilon_{t+2}^g,
$$

且 $E_t\varepsilon_{t+2}^g=0$，则：

$$
E_t(\widetilde P_{t+2}+\widetilde C_{t+2})
=
\gamma_gE_t\widetilde g_{t+1}
+E_t\widetilde M_{t+1}.
\tag{13.26}
$$

这不是把方程机械地整体平移一期，而是两步：先用 CIA 做严格代数代换，再用外生 AR(1) 过程在条件期望下替换未来创新。它依赖本模型中特定的恒等式，并非任何 $t+2$ 变量都能这样消去。

### 2.17 状态变量与 price column 为零

作者选择：

$$
x_t=[\widetilde K_{t+1},\widetilde M_t,
\widetilde P_t,\widetilde B_t,\widetilde r_t^f]',
$$

$$
y_t=[\widetilde C_t,\widetilde r_t,
\widetilde w_t,\widetilde H_t,
\widetilde e_t,\widetilde X_t]',
$$

$$
z_t=[\widetilde\lambda_t,
\widetilde g_t,\widetilde P_t^*]'.
$$

求解后的政策矩阵中，price column 为零，说明 $P_t$ 虽然最初被放入 state vector，却不提供额外的预测信息。价格由当前 money、consumption 和 foreign price 等变量当期决定，不是独立的 predetermined state。

原文还指出，money state 本身只直接影响 money、domestic price 和 exchange rate；这不等于 money-growth shock 对真实变量完全中性。冲击会同时改变家庭 CIA 与预期路径，从而通过一般均衡使消费、劳动和资产配置响应。这里要区分“政策矩阵中某一状态列的直接系数”与“外生货币冲击的完整 IRF”。

> ⚠️【需要回原文看图】本节 A–N 矩阵和 P/Q/R/S 数值矩阵非常密集，且 net exports 的对数系数因其稳态水平较小而数值很大。理解时应关注变量顺序和经济结构；coding 时再回原文逐项核对。

### 2.18 技术冲击：货币存在后的开放经济

净储蓄国的技术冲击 IRF 为：

![Figure 13.4 — Technology shock with money, net foreign saver](../Figures/Ch13/figure_13_4_money_open_economy_technology_net_saver.png)

与没有货币的 Figure 13.1 相比，资本响应更慢、更平滑，外国债券调整更快；其他真实变量整体相近。国内价格和汇率因 PPP 同向变化。

净借款国的结果为：

![Figure 13.5 — Technology shock with money, net foreign borrower](../Figures/Ch13/figure_13_5_money_open_economy_technology_net_borrower.png)

总体机制仍然相同：正向技术冲击提高净外国资产。净债务国表现为减少外债。图中外国利率和债券响应重合，是 $r^*=0$ 这一特定校准下的数量结果，不是一般恒等关系。

### 2.19 国内货币冲击

净储蓄国的货币冲击：

![Figure 13.6 — Monetary shock, net foreign saver](../Figures/Ch13/figure_13_6_monetary_shock_net_saver.png)

净借款国的货币冲击：

![Figure 13.7 — Monetary shock, net foreign borrower](../Figures/Ch13/figure_13_7_monetary_shock_net_borrower.png)

作者在图中省略了 money、domestic price 和 exchange rate，因为它们都向同一个正的新水平收敛，且价格与汇率比货币更快接近长期水平。图中消费在冲击后明显下降，反映家庭端 monetary transfer/CIA 结构的通胀税性质。净外国资产和外国利率的响应取决于国家在稳态是债权人还是债务人，但两种经济中的国内消费和劳动都会通过国际资产市场重新配置。

### 2.20 外国价格冲击

外国价格冲击下，净储蓄国的响应为：

![Figure 13.8 — Foreign price shock, net foreign saver](../Figures/Ch13/figure_13_8_foreign_price_shock_net_saver.png)

净债务国的响应为：

![Figure 13.9 — Foreign price shock, net foreign borrower](../Figures/Ch13/figure_13_9_foreign_price_shock_net_borrower.png)

外国价格通过三条关系进入本国：PPP 决定汇率；外国债券的 real value 是 $B_t/P_t^*$；balance of payments 用外国价格给净出口计价。因此即使国内技术和货币没有变化，外国价格仍会改变汇率、净外国资产的真实价值、country premium 和国内消费配置。

冲击衰减较快，但净储蓄国和净债务国的资产、利率反应方向和幅度明显不同。开放经济的好处是能够通过国际资产平滑国内冲击，风险则是本国暴露于外部价格和资本流动变化。

### 2.21 本章 closure 的地位与边界

本章使用的 debt-elastic interest-rate premium 是一种方便的 closure，不是唯一正确结构。它通过一个小参数 $a$ 在净外国资产偏离稳态时改变世界融资条件，从而人为地加入均值回复。

这种做法适合局部一阶 DSGE，因为它简单、容易求稳态，也保留小国对基准世界利率没有影响的近似。但它没有从国外债权人的最优化、违约风险或主权风险中微观推导 country premium。其他闭合方法还可以包括债券持有成本、内生贴现因子、portfolio adjustment costs 或其他资产市场摩擦。

本章最后强调，开放经济能够提高消费平滑能力，但也使一国更容易受到 foreign price shocks 和 international capital-flow shocks。现实中的 sudden stop 往往比本章线性、无违约模型更剧烈；本章提供的是最基础的资产闭合框架，而不是完整的新兴经济体危机模型。

## 3. Compact Summary: What You Must Retain

- 加入外国无风险债券后，家庭同时持有国内资本和外国资产；若二者预期回报相同，一阶模型无法决定资产组合。
- 基础模型有无穷多个净外国资产稳态。不同 $\bar B$ 对应不同的国内资本、劳动和产出，因此没有唯一线性化中心。
- Capital adjustment costs 能区分资本和债券的短期动态，却仍留下资本 unit root 和债券爆炸根，不能真正阻止经济漂离初始稳态。
- 本章用 $r_t^f=r^*-aB_t$ 闭合模型，使净外国资产改变本国面对的外国利率，并唯一确定 $\bar B$。
- Closure 的关键动态表现是债券 Euler equation 中出现 $\widetilde B_t$，从而给消费增长和资产路径加入均值回复。
- 国际资产像 shock absorber：国内技术冲击后，一部分资源通过国外储蓄或偿债吸收，使国内资本与产出的响应更平滑。
- 带货币模型加入 PPP 汇率、国际收支、外国价格和国内 CIA；高阶 $t+2$ 项可借 CIA 与 money-growth law 在条件期望下降阶。
- 开放经济提高消费平滑能力，同时暴露于外国价格和资本流动冲击；debt-elastic premium 只是众多 closure devices 之一。

## 4. Figures, Tables, and Formulas to Check in the Original

本章重要图表已作为原文截图嵌入 `Figures/Ch13/`：

- Tables 13.1–13.2：净储蓄国和净借款国的唯一稳态。
- Figures 13.1–13.2：两类国家对技术冲击的响应。
- Figure 13.3：封闭经济和开放经济的技术冲击对照。
- Table 13.3：带货币开放经济在不同外债和趋势通胀下的稳态。
- Figures 13.4–13.5：带货币模型中的技术冲击。
- Figures 13.6–13.7：国内货币冲击。
- Figures 13.8–13.9：外国价格冲击。

必须掌握的公式包括：

$$
\frac1\beta=1+r^f,
$$

$$
r_t^f=r^*-aB_t,
$$

$$
\bar B=\frac{r^*+1-1/\beta}{a},
$$

$$
0=\widetilde C_t-E_t\widetilde C_{t+1}
-\beta a\bar B\widetilde B_t,
$$

$$
B_t-(1+r_{t-1}^f)B_{t-1}=P_t^*X_t,
$$

$$
e_t=\frac{P_t}{P_t^*}.
$$

> ⚠️【需要回原文看图】资本调整成本部分的高阶 lead 推导、政策根筛选、完整 A–N 矩阵以及负稳态债券变量的符号解释，PDF 排版密集。coding 前需回原文核对，并避免对负债水平直接做普通 log transformation。

## 5. Questions and Answers

**Q1：为什么增加一种外国资产会破坏模型，而不是只让家庭多一个选择？**  
因为在线性无风险模型中，国内资本和外国债券若提供相同预期回报，家庭对两种资产无差异。预算约束只能决定总储蓄，不能决定资本和债券各自数量。

**Q2：为什么世界利率必须满足 $1+r^f=1/\beta$？**  
只有这样，常数消费才满足外国债券 Euler equation。若世界利率过高或过低，家庭会持续把消费向未来或现在移动，无法形成常数消费稳态。

**Q3：有很多稳态为什么会妨碍 log-linearization？**  
线性化需要选定一个局部中心。若净外国资产没有回归力量，经济会沿稳态族漂移并离开该中心，局部一阶近似不再可靠。

**Q4：capital adjustment costs 已经改变了资本回报，为什么仍不能闭合？**  
它能分离资本和债券的短期政策函数，但没有确定长期净外国资产锚。保留解中资本有 unit root，外国债券方向仍是爆炸的。

**Q5：debt-elastic interest rate 如何恢复唯一稳态？**  
净外国资产偏离会改变国家面对的国外利率。稳态必须让该利率恰好等于 $1/\beta-1$，从而唯一确定 $\bar B$；动态上利率反馈使资产路径均值回复。

**Q6：为什么正向技术冲击对净债务国也意味着“国际储蓄增加”？**  
净债务国的 $B<0$。技术冲击后它偿还部分外债，使 $B$ 上升、变得没那么负；这就是净外国资产增加。

**Q7：开放经济为什么能平滑国内技术冲击？**  
家庭不必把全部新增资源立即转化为国内资本或消费，可以增加国外资产或偿还外债。外国资产吸收了一部分冲击，减小国内变量的峰值。

**Q8：为什么 $t+2$ 项在带货币模型里能够消去？**  
因为它们总以 $P_{t+2}+C_{t+2}$ 的组合出现；CIA 把该组合等同于 money，money law 再把两期后的 money 写成一期后 money 与可预测货币增长的函数。这是模型特定关系，不是普遍技巧。

**Q9：PPP 在本章中起什么作用？**  
它直接规定名义汇率等于国内外价格之比，使外国价格冲击立即传到汇率。它提供闭合汇率的简单方式，但排除了偏离 PPP、粘性价格和不完全传递。

**Q10：debt-elastic premium 是不是对 country risk 的完整微观解释？**  
不是。它是 reduced-form closure，用来生成唯一稳态与资产均值回复。它没有显式建模主权违约、债权人损失或风险定价。
