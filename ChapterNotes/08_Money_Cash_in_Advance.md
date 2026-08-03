# Chapter 8 — Lecture Note

> Importance: ★★★★★  
> Suggested audit model: xhigh  
> Reading mode: careful  
> Estimated note reading time: 110-145 minutes  
> Source reliability: text OK; major figures/tables embedded as source screenshots; long LQ/log-linear matrix formulas and appendix matrix equations should be checked against the original before coding

## 0. How to read this note

这一章开始把 money 放进 RBC framework。前面几章的 RBC 模型基本是 real model：技术、资本、劳动和消费决定真实经济波动，货币不发挥实质作用。第 8 章讨论 Cooley and Hansen 的 cash-in-advance model，核心问题是：如果家庭必须提前持有货币才能购买消费品，那么货币增长、通货膨胀和真实经济活动之间会出现怎样的联系？

读这一章时建议抓住三条线。

第一，**模型结构线**：cash-in-advance constraint 让 money 成为购买消费品的必要条件。家庭进入当期时持有上一期带来的钱，再加上政府货币转移，然后才能购买消费品。投资品则可以用当期收入购买。因此，货币约束主要扭曲 consumption-leisure / labor decision，而不是直接约束资本品购买。

第二，**均衡求解线**：加入 money 后，模型不再能完全依赖 Robinson Crusoe planner shortcut。原因是价格、工资、租金、货币供给和个体决策之间存在市场均衡关系。作者因此需要写出家庭问题、企业定价、cash-in-advance constraint、money growth process 和 aggregation conditions。

第三，**经济结论线**：通胀在这里像一种消费税或 cash tax。更高的货币增长提高持有货币的机会成本，降低真实余额和经济活动；而用 seigniorage 购买政府支出时，通胀税还会带来 Bailey curve，也就是通胀与铸币税收入之间的非线性关系。

## 1. Opening: 本章的核心问题

前面的 Hansen RBC 模型已经能够通过技术冲击生成 output、investment、hours 和 consumption 的商业周期波动。但它没有 money，也无法讨论通货膨胀、货币增长、价格水平和铸币税。

Cooley and Hansen 的思路是在 Hansen indivisible labor model 上加入一个简单但有力的货币摩擦：**consumption goods 必须用事先持有的 cash 购买。** 这就是 cash-in-advance constraint。货币本身不进入效用函数，也不提高生产率，但它通过交易约束影响消费和劳动选择。

本章要回答的问题是：

1. cash-in-advance constraint 如何改变 RBC 模型的家庭问题和均衡条件？
2. 稳态下，货币增长率和通胀如何影响 output、consumption、investment、capital 和 hours？
3. 技术冲击和货币增长冲击分别会产生怎样的 impulse responses？
4. 如果政府用印钞收入购买商品，而不是把新货币 lump-sum transfer 给家庭，会出现怎样的 seigniorage 机制？

## 2. Main Lecture

### 2.1 Cash-in-advance 的直觉：为什么 money 会影响 real allocation？

在没有货币摩擦的 RBC 模型中，money 通常是 neutral 的。家庭真正关心的是消费、闲暇和资本积累；如果所有价格同比例变化，真实资源配置不变。

cash-in-advance model 改变了这一点。家庭购买消费品时，不能只凭未来收入或当期生产收入，而必须使用进入当期时已经持有的 money。书中的叙事可以理解为一个家庭里有 shopper 和 worker：shopper 拿着上一期带回家的钱去市场购买消费品；worker 当期工作并出售产品，换回的钱要到下一期才能用于消费。

这个时间顺序让货币具有真实效应。更高的货币增长通常意味着更高通胀，而更高通胀降低持有货币的真实回报。因为消费必须用 cash 买，家庭会减少受现金约束影响的消费与相关劳动供给，真实经济变量也会受到影响。

### 2.2 Cooley and Hansen model：家庭、企业与货币过程

模型中有连续统的相同家庭，质量为 1。每个家庭把价格、工资、租金和 aggregate variables 视为给定；在 symmetric equilibrium 中，个体选择与 aggregate variables 一致。

偏好延续 Hansen 的 indivisible labor structure。家庭效用可以写成：

$$
\sum_{t=0}^{\infty}\beta^t\left[\ln c_t^i+B h_t^i\right],
$$

其中 $B=A\ln(1-h_0)/h_0<0$。这里 $h_t^i$ 可以理解为 indivisible labor lottery 后的 expected hours 或 employment margin。

企业使用 Cobb-Douglas 技术：

$$
y_t=\lambda_t K_t^\theta H_t^{1-\theta}.
$$

在竞争性要素市场中，工资和资本租金等于边际产品：

$$
w_t=(1-\theta)\lambda_t\left(\frac{K_t}{H_t}\right)^\theta,
$$

$$
r_t=\theta\lambda_t\left(\frac{K_t}{H_t}\right)^{\theta-1}.
$$

技术冲击通常写成：

$$
\ln \lambda_{t+1}=\gamma\ln \lambda_t+\varepsilon_{t+1}^\lambda.
$$

货币供给按增长率 $g_t$ 增长。书中先讨论一种简单情形：新发行货币以 lump-sum transfer 的方式给家庭。若 $M_t=g_tM_{t-1}$，家庭在期初获得 transfer：

$$
(g_t-1)M_{t-1}.
$$

为了让 cash-in-advance constraint 绑定，通常需要货币增长率不低于家庭贴现因子所隐含的持币回报条件。直观地说，如果货币增长太低、货币回报太高，家庭可能愿意持有超过当期消费所需的 cash，CIA 约束就未必 bound。

### 2.3 家庭约束：CIA constraint 与 budget constraint

家庭进入时期 $t$ 时，持有上一期留下来的 money $m_{t-1}^i$，并收到政府转移 $(g_t-1)M_{t-1}$。消费品必须用这些 cash 购买：

$$
p_t c_t^i\leq m_{t-1}^i+(g_t-1)M_{t-1}.
$$

在约束绑定时，就是等号。

家庭的 flow budget constraint 是：

$$
c_t^i+k_{t+1}^i+\frac{m_t^i}{p_t}
=w_t h_t^i+r_t k_t^i+(1-\delta)k_t^i+
\frac{m_{t-1}^i+(g_t-1)M_{t-1}}{p_t}.
$$

左边是消费、下一期资本和带到下期的 real money balances；右边是工资收入、资本收入、未折旧资本和期初可用现金的真实价值。

由于 money supply 和 price level 都可能随时间增长，直接用 nominal money 写模型会有非平稳问题。作者因此把变量除以 aggregate money stock $M_t$。定义：

$$
\hat p_t=\frac{p_t}{M_t},\quad \hat m_t^i=\frac{m_t^i}{M_t}.
$$

标准化后，aggregate money stock 恒等于 1，模型可以围绕 stationary state 求解。标准化后的 CIA constraint 可以写成：

$$
\hat p_t c_t^i=\frac{\hat m_{t-1}^i+(g_t-1)}{g_t}.
$$

这一步的直觉是：与其同时追踪不断增长的 $M_t$ 和 $p_t$，不如追踪每单位货币供给对应的价格 $\hat p_t$ 和家庭持有的相对货币份额 $\hat m_t^i$。

### 2.4 Stationary state：货币增长如何改变真实经济变量？

在查看下面的 FOC 之前，可以先把本节使用的模型设置集中写在这里，方便就地核对。

**家庭问题：**

$$
\max_{\{c_t^i,h_t^i,k_{t+1}^i,\hat m_t^i\}_{t=0}^{\infty}}
E_0\sum_{t=0}^{\infty}\beta^t
\left[\ln c_t^i+B h_t^i\right],
\qquad
B=\frac{A\ln(1-h_0)}{h_0}<0,
$$

subject to 标准化后的 cash-in-advance constraint：

$$
\hat p_t c_t^i
=
\frac{\hat m_{t-1}^i+(g_t-1)}{g_t},
$$

以及 flow budget constraint：

$$
c_t^i+k_{t+1}^i+\frac{\hat m_t^i}{\hat p_t}
=
w_t h_t^i+r_t k_t^i+(1-\delta)k_t^i
+
\frac{\hat m_{t-1}^i+(g_t-1)}{g_t\hat p_t}.
$$

这里使用 CIA 约束绑定的情形；$\hat p_t=p_t/M_t$、$\hat m_t^i=m_t^i/M_t$，且 $M_t=g_tM_{t-1}$。

**竞争厂商问题：**

$$
\max_{K_t,H_t}
\left\{
\lambda_tK_t^\theta H_t^{1-\theta}
-w_tH_t-r_tK_t
\right\}.
$$

因此厂商的一阶条件为：

$$
w_t=(1-\theta)\lambda_t
\left(\frac{K_t}{H_t}\right)^\theta,
\qquad
r_t=\theta\lambda_t
\left(\frac{K_t}{H_t}\right)^{\theta-1}.
$$

在 symmetric equilibrium 中还要求：

$$
c_t^i=C_t,\qquad
h_t^i=H_t,\qquad
k_t^i=K_t,\qquad
\hat m_t^i=1.
$$

在 symmetric stationary equilibrium 中，个体变量等于 aggregate variables，且 $\lambda=1$、$g_t=\bar g$。模型的一阶条件和市场出清条件可以整理为一组稳态方程。

> ### FOC 的思路
>
> 下面用 $\mu_t$ 表示 flow budget constraint 的乘子；技术状态继续写成 $\lambda_t$，避免同一个符号承担两个含义。这里采用“乘子不包含 $\beta^t$”的记号 convention。
>
> 1. 劳动力 ht
>     - marginal gain：$w_t\mu_t$（工资收入按当期资源影子价值计价）
>     - marginal loss：$-\beta^tB$（因为 $B<0$）
>     - 均衡：$w_t\mu_t+\beta^tB=0$；
> 2. 资本 $k_{t+1}$
>     - marginal gain：$E_t[\mu_{t+1}(r_{t+1}+1-\delta)]$（增加下一期可用资源的影子收益）
>     - marginal loss：$\mu_t$（占用当期一单位资源）
>     - 均衡：$\mu_t=E_t[\mu_{t+1}(r_{t+1}+1-\delta)]$；
> 3. 货币 $\hat{m}_t$（这里直接通过约束式，用 mt 替换掉 ct，这样更加简洁）
>     - marginal gain：$\beta^{t+1}E_t[1/(c_{t+1}g_{t+1}\hat p_{t+1})]$；
>     - marginal cost：$\mu_t/\hat p_t$；
>     - 均衡：gain = cost
> 4. 再代入均衡状态，没有冲击、工资，利率稳定、\hat{m}，\hat{p} 也稳定，就能得到下面的 “核心稳态关系”；

核心稳态关系包括：

$$
\frac{1}{\beta}=(1-\delta)+\bar r,
$$

$$
\frac{B}{\bar w}=-\frac{\beta}{\bar g\bar C},
$$

$$
\bar{\hat p}\bar C=1,
$$

以及企业边际产品条件。由这些条件可以解出：

$$
\bar r=\frac{1}{\beta}-(1-\delta),
$$

$$
\bar C=-\frac{\beta\bar w}{\bar g B},
$$

$$
\bar{\hat p}=\frac{1}{\bar C}.
$$

由于 $B<0$，消费为正。这里最重要的是 $\bar C$ 与 $\bar g$ 的关系：货币增长率越高，稳态消费越低。因为更高的 money growth 对应更高 inflation tax，持有 cash 的成本上升，而 cash 又是消费的必要条件。

书中给出了不同 $\bar g$ 下的 stationary state：

![Table 8.1 — Stationary state as a function of money growth](../Figures/Ch08/table_8_1_stationary_state_g.png)

表 8.1 可以这样读：$\bar r$ 和 $\bar w$ 不随 $\bar g$ 变化，但 consumption、capital、hours 和 output 都大体随 $1/\bar g$ 下降。这反映了 CIA friction 下 inflation tax 对真实经济活动的收缩作用。

Cooley and Hansen 进一步把不同年化通胀率对应的稳态结果列成表：

![Table 8.2 — Cooley-Hansen steady states under different inflation rates](../Figures/Ch08/table_8_2_cooley_hansen.png)

表 8.2 的主线非常明确：通胀越高，output、consumption、investment、capital 和 hours 越低，welfare loss 越大。这个结果不是因为货币直接进入效用函数，而是因为 cash-in-advance constraint 让通胀变成了对消费交易的扭曲税。

> #### 注释：state、control 应当怎样区分？ market Price 应当怎样对待？
>
> 对一个模型，一般我们的思想都是列出 FOC、再加上资源约束方程，得到最优行为/政策下的递推方程，因此我们需要知道 (1).“如何判断变量是否应该归类为 state variable、control variable”、(2).“政策函数应该如何假设？control var = g(...)，g 函数里面是否应该包含 market price 变量？”
>
> 判断 state variable 的关键不是它写在等式哪一边，而是**<u>家庭进入时期 $t$、开始作当期决策时，它是否已经确定</u>**。对本章家庭而言，$k_t^i$ 和 $\hat m_{t-1}^i$ 是由过去带入当期的 endogenous states；当期已经实现的 $\lambda_t$、$g_t$ 则是 exogenous states。总体资本 $K_t$ 在时期 $t$ 也已经由过去决定，但它不是单个家庭自己的 state/control；家庭只是把它当作给定的 aggregate environment，最终再由 aggregation consistency 确定。
>
> 原始家庭问题中的当期 choices 包括：
>
> $$
> c_t^i,\quad h_t^i,\quad k_{t+1}^i,\quad \hat m_t^i.
> $$
>
> 其中 $k_{t+1}^i$ 和 $\hat m_t^i$ 是时期 $t$ 的 controls，但会分别成为下一期的 $k_{t+1}^i$ 和期初货币状态。约束方程不会把这些选择变量简单地“取消”，而是减少独立自由度。利用绑定的 CIA constraint 和 flow budget constraint 消元以后，**<u>可以选取不同的独立控制变量</u>**。本书的 LQ 表示选择：
>
> $$
> y_t^i=
> \begin{bmatrix}
> k_{t+1}^i\\
> \hat m_t^i
> \end{bmatrix},
> $$
>
> 再由约束恢复 $c_t^i$ 和 $h_t^i$。这只是对同一个家庭选择问题采用了更方便的参数化。（其实也可以选 c、去掉 m...反正这个不是那么严格的，只要注意好有哪些是 “具备自由度” 的即可）
>
> $w_t,r_t,\hat p_t$ 则是 market variables，而不是单个家庭的 controls。推导家庭 FOC 时，家庭把这些价格视为给定；一旦 FOC 按照这种 “视价格给定” 的方式推导出来之后，这个结构特征已经被保留下来了。随后把家庭 FOC、厂商 FOC、市场出清和 symmetric equilibrium conditions 收拢起来，可以利用
>
> $$
> w_t=W(K_t,H_t,\lambda_t),\qquad
> r_t=R(K_t,H_t,\lambda_t),\qquad
> \hat p_tC_t=1
> $$
>
> 消去市场价格（本质上市场价格就是引入了新变量 “价格”、以及一个均衡方程，因此没有任何自由度的），我们完全可以消元消去 “市场价格”，这里没有重新改变家庭的最优化问题，只是在对已经得到的均衡方程组作代数上的简化。因此在最终简化的递推系统中，市场变量确实存在，但是本质上它不是 control var、也不是 state var，它是可以被替换掉的符号，被替换掉以后，递推公式里面就只剩下了 Kt, Ht, λt。
>
> 而对于 K、H 本质也是一样，这个新符号的引入其实也伴随着一个约束方程 K = n\*k，因此自由度还是没变；
>
> - 关于递推系统我们只需要知道一件事，我们只在乎自由度，至于这个自由度赋予给哪个变量是无所谓的（主要看怎么方便怎么来），其他的符号虽然有，但是它们并没有自由度、它们只是 “方便形式” 的符号助记。递推推的是具有自由度的变量。
>
> - 关于政策函数，政策函数的自变量的选取主要依赖的是马尔科夫性，当前状态下有多少是不可变的固定变量？

### 2.5 LQ solution：为什么有 money 后问题更复杂？

这一节先不追随书中同时保留个体变量与总量变量的矩阵记号，而是按照“先把均衡方程列齐，再逐步消元”的思路重新组织。目标是弄清楚：最后究竟需要递推哪些变量，均衡价格又是怎样被确定的。

#### 2.5.1 第一步：家庭问题从四个 choices 降到两个独立 controls

家庭原始的当期 choices 是：

$$
c_t^i,\qquad h_t^i,\qquad k_{t+1}^i,\qquad m_t^i.
$$

先暂时使用未标准化的 nominal money 和 price level，这样最简单；

> 其实也可以直接开始用 mt/Mt，因为毕竟如果在增长模型中，二者都是不断增加的，我们需要一个“不变量”的稳态点，才能够在这一点上进行线性近似；

令政府在期初给家庭 $i$ 的货币转移为 $T_t^i$。书中的 unit-mass economy 对应：

$$
T_t^i=(g_t-1)M_{t-1}.
$$

绑定的 CIA constraint 是：

$$
\boxed{
p_tc_t^i=m_{t-1}^i+T_t^i.
}
\tag{8.2.1}
$$

因此：

$$
\boxed{
c_t^i=\frac{m_{t-1}^i+T_t^i}{p_t}.
}
\tag{8.2.2}
$$

家庭的 flow budget constraint 为：

$$
c_t^i+k_{t+1}^i+\frac{m_t^i}{p_t}
=
w_th_t^i+(r_t+1-\delta)k_t^i
+\frac{m_{t-1}^i+T_t^i}{p_t}.
\tag{8.2.3}
$$

利用 CIA constraint，式（8.2.3）两边最后的真实现金购买力正好等于 $c_t^i$，所以消费可以约掉：

$$
\boxed{
k_{t+1}^i+\frac{m_t^i}{p_t}
=
w_th_t^i+(r_t+1-\delta)k_t^i.
}
\tag{8.2.4}
$$

> 意思是通过两个约束方程，将一开始的家庭决策的 choice 变量从 4 个缩减为 2 个；

现在可以选择：
$$
\boxed{
k_{t+1}^i,\qquad m_t^i
}
$$

作为两个独立 controls，再由两个约束恢复：

$$
c_t^i
=
\frac{m_{t-1}^i+T_t^i}{p_t},
\tag{8.2.5}
$$

$$
h_t^i
=
\frac{
k_{t+1}^i+m_t^i/p_t-(r_t+1-\delta)k_t^i
}{w_t}.
\tag{8.2.6}
$$

所以这里并不是说 $c_t^i,h_t^i$ 不再是经济变量，而是说它们不再需要被当作独立自由度。

> 截此位置，对于家庭问题而言，它们把市场价格 p、r、w 都当成给定的市场环境，而不是家庭自己的 state variables。因此如果把这些价格当作给定，那么仅仅针对家庭问题而言，如果我们列出 FOC + 约束方程（如果消元了，那么那个约束方程就相当于用完了这里就不需要再加了），整个方程系统可以看作是：我们得到了一个关于 $(k_{t+1},m_t)$ 的条件选择关系（c、h 能够从约束方程中恢复，因此这里不需要单独保留它们的自由度）
>
> $(k_{t+1},m_t)=g(k_t,m_{t-1},λ_t,g_t,p_t,r_t,w_t)$；
>
> 这其实就类似于我们之前的简化模型中的求解：单纯的家庭问题中，p、r、w 都是给定的 market inputs；
>
> 但是对于整个经济体统而言，任务还没有完成，我们如果要得到整个经济系统的内生变量的递推结构，还需要进一步消除这些家庭问题中的这些内生变量（例如 p、r、w），这样才能变成 “整体经济系统内的内生递推”；

#### 2.5.2 第二步：用厂商最优条件消去 \(w_t,r_t\)

这一步的顺序非常重要。

家庭先在给定：

$$
p_t,\qquad w_t,\qquad r_t
$$

以及给定整体经济环境和对未来市场变量的预期时，完成自己的最优化。也就是说，家庭的 FOC 或 LQ 选择关系必须先按 price-taking 方式推导出来：

$$
\boxed{
\begin{bmatrix}
k_{t+1}^i\\
m_t^{i,d}
\end{bmatrix}
=
g^i\left(
k_t^i,m_{t-1}^i,\lambda_t,g_t;
p_t,w_t,r_t,\text{expected future market variables}
\right).
}
\tag{8.2.7}
$$

这里的 $p_t,w_t,r_t$ 是家庭视为给定的市场价格，而不是家庭自己的 state variables。式（8.2.7）只是在说：给定这些市场条件，家庭会怎样选择两个 controls。

**只有在这条家庭最优关系已经形成以后**，我们才把它与厂商 FOC、市场出清和 aggregation conditions 收拢成完整均衡方程组，再做第二轮代数消元。

竞争厂商满足：

$$
w_t=(1-\theta)\lambda_t
\left(\frac{K_t}{H_t}\right)^\theta,
\tag{8.2.8}
$$

$$
r_t=\theta\lambda_t
\left(\frac{K_t}{H_t}\right)^{\theta-1}.
\tag{8.2.9}
$$

所以，在完整均衡方程组中，$w_t,r_t$ 可以由厂商条件替换掉。这个替换发生在家庭 FOC 已经推导完以后，因此不会让家庭错误地认为自己的个体选择会改变市场工资或租金【**<u>不会被偷换成planner problem</u>**】。

#### 2.5.3 第三步：在完整均衡方程组中消去总量记号

接下来才使用同质家庭和 symmetric equilibrium。若有 $n$ 个相同家庭：

$$
K_t=nk_t,\qquad
H_t=nh_t,\qquad
K_{t+1}=nk_{t+1}.
\tag{8.2.10}
$$

本书把家庭总质量标准化为 1，因此在最终对称均衡方程组中可以写成：

$$
K_t=k_t,\qquad
H_t=h_t,\qquad
K_{t+1}=k_{t+1}.
\tag{8.2.11}
$$

这里必须强调两件事。

第一，式（8.2.11）是在家庭 price-taking FOC 或家庭 LQ 选择关系已经推导完成以后，才用于简化整个均衡方程组。不能先把 $K_t=k_t^i,H_t=h_t^i$ 塞进单个家庭目标函数，再对这个目标重新求导；那会让家庭错误地 internalize aggregate production effects。【**<u>一样的意思，就是说不能在家庭求 FOC 之前先把市场价格用这两个给替换了，不然求 FOC 的时候，会错误地变成 social planner problem。正常来说，这些市场价格对家庭来说是 “给定的”</u>**】

第二：

$$
\boxed{
K_{t+1}\text{ 不是时期 }t\text{ 的 state variable。}
}
$$

它只是所有家庭当期资本选择的总量。施加对称均衡以后，$K_{t+1}$ 与 $k_{t+1}$ 是同一个均衡量的总量和人均记号；可以在最终方程组中合并为一个未知的当期 control/outcome。

因此，我们仍然坚持原来的 workflow：

$$
\boxed{
\text{先形成家庭最优关系}
\longrightarrow
\text{再把所有均衡方程收拢}
\longrightarrow
\text{最后用 }K=nk,\ H=nh\text{ 消去重复记号}.
}
$$

但这种“消去总量变量”的泛化能力有限。若家庭异质，通常只有：

$$
K_t=\int k_t^i\,di,
$$

而不能根据任意一个家庭的 $k_t^i$ 恢复 $K_t$。此时财富分布、生产率分布或约束家庭的比例本身可能成为 aggregate state，不能把大写变量简单换成小写变量。类似地，在重叠世代、多类家庭、不完全市场、异质生产率或具有 aggregate externality 的模型中，也必须单独保留总量及其分布信息。

因此，一般原则是：

> 只有当 symmetric aggregation 给出一对一的代数映射，而且均衡不需要额外的分布信息时，才能把 aggregate variables 完整消去。

> 还有就是，当我们经济中各个个体的 FOC、外加各种约束、市场均衡...，把这些方程攒在一起其实整个经济的迭代就已经有了，后续所谓的消去这个、消去那个，都是为了更加简化地来进行递推系统的表示，只在一个小范围内考虑我们关心的变量。
>
> - 还有，列出 FOC、外加约束，其实解不出个体的政策函数，它只能说是 “筛选出合理的候选解”，我们这里是为了方便理解，但其实也可以算 “解出来了” 吧。

#### 2.5.4 第四步：价格与下一期资本为什么要联立确定？

经过前三步，家庭最优关系、厂商条件和对称均衡条件已经进入同一个方程组。重复的总量记号可以被消去，但还有两个关键的当期内生未知量：

$$
k_{t+1},\qquad p_t.
$$

其中 $k_{t+1}$ 是当期资本选择，$p_t$ 是竞争性货币市场的均衡价格。$p_t$ 与 $w_t,r_t$ 的区别在于确定机制不同：

- $w_t,r_t$ 可以（并且已经）由厂商静态边际产品条件直接表示；
- $p_t$ 必须通过家庭货币需求与给定货币供给的市场出清来确定。

我们现在消去了 w、r，但是还剩一个 p，因此我们应该这样处理：

$$
\begin{bmatrix}
k_{t+1}^i\\
m_t^{i,d}
\end{bmatrix}
=
g^i(\text{states variable (and Expectation)};  p_t\text{(and Expectation)}).
\tag{8.2.15}
$$

**<u>通过这个迭代方程，再联合剩下没用到的货币市场均衡条件</u>**：

若有 $n$ 个同质家庭，给定 aggregate nominal money supply $M_t^s$：
$$
\boxed{
n\,m_t^d(s_t,k_{t+1},p_t)=M_t^s.
}
\tag{8.2.17}
$$

更一般地，对异质家庭应写成：

$$
\boxed{
\int m_t^{i,d}\,di=M_t^s.
}
\tag{8.2.18}
$$

联合起来，就能够同时解出：

$$
k_{t+1},\qquad p_t.
$$

在此基础上还能够进行进一步的修改：因为实际上对于同质化的家庭，我们实际上都知道每一期的 mt 是多少（Mt 除个家庭数量就行了），所以我们把它放到递推方程里面意义不是很大，因此我们整个综合之后的经济系统内的递推方程可以变为：
$$
\begin{bmatrix}
k_{t+1}^i\\
p_t
\end{bmatrix}
=
g^i(\text{states variable (and Expectation)}).
\tag{8.2.19}
$$
这代表的就是联立解出 $k_{t+1},p_t $ 后，整个递推系统是什么状况；

#### 2.5.5 第五步：解出 \(k_{t+1},p_t\) 后恢复其他变量

先列清楚时期 $t$ 开始时已经给定的东西。家庭从过去带入：

$$
k_t,\qquad m_{t-1}.
$$

当期外生状态 $\lambda_t,g_t$ 已经实现，货币供给 $M_t^s$ 也由货币政策给定。由于通常：

$$
M_t^s=g_tM_{t-1}^s,
$$

所以 $g_t$ 与 $M_t^s$ 不应被重复计算成两个独立自由度。记状态时可以任选一种方式：

$$
\boxed{
\begin{aligned}
s_t&=(k_t,m_{t-1},\lambda_t,g_t),
&&\text{并由 }M_t^s=g_tM_{t-1}^s\text{ 恢复货币供给；}\\
\text{或}\qquad
s_t&=(k_t,m_{t-1},\lambda_t,M_t^s),
&&\text{直接给定货币供给过程。}
\end{aligned}
}
\tag{8.2.20}
$$

式（8.2.19）联立决定：

$$
\boxed{
\begin{bmatrix}
k_{t+1}\\
p_t
\end{bmatrix}
=
\mathcal G(s_t;M_t^s).
}
\tag{8.2.21}
$$

这里 $\mathcal G$ 只是整个均衡方程组解出来的映射记号：第一行给出资本递推，第二行给出当期市场出清价格。它不表示 $p_t$ 是家庭 control。

货币市场出清同时保证：

$$
\boxed{
m_t=\frac{M_t^s}{n}.
}
\tag{8.2.22}
$$

得到 $p_t,k_{t+1},m_t$ 后，再由原约束计算当期消费和劳动：
$$
c_t
=
\frac{m_{t-1}+T_t}{p_t},
\tag{8.2.23}
$$

$$
h_t
=
\left[
\frac{
k_{t+1}+m_t/p_t-(1-\delta)k_t
}{
\lambda_tk_t^\theta
}
\right]^{\frac1{1-\theta}}.
\tag{8.2.24}
$$

这里的劳动恢复式是在家庭 FOC 已经推导、并且厂商条件与 symmetric equilibrium 已经施加以后，对最终均衡方程组作的代数恢复；不能把它提前代回单个家庭目标函数再重新求导。

因此这一步的先后关系是：

$$
\boxed{
\begin{aligned}
&\text{给定 }s_t\text{，收拢家庭最优、厂商条件和市场出清}\\
&\Longrightarrow
\text{联立确定 }(k_{t+1},p_t)\\
&\Longrightarrow
\text{货币市场出清给出 }m_t=M_t^s/n\\
&\Longrightarrow
\text{由约束计算 }c_t,h_t.
\end{aligned}
}
$$

书中使用标准化变量时，unit-mass economy 的货币市场出清写成 $\hat m_t=1$；这只是式（8.2.22）的标准化形式。

外生变量则按照模型给定的过程演化：

$$
\lambda_{t+1}
=
\Lambda(\lambda_t,\varepsilon_{t+1}^{\lambda}),
\qquad
g_{t+1}
=
\Gamma(g_t,\varepsilon_{t+1}^{g}).
$$

#### 2.5.6 LQ 方法在这套流程中做什么？

上面的步骤给出了整个 workflow，但尚未求出家庭 price-taking 选择关系。LQ 方法从家庭层面开始时，只能精确消去**家庭自身约束内部**的变量。

用 CIA 和 household budget constraint 消去 $c_t^i,h_t^i$ 后，家庭的复合单期效用是：

$$
\boxed{
\ln\left(\frac{m_{t-1}^i+T_t^i}{p_t}\right)
+B
\frac{
k_{t+1}^i+m_t^i/p_t-(r_t+1-\delta)k_t^i
}{
w_t
}
.
}
\tag{8.2.25}
$$

在对这个 household objective 求导或作二阶近似时，家庭仍把 $p_t,w_t,r_t$ 以及它预期的未来市场环境视为给定。此时不能先令 $K_t=k_t^i,H_t=h_t^i$，也不能把 aggregate production function 改写成家庭自己的生产函数。

具体步骤是：

1. 对式（8.2.25）的 household composite return 作二阶 Taylor approximation；
2. 对家庭状态转移和它面对的市场环境 law of motion 作一阶近似；
3. 处理 Bellman continuation value 中的条件期望；
4. 得到家庭在给定市场环境时的近似线性选择关系：

$$
\begin{bmatrix}
\widetilde k_{t+1}^i\\
\widetilde m_t^{i,d}
\end{bmatrix}
=
F_x\widetilde x_t^i+F_q\widetilde q_t,
\tag{8.2.26}
$$

其中 $\widetilde q_t$ 统一表示家庭视为给定的市场价格和整体经济环境。这里不必把某个 aggregate variable 重新称为家庭 state；关键只在于家庭求导时不把这些市场量当作自己的选择。

5. 家庭选择关系形成以后，再加入厂商 FOC、aggregation、symmetric equilibrium 和货币市场出清；
6. 在完整线性均衡方程组中消去 $w_t,r_t,K_t,H_t$ 等重复符号，并联立解出 $\widetilde k_{t+1}$ 与 $\widetilde p_t$。

在 additive、zero-mean shocks 下：

$$
E_t\varepsilon_{t+1}=0,
$$

continuation value 中状态与创新的交叉项消失，创新平方项只改变 value function 的常数项。因此，期望算符不会阻止我们得到近似 LQ 模型的线性反馈政策。

最终的总剧本是：

$$
\boxed{
\begin{aligned}
&\text{两个家庭约束}
\Longrightarrow
\text{四个 choices 降为 }(k_{t+1},m_t);\\
&\text{厂商 FOC}
\Longrightarrow
\text{消去 }(w_t,r_t);\\
&\text{同质家庭与 symmetric aggregation}
\Longrightarrow
\text{在家庭最优关系形成后消去重复总量记号};\\
&\text{资本最优条件}+\text{货币市场出清}
\Longrightarrow
\text{联立解出 }(k_{t+1},p_t);\\
&\text{LQ approximation}
\Longrightarrow
\text{把上述关系写成线性递推系统。}
\end{aligned}
}
$$

#### 2.5.7 实际使用 LQ 时的顺序

构造 LQ approximation 时有两种合法的顺序。“先精确消元”是本书选择的便利路线，但不是 LQ 方法唯一允许的顺序。

##### 方法 A：先精确消元，再作近似（本书采用）

先利用**同一家庭优化问题内部**的 CIA constraint 和 household budget constraint，把 $c_t^i,h_t^i$ 精确写成家庭 controls、individual states 和家庭视为给定的市场环境的函数。由此得到 household composite return：

$$
\Psi^i(x_t^i,u_t^i;q_t),
$$

其中 $q_t$ 统一表示家庭视为给定的价格和整体经济环境。

然后：

1. 对 household composite return $\Psi^i$ 作二阶 Taylor approximation；
2. 对家庭状态转移及其面对的市场环境过程作一阶近似；
3. 求出家庭在给定 $q_t$ 时的 LQ 选择关系；
4. 最后才加入厂商条件、aggregation、symmetric equilibrium 和 market clearing，在完整方程组中消去重复市场和总量记号。

方法 A 的边界是：

$$
\boxed{
\text{可以先精确消去家庭内部约束，}
\quad
\text{不能在家庭求导前把 aggregate variables 直接替换成个体变量。}
}
$$

这条路线的优点是：

- **<u>非线性约束的曲率已经通过复合函数自动进入二阶目标，不容易漏项</u>**；
- 消元后变量较少，最终 LQ 矩阵规模较小；
- 对本章这种能够显式解出 $c_t,h_t$ 的模型尤其方便。

缺点是：

- 精确消元后的复合效用可能很长，二阶偏导计算繁重；
- 有些约束无法显式解出，或消元会产生难处理的分式、根式；
- 在异质主体、偶尔绑定约束等模型中，精确消元可能并不可行。

本书第 8.3 节采用的就是这条路线：

$$
\boxed{
\text{家庭内部精确消元}
\longrightarrow
\text{household composite return 二阶近似}
+
\text{家庭状态转移一阶近似}
\longrightarrow
\text{家庭 LQ 选择关系}
\longrightarrow
\text{aggregation 与 market clearing}.
}
$$

##### 方法 B：先近似原问题，再在近似系统中消元

这也是正式存在的 LQ 构造方法，不是临时想出来的。不过它不能简单地理解成“效用二阶展开、约束一阶展开，然后直接代入”。

把一般问题写成：

$$
\max_y U(y,\xi)
\qquad
\text{s.t.}\qquad
F(y,\xi)=0,
$$

并在无扰动的最优稳态 $(\bar y,0)$ 附近展开。令 $\bar\lambda$ 是该稳态约束的 Lagrange multiplier，Lagrangian 为：

$$
\mathcal L(y,\xi,\lambda)
=
U(y,\xi)+\lambda'F(y,\xi).
$$

正确的 LQ approximation 使用：

1. 结构约束的一阶线性形式：

$$
F_y\widetilde y+F_\xi\xi=0;
$$

2. 以 Lagrangian Hessian 为基础构造的 quadratic objective：

$$
\boxed{
\mathcal L_{yy}
=
U_{yy}
+\sum_j\bar\lambda_jF_{j,yy}.
}
$$

因此，约束的曲率虽然没有作为 quadratic constraint 留在最终问题中，但会通过：

$$
\sum_j\bar\lambda_jF_{j,yy}
$$

进入 quadratic objective。最终求解的问题仍然是：

$$
\boxed{
\text{quadratic objective}
\quad+\quad
\text{linear constraints}.
}
$$

为什么这样构造是正确的？原问题的精确 KKT conditions 是：

$$
U_y+\lambda'F_y=0,
\qquad
F=0.
$$

把这组条件在 $(\bar y,0,\bar\lambda)$ 附近作一阶展开，其中自然会出现：

$$
\left(
U_{yy}
+\sum_j\bar\lambda_jF_{j,yy}
\right)\widetilde y.
$$

这正是上述 LQ 问题 FOC 中的二次目标系数。因此，在适当的正则性、二阶条件与局部唯一性条件下：

$$
\boxed{
\text{正确构造的 LQ 问题的 FOC}
=
\text{原非线性问题 KKT conditions 的一阶展开}.
}
$$

所以它能够给出原最优政策在基准点附近的正确一阶近似。

这条路线的优点是：

- 不需要先把每个约束显式解出来；
- 更适合变量多、约束复杂或消元困难的模型；
- 可以系统地利用 Lagrangian Hessian 和自动微分构造二阶近似。

缺点是：

- 变量和乘子更多，矩阵系统通常更大；
- 必须计算稳态乘子以及约束的二阶导数；
- 记号与实现更复杂，较容易混淆 feasibility approximation 与 objective approximation。

需要特别避免所谓的 naive LQ approximation：

$$
\boxed{
\text{效用二阶近似}
+
\text{非线性约束只作一阶近似}
+
\text{目标中不加入乘子加权的约束曲率}.
}
$$

这种做法一般会遗漏 $\bar\lambda_jF_{j,yy}$，从而可能得到错误的一阶政策系数。Benigno and Woodford 将这种简单拼接明确称为 naive LQ approximation。

因此，方法 B 的准确含义不是“在最终 LQ 问题中保留二次约束”，而是：

$$
\boxed{
\text{用约束的二阶信息修正 quadratic objective，}
\quad
\text{最终仍只保留线性约束。}
}
$$

两条路线在二阶信息都被正确保留时，应当描述同一个局部 LQ approximation。

最后还要区别方法 B 与下一节的 log-linearization。若直接对原模型的 FOC、约束和均衡条件全部作一阶近似，再联立求解，那么求解的是一阶线性化的 equilibrium conditions；这属于第 2.6 节的路线，而不是通过完整二阶信息构造 LQ objective。



#### 2.5.Appendix：解动态宏观模型的一般思维框架

> 这一节的具体消元过程，也可以提炼成以后分析其他动态宏观模型时通用的思维框架。
>
> #### 1. 先区分四类变量
>
> 给定时期 \(t\)，模型中的变量可以先分成：
>
> 1. **state variables**：进入 \(t\) 期时已经确定、当期不能重新选择的量，例如
>    \[
>    s_t=(k_t,m_{t-1},\lambda_t,g_t);
>    \]
> 2. **control variables**：家庭在 \(t\) 期需要决定的量，例如
>    \[
>    u_t=(c_t,h_t,k_{t+1},m_t);
>    \]
> 3. **future variables**：跨期 FOC 中出现的 \(c_{t+1},h_{t+1},m_{t+1}\) 等，或它们的条件期望；
> 4. **可消元的中间变量**：例如 \(p_t,w_t,r_t\)。它们不是家庭的 controls，也不是预定状态，但通常可以利用厂商 FOC、市场出清和其他均衡关系，改写成 state 与 control 的函数。
>
> 对价格和总量变量的消元必须注意顺序：家庭先把市场价格和 aggregate environment 视为给定，推导 price-taking FOC；之后才能在完整均衡方程组中用厂商条件、aggregation 和 market clearing 消去这些符号，不能在家庭求导前把它偷换成 planner problem。
>
> #### 2. 当前方程真正缺少的是什么？
>
> 把可消元的变量替换掉以后，均衡条件的方程组可抽象写成：
>
> \[
> F\!\left(s_t,u_t,E_tz_{t+1}\right)=0,
> \]
>
> 其中 \(z_{t+1}\) 收集尚未闭合的未来内生变量。
>
> - 【一般而言，$z_{t+1}$ 就是 t+1 期的 u】
>     - 它不可能是中间变量，如果是 r、w、p，那么一般都可以被市场均衡条件替换掉，变成对应期的 control or state variable，不会进入死亡递归：rt 依赖于 r\_{t+1}、r\_{t+1}依赖于r\_{t+2}...；
>     - 它不可能是 state variable，因为未来的 state variable 肯定是由当期的 control + state variable 决定的，因此根本不涉及“未来变量”；
>     - 它只能是未来的 control variable；（这里 gpt 的意思是 z 只是 control variable u 的一个子集，因为毕竟不是所有“未来变量”都会产生无限依赖的循环，因此并不是 “出现了未来变量” 就需要设置政策函数来处理，因此这里单独用了一个 z，就表示那些需要专门设置政策函数的“独立的”那部分 control variable）
>
> 思考时可以先假设 \(E_tz_{t+1}\) 已经给定。对于标准、正则的宏观模型，给定当前 state 和这些未来变量后，当前 controls 通常可以局部唯一解出：
>
> \[
> u_t=H\!\left(s_t,E_tz_{t+1}\right).
> \]
>
> 因此，模型的主要困难通常不是“当前 controls 完全没有方程决定”，而是：**当前最优选择依赖未来变量，但未来变量本身尚未被写成未来 state 的函数**。这些未来变量需要通过假设政策函数来解决这个 t 依赖于 t+1、t+1 依赖于 t+2...... 这种无限的循环。
>
> #### 3. 应当寻找多少个政策函数？
>
> 不能简单按照期望符号出现的次数来数，而要先完成所有可能的代换，再看还剩多少个**相互独立的未来变量方向**。
>
> 若消元后只剩：
>
> \[
> E_tc_{t+1},
> \]
>
> 就寻找一个政策函数：
>
> \[
> c_t=g_c(s_t).
> \]
>
> 若还剩两个彼此独立的未来变量，例如：
>
> \[
> E_tc_{t+1},\qquad E_th_{t+1},
> \]
>
> 就寻找二维政策函数：
>
> \[
> \begin{bmatrix}
> c_t\\
> h_t
> \end{bmatrix}
> =
> \begin{bmatrix}
> g_c(s_t)\\
> g_h(s_t)
> \end{bmatrix}.
> \]
>
> 但如果已有静态关系：
>
> \[
> c_t=C(s_t,h_t),
> \]
>
> 那么下一期：
>
> \[
> c_{t+1}=C(s_{t+1},h_{t+1}),
> \]
>
> 此时 \(c_{t+1}\) 不再是独立的未来方向，只需独立求 \(h_t=g_h(s_t)\)；消费政策再由
>
> \[
> g_c(s_t)=C\!\left(s_t,g_h(s_t)\right)
> \]
>
> 派生出来。
>
> - <u>意思就是说，尽管我们的线性方程组里面可能会出现很多未来变量，但是并不是每个未来变量都需要单独设置政策函数，我们只有遇到那种 “t 依赖于 t+1、t+1 依赖于 t+2......” 的这种无限的循环，才需要设置一个政策函数来进行 “截断”，有些情况下你看到方程里出现了 $E_t[h_{t+1}]$，但实际上有些情况下可以做一个变量代换， $h_t$ 可以表示成 state variable + 其他 control var 的函数（例如 ct），那么实际上我们处理 $h_{t+1}$ 的时候就不会进入这种无限循环，通过代换把 $h_{t+1}$ 变成下一期的 state var 以及 $c_{t+1}$ 的函数即可，因此此时就只需要设置消费的政策函数、处理 $c_{t+1}$ 即可</u>。
>
> 因而更准确的原则是：
>
> \[
> \boxed{
> \text{消元后剩多少个独立未来方向，就需要多少个独立政策函数分量。}
> }
> \]
>
> 其他 control 即使没有被独立“猜测”，最终仍会通过约束和均衡关系得到自己的派生政策函数。
>
> #### 4. 政策函数如何关闭未来变量？
>
> 假设需要寻找：
>
> \[
> z_t=g(s_t).
> \]
>
> 状态转移为：
>
> \[
> s_{t+1}=T(s_t,u_t,\varepsilon_{t+1}).
> \]
>
> 那么下一期同一规律仍然成立：
>
> \[
> z_{t+1}=g(s_{t+1}),
> \]
>
> 因而随机模型中：
>
> \[
> E_tz_{t+1}
> =
> E_t\!\left[
> g\!\left(T(s_t,u_t,\varepsilon_{t+1})\right)
> \right].
> \]
>
> 将它代回当前 FOC 和约束后，模型会重新给出一套当期决策。真正的政策函数必须满足：重新推导出来的当期 \(z_t\)，恰好等于原来假设的 \(g(s_t)\)。因此政策函数本质上是一个自洽的函数固定点：
>
> \[
> \boxed{g=\mathcal T[g].}
> \]
>
> 确定性模型只是没有对未来冲击积分；随机模型则还要结合冲击分布计算条件期望，二者的闭合逻辑相同。
>
> - **<u>Finally</u>**
>
>     我们对“独立的”（即需要专门设置政策函数的 control var）变量设置的政策函数解出来后、（代回）再加上原来的方程组，就能够得到完整的、所有 control variable 的政策函数 + state variable 的递推方程组；
>
> #### 5. \(k_{t+1}\) 为什么既像 control，又像 state？
>
> \(k_{t+1}\) 是家庭在时期 \(t\) 选择的 control，但一旦进入时期 \(t+1\)，它已经由过去决定，便成为下一期的 predetermined state：
>
> \[
> \boxed{
> k_{t+1}\text{ 是 }t\text{ 期的 control，也是 }t+1\text{ 期的 state。}
> }
> \]
>
> \(m_t\) 同理。因此，“control / state”取决于所站的决策时点；而 Schur/BK 中的 jump variable 则是另一套分类，它关心某个**当期变量**能否立即调整以消除爆炸方向。
>
> #### 6. 一般非线性模型、LQ 与 Schur/QZ 的关系
>
> 在一般非线性模型中，\(g\) 的形状通常未知，需要用 value-function iteration、policy iteration、time iteration 或 projection 等方法求函数固定点。
>
> LQ 问题具有线性—二次闭合性，最优政策属于线性函数族：
>
> \[
> z_t=Fs_t.
> \]
>
> 此时无限维的函数固定点降为有限维矩阵 \(F\) 的固定点，可以通过：
>
> - Bellman–Riccati；
> - 待定系数；
> - policy iteration；
> - Schur/QZ；
>
> 来求解。
>
> 若采用第 2.6 节的 log-linearization 路线，则不必先手工把所有变量消掉。可以把家庭 FOC、约束、厂商条件和市场出清一起线性化，拼成完整的线性理性预期系统。Schur/QZ 并不是在原方程组之外再增加一批条件，而是从原系统的稳定不变子空间中选出满足稳定性/TVC 的路径，并同时得到：
>
> \[
> j_t=Fs_t,
> \qquad
> s_{t+1}=Gs_t+C\varepsilon_{t+1}.
> \]
>
> 第一式给出当期 jump variables（的政策函数），第二式给出 \(k_{t+1},m_t\) 等下一期 states 的递推。因此，Schur/QZ 与“猜测政策函数并要求自洽”解决的是同一个闭合问题，只是它利用线性系统的稳定子空间一次性完成了系数求解和稳定根选择。
>


#### 2.5.Appendix 2：CIA 何时绑定，以及为什么不能提前约掉预算中的货币项

> 本节处理两个容易混在一起的问题：
>
> 1. CIA 原本是不等式，为什么本章可以把它写成等号？它什么时候会真正约束家庭，什么时候不会？
> 2. 在最终对称均衡中，家庭持有的货币与政府提供的人均货币数量看起来必然相等，为什么不能在推导家庭 FOC 之前把预算约束两边的货币项直接约掉？

##### 1. 先保留 CIA 的不等式形式

家庭在时期 \(t\) 能用于购买消费品的现金为：

\[
A_t^i=m_{t-1}^i+T_t^i.
\]

CIA constraint 应先写成：

\[
\boxed{
p_tc_t^i\leq A_t^i.
}
\]

它只表示“消费支出不能超过期初可用现金”，并没有在会计上要求家庭必须把现金全部花完。令 \(\nu_t^i\geq0\) 表示 CIA 的乘子（影子价格），则互补松弛条件是：

\[
\nu_t^i\left(A_t^i-p_tc_t^i\right)=0.
\]

因此存在三种直观情形：

1. **严格绑定**
   \[
   p_tc_t^i=A_t^i,\qquad \nu_t^i>0.
   \]
   家庭已经把现金花完，但在边界上仍希望增加消费；多一单位流动性具有正的边际价值。

2. **松弛**
   \[
   p_tc_t^i<A_t^i,\qquad \nu_t^i=0.
   \]
   家庭还有闲置现金，但已经不愿继续增加消费。此时消费的边际效用已经与损失当前资源、资本积累和未来消费的机会成本相平衡。

3. **弱绑定**
   \[
   p_tc_t^i=A_t^i,\qquad \nu_t^i=0.
   \]
   家庭恰好停在现金边界上，但稍微放宽 CIA 也不会改变最优选择。等号成立，并不自动意味着约束具有真实的扭曲作用。

所以必须区分：

\[
\boxed{
\text{CIA 取等号}
\quad\neq\quad
\text{CIA 的乘子一定为正。}
}
\]

真正表示 CIA 在经济上“卡住”家庭的是 \(\nu_t^i>0\)，而不只是等号成立。

##### 2. 为什么标准 CIA 模型通常会落在严格绑定情形？

关键要看家庭在时期 \(t\) 为什么愿意持有 \(m_t^i\)。

多持有一单位名义货币，会占用当期：

\[
\frac{1}{p_t}
\]

单位真实资源（占用家庭预算约束这一个约束式的资源）。这些资源原本可以用于资本积累，或者通过其他选择改善当前与未来消费。因此这部分占用带来的 “代价” 就是 $\lambda_t·\frac{1}{p_t\\}$ （这里λt 是家庭预算约束的影子价格）；

> 这里 p 就跟 w、r 一样，是价值关系 gain = loss 维持稳定的一个中介 / 转换系数；

它的未来收益则包括两部分：

1. 货币在下一期仍是一项财富，具有真实购买力；【下一期的预算约束式的影子价格】
2. 如果下一期 CIA 绑定，它还可以放松交易约束，提供额外的流动性服务。【下一期的CIA 约束式的影子价格】

用 \(\mu_t^i\) 表示预算约束的资源影子价值，货币 FOC 的主线可以概括为：

\[
\boxed{
\frac{\mu_t^i}{p_t}
=
\beta E_t\left[
\frac{\mu_{t+1}^i+\nu_{t+1}^i}{p_{t+1}}
\right].
}
\]

左边是持有一单位货币占用当前资源的边际成本；右边是下一期的普通财富价值，加上可能存在的流动性价值。

如果当前和未来的 CIA 都松弛：

\[
\nu_{t+1}^i=0,
\]

那么货币就只是一种普通储蓄资产。<u>此时要让家庭自愿持有正数量货币，它的真实回报必须能够与资本等其他资产竞争</u>（在 CIA 约束的影子价格都是 0 的时候，持有一单位货币给“现期预算约束”带来的损失要等于给“未来的预算约束”带来的收益）。若货币的真实回报严格低于资本，而它又不提供流动性服务，家庭就会减少货币需求，把资源转向回报更高的资产。

因此，在通常的正名义利率情形下：

\[
\text{货币金融回报较低}
\quad\Longrightarrow\quad
\text{必须依靠正的流动性价值补偿}
\quad\Longrightarrow\quad
\nu_t^i>0,
\]

> 这里意思是未来的预算约束式的影子价格往往没有现期高，毕竟因为有折现，或者这么说，未来一单位的消费的收益没有现在一单位的消费的收益高
>
> （因为如果 CIA 约束的影子价格是 0，那么消费 c 的收益就等于其给预算约束式带来的损失，因此可以说预算约束的影子价格由 c 来衡量；其实由资本 k 来衡量也可以，反正二者都是一样的；）

从而 CIA 严格绑定：
\[
p_tc_t^i=A_t^i.
\]

但是这不是纯逻辑必然。在零名义利率或 Friedman rule 一类边界情形中，货币与其他资产的回报可能相同。此时即使 \(\nu_t^i=0\)，家庭也可能愿意持有货币，CIA 可以松弛，也可以只是弱绑定。

所以本章把 CIA 直接写成等号，准确的理解是：

\[
\boxed{
\text{模型研究的是 CIA 在稳态处严格绑定，并且小冲击不改变这一状态的局部区域。}
}
\]

如果冲击足够大，或者模型允许约束在不同状态间切换，就必须保留不等式与互补条件，分 binding / slack 两个 regime 求解，不能从一开始永久写成等号。

##### 3. 预算约束中究竟是哪两组货币项“看起来相等”？

家庭的实际预算约束是：

\[
c_t^i+k_{t+1}^i+\frac{m_t^i}{p_t}
=
w_th_t^i+(r_t+1-\delta)k_t^i
+
\frac{m_{t-1}^i+T_t^i}{p_t}.
\]

其中：

- 右边的
  \[
  \frac{m_{t-1}^i+T_t^i}{p_t}
  \]
  是家庭进入当期时已经拥有的真实现金购买力；
- 左边的
  \[
  \frac{m_t^i}{p_t}
  \]
  是家庭在当期重新选择、准备带到下一期的真实货币余额。

在最终的 symmetric equilibrium 中，若家庭总质量为 1，货币市场出清给出：

\[
m_t^i=M_t.
\]

同时，若政府把新增货币全部 lump-sum transfer 给家庭：

\[
m_{t-1}^i+T_t^i
=
M_{t-1}+(g_t-1)M_{t-1}
=
M_t.
\]

所以站在已经知道均衡结果的“上帝视角”看，确实有：

\[
m_t^i=m_{t-1}^i+T_t^i=M_t,
\]

从而预算约束两边的货币项数值相等。

问题在于：**这个相等是家庭完成最优化以后，由政府规则、对称均衡和货币市场出清共同产生的结果；它不是单个家庭在作选择时面对的私人约束。**

##### 4. 为什么不能在家庭求 FOC 前把它们约掉？

单个家庭在选择 \(m_t^i\) 时，把：

\[
M_t,\qquad p_t,\qquad w_t,\qquad r_t
\]

看作给定的市场环境。它可以尝试多持或少持货币，并比较：

\[
\text{多持货币的当前资源成本}
\]

与：

\[
\text{未来财富回报和流动性收益}.
\]

正是这个边际比较产生了货币 FOC。

如果在家庭优化之前就直接代入：

\[
m_t^i=M_t
\]

并把预算约束两边的货币项约掉，那么 \(m_t^i\) 会被错误地从家庭的选择集合中删除。家庭将不再能够比较“多持一单位货币是否值得”，货币 FOC 也随之消失。这样会遗漏本章最重要的机制：

\[
\text{货币增长与通胀}
\longrightarrow
\text{货币真实回报变化}
\longrightarrow
\text{持币机会成本与流动性价值变化}
\longrightarrow
\text{消费、劳动和资本选择变化}.
\]

因此，正确顺序是：

\[
\boxed{
\begin{aligned}
&\text{家庭先在给定价格和总量环境下选择 }m_t^i;\\
&\text{由家庭最优化得到货币需求和货币 FOC;}\\
&\text{所有家庭都完成选择后，再施加 }
\int m_t^{i,d}\,di=M_t;\\
&\text{价格 }p_t\text{ 调整，使货币需求等于给定货币供给。}
\end{aligned}
}
\]

这与“不能在家庭求导前令 \(K_t=k_t^i\)、\(H_t=h_t^i\)”是同一条方法论：

\[
\boxed{
\text{个体先把市场环境视为给定并完成最优化，市场出清只能在最优化之后施加。}
}
\]

否则就会把竞争均衡中的个体选择，错误地改写成一个已经 internalize aggregate equilibrium 的 planner problem。

##### 5. 但 CIA 自身若已确认绑定，可以在家庭问题内部代入

这里要避免走向另一个极端。

如果已经确认家庭自己的 CIA 严格绑定：

\[
p_tc_t^i=m_{t-1}^i+T_t^i,
\]

那么可以在家庭预算约束中用：

\[
c_t^i
=
\frac{m_{t-1}^i+T_t^i}{p_t}
\]

作代数替换，于是预算约束化为：

\[
k_{t+1}^i+\frac{m_t^i}{p_t}
=
w_th_t^i+(r_t+1-\delta)k_t^i.
\]

这一步是合法的，因为 CIA 是家庭自身面对的私人约束。

真正不能提前使用的是：

\[
m_t^i=M_t,
\]

因为它来自货币市场出清，而不是家庭的私人约束。

所以最后应当记住：

\[
\boxed{
\begin{aligned}
&\text{家庭自身的约束，在确认适用后可以用于家庭内部消元；}\\
&\text{市场出清和对称均衡关系，必须在家庭 FOC 推导完成后再施加。}
\end{aligned}
}
\]

##### 6. 一句话总结

$$
\boxed{
\begin{aligned}
&\text{CIA 是否真正绑定，要看其乘子是否为正；}\\
&\text{正的持币机会成本通常使流动性价值为正，从而令 CIA 严格绑定；}\\
&\text{预算两边货币项的相等是最终均衡结果，不是家庭的私人约束；}\\
&\text{先保留 }m_t^i\text{ 的选择并推导货币 FOC，之后才能施加货币市场出清。}
\end{aligned}
}
$$



### 2.6 Log-linear solution：更透明的均衡条件系统

上一节的 LQ 路线是：先处理目标函数与约束，构造一个 quadratic objective + linear constraints 的新问题，再求这个新问题的最优政策。

这一节换一条入口。我们直接取前面已经得到的：

- 家庭 FOC；
- CIA constraint 与 flow budget constraint；
- 厂商边际产品条件；
- aggregation 和 market-clearing conditions；
- 技术与货币增长过程；

然后把这些均衡条件分别在稳态附近作一阶 log-linearization，最后联立求解。也就是说：

$$
\boxed{
\text{原模型的均衡方程组}
\longrightarrow
\text{逐条 log-linearize}
\longrightarrow
\text{线性方程组}
\longrightarrow
\text{递推公式}.
}
$$

#### 2.6.1 aggregate CIA relation 从哪里来？

个体家庭的标准化 CIA constraint 是：

$$
\hat p_t c_t^i
=
\frac{\hat m_{t-1}^i+(g_t-1)}{g_t},
\tag{8.3.1}
$$

其中：

$$
\hat p_t=\frac{p_t}{M_t},
\qquad
\hat m_{t-1}^i=\frac{m_{t-1}^i}{M_{t-1}},
\qquad
M_t=g_tM_{t-1}.
$$

在 symmetric equilibrium 和 unit-mass economy 中：

$$
c_t^i=C_t,
\qquad
\hat m_{t-1}^i=1.
$$

所以式（8.3.1）变成：

$$
\hat p_tC_t
=
\frac{1+(g_t-1)}{g_t}
=1.
\tag{8.3.2}
$$

为什么这里的 $g_t$ 消掉了？因为本章假设政府把当期新增货币全部 lump-sum transfer 给家庭。家庭进入时期 $t$ 时拥有的旧货币加新增转移，合计正好等于当期总货币供给 $M_t$。把 nominal variables 除以 $M_t$ 后，可用于消费的 aggregate normalized cash 就恒等于 1。

因此：

$$
\boxed{\hat p_tC_t=1}
$$

> #### Comment：求解顺序
>
> 这里直接把 mt = 1 代入进去了，然后得到了 pt \* Ct = 1，实际上是这样的，这个 mt=1 是货币市场均衡条件，因此我们并不是凭空制造了一个条件，然后代入进去，我们只是利用了一个市场均衡条件；
>
> 

是 aggregate CIA constraint 的精确形式，而不是突然附加的一条新假设。

在稳态也有：

$$
\bar{\hat p}\,\bar C=1.
$$

将动态等式除以稳态等式：

$$
\frac{\hat p_t}{\bar{\hat p}}
\cdot
\frac{C_t}{\bar C}
=1.
$$

取对数：

$$
\widetilde{\hat p}_t+\tilde C_t=0.
\tag{8.3.3}
$$

所以这条关系的意思是：

$$
\boxed{\tilde C_t=-\widetilde{\hat p}_t.}
$$

这里的 $\hat p_t=p_t/M_t$ 是 normalized price，而不是未经标准化的 nominal price。给定 aggregate normalized cash purchasing power 为 1，normalized price 比稳态高 1%，家庭能够购买的真实消费就比稳态低约 1%。CIA constraint 因而把 normalized price movement 与 real consumption movement 直接绑在一起。

有了这条关系以后，可以在其他 log-linearized equations 中用：

$$
\tilde C_t=-\widetilde{\hat p}_t
$$

消去消费，只保留价格；也可以反过来消去价格，只保留消费。选择哪一个只是代数便利。

后文为简化记号，会把 normalized price 的 log deviation $\widetilde{\hat p}_t$ 简写为 $\tilde p_t$。

#### 2.6.2 其余方程如何进入线性系统？

factor price 条件 log-linearize 后大致给出：

$$
\tilde r_t=\tilde\lambda_t+(\theta-1)\tilde K_t-(\theta-1)\tilde H_t,
$$

$$
\tilde w_t=\tilde\lambda_t+\theta\tilde K_t-\theta\tilde H_t.
$$

货币增长过程可以写成：

$$
\tilde g_{t+1}=\pi\tilde g_t+\varepsilon_{t+1}^g.
$$

技术过程则是：

$$
\tilde\lambda_{t+1}=\gamma\tilde\lambda_t+\varepsilon_{t+1}^\lambda.
$$

最后模型被整理成状态空间形式。状态变量包括 capital，外生状态包括 technology 和 money growth，控制变量包括 wage、rental rate、hours 和 price。解出来后，可以写成类似：

$$
\tilde K_{t+1}=P\tilde K_t+Qz_t,
$$

$$
y_t=R\tilde K_t+Sz_t,
$$

其中 $z_t=(\tilde\lambda_t,\tilde g_t)'$。书中给出了具体矩阵数值，例如 $P\approx0.9418$，说明资本仍然高度持久；$Q$ 中技术冲击和货币增长冲击的系数则描述两种外生冲击如何改变资本积累路径。

表 8.3 和表 8.4 给出不同 money growth shock volatility 下的模型 moments：

![Table 8.3 — Standard errors in the cash-in-advance model](../Figures/Ch08/table_8_3_cia_standard_errors.png)

![Table 8.4 — Correlations in the cash-in-advance model](../Figures/Ch08/table_8_4_cia_correlations.png)

这两张表的核心读法是：当 money growth shock 的标准差提高时，价格和名义/货币相关变量的波动会明显上升，但 output、hours、capital 等真实变量的波动变化相对有限。这说明在这个具体校准下，技术冲击仍然是主要的 real business cycle driver，money growth shock 更多体现在 price dynamics 和 consumption/investment 的局部调整上。

### 2.7 Impulse responses：技术冲击与货币冲击的区别

本章把 Cooley-Hansen model 的 impulse responses 与 Hansen real model 做对照。

图 8.1 先回顾 Hansen indivisible labor model 对一次技术冲击的响应：

![Figure 8.1 — Hansen model response to a technology shock](../Figures/Ch08/figure_8_1_hansen_tech_shock.png)

图 8.2 展示加入 cash-in-advance friction 后，Cooley-Hansen model 对同样技术冲击的响应：

![Figure 8.2 — Cooley-Hansen model response to a technology shock](../Figures/Ch08/figure_8_2_cooley_hansen_tech_shock.png)

两者的真实变量响应方向大体相似：技术上升提高 output、hours、investment 和 consumption，并通过资本积累产生持久效应。但 CIA model 多了价格和货币约束关系。由于 aggregate CIA constraint 近似给出 $\tilde p_t+\tilde C_t=0$，消费上升往往伴随 normalized price level 下降。

图 8.3 展示一次 money growth shock 的响应：

![Figure 8.3 — Response to a money growth shock](../Figures/Ch08/figure_8_3_money_growth_shock.png)

货币增长冲击的动态与技术冲击不同。书中设定 money growth process 的 persistence 通常低于 technology process，因此 money shock 消退更快。它对 price level 的影响更直接，对真实产出和资本的影响相对较小。直观地说，技术冲击改变生产能力，货币冲击主要改变交易约束和通胀税。

### 2.8 Seigniorage：从 lump-sum transfer 到政府购买

#### 2.8.Appendix：如何写约束式

核心思维链路：

- 每一个 agent 都有收支两面

    **<u>只要连接上有直接关系的项目即可</u>**；

    - 例如对于家庭，在前一个例子里面，政府直接给家庭收入来源，在这里面，政府本身没有任何具体的购买行为，因此实际上我们完全不用对政府进行建模，只需要再家庭的收入端加一个转移支付项即可；

    - 在目前这个例子里面，引入了政府，政府收支两端与消费者没有直接联系，因此家庭的收支两端没有跟政府相关的变量，收入端就只是 w、r 以及自己以前存的资本 + 货币，支出端也是一样的，购买力能够转化为商品、资本、货币；

        由于政府有实质的购买行为，因此需要单独对政府进行建模，也就是列一个政府行为方程出来（就是政府的预算约束，政府本身没有最优化动作）；

- 每个“商品”的市场都需要均衡

    - 对于要素市场，直接变量共用就代表体系已经隐性融入了要素市场的出清

        > 例如一般是 Qs = F(p,...)，Qd = G(p,...)，然后 Qs = Qd 代表显式地写出这个均衡；但实际上我们不会都这样写，这个太麻烦了，我们一般是直接 Q = F(p,...)，Q = G(p,...)，如果这样写，其实已经隐性地包含了“市场出清”的条件；

    - 对于货币市场，需要显式写出来 ∑m\_{t-1} + M\_G = ∑m\_t

        > 这主要是由于货币市场的特性，它是有多个不同的供给/需求者参与（不像那种只有一个需求者 + 一个供给者），因此没有办法像要素市场一样直接隐式地写好，需要显式给定；
        >
        > 其次需要注意这个不等于 CIA 约束，CIA 约束说的是消费者对于 ct 的一个限制，不是货币市场均衡；
        >
        > - 这里需要注意有些情况下在写出 FOC 之前最好别替换，否则有可能从 “分布式决策问题” 被悄悄改写为了 “social planner problem”；

    - 商品市场呢？不需要写商品市场均衡

        > 当所有市场都均衡以后，这个商品市场必然达成均衡，这是代数规律；
        >
        > - 背后的 Walras’ law 思想：
        >
        >     当所有主体的预算约束都正确、政府预算正确，而且除一个市场外的其他市场全部出清时，最后一个市场出清条件通常是冗余的。因此有时候为了方便我们可能会显式写出商品市场的出清，而省略其他某个市场的出清条件。

- 每个 agent 的收支两面把 “有直接关系的” 写好 + 市场均衡都有，那么整个经济系统自然就是 “完全” 的，不用担心错误；



#### 2.8.Appendix2：如何进行均衡的比较静态分析





#### 2.8.1：正文——完整均衡系统与 Bailey curve

前面的 transfer 版本把新增货币直接交给家庭；本节改为政府发行新货币并购买商品。时期内的关键时序只有一句话：

$$
\boxed{
\text{家庭用旧货币购买私人消费，政府用新增货币购买 }G_t.
}
$$

因此，家庭的 CIA 不再包含政府转移，政府则多出一条预算约束。政府购货款已经作为厂商销售收入，通过工资、资本租金与利润进入私人部门，所以不能再把同一笔新增货币作为 transfer 加进家庭预算。

下面不再逐个主体重复叙述，而是直接把模型转换成实际量与平稳变量，并集中列出完整均衡方程组。在此基础上，再用“变量之间的联通关系—影子价格—数量调整”解释 Bailey curve。

##### 1. 转换为实际量后，完整均衡方程组是什么？

定义货币增长因子、标准化价格与标准化个体货币余额：

$$
\boxed{
\phi_t=\frac{M_t}{M_{t-1}},
\qquad
\hat p_t=\frac{p_t}{M_t},
\qquad
\hat m_t^i=\frac{m_t^i}{M_t}.
}
\tag{8.5.1}
$$

因此：

$$
\frac{m_t^i}{p_t}=\frac{\hat m_t^i}{\hat p_t},
\qquad
\frac{m_{t-1}^i}{p_t}
=
\frac{\hat m_{t-1}^i}{\phi_t\hat p_t}.
\tag{8.5.2}
$$

令 $\eta_t^i$ 表示家庭预算约束的 current-value 影子价格，$\zeta_t^i$ 表示 CIA 约束的 current-value 影子价格。模型的全部核心条件可写成：

**家庭约束**

$$
\boxed{
\hat p_tc_t^i
=
\frac{\hat m_{t-1}^i}{\phi_t},
}
\tag{8.5.3}
$$

$$
\boxed{
c_t^i+k_{t+1}^i+\frac{\hat m_t^i}{\hat p_t}
=
w_th_t^i+(r_t+1-\delta)k_t^i
+\frac{\hat m_{t-1}^i}{\phi_t\hat p_t}.
}
\tag{8.5.4}
$$

式（8.5.3）使用 CIA 严格绑定的局部区域。家庭当期消费只能使用上一期带来的旧货币。

**家庭最优条件**

$$
\boxed{
u_c(c_t^i,h_t^i)=\eta_t^i+\zeta_t^i,
}
\tag{8.5.5}
$$

$$
\boxed{
u_h(c_t^i,h_t^i)+\eta_t^iw_t=0,
}
\tag{8.5.6}
$$

$$
\boxed{
\eta_t^i
=
\beta E_t\!\left[
\eta_{t+1}^i(r_{t+1}+1-\delta)
\right],
}
\tag{8.5.7}
$$

$$
\boxed{
\frac{\eta_t^i}{\hat p_t}
=
\beta E_t\!\left[
\frac{\eta_{t+1}^i+\zeta_{t+1}^i}
{\phi_{t+1}\hat p_{t+1}}
\right].
}
\tag{8.5.8}
$$

这里最重要的是式（8.5.5）与式（8.5.8）：

- 消费边际效用连接了预算资源影子价格 $\eta_t$ 与现金流动性影子价格 $\zeta_t$；
- 多持一单位货币的当期成本只连接预算约束，未来收益却同时连接预算约束与 CIA；
- 货币增长率提高会降低货币的金融回报，均衡必须通过 $\eta,\zeta,C,\hat p$ 等变量的共同变化重新满足式（8.5.8）。

**厂商条件**

$$
\boxed{
Y_t=\lambda_tK_t^\theta H_t^{1-\theta},
}
\tag{8.5.9}
$$

$$
\boxed{
w_t=(1-\theta)\lambda_t
\left(\frac{K_t}{H_t}\right)^\theta,
\qquad
r_t=\theta\lambda_t
\left(\frac{K_t}{H_t}\right)^{\theta-1}.
}
\tag{8.5.10}
$$

**政府预算、市场出清与资源约束**

$$
\boxed{
p_tG_t=M_t-M_{t-1}
\quad\Longleftrightarrow\quad
\hat p_tG_t=1-\frac{1}{\phi_t},
}
\tag{8.5.11}
$$

$$
\boxed{
\int\hat m_t^{i,d}\,di=1.
}
\tag{8.5.12}
$$

在 unit-mass symmetric equilibrium 中：

$$
\boxed{
\hat m_t^i=1,
\qquad
c_t^i=C_t,
\qquad
h_t^i=H_t,
\qquad
k_t^i=K_t.
}
\tag{8.5.13}
$$

总资源约束为：

$$
\boxed{
C_t+K_{t+1}+G_t
=
Y_t+(1-\delta)K_t.
}
\tag{8.5.14}
$$

**Bailey curve 问题：**

把 $\hat m_{t-1}=1$ 代入 CIA（货币市场出清），并与政府预算联立，立即得到：
$$
\boxed{
\hat p_tC_t=\frac{1}{\phi_t},
\qquad
\hat p_tG_t=1-\frac{1}{\phi_t},
}
\tag{8.5.15}
$$

$$
\boxed{
\hat p_t(C_t+G_t)=1,
\qquad
\frac{G_t}{C_t}=\phi_t-1.
}
\tag{8.5.16}
$$

实际铸币税收入等于政府购买：

$$
\boxed{
S_t=G_t
=
\frac{M_t-M_{t-1}}{p_t}
=
\left(1-\frac{1}{\phi_t}\right)
\frac{M_t}{p_t}.
}
\tag{8.5.17}
$$

因此 Bailey curve 的问题可以压缩成：

$$
\boxed{
S(\phi)
=
\underbrace{\left(1-\frac1\phi\right)}_{\text{通胀税率}}
\underbrace{\frac{M}{p}}_{\text{真实货币余额税基}}.
}
\tag{8.5.18}
$$

税率必然随 $\phi$ 上升；曲线是否最终下降，完全取决于均衡中的真实货币余额 $M/p$ 是否收缩得足够快。

##### 2. Log utility 基准：为什么 Bailey curve 只会上升并趋于上限？

基准效用为：

$$
\boxed{
u(C,H)=\ln C+BH,
\qquad B<0.
}
\tag{8.5.19}
$$

这时：

$$
u_C=\frac1C,
\qquad
u_H=B.
$$

先看几条“联通器”。

资本 Euler equation 在确定性稳态中给出：

$$
\boxed{
1=\beta(\bar r+1-\delta),
}
\tag{8.5.20}
$$

> 资本连通的是前后两期的家庭预算约束式的影子价格，由于效用函数上有个折现，因此保留一单位现期资本带来的收益会乘上一个乘子（$r_{t+1}+1-\delta$）来跟折现 beta 刚好对冲掉，以此保证增加一单位资本储蓄的未来收益 = 当期的损失；
>
> 在稳态中，影子价格应当是不变的（我们把折现移到影子价格外面），不论货币增速改成啥样了（稳态变成啥样），只要在稳态中，两期之间的这个比例关系就一定是维持的，因此不论在何种稳态，稳态利率 r 是一定不变的，这意味着经济系统中劳动、资本的比例一定是不变的、工资 w 也是不变的。
>
> - 例如 $\phi$ 增加前后的两种稳态中，它们的其他内生变量可能会不一致，但是 w、r 一定是一样的；

所以 $\bar r$ 被固定。厂商资本 FOC 随即固定资本劳动比：
$$
\boxed{
q\equiv\frac{\bar K}{\bar H}
=
\left(\frac{\theta}{\bar r}\right)^{\frac{1}{1-\theta}},
}
\tag{8.5.21}
$$

从而实际工资也被固定：
$$
\boxed{
\bar w=(1-\theta)q^\theta.
}
\tag{8.5.22}
$$

由于 indivisible labor 使劳动边际福利损失为常数，劳动 FOC：

$$
B+\bar\eta\bar w=0
$$

> 因为劳动的边际损失不变、劳动到预算式的乘子（工资 w）不变，因此预算式的影子价格被劳动锚定了；

把预算约束影子价格锚定为：
$$
\boxed{
\bar\eta=-\frac{B}{\bar w}.
}
\tag{8.5.23}
$$

这一步是基准模型最关键的特殊性：消费变化虽然会改变总边际效用，但不能带动 $\bar\eta$ 同比例变化；增加的边际效用主要由 CIA 影子价格 $\bar\zeta$ 吸收。

> 当货币增速 $\phi$ 永久增加后，导致家庭持有实际货币的意愿降低，因此必须补上这块的损失、增加 $u_c=η+ζ$，但是我们上面说了，预算式的影子价格 η 被锁定了，因此当 c 下降的时候，增加的 $u_c$ 主要由 CIA 的影子价格 ζ 吸收；

稳态货币 FOC 与消费 FOC 联立：

$$
\bar\eta
=
\frac{\beta}{\bar\phi}
(\bar\eta+\bar\zeta)
=
\frac{\beta}{\bar\phi\bar C}.
\tag{8.5.24}
$$

> 第一个等式是要求持有实际货币的损失（η，对当期预算式带来的损失）等于收益（...\*(η+ζ)，未来的 CIA 的影子价格 + 未来的预算式的影子价格）；第二个等式是 $u_c=1/C=η+ζ$；

因此：
$$
\boxed{
\bar C
=
\frac{\beta}{\bar\phi\bar\eta}
\equiv
\frac{A}{\bar\phi},
\qquad
A\equiv\frac{\beta}{\bar\eta}>0.
}
\tag{8.5.25}
$$

> 这里利用了预算式的影子价格 η 被锚定而变成一个常数的有点，将 C 变成了 φ 的函数，可以方便更加精确地数值分析；

货币增长率越高，消费恰好按照 $1/\bar\phi$ 下降。再代入 CIA：
$$
\frac{M}{p}
=
\frac1{\bar{\hat p}}
=
\bar\phi\bar C
=
A.
\tag{8.5.26}
$$

> （pC = M）有了 C，可以代入计算均衡价格 p；

所以真实货币余额税基完全不变。Bailey curve 因而是：
$$
\boxed{
\bar S(\bar\phi)
=
A\left(1-\frac1{\bar\phi}\right).
}
\tag{8.5.27}
$$

其一、二阶导数为：

$$
\boxed{
\bar S'(\bar\phi)=\frac{A}{\bar\phi^2}>0,
\qquad
\bar S''(\bar\phi)=-\frac{2A}{\bar\phi^3}<0.
}
\tag{8.5.28}
$$

也就是说，基准 Bailey curve：

$$
\boxed{
\text{单调上升，但越来越平缓，并最终逼近 }A.
}
\tag{8.5.29}
$$

它不是倒 U 型。政府购买增加完全来自对私人消费的一比一挤出：

$$
\boxed{
\bar C+\bar G
=
\frac{M}{p}
=
A.
}
\tag{8.5.30}
$$

> 这里直接通过 pG = ∆M 代入计算出 G、再加上已有的 C，算出该结果；
>
> 既然得到了这个结果，那么显然产出总量不变，因此家庭的劳动 h、资本储蓄 k 都是不变的；

进一步，由稳态家庭预算可得：
$$
\frac{M}{p}
=
\bar w\bar H+(\bar r-\delta)\bar K.
\tag{8.5.31}
$$

又因为 $\bar K=q\bar H$，所以：

$$
\boxed{
\bar H
=
\frac{M/p}
{\bar w+(\bar r-\delta)q}.
}
\tag{8.5.32}
$$

在 log utility 下，$M/p$、$\bar w$、$\bar r$、$q$ 全部固定，因此：

$$
\boxed{
\bar H,\bar K,\bar Y,\bar w,\bar r,\bar\eta,\bar{\hat p}
\text{ 均不随 }\bar\phi\text{ 改变}.
}
\tag{8.5.33}
$$

货币增长永久提高后的变化集中表现为：

$$
\boxed{
\bar C\downarrow,
\qquad
\bar G=\bar S\uparrow,
\qquad
\bar\zeta\uparrow.
}
\tag{8.5.34}
$$

> #### 思路直觉
>
> **第一步：预期未来货币增长上升，降低今天持有货币的预期真实回报。**
>
> > 可以看一下 CIA、家庭预算约束，这两个是直接包含有 $\phi_t$ 这个变量的；
> >
> > 当 $\phi_t$ 发生改变时，很显然家庭选择的实际货币余额会发生改变，因为对于 $\hat{m}_t$ 而言，（假设均衡体系没变）它的收益降低了，但是损失却没变，主要体现在影子价格上，增加一单位 $\hat{m}_t$ 带来的影子收益因为乘数减小了，因此收益减小，与此同时损失那一侧的乘子却没变，因此家庭有动力减小 $\hat{m}_t$ ，但我们从整个系统的均衡来说，$\hat{m}_t$ 一定等于 1，因此系统必须进行调整，使得家庭对于货币这一块的收益/损失重新恢复平衡；
>
> 家庭今天选择 $\hat m_t$ 时满足：
> $$
> \frac{\eta_t}{\hat p_t}
> =
> \beta E_t\!\left[
> \frac{\eta_{t+1}+\zeta_{t+1}}
> {\phi_{t+1}\hat p_{t+1}}
> \right].
> \tag{8.5.40}
> $$
>
> 当前的 $\phi_t$ 影响旧货币在当期的购买力和当期 $C_t/G_t$ 分配；预期的 $\phi_{t+1}$ 则直接进入今天的持币 FOC。若冲击具有持续性，家庭预期未来 $\phi_{t+1}$ 也较高，于是货币的预期金融回报下降。为了让家庭在货币市场出清时仍愿意持有 $\hat m_t=1$，右边必须通过其他内生变量得到补偿。
>
> > 等式左边就是多持有一单位真实货币给本期的预算约束带来的损失；
> >
> > 等式右边就是～给下一期的: (1).预算约束带来的影子收益；(2).CIA 约束带来的影子收益；因此实际上这边有两块收益；
>
> **第二步：价格不可能一直变动**
>
> 回去看看 CIA 约束以及家庭预算约束，其实可以发现对于上一期的货币储备，除了 $\phi$ 会降低其乘子系数、如果我们提高一点 $p$ 能不能把这块由于乘子降低导致持币收益降低的部分补回来呢？
>
> 我们可以这么去想，比如 $\hat{p}_{t+1}$ 降低、$\hat{p}_t$ 增加/不变，那么这样是不是可以重新把平衡补回来？确实可以，但是这个不是我们想要的均衡，因为在原来的均衡中，我们有 $\hat{p}_{t+1}=\hat{p}_t=p^*$，如果我们要增大收益来维持平衡，那么就需要让 $\{\hat{p}\}$ 序列保持单调下降，这个一直到最后就接近 0 了，**<u>这个不是我们想要的均衡</u>**；
>
> > 我们理想中的均衡都是变量保持不变 or 维持固定增速，不是这种逐渐降低到 0 的，因为这种奇异值往往会导致变量爆炸，不符合经济定义的合理性要求 or TVC；
> >
> > - 我们也可以举出反例，如果 p 不断接近与 0，那么显然最后 CIA 一定不会 bind，否则 c 就趋近于无穷大，这显然是不可能的；
>
> **第三步：消费下降提高总边际效用，但增加的影子价值不会平均分配给两个乘子。**
>
> > 整体思路：
> >
> > 如果 p 不行那怎么办呢？只能想办法增加未来的影子价格，这样即便乘子减小了，只要影子价格增加，依然可以存在平衡效果；这次就需要吸取 p 的教训，一般稳态要求而言都是 “一起变动” 的，也就是说你不可能要求 “未来的变量增加/减少”，同时现期的变量 “不变”，要么就一起增加、要么就一起减小，毕竟这是均衡的要求：$c_{t+1}=c_t=c^*$；
> >
> > 在这个思路下，我们假设消费 c 降低，这样由于 c 的收益直接连接到效用函数、loss 连接到两个约束函数上，因此对于 c 而言，其边际收益是分配给两个约束的影子价格的（$u_c=λ+μ$，前者 λ 是预算式的影子价格、后者 μ 是 CIA 的影子价格）；
> >
> > 因此如果 c 减小，那么 c 的边际收益增加，因此 CIA 的影子价格 + 家庭预算约束的影子价格（二者之和）会增大，但同时由于劳动 ht 的连通器作用，ht 的边际劳动效用损失，会强制等于家庭预算约束的影子价格 λ（也就是增加一单位劳动的收益），因此 “家庭预算约束的影子价格 λ ” 其实变动不会很大，因为λ要同时等于从消费 c 上面分配得来的收益以及劳动的边际效用损失，（相当于是说 c 的变动会导致 λ 产生变动倾向，但是劳动 h 的存在会 “减缓/拖慢” 这种变动）因此 λ 的变动会更小一些，所以 c 减小导致的边际收益的增加，大部分都分配给了 CIA 的影子价格。所以对于家庭而言，其每增加一单位持币的收益会增加（下一期的预算式+CIA 约束的影子价格 λ + μ），同时其损失增加不大（本期的预算式的影子价格 λ），这样就能够继续达成平衡；
> >
> > - 事实上，由于我们这里是 indivisible labor，劳动的边际福利损失是固定值，因此 ht 的连通作用，相当于强制固定了预算式的影子价格 λ，此时 λ 就是一个不变的量，因此 $u_c$ 带来的改变会全部被 CIA 的影子价格 μ 吸收；
>
> **第四步：Bailey 曲线的变动**
>
> $S_t=\left(1-\frac{1}{\phi_t}\right)\frac{M_t}{p_t\\}=\left(1-\frac{1}{\phi_t}\right)\frac{1}{\hat{p}_t\\}$
>
> > 这个还是要通过均衡方程组里面的关系来确定，基本方法思路就是逐个逐个地**<u>定性</u>**变量的变化方向，例如我们确定了 c 的变动、劳动 h 的变动...依次这样来看。当然有些时候不好定性分析，确实就没办法心算了。
>
> - 先上升
>
>     St 其实就是政府购买 Gt，我们知道 c 是下降的、劳动投入 h 是增加的、现在关键就是资本 k 会如何变化，假设我们知道 k 也增加，那么显然产出总量会增加、消费 c 又不高，那么肯定政府拿走的就多；
>
>     资本 k 是联系前后两期的家庭约束的变量，虽然稳态的 c 会下降，但是前后两期一起下降，因此两期之间的影子价格的相对比值其实还是不变，依然是折现值 β。现在我们知道劳动 h 一定增加，那么此时资本边际产出就会增加，这会让利率增加，也就是增大了未来的预算约束式里面资本 k 的乘数系数，使得未来的 k 更“值钱”，导致储蓄增加，因此 k 一定会增加，并且由于我们的生产函数的特点，k 增加的比例肯定是跟 ht 一样的。
>
> - 后下降？
>
>     那么为什么说到后面 Bailey 曲线会下移？我们需要注意到一点：ht 的增加是有极限的，它最多到 1，再多就触及到上限了，因此当这个过程进行到一定程度时，劳动力触顶，因此 “劳动力 ht 对预算约束式的调节能力到顶了，影子价格不再等于边际劳动的效用损失”。这个时候影子价格仅由消费的边际效用来决定了。
>
>     但是需要注意的是，在这个时候，资本的跨期 “联通器” 的作用依然存在，因此资本配合 ht 到顶之后它也就不动了，此时产出真正到顶，Gt 应该是不会增加了（反正肯定不会减少），毕竟 ct 应该也是不会降低了（没有仔细检查过）；
>
>     **<u>因此在我们这个基础模型里面，Bailey curve 是不会下降的</u>**！
>
> - ##### 更加需要注意的！！
>
>     在 indivisible labor 里面，劳动的边际损失是一个常数，因此这就代表了在 ht 还没有触顶的时候，家庭预算约束式的影子价格一定是不变的！因此消费减少带来的的边际效用的增加全都分给 CIA 的影子价格了（$u_c=λ+μ$，$λ=λ_{fix}$）；
>
>     因此当货币供给增速永久增加后，实际上劳动 h 是不会变的、因此资本 k 也不变、产出也不变，政府只是拿走了消费者的那部分减少的消费所节约下来的东西



##### 3. CES 下为什么 Bailey curve 有可能先增后降？

> 需要注意，CES 效用只是改变了消费 c 对效用的影响，劳动的损耗完全一样，indivisible labor、固定边际损失；

现在只改变消费效用的曲率，仍然保留 indivisible labor：
$$
\boxed{
u(C,H)
=
\frac{C^{1-\sigma}-1}{1-\sigma}+BH,
\qquad
\sigma>0.
}
\tag{8.5.49}
$$

其中：

$$
u_C=C^{-\sigma},
\qquad
u_H=B.
$$

> 剧透：CES 改变 Bailey 曲线的主要渠道并不是跟固定的 indivisible labor 有关，最主要的渠道其实很简单：为了扳回 mt 失控的平衡，我们需要减少消费、增加现期的两个预算式的影子价格。(1).如果需要降低很多 c 才能达到效果，那么 c + G -> Y 就会导致产出减少；(2).如果只需要降低一点点 c，那么最终产出就会增加；

> 以前我们的惯性就是通过价格来判断数量，比如依赖于工资-劳动关系，工资涨了那肯定是劳动力的数量增加了（导致劳动的边际损耗高了、进而才会需要高工资补偿），但是固定损耗情况下，这种判断不再可靠。 所以其实本质就在于 c 需要降低多少来补上这个货币的边际收益、损失的不平衡。

稳态货币 FOC 与消费 FOC 给出：

$$
\bar\eta
=
\frac{\beta}{\bar\phi}\bar C^{-\sigma}.
\tag{8.5.51}
$$

> (8.5.24) 的翻版；

因此：
$$
\boxed{
\bar C(\bar\phi)
=
\left(\frac{\beta}{\bar\eta}\right)^{1/\sigma}
\bar\phi^{-1/\sigma}
\equiv
A_\sigma\bar\phi^{-1/\sigma}.
}
\tag{8.5.52}
$$

这条式子就是 CES 分析的核心：货币增长提高后，货币 FOC 要求 $u_C$ 上升；$\sigma$ 决定<u>**为了产生足够大的边际效用，消费必须下降多少**</u>。

由 CIA：

$$
\boxed{
\frac{M}{p}
=
\frac1{\bar{\hat p}}
=
\bar\phi\bar C
=
A_\sigma\bar\phi^{\,1-1/\sigma}.
}
\tag{8.5.53}
$$

因此，消费的下降速度会通过 $\bar\phi\bar C$ 直接转化为真实货币余额税基的变化。

所以真正的数量传导链是：

$$
\boxed{
\bar C\text{ 相对于 }1/\bar\phi\text{ 的下降速度}
\Longrightarrow
\frac{M}{p}=\bar\phi\bar C
\Longrightarrow
\bar H,\bar K,\bar Y.
}
\tag{8.5.55}
$$

铸币税收入为：

$$
\boxed{
\bar S(\bar\phi)
=
\left(1-\frac1{\bar\phi}\right)\frac{M}{p}
=
A_\sigma(\bar\phi-1)\bar\phi^{-1/\sigma}.
}
\tag{8.5.56}
$$

求导：

$$
\boxed{
\bar S'(\bar\phi)
=
\frac{A_\sigma}{\sigma}
\bar\phi^{-1/\sigma-1}
\left[1+(\sigma-1)\bar\phi\right].
}
\tag{8.5.57}
$$

于是出现三个清楚的分支。

**当 $\sigma=1$ 时：log utility**

$$
\bar C\propto\bar\phi^{-1},
\qquad
\frac{M}{p}=\text{常数}.
$$

所以 Bailey curve 单调上升并趋于上限。

**当 $\sigma<1$ 时：可能出现先增后降**

此时：

$$
\frac1\sigma>1,
$$

所以消费下降得比 $1/\bar\phi$ 更快：

$$
\bar C\propto\bar\phi^{-1/\sigma}.
$$

消费边际效用曲线相对较平，消费下降一点不能产生足够大的 $u_C$。为了让 CIA 影子价格上升到足以补偿货币回报损失的程度，消费必须大幅收缩。于是：

$$
\boxed{
\bar\phi\bar C=\frac{M}{p}\downarrow,
}
\tag{8.5.58}
$$

并带动：

$$
\bar H,\bar K,\bar Y\downarrow.
$$

Bailey curve 的峰值满足：

$$
1+(\sigma-1)\bar\phi=0,
$$

即：

$$
\boxed{
\bar\phi^*
=
\frac{1}{1-\sigma}.
}
\tag{8.5.59}
$$

当 $\bar\phi<\bar\phi^*$ 时，税率上升效应占主导，铸币税收入增加；当 $\bar\phi>\bar\phi^*$ 时，真实余额税基收缩得更快，铸币税收入下降。

**当 $\sigma>1$ 时：税基不降反升**

消费只需下降较小幅度，就能产生足够大的边际效用上升。因此：

$$
\bar C\text{ 下降得慢于 }1/\bar\phi,
\qquad
\bar\phi\bar C=\frac{M}{p}\uparrow.
$$

在内点解仍然有效的范围内，劳动、资本和产出也随真实余额规模上升，Bailey curve 不会出现下降段。

所以 CES 分析最终可以压缩成一句话：

$$
\boxed{
\text{关键不是消费会不会下降，而是为了补上持币收益—成本缺口，}
\ C\text{ 必须相对于 }1/\phi\text{ 下降多少。}
}
\tag{8.5.60}
$$

- 若下降得更快：真实货币余额、劳动、资本和产出收缩，Bailey curve 可能先升后降；
- 若恰好按 $1/\phi$ 下降：税基固定，Bailey curve 上升并趋于上限；
- 若下降得更慢：税基扩大，Bailey curve继续上升。

![Figure 8.4 — Bailey curve for seigniorage](../Figures/Ch08/figure_8_4_bailey_curve.png)

表 8.5 给出标准 seigniorage economy 的矩阵数值：

![Table 8.5 — Matrix values for the standard seigniorage economy](../Figures/Ch08/table_8_5_matrix_values_standard.png)

进入 LQ 或 log-linear solution 时，方法本身不变：删除家庭约束中的 transfer，加入政府预算 $p_tG_t=M_t-M_{t-1}$，并把资源约束改为 $C_t+K_{t+1}+G_t=Y_t+(1-\delta)K_t$，然后对上述完整均衡系统求稳态并作局部近似。



### 2.9 CES appendix：为什么换效用函数会改变 Bailey curve？

第 8.7 节附录讨论 CES utility functions。它的作用是说明：seigniorage 和 inflation 的结论并不只由 cash-in-advance constraint 决定，也取决于 household 对消费和 real balances 的替代弹性。

在 log utility 情形下，家庭对现金约束下消费的反应有一种特殊比例结构，导致一些稳态关系非常简洁。换成 CES utility 后，通胀变化会改变真实货币余额需求，Bailey curve 的形状也会随 elasticity 改变。

图 8.5 展示不同 CES 参数下的 Bailey curves：

![Figure 8.5 — Bailey curves under CES utility](../Figures/Ch08/figure_8_5_ces_bailey_curves.png)

图 8.6 展示不同 seigniorage 水平下的 utility：

![Figure 8.6 — Utility with seigniorage](../Figures/Ch08/figure_8_6_utility_with_seigniorage.png)

表 8.6 给出 CES economy 下的矩阵数值：

![Table 8.6 — Matrix values for the CES economy](../Figures/Ch08/table_8_6_matrix_values_ces.png)

这部分不是本章主干求解的必要条件，但对理解货币模型很重要：货币政策和通胀税的 welfare effect 往往取决于货币需求弹性。如果真实余额需求对通胀很敏感，政府提高货币增长不一定能持续提高 seigniorage revenue，因为税基会快速缩小。

### 2.10 Appendix on matrix quadratic equations

本章最后还给出矩阵二次方程的技术附录。它服务于 LQ 和 log-linear solution 中出现的矩阵求解问题。宏观直觉层面，你只需要知道：许多动态线性系统最后都会化成“找到稳定根 / stable matrix solution”的问题。

如果你的目标是阅读经济机制，可以先跳过这部分。如果你的目标是复现代码，则必须回到原文核对矩阵方程、特征值选择和变量排序。很多 DSGE 解法的数值错误不是来自经济逻辑，而是来自把 predetermined variables、jump variables 和 exogenous states 的顺序放错。

## 3. Compact Summary: What You Must Retain

本章最重要的内容可以压缩成六点。

第一，cash-in-advance constraint 让 money 产生真实效应。消费必须用事先持有的 cash 购买，因此通胀提高了消费交易的机会成本。

第二，加入 money 后，模型从简单 planner problem 转向 competitive equilibrium problem。需要同时处理家庭最优、企业边际产品定价、货币供给、价格水平和 aggregation consistency。

第三，稳态下更高的 money growth / inflation 会降低 consumption、capital、hours 和 output，并带来 welfare loss。表 8.1 和表 8.2 是这一结论的核心证据。

第四，在 log-linear CIA model 中，aggregate CIA constraint 给出关键关系：

$$
\tilde p_t+\tilde C_t=0.
$$

它说明 normalized price level 和 real consumption 在约束下反向运动。

第五，技术冲击仍然是主要 real fluctuation driver；money growth shock 对 price level 更直接，对真实变量影响相对有限，而且因为 money growth process 的 persistence 较低，冲击消退更快。

第六，seigniorage 把货币增长变成财政收入工具。它会产生 Bailey curve：通胀税率上升一开始可能增加收入，但过高通胀会压缩真实货币余额需求，导致税基萎缩。

## 4. Figures, Tables, and Formulas to Check in the Original

本章最应该对照原文检查的是以下内容。

> ⚠️【需要回原文看图】这里涉及重要图表/表格/公式，PDF 文本提取可能不足以完整保留信息。建议回到原文核对。

**Table 8.1** 给出不同 money growth rate 下的 stationary state。重点看 consumption、capital、hours 和 output 如何随 $\bar g$ 上升而下降。

**Table 8.2** 把通胀率、稳态变量和 welfare loss 放在一起，是本章最重要的定量结果表。

**Table 8.3** 和 **Table 8.4** 分别给出 CIA model 的 standard errors 和 correlations。重点看 money shock volatility 增加后，价格变量和真实变量的反应差异。

**Figure 8.1** 和 **Figure 8.2** 对比 Hansen real model 与 Cooley-Hansen CIA model 对技术冲击的响应。

**Figure 8.3** 展示 money growth shock 的 impulse response，是理解货币冲击动态的核心图。

**Figure 8.4** 是 Bailey curve，展示 seigniorage revenue 与 inflation / money growth 的非线性关系。

**Figure 8.5、Figure 8.6、Table 8.6** 属于 CES appendix，主要用于理解效用函数弹性如何改变货币需求、seigniorage 和 welfare conclusions。

需要特别核对的公式包括：

$$
\hat p_t c_t^i=\frac{\hat m_{t-1}^i+(g_t-1)}{g_t},
$$

$$
\bar{\hat p}\bar C=1,
$$

$$
\tilde p_t+\tilde C_t=0,
$$

以及 seigniorage 版本中的政府预算约束：

$$
\bar g\hat g_t=\frac{1-1/\phi_t}{\hat p_t}.
$$

如果要复现本章 Matlab code，还必须逐项检查变量顺序。尤其是 LQ 解法中 individual variables 与 economy-wide variables 并存，最容易出现维度和排序错误。

## 5. Questions and Answers

**Q1：为什么加入 money 后不能简单用 Robinson Crusoe planner problem？**

因为 money model 涉及价格水平、工资、租金、货币供给和个体持币决策。家庭把这些市场变量当作给定，但均衡中它们又必须由 aggregate decisions 决定。planner shortcut 在很多 real RBC 模型中成立，是因为福利定理可以把竞争均衡对应到社会规划问题；加入交易摩擦后，这个捷径不再那么直接。

**Q2：cash-in-advance constraint 到底约束了什么？**

它约束的是消费品购买。家庭不能用当期劳动收入直接购买当期消费，而必须用期初已经可用的 cash。投资品在本章设定中不受同样的 CIA 约束，因此货币摩擦主要通过消费和劳动选择影响真实经济。

**Q3：为什么要把 money 和 price 都除以 $M_t$？**

因为 nominal money supply 和 nominal price level 会随货币增长长期上升，直接建模会产生非平稳变量。用 $M_t$ 标准化后，模型转向 stationary ratios，便于求稳态和 log-linearization。

**Q4：为什么更高通胀会降低 output 和 hours？**

在 CIA model 中，通胀提高了持有 cash 的机会成本，而 cash 是消费的必要条件。家庭面对更高 inflation tax，会降低受现金约束影响的消费和劳动供给，进而降低产出、投资和资本积累。

**Q5：货币增长冲击为什么不像技术冲击那样强烈影响真实变量？**

技术冲击直接改变生产函数和边际产品，因此会强烈影响劳动、投资和资本积累。货币增长冲击主要通过 CIA constraint 和价格水平发挥作用。在本章校准下，它对真实变量的影响较小，而且 money growth process 的 persistence 低于 technology process，所以响应衰减更快。

**Q6：seigniorage 和 lump-sum money transfer 的区别是什么？**

lump-sum transfer 版本中，新发行货币被转移给家庭；seigniorage 版本中，政府用新发行货币直接购买商品和服务。后者会占用真实资源，因此更像一种财政融资方式，也更直接地引出 inflation tax 和 Bailey curve。

**Q7：Bailey curve 为什么可能先上升后下降？**

seigniorage revenue 可以粗略理解为 inflation tax rate 乘以 real money balance tax base。通胀上升会提高税率，但也会降低公众愿意持有的真实货币余额。当税基收缩效应超过税率上升效应时，seigniorage revenue 就会下降。

**Q8：CES appendix 的意义是什么？**

它说明货币模型结论依赖货币需求弹性。log utility 给出一些非常简洁的比例关系，但这可能过于特殊。CES utility 允许替代弹性变化，从而改变 Bailey curve 和 welfare loss 的形状。
