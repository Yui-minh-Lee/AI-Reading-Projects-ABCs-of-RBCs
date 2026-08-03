# Chapter 6 — Lecture Note

> Importance: ★★★★★  
> Suggested audit model: xhigh  
> Reading mode: careful  
> Estimated note reading time: 110-140 minutes  
> Source reliability: text OK; major figures/tables embedded as source screenshots; matrix formulas and appendix derivations should be checked against the original before coding

## 0. How to read this note

这一章是全书前半部分的技术核心，也是标准 RBC 学习路径中的一个“瓶颈章”。第 5 章告诉我们如何把随机状态放进递归模型；第 6 章真正把这个思路应用到 Hansen 的 RBC model，并展示现代动态宏观模型的一整套工作流：写出家庭或 planner 的优化问题，求一阶条件和稳态，围绕稳态 log-linearize，把非线性随机系统变成线性系统，校准参数，求 linear policy rules，计算模型变量的方差和相关性，最后画 impulse response functions。

读这一章时建议把注意力放在三条主线上。

第一，**经济模型主线**：Hansen 先给出一个 divisible labor 的基本 RBC 模型，再改成 indivisible labor 模型。两者的生产函数、资本积累和技术冲击很像，真正不同的是劳动供给的效用结构。这个小改动会改变劳动供给对冲击的反应弹性，从而改善模型对美国数据中 hours 和 investment 波动的匹配。

第二，**求解技术主线**：直接 value function iteration 会遇到状态维度问题，尤其技术冲击是持久的随机过程时，外生状态不再只是两个离散点。因此作者采用 log-linearization，把模型在 stationary state 附近近似成线性系统，再用 Uhlig-style solution method 求解。

第三，**模型评估主线**：RBC 模型的成败不是看它能不能写出漂亮的 Bellman equation，而是看它能否在合理校准下生成类似真实经济的 second moments 和 impulse responses。表 6.1-6.4 与图 6.4-6.8 就是这一章的评估核心。

这一章后续学习时可以配合几份额外讲义，但不需要一开始全部读完。遇到对应卡点时再回看即可：

- 对 log-linearization 和期望算子不清楚时，看 [stochastic_RBC_log_linearization.md](stochastic_RBC_log_linearization.md)。
- 对 calibration 流程和第六章数值从哪里来不清楚时，看 [calibration_revised.md](calibration_revised.md)。
- 对 TVC 为什么排除爆炸路径不清楚时，看 [TVC intuition.md](<TVC intuition.md>)。
- 对 BK 条件、Schur/QZ、稳定流形和 jump variables 不清楚时，看 [Schur_method.md](Schur_method.md)。

## 1. Opening: 本章的核心问题

Kydland and Prescott 的早期 RBC 模型可以生成较强的 persistence 和 amplification，但它包含 time to build、带有过去 leisure 的效用、inventories、临时和永久技术冲击等多个复杂机制。模型能匹配一些数据事实，但很难判断到底是哪一个机制在起作用。

Hansen 的贡献是提供两个更清晰的 benchmark models：一个是标准的 stochastic variable labor model，另一个在几乎相同结构上加入 indivisible labor。Hansen 的目标不是建一个包罗万象的模型，而是检验：**仅仅把劳动供给从连续可调改成带有 indivisibility 和 lottery / insurance 的结构，能否明显提高 RBC 模型匹配美国宏观波动的能力？**

因此，本章要回答三个问题：

1. Hansen 的 basic RBC model 如何写成 Bellman equation，并如何得到 FOCs 和 stationary state？
2. 如何把这个非线性随机动态模型 log-linearize，并求得线性 laws of motion？
3. indivisible labor 为什么会改变模型的波动性质，尤其为什么会让 hours worked 的相对波动更接近数据？

## 2. Main Lecture

### 2.1 Hansen basic model：从 Robinson Crusoe 到 stochastic labor RBC

Hansen 的 basic model 可以理解为第 4 章带劳动选择的 Robinson Crusoe 模型加上第 5 章的 stochastic technology shock。一个代表性 agent 最大化：

$$
\max \sum_{t=0}^{\infty}\beta^t u(c_t,l_t),
$$

其中 $l_t=1-h_t$ 是 leisure，$h_t$ 是 labor。具体效用函数为：

$$
u(c_t,1-h_t)=\ln c_t+A\ln(1-h_t),\quad A>0.
$$

生产函数是 Cobb-Douglas，并带有随机技术：

$$
f(\lambda_t,k_t,h_t)=\lambda_t k_t^\theta h_t^{1-\theta}.
$$

技术过程写成：

$$
\lambda_{t+1}=\gamma\lambda_t+\varepsilon_{t+1},\quad 0<\gamma<1.
$$

书中设定冲击有界、正且均值为 $1-\gamma$，因此 $\lambda_t$ 的均值为 1，并避免产出为负。资本积累为：

$$
k_{t+1}=(1-\delta)k_t+i_t,
$$

可行性约束为：

$$
\lambda_t k_t^\theta h_t^{1-\theta}\geq c_t+i_t.
$$

把投资消去后，消费可写为：

$$
c_t=\lambda_tk_t^\theta h_t^{1-\theta}+(1-\delta)k_t-k_{t+1}.
$$

于是 Bellman equation 是：

$$
V(k_t,\lambda_t)=\max_{k_{t+1},h_t}\left\{
\ln\left(\lambda_tk_t^\theta h_t^{1-\theta}+(1-\delta)k_t-k_{t+1}\right)+A\ln(1-h_t)
+\beta E_t[V(k_{t+1},\lambda_{t+1})\mid \lambda_t]\right\}.
$$

这里 state variables 是 $k_t$ 和 $\lambda_t$，control variables 是 $k_{t+1}$ 和 $h_t$。经济含义很清楚：今天看到资本和技术后，agent 决定劳动和储蓄；未来价值取决于下一期资本和下一期技术，而下一期技术是随机的。

### 2.2 FOCs：Euler equation 和劳动-消费权衡

对 $k_{t+1}$ 的一阶条件表达了跨期消费-储蓄权衡。书中将其整理后可写为：

$$
\frac{1}{c_t}=\beta E_t\left[\frac{r_{t+1}+1-\delta}{c_{t+1}}\mid \lambda_t\right],
$$

> #### 这是什么意思？
>
> 我们不妨泛化一下：直接列出非递归形态下的 Euler Equation：
> $$
> U^′(c_t)=β·E_t[U^′(c_{t+1})·\big(f_k(k_{t+1},λ_{t+1})+(1−δ)\big)]
> $$
>
> - 思想/来源：与确定性模型中的是一样的，当期多消费一单位带来一个 gain，即当期的边际效用增加；但是这同时会给当期的预算约束方程带来压力，这个压力传导至 $k_{t+1}$ 这会要求降低下一期的消费 $c_{t+1}$，因此需要达到一个平衡：当期的效用增加 = 下一期效用损失的**<u>预期</u>**，这个就是该 Euler 方程的由来。至于期望，这是因为给定 $k_{t+1}$ 的压力之后，在不同的 case 下会导致不同程度的 $c_{t+1}$ 的减少，在不确定情况下，那么就只能追求 Gain = $E_t$[Loss]；
>
> - 递推关系：我们在这个 Euler 方程的基础上，不妨进行一些简化：
>     $$
>     c_{t}=E_t[F(c_{t+1},\lambda_{t+1},k_{t+1})]
>     $$
>     注意这里跟确定性情况下有本质的不同，这里是带期望的，而并不是一个确定性的迭代方程、因此也不能够确定 $c_{t+1}$ 的取值，因此并不是 “ct、k\_{t+1}、λ\_{t+1} 一起来确定 c\_{t+1} 的取值”，而是 “c\_{t+1} 的期望与k\_{t+1}、λ\_{t+1} 一起决定 ct”（因为 k）
>
>     > - 因此我们要找的 ct 依然是一个“政策函数”，$c_t = g(k_t,λ_t)$ 还真没错；
>     >
>     >     这个主要是这么去想的：要确定 c\_{t+1} 的期望，那肯定在每个确定性的子 case 里面，c\_{t+1} 肯定是有某种确定规则的，即 given λ\_{t+1} 之后（再加上当前时刻的信息），肯定能够确定应该选哪个 c\_{t+1}，因此我们应该想到是需要一个政策函数（即 c\_{t+1} 的确定规则）；
>     >
>     > - 将我们猜测的这个函数 “$c_{t}=g(k_t,λ_t)$” 代入这个 Euler equation，理论上就能够得到 g 应该满足的要求（即政策函数 g 必须要满足的自洽性质；类比于 Bellman 递归结构一样，需要满足 bellman 方程、FOC 条件所施加的自洽性要求）
>
> - 最终如何解决？
>
>     - 资源约束方程：都是确定性的，它回答的是，你选好 ct 之后，kt+1 怎么变，这个没有难度；
>     - Euler 方程：这个涉及到向未来的预期，你得先有了预期之后，才能够确定好应该选哪个 ct，这个是困难所在；
>
>     困难如何解决？对于这种带期望的递推，一般是这样，我们先假设一个抽象的函数形式 $c_t = g(k_t,λ_t)$，然后把这个 g 函数代入到 Euler 方程中，看 g 函数应该满足哪些性质，这样就解出来了所有符合要求的 g 函数。
>
>     更加具体一点的话，**<u>例如在对数线性化里面</u>**，通过 Schur 方法，首先求出稳定方向，然后令 ct 必须要配合好 kt，这样就相当于强行规定了 ct 的政策函数（一个 kt、λt 的线性函数），然后我们把这个现行政策函数代入递归结构就能够求出系数矩阵；因此实际上为了简化，我们可以不使用抽象的函数形式去求一个复杂的期望，有时候可以进行线性近似化，不光是对 Euler 方程的 F 函数进行简化，也对政策函数 g 进行简化，这样就能直接线性地计算出期望。

其中资本租金等于资本边际产出：
$$
r_t=\theta\lambda_tk_t^{\theta-1}h_t^{1-\theta}.
$$

这个 Euler equation 的含义是：今天少消费一单位，增加下一期资本，明天得到资本租金加未折旧资本；但明天的回报和消费边际效用都受随机技术影响，所以要取条件期望。

对劳动 $h_t$ 的一阶条件可以写成：

$$
(1-h_t)w_t=Ac_t,
$$

其中工资等于劳动边际产出：

$$
w_t=(1-\theta)\lambda_tk_t^\theta h_t^{-\theta}.
$$

这条式子是劳动-闲暇权衡。劳动多一点带来工资收入，从而增加消费；但劳动也减少 leisure，带来效用损失。式子中的 $(1-h_t)w_t$ 可以理解为闲暇边际效用与消费边际效用调整后的劳动机会成本，而右边 $Ac_t$ 来自 leisure 在效用中的权重。

为了后面 log-linearize，作者把模型改写成 aggregate variables，并使用 competitive factor prices：

$$
1=\beta E_t\left[\frac{C_t}{C_{t+1}}(r_{t+1}+1-\delta)\right],
$$

$$
(1-H_t)(1-\theta)\frac{Y_t}{H_t}=AC_t,
$$

$$
C_t=Y_t+(1-\delta)K_t-K_{t+1},
$$

$$
Y_t=\lambda_tK_t^\theta H_t^{1-\theta},
$$

$$
r_t=\theta\frac{Y_t}{K_t}.
$$

这五条方程包含了 Euler equation、劳动供给条件、资源约束、生产函数和资本租金定义，是 basic Hansen model 的核心系统。

> 其实可以这么看，主方程就是前面两个；后面三个是解释性的，因为对于我们研究的问题而言，state variable 是 kt、control variable 是 k\_{t+1}, ht，这些变量就足够问题的研究了。但是为了清晰，我们又引入了 ct、r\_{t} 这些新变量（后面还有 yt），因此需要后续三个解释方程来解释这些引入的新变量；

### 2.3 Stationary state：先定长期位置，再研究附近动态

在 stationary state 中，$K_t=K_{t+1}=K_{t+2}=\bar K$，$H_t=H_{t+1}=\bar H$，随机技术等于均值 $\bar\lambda=1$。由于没有不确定性，expectation operator 在稳态条件下消失。

> 直接假设经济已经处在动态，那么 state variable、control variable 都不随时间改变（or 某些情况下可能是维持一个不变的增长率），然后求解出稳态；

资本 Euler equation 给出稳态资本回报：

$$
\frac{1}{\beta}=\bar r+1-\delta.
$$

因此：

$$
\bar r=\frac{1}{\beta}-(1-\delta).
$$

结合 $\bar r=\theta\bar Y/\bar K$ 和生产函数，可以求得资本-劳动比，并进一步得到稳态资本：

$$
\bar K=\bar H\left[\frac{\theta\bar\lambda}{1/\beta-(1-\delta)}\right]^{1/(1-\theta)}.
$$

劳动稳态来自劳动供给条件。作者给出的形式是：

$$
\bar h=
\frac{1}{1+\frac{A}{1-\theta}\left(1-\frac{\beta\delta\theta}{1-\beta(1-\delta)}\right)}.
$$

这条式子很适合理解参数作用。$A$ 越大，leisure 的效用权重越大，稳态劳动越低；$\theta$ 和 $\delta$ 通过生产和资本回报影响劳动与消费的长期权衡。

### 2.4 为什么不直接用 value function iteration？

第 5 章已经告诉我们，可以把随机状态放进 value function，然后对不同状态分别迭代。但 Hansen 模型的技术过程不是简单二状态独立过程，而是：

$$
\lambda_{t+1}=\gamma\lambda_t+\varepsilon_{t+1}.
$$

即使 $\varepsilon_{t+1}$ 只有两个可能值，$\lambda_t$ 的可能取值也会随着时间不断扩张。若从 $\lambda_t=1$ 出发，下一期有两个值，再下一期最多有四个值，$n$ 期后可能有 $2^n$ 个值。直接把所有可能技术状态都放进网格，很快就遇到维度问题。

当然，现代计算可以在 $K$ 和 $\lambda$ 上设定二维网格，用插值迭代 value function。但一旦模型加入更多状态变量，例如货币、价格、债券、外生政策规则，直接动态规划会迅速变得昂贵。于是本章采用当时以及后来 DSGE 文献中非常常用的办法：**围绕 stationary state 做 log-linear approximation。**

> 第 5 章能直接做 VFI，是因为外生随机状态很少；第 6 章的技术冲击是 AR(1) 连续过程，value function 是 $V(k,\lambda)$ 的二维函数。要用 VFI 就必须把 $\lambda$ 离散化，近似为有限状态 Markov chain（就是说把λ也离散化/网格化），再对 $(k,\lambda)$ 的联合网格做迭代。这样可行，但计算量和插值复杂度明显增加。

### 2.5 Log-linearization 的基本思想

非线性模型很难直接求全局解，但在稳态附近，许多变量可以用一阶近似来描述。log-linearization 的做法是把变量写成稳态的比例偏离：

$$
\tilde X_t=\ln X_t-\ln\bar X.
$$

当 $\tilde X_t$ 很小时，$X_t=\bar X e^{\tilde X_t}\approx \bar X(1+\tilde X_t)$。因此乘法关系可以变成加法关系，幂函数也可以变成系数乘以 log deviation。例如 Cobb-Douglas 生产函数：

$$
Y_t=\lambda_tK_t^\theta H_t^{1-\theta}
$$

log-linearize 后大致变成：

$$
\tilde Y_t=\tilde\lambda_t+\theta\tilde K_t+(1-\theta)\tilde H_t.
$$

这一步的经济含义是：在稳态附近，产出的百分比偏离可以近似写成技术、资本、劳动百分比偏离的线性组合，系数就是生产弹性。

作者在 6.2 节还介绍了 Uhlig 的 log-linearization 方法。它的实用思想是：先把变量写成稳态值乘以指数偏离，例如 $X_t=\bar X e^{\tilde X_t}$；再代入原方程；最后用 $e^{x}\approx 1+x$ 作一阶近似。这样可以系统地把非线性方程转成线性方程，尤其适合写成矩阵系统。

这里有一个容易犯错的地方：如果方程是 Cobb-Douglas 这种乘法关系，直接取 log 很自然；但如果方程是资源约束或资本积累这种加法关系，例如 $Y_t=C_t+I_t$，不能把整条等式直接取 log 后拆开。正确做法仍然是把每个变量写成 $\bar X e^{\tilde X_t}$，代回原方程，再对所有偏离量做一阶 Taylor 展开，并用稳态方程消掉常数项。更细的推导见 [stochastic_RBC_log_linearization.md](stochastic_RBC_log_linearization.md)。

### 2.6 Hansen 模型的 log-linear system

对 basic Hansen model 的五条核心方程 log-linearize 后，得到一个线性系统。作者最终要找的是两条 laws of motion：

$$
\tilde K_{t+1}=P\tilde K_t+Q\tilde\lambda_t,
$$

以及：

$$
y_t=R\tilde K_t+S\tilde\lambda_t,
$$

其中：

$$
y_t=[\tilde Y_t,\tilde C_t,\tilde H_t,\tilde r_t]'.
$$

这两条式子就是模型的 linear policy rules。给定当前资本偏离和技术偏离，第一条决定下一期资本，第二条决定当期产出、消费、劳动和资本租金。

更一般地，Uhlig-style system 可以写成：

$$
0=A x_t+B x_{t-1}+C y_t+D z_t,
$$

$$
0=E_t(Fx_{t+1}+Gx_t+Hx_{t-1}+Jy_{t+1}+Ky_t+Lz_{t+1}+Mz_t),
$$

$$
z_{t+1}=Nz_t+\varepsilon_{t+1}.
$$

这里 $x_t$ 是 endogenous state variable，例如资本；$z_t$ 是 exogenous stochastic state，例如技术；$y_t$ 是一组当期非状态变量，可能包括真正的 jump variables，也可能包括由当期静态条件直接决定的变量，例如产出、劳动、租金等。严格说，control variable 不一定都是独立 jump variable；BK 条件数的是“没有历史给定初值、且具有独立前瞻自由度”的变量，而不是所有当期变量。

目标是求：

$$
x_t=Px_{t-1}+Qz_t,
$$

$$
y_t=Rx_{t-1}+Sz_t.
$$

矩阵 $P$ 通常要通过 matrix quadratic equation 求出。这个步骤是本章技术上最难的地方，但直觉很简单：我们猜测线性政策规则存在，把猜测代回线性系统，要求所有 $x_{t-1}$ 和 $z_t$ 的系数都匹配，于是得到关于 $P,Q,R,S$ 的矩阵方程。

> #### Key: very important idea
>
> 这一步最容易让人困惑：Euler equation / FOC 里面明明有 $K_{t+1},C_{t+1},r_{t+1}$，甚至继续往前还有 $K_{t+2},C_{t+2}$，看起来今天的变量好像依赖于无穷远的未来变量；但解出来以后，policy rule 却写成“当前状态决定当前选择和下一期状态”。
>
> 更准确的理解是：FOC 是均衡必须满足的跨期一致性条件，policy rule 是把这些跨期一致性条件解完以后得到的行为规则。**<u>FOC 里面出现未来变量，不等于 agent 在今天“观察未来变量后再决定今天”。今天能依赖的只能是当前信息，例如当前资本和当前技术状态</u>**。未来变量之所以出现在 FOC 中，是因为今天的选择会改变明天的状态，而明天的 agent 也会按照同一套最优规则行动，为了保证行动规则确实是“最优”，它就要求前后变量之间满足一定的关系，不能够是任意的，表现出来就是 FOC；
>
> 对确定性问题来说，如果当前状态是 $K_t$，递归解要找的是一条规则：
>
> $$
> K_{t+1}=H_K(K_t),\quad C_t=H_C(K_t).
> $$
>
> 一旦这条规则存在，明天也会使用同一条规则：
>
> $$
> K_{t+2}=H_K(K_{t+1}),\quad C_{t+1}=H_C(K_{t+1}).
> $$
>
> 所以 Euler equation 中的未来变量可以被理解为“未来状态经过同一套 policy rule 生成的变量”。不是今天真的被未来牵着走，而是今天的选择必须和未来也会最优行动这件事相一致。
>
> 对随机问题来说，差别不是“先把未来所有随机路径都确定下来，然后逐条算确定性最优路径再加权”。真正的 recursive stochastic plan 是 contingent plan：每一期看到当期状态后重新按同一套规则决策。站在 $t$ 期，当前 $\lambda_t$ 已经观察到，下一期 $\lambda_{t+1}$ 还不确定，所以 continuation value 写成：
>
> $$
> E_t[V(K_{t+1},\lambda_{t+1})\mid \lambda_t].
> $$
>
> 这里的 $V(K_{t+1},\lambda_{t+1})$ 已经把 $t+1$ 以后所有未来随机性下的最优 contingent decisions 压缩进去了。因此在 Markov 设定下，今天只需要对下一期状态 $\lambda_{t+1}$ 的条件分布求期望，而不用在今天显式列出整棵未来随机树。
>
> 因此，第 6 章的 log-linear solution 不是否认“变量之间有跨期依赖”，而是把跨期依赖压缩进状态变量和 policy matrices 中。给定当前 predetermined state 和 exogenous state，例如 $(K_t,\lambda_t)$，模型解告诉我们：
>
> $$
> K_{t+1}=H_K(K_t,\lambda_t),\quad
> C_t=H_C(K_t,\lambda_t),\quad
> H_t=H_H(K_t,\lambda_t).
> $$
>
> 未来当然重要，但未来的重要性已经通过 Bellman equation / rational expectations consistency 体现在这些 policy functions 里。FOC 是“跨期一致性条件”；**<u>policy rule 就是“解完一致性条件（FOC）后，那些所有的行动规则中，筛剩下的、满足最优性关系要求的行动规则，即当前状态到当前选择（state -> action）的映射”</u>**。

> ### 直接列出欧拉方程
>
> 其实可以直接列出非递归形态下的 Euler Equation：
> $$
> U^′(c_t)=β·E_t[U^′(c_{t+1})·\big(f_k(k_{t+1},λ_{t+1})+(1−δ)\big)]
> $$
>
> - 思想是一样的，当期多消费一单位带来一个 gain，即当期的边际效用增加；但是这同时会给当期的预算约束方程带来压力，这个压力传导至 $k_{t+1}$ 这会要求降低下一期的消费 $c_{t+1}$，因此需要达到一个平衡：当期的效用增加 = 下一期效用损失的**<u>预期</u>**，这个就是该 Euler 方程的由来。至于期望，这是因为给定 $k_{t+1}$ 的压力之后，在不同的 case 下会导致不同程度的 $c_{t+1}$ 的减少，在不确定情况下，那么就只能追求 Gain = $E_t$[Loss]；
>

### 2.7 Calibration：参数不是估计出来的，而是按经济含义和数据矩选择

本章采用的参数是 Hansen 标准季度校准：

- $\beta=0.99$：季度贴现因子。
- $\delta=0.025$：季度折旧率。
- $\theta=0.36$：资本收入份额。
- $\gamma=0.95$：技术冲击持久性。
- $A$：leisure 在效用中的权重，用来让稳态劳动约为三分之一。

作者选择 $A$ 的方法很直观：希望 $\bar H\approx 0.3335$，即平均工作时间约为可用时间的三分之一。Figure 6.1 展示不同 $A$ 对应的稳态劳动 $\bar H$，最终选择 $A=1.72$。

![Figure 6.1 — Finding the value for A](../Figures/Ch06/figure_6_1_finding_A.png)

这张图的作用不是展示动态，而是展示校准逻辑：某些参数不是随意给的，而是为了匹配一个稳态目标。RBC 校准经常这样做：**<u>先用长期平均值或外部研究确定一组参数，再用某些 moments 反推剩余参数</u>**。

更一般地说，如果一个 DSGE / RBC 模型交到你手里，校准通常按下面的顺序做。

第一步，先分清哪些参数可以直接从制度、频率或外部研究中拿。比如季度模型里，折旧率 $\delta$ 常常按季度资本折旧率设定；资本份额 $\theta$ 常用国民收入账户中的资本收入份额；贴现因子 $\beta$ 常用稳态利率反推；技术冲击持久性 $\gamma$ 可以来自对 Solow residual 或 TFP 序列的 AR(1) 估计。

第二步，写出模型的 stationary state equations。校准不是先随便给参数再跑模型，而是先问：这些参数在稳态里决定哪些长期比率？例如 Hansen 模型里，Euler equation 给出稳态资本回报：

$$
\bar r=\frac{1}{\beta}-(1-\delta).
$$

生产函数和 factor prices 又把 $\bar r$ 转成资本-劳动比、资本产出比等对象。也就是说，有些参数不是孤立地定，而是通过稳态方程和一组长期 moments 绑在一起。

第三步，选择 target moments。校准常用的目标不是某一期数据，而是长期平均或比较稳定的宏观比率，例如平均工作时间 $\bar H$、资本产出比 $K/Y$、投资产出比 $I/Y$、消费产出比 $C/Y$、平均利率、劳动收入份额等。Hansen 这里选择 $A$，就是为了让稳态劳动 $\bar H$ 接近数据中的三分之一。

第四步，用剩余参数匹配这些 target moments。一个典型例子是 leisure 权重 $A$。偏好参数 $A$ 很难直接从账户数据里读出来，所以就把它当成“让模型稳态劳动等于数据平均劳动”的自由参数。给定 $\beta,\delta,\theta$ 后，模型稳态劳动 $\bar H(A)$ 是 $A$ 的函数，于是选一个 $A$ 使：

$$
\bar H(A)=H^{data}.
$$

这就是 Figure 6.1 的含义。它不是在估计一个统计回归系数，而是在用一个稳态事实钉住一个偏好参数。

第五步，再处理 shock process。动态冲击参数通常分两类：持久性和波动率。持久性如 $\gamma$ 可以从外生冲击序列的自相关估计；波动率 $\sigma_\varepsilon$ 常常被选择为让模型生成的某个核心变量波动率匹配数据。Hansen 后面就是选择技术冲击标准差，使模型产出标准差匹配美国数据，然后再看消费、劳动、投资等相对波动是否也能匹配。

所以校准的实用口诀是：**先定频率和外部参数，写稳态方程，选长期 moments，反推难以直接观察的偏好/技术参数，再用 shock 参数匹配动态 moments，最后检验未被用来校准的 moments。** 如果模型只匹配了被拿来校准的目标，不算太有说服力；真正的检验在于它能否同时解释没有被直接钉住的 second moments、correlations 和 impulse responses。

如果想把本章的数值从头手算一遍，尤其是 $A$、稳态变量、shock size 和 indivisible labor 的 $h_0$，可以直接看 [calibration_revised.md](calibration_revised.md)。第六章正文只保留主线，完整算账放在那份额外讲义里更清楚。

### 2.8 Basic model 的 second moments：哪里成功，哪里失败

求得 $P,Q,R,S$ 后，可以把模型写成一套线性随机系统。技术冲击满足：

$$
\tilde\lambda_t=\gamma\tilde\lambda_{t-1}+\varepsilon_t.
$$

资本和其他变量对技术冲击的反应由政策矩阵决定。作者进一步选择技术冲击的标准差 $\sigma_\varepsilon$，使模型产出的标准差匹配 Hansen 对美国数据估计得到的产出波动。然后计算消费、劳动、租金、投资等变量的相对标准差。

![Table 6.1 — Standard errors from model](../Figures/Ch06/table_6_1_model_standard_errors.png)

Table 6.1 显示 basic model 生成的标准差。以产出为 100%，消费约为产出的 74%，劳动约为 30%，投资约为 214%。

![Table 6.2 — Standard errors from Hansen's data](../Figures/Ch06/table_6_2_hansen_data_standard_errors.png)

Table 6.2 是 Hansen 使用的美国数据 moments：消费约为产出的 73%，劳动约为 94%，投资约为 489%。比较两张表可以看出 basic model 的典型问题：**消费波动匹配得还不错，但劳动和投资波动太低。**

这正是 indivisible labor 模型要解决的问题。RBC 模型如果只让每个家庭连续调节工作小时，劳动供给对冲击的反应不够强；如果劳动参与有 indivisibility，aggregate hours 可以通过更多人进入工作而大幅调整，模型就更容易产生劳动波动。

### 2.9 Indivisible labor：为什么一个小改动会改变劳动波动

现实生产往往需要固定班次和团队协作，不是每个人每天可以连续选择工作 0.317 小时、0.328 小时或 0.341 小时。Hansen 的 indivisible labor 假设是：工作的人在一个时期内工作固定时长 $h_0$，不工作的人工作 0；但每个家庭以概率 $\alpha_t$ 工作。因此 aggregate hours 是：

$$
H_t=\alpha_t h_0.
$$

如果没有保险，这会让个体效用集合非凸：工作与不工作之间有跳跃。Figure 6.2 展示了这种 nonconvex set。

![Figure 6.2 — Nonconvex set](../Figures/Ch06/figure_6_2_nonconvex_set.png)

> 💡 Clarification
> Figure 6.2 不是动态路径图，而是在解释个体劳动选择为什么会变成 nonconvex set。横轴可以理解为 wage，纵轴是 goods consumption，灰色区域表示在不同工资下家庭可达到的商品消费集合。在 indivisible labor 中，个体不能选择连续工作时间，而是在“不工作”和“工作固定时长 $h_0$”之间跳变。当工资低于某个临界值 $w^*$ 时，家庭选择不工作，只靠资本收入消费；当工资高过 $w^*$ 时，家庭突然选择工作一个固定班次，于是劳动收入和商品消费向上跳。点 A 和点 B 都可行，但 A、B 之间连线上的一些中间点不可行，因为它们对应“工作一部分固定班次”这类个体无法选择的状态。凸集要求任意两个可行点之间的连线也可行；这里不满足，所以是 nonconvex。Hansen 引入 lottery 和 insurance 的目的，就是把个体层面的离散选择 $h_t^i\in\{0,h_0\}$ 转成 aggregate 层面的连续就业概率 $\alpha_t$，从而让 $H_t=\alpha_t h_0$ 可以平滑变化，并保留“更多人进入工作”这个 extensive margin。

Hansen 的关键设定是加入 lottery 和 insurance。每个家庭事前有相同工作概率，事后无论是否被抽中工作，都通过保险获得相同消费。这样从个体角度看，效用是关于工作概率 $\alpha_t$ 的期望效用；从 aggregate 角度看，劳动供给可以连续变化，因为调整的是工作人口比例，而不是每个工作者的小时数。

推导可以从单个家庭成员的劳动状态开始。若本期被抽中工作，他工作固定时长 $h_0$，leisure 是 $1-h_0$；若没有被抽中工作，他工作 0，leisure 是 1。因为保险使不同劳动状态下的消费被平滑掉，劳动部分的期望效用就是：

$$
\alpha_t A\ln(1-h_0)+(1-\alpha_t)A\ln(1).
$$

由于 $\ln(1)=0$，上式变成：

$$
\alpha_t A\ln(1-h_0).
$$

再利用 aggregate hours 的定义：

$$
H_t=\alpha_t h_0
\quad\Rightarrow\quad
\alpha_t=\frac{H_t}{h_0},
$$

所以劳动相关效用可以写成：

$$
\alpha_t A\ln(1-h_0)
=
A\frac{\ln(1-h_0)}{h_0}H_t.
$$

定义：

$$
B\equiv A\frac{\ln(1-h_0)}{h_0}.
$$

因为 $0<h_0<1$，所以 $\ln(1-h_0)<0$，从而 $B<0$。因此 indivisible labor 模型里的 period utility 可以写成：

$$
u(C_t,H_t)=\ln C_t + B H_t.
$$

这里千万不要把 $B H_t$ 理解成“劳动越多越快乐”。由于 $B<0$，劳动增加仍然降低效用；真正变化的是 marginal disutility 的形状。Basic model 中：

$$
u(C_t,H_t)=\ln C_t + A\ln(1-H_t),
$$

劳动的边际效用成本是：

$$
\frac{\partial}{\partial H_t}A\ln(1-H_t)
=-\frac{A}{1-H_t}.
$$

它会随着 $H_t$ 上升而变得越来越大。也就是说，如果每个人都靠“多干一点小时”来增加劳动，越往后越痛苦。Indivisible labor 加 lottery 后：

$$
\frac{\partial}{\partial H_t}BH_t=B,
$$

边际效用成本是常数。直觉是：aggregate hours 的增加主要来自更多人被抽中工作，而不是已经工作的人继续延长工时；因此宏观劳动调整走的是 extensive margin，而不是 intensive margin。

把这个 utility 放回 planner problem：

$$
\max_{C_t,H_t,K_{t+1}}
\ln C_t+BH_t+\beta E_t[V(K_{t+1},\lambda_{t+1})]
$$

subject to

$$
C_t+K_{t+1}
=
\lambda_tK_t^\theta H_t^{1-\theta}+(1-\delta)K_t.
$$

对 $H_t$ 求一阶条件：

$$
\frac{1}{C_t}(1-\theta)\lambda_tK_t^\theta H_t^{-\theta}+B=0.
$$

因为

$$
Y_t=\lambda_tK_t^\theta H_t^{1-\theta},
$$

所以上式也可以写成：

$$
\frac{1}{C_t}(1-\theta)\frac{Y_t}{H_t}=-B.
$$

这就是 indivisible labor 模型的核心劳动条件。它和 basic model 的劳动 FOC 很像，但少了 leisure term $1-H_t$：

$$
\text{basic model:}\quad
\frac{1}{C_t}(1-\theta)\frac{Y_t}{H_t}
=
\frac{A}{1-H_t}.
$$

这个差别解释了为什么一个看起来很小的劳动设定变化会改变波动结果：在 basic model 中，劳动多了以后 leisure 变少，继续增加劳动的边际成本迅速上升；在 indivisible labor 模型中，aggregate labor 通过就业概率 $\alpha_t$ 调整，边际成本变成常数 $B$，所以劳动对技术冲击的响应会更强。

### 2.10 Indivisible labor 的稳态校准

Indivisible labor 模型需要确定 $h_0$ 和 $\alpha$。作者希望 aggregate labor 仍为 $\bar H=0.3335$，并求得 $h_0\approx 0.583$，对应 $\bar\alpha=\bar H/h_0\approx 0.572$。Figure 6.3 展示了求解 $h_0$ 的图形方法。

![Figure 6.3 — Finding h0](../Figures/Ch06/figure_6_3_finding_h0.png)

这个校准可以从上一节的劳动 FOC 推出来。稳态时 indivisible labor 的劳动条件是：

$$
\frac{1}{\bar C}(1-\theta)\frac{\bar Y}{\bar H}=-B.
$$

整理得：

$$
\bar H
=
-\frac{1-\theta}{B}\frac{\bar Y}{\bar C}.
$$

令

$$
s_C\equiv \frac{\bar C}{\bar Y},
$$

这个 $s_C$ 也来自稳态方程。稳态 Euler equation 给出：

$$
\bar r=\frac{1}{\beta}-(1-\delta)
=
\frac{1-\beta(1-\delta)}{\beta}.
$$

竞争性资本价格满足：

$$
\bar r=\theta\frac{\bar Y}{\bar K},
$$

所以：

$$
\frac{\bar K}{\bar Y}
=
\frac{\theta}{\bar r}
=
\frac{\beta\theta}{1-\beta(1-\delta)}.
$$

稳态中 $\bar I=\delta\bar K$，因此：

$$
s_C
=
\frac{\bar C}{\bar Y}
=
1-\frac{\bar I}{\bar Y}
=
1-\delta\frac{\bar K}{\bar Y}
=
1-\frac{\beta\delta\theta}{1-\beta(1-\delta)}.
$$

则：

$$
\bar H=-\frac{1-\theta}{B s_C}.
$$

而 $B$ 又由 $h_0$ 决定：

$$
B=A\frac{\ln(1-h_0)}{h_0}.
$$

所以 $h_0$ 不是凭感觉选出来的，而是要让 indivisible labor 模型的稳态 aggregate hours 仍然等于 basic model 里校准出来的 $\bar H$。Basic model 的稳态劳动可以写成：

$$
\bar H
=
\frac{1}{1+\frac{A}{1-\theta}s_C}.
$$

要求两个模型有同一个 $\bar H$，得到：

$$
\frac{1}{1+\frac{A}{1-\theta}s_C}
=
-\frac{1-\theta}{\left(A\frac{\ln(1-h_0)}{h_0}\right)s_C}.
$$

把含 $h_0$ 的部分整理到一边：

$$
\frac{h_0}{\ln(1-h_0)}
=
-
\frac{A s_C}{(1-\theta)+A s_C}.
$$

给定本章校准值 $A=1.72,\theta=0.36$，并由稳态方程得到 $s_C\approx 0.7436$，右边约为：

$$
-
\frac{1.72\times 0.7436}{0.64+1.72\times 0.7436}
\approx -0.6665.
$$

因此 $h_0$ 由下面这个方程确定：

$$
\frac{h_0}{\ln(1-h_0)}=-0.6665.
$$

数值解约为：

$$
h_0\approx 0.583.
$$

有了 $h_0$ 后，就能由 $\bar H=\bar\alpha h_0$ 反推出稳态就业概率：

$$
\bar\alpha=\frac{\bar H}{h_0}
\approx
\frac{0.3335}{0.583}
\approx 0.572.
$$

所以这里的校准逻辑是：先保持 basic model 的长期平均劳动 $\bar H$ 不变，再选择固定工作时长 $h_0$，使 lottery 后的线性劳动效用和原模型的稳态劳动目标一致，最后由 $\bar H=\bar\alpha h_0$ 得到就业概率 $\bar\alpha$。

稳态变量如下：

![Table 6.3 — Value of variables in stationary state](../Figures/Ch06/table_6_3_stationary_state_indivisible.png)

这些稳态值与 basic model 接近。原因是 indivisible labor 的校准刻意保留了相同的 $\bar H$，而 $\beta,\delta,\theta$ 也没有变，所以稳态资本回报、资本劳动比、产出、消费和投资都会非常接近。模型真正的差别不在长期均值，而在面对冲击时的动态反应和 second moments。

> ### 【My Step】
>
> 1. 列出 FOC 方程组；
> 2. 从中推出稳态 FOC 方程组；
> 3. 利用稳态 FOC 进行参数校准；
> 4. 校准完毕求出稳态变量（C、K、H、Y...）；
> 5. 对数线性化，将 control variable、未来的 state variable 表示成当期的 state variable 的线性方程组；

### 2.11 Indivisible labor 的 log-linear model 和波动结果

Indivisible labor 模型的 log-linearization 与 basic model 类似，只是劳动变量从 $H_t$ 的连续工作时长解释转为工作概率 / aggregate employment margin。最终仍然可以写成：

$$
\tilde K_{t+1}=P\tilde K_t+Q\tilde\lambda_t,
$$

$$
y_t=R\tilde K_t+S\tilde\lambda_t.
$$

但 $y_t$ 中劳动响应的系数不同，导致变量波动不同。作者计算出新的标准差：

![Table 6.4 — Standard errors of indivisible labor model](../Figures/Ch06/table_6_4_indivisible_standard_errors.png)

与 basic model 相比，hours 的相对标准差从约 30% 上升到约 54%，投资波动也从约 214% 上升到约 245%。这明显更接近美国数据，但仍然低于数据中的 hours 94% 和 investment 489%。因此 Hansen 的 indivisible labor 是重要改进，但不是全部答案。

这里要抓住一个常见的 RBC 评价方式：模型不是被要求逐点预测每个季度，而是被要求在一组可解释的结构和参数下，生成合理的相对波动、相关性和动态响应。Indivisible labor 的意义就在于，它把一个经济机制——劳动供给的 extensive margin——引入模型，并改善了 moments。

### 2.12 Impulse response functions：从随机系统看冲击传播

Second moments 告诉我们长期模拟中变量波动大小，但 impulse response functions（IRFs）告诉我们一次冲击后变量如何随时间恢复。作者给定技术冲击：

$$
\tilde\lambda_t=\gamma\tilde\lambda_{t-1}+\varepsilon_t,
$$

并令某期 $\varepsilon_t=0.01$，之后冲击为 0。由于 $\gamma=0.95$，技术偏离会缓慢衰减。

![Figure 6.4 — Response of technology to a .01 impulse](../Figures/Ch06/figure_6_4_technology_impulse.png)

Figure 6.4 显示纯技术过程本身的衰减。它的形状主要由 $\gamma$ 决定。然后通过线性 laws of motion：

$$
\tilde K_{t+1}=P\tilde K_t+Q\tilde\lambda_t,
$$

$$
y_t=R\tilde K_t+S\tilde\lambda_t,
$$

可以计算资本、产出、消费、劳动、租金等变量的动态路径。

![Figure 6.5 — Responses of Hansen's basic model](../Figures/Ch06/figure_6_5_basic_irf.png)

Figure 6.5 是 basic model 对技术冲击的反应。一般而言，正技术冲击提高产出，带动消费和投资，资本随后积累并缓慢回落；资本租金可能因资本逐步积累而出现动态调整。这个图展示了 RBC 模型的基本 propagation mechanism：一次技术冲击通过劳动选择、储蓄投资和资本积累影响多个时期。

![Figure 6.6 — Responses for Hansen's model with indivisible labor](../Figures/Ch06/figure_6_6_indivisible_irf.png)

Figure 6.6 显示 indivisible labor 模型的响应。相较 basic model，多个变量的响应幅度更大，尤其劳动相关变量更强。这就是 amplification：同样大小的技术冲击，在模型内部机制作用下转化为更大的内生变量波动。

作者还用三维图和二维比较图把两个模型的 responses 放在一起：

![Figure 6.7 — Responses for both Hansen models](../Figures/Ch06/figure_6_7_both_models_3d.png)

![Figure 6.8 — Comparing the response of the two models](../Figures/Ch06/figure_6_8_model_response_comparison.png)

Figure 6.8 最值得看。横轴是 basic model 的响应，纵轴是 indivisible labor model 的响应；45 度线表示两个模型响应相同。如果某条变量响应路径在 45 度线上方，说明 indivisible labor 模型对该变量的响应更大。图中多数变量显示 indivisible labor 模型的反应更强。

### 2.13 附录 1：log-linear system 的求解逻辑

附录 1 展示了 Uhlig-style solution 的一般形式。真正要掌握的是逻辑而不是每个矩阵元素。它处理的问题是：我们已经把非线性的 FOC、资源约束、冲击过程在稳态附近做了 log-linearization，现在要从这堆线性方程中解出 policy rules。

先把变量分成三类：

- $x_t$：endogenous state variables，例如资本。它们通常是 predetermined 的，因为 $K_t$ 由上一期投资决定。
- $y_t$：jump / control variables，例如消费、劳动、租金等。它们可以在当期根据状态立刻调整。
- $z_t$：exogenous state variables，例如技术冲击 $\lambda_t$。

模型被整理为：

$$
0=A x_t+B x_{t-1}+C y_t+D z_t,
$$

$$
0=E_t(Fx_{t+1}+Gx_t+Hx_{t-1}+Jy_{t+1}+Ky_t+Lz_{t+1}+Mz_t),
$$

$$
z_{t+1}=Nz_t+\varepsilon_{t+1}.
$$

第一组方程没有期望，通常来自当期资源约束、劳动 FOC、价格定义等“当期就必须成立”的条件。它们只把当期变量 $x_t,y_t,z_t$ 和 predetermined state $x_{t-1}$ 联系起来。

第二组方程就是你问到的重点：它确实是条件期望方程。它通常来自 Euler equation 这类跨期最优条件。写成：

$$
0=E_t(\cdots)
$$

意思是：站在 $t$ 期，已知的信息包括 $x_{t-1},x_t,y_t,z_t$，但还不知道 $t+1$ 的新冲击 $\varepsilon_{t+1}$。因此涉及 $x_{t+1},y_{t+1},z_{t+1}$ 的部分要取条件期望。

不过 log-linearization 之后，一个很大的简化是：括号里面已经是一堆变量偏离稳态值的线性组合，所以期望算子可以直接分配进去：

$$
E_t(aX_{t+1}+bY_t+cZ_{t+1})
=
aE_tX_{t+1}+bY_t+cE_tZ_{t+1}.
$$

这里 $Y_t$ 这类当期变量已经在 $t$ 期信息集中，所以 $E_tY_t=Y_t$。真正需要处理的是未来变量。外生冲击过程给出：

$$
z_{t+1}=Nz_t+\varepsilon_{t+1},
$$

并且通常假设：

$$
E_t\varepsilon_{t+1}=0.
$$

所以：

$$
E_tz_{t+1}=Nz_t.
$$

这就是期望算子在一阶 log-linear 模型里的核心处理方式：先把期望内部的非线性对象在稳态附近线性化，再对线性化后的表达式取条件期望。它不是在原非线性模型中宣称 $E_t[g(X_{t+1})]=g(E_tX_{t+1})$，而是因为一阶 Taylor 展开已经把 $g$ 近似成了线性函数。未来外生状态的期望等于它的条件均值，下一期意外冲击因为均值为 0 被消掉。注意，这不是说冲击不存在，而是说在一阶近似里，policy rule 主要由条件均值决定；冲击的方差会影响 second moments，但不会像二阶近似那样直接改变决策规则。更完整的推导见 [stochastic_RBC_log_linearization.md](stochastic_RBC_log_linearization.md)。

接下来猜测解为：

$$
x_t=Px_{t-1}+Qz_t,
$$

$$
y_t=Rx_{t-1}+Sz_t.
$$

这个猜测的意思是：如果我们知道上一期留下来的 endogenous state $x_{t-1}$ 和当期外生状态 $z_t$，那么当期的 endogenous state $x_t$ 和当期变量 $y_t$ 都可以由线性 policy rules / static equations 决定。对于 Hansen 模型来说，可以把它想成：

$$
\tilde K_{t+1}=P\tilde K_t+Q\tilde\lambda_t,
$$

$$
y_t=R\tilde K_t+S\tilde\lambda_t.
$$

为了和附录记号一致，附录里用 $x_t$ 表示“本期内生状态”，用 $x_{t-1}$ 表示“进入本期时已经给定的状态”。所以具体到资本时，可以理解为：$x_{t-1}$ 对应进入本期的资本，$x_t$ 对应本期选择后形成的下一期资本。

先看第一组无期望方程。把猜测解代进去：

$$
0=A(Px_{t-1}+Qz_t)+Bx_{t-1}+C(Rx_{t-1}+Sz_t)+Dz_t.
$$

因为这个等式要对任意 $x_{t-1}$ 和 $z_t$ 都成立，所以分别匹配 $x_{t-1}$ 和 $z_t$ 的系数：

$$
AP+B+CR=0,
$$

$$
AQ+CS+D=0.
$$

若 $C$ 可逆，就有：

$$
R=-C^{-1}(AP+B).
$$

以及：

$$
S=-C^{-1}(AQ+D).
$$

但现在还不知道 $P,Q$。所以第一组方程的作用不是直接完成求解，而是把 $R,S$ 和 $P,Q$ 绑在一起。

再看第二组含期望的方程。关键是先写出未来变量在猜测解下是什么：

$$
x_{t+1}=Px_t+Qz_{t+1},
$$

$$
y_{t+1}=Rx_t+Sz_{t+1}.
$$

对它们取 $t$ 期条件期望：

$$
E_t x_{t+1}=Px_t+QE_t z_{t+1}=Px_t+QNz_t,
$$

$$
E_t y_{t+1}=Rx_t+SE_t z_{t+1}=Rx_t+SNz_t.
$$

把这些放回第二组方程：

$$
0=E_t(Fx_{t+1}+Gx_t+Hx_{t-1}+Jy_{t+1}+Ky_t+Lz_{t+1}+Mz_t).
$$

由于当期变量已知、未来冲击均值为 0，可以写成：

$$
0=(FP+G+JR)x_t+Hx_{t-1}+Ky_t+(FQ+JS+L)Nz_t+Mz_t.
$$

再代入当期 policy rules $x_t=Px_{t-1}+Qz_t$ 和 $y_t=Rx_{t-1}+Sz_t$，得到：

$$
0=
\left[(FP+G+JR)P+H+KR\right]x_{t-1}
+
\left[(FP+G+JR)Q+KS+(FQ+JS+L)N+M\right]z_t.
$$

这个等式也必须对任意 $x_{t-1},z_t$ 成立，所以两组系数都要等于 0：

$$
(FP+G+JR)P+H+KR=0,
$$

$$
(FP+G+JR)Q+KS+(FQ+JS+L)N+M=0.
$$

第一条主要用来求 $P$。因为 $R$ 又等于 $-C^{-1}(AP+B)$，所以代进去之后，会得到一个关于 $P$ 的 matrix quadratic equation。求出满足稳定性要求的 $P$ 后，再回头求：

$$
R=-C^{-1}(AP+B).
$$

然后用关于 $Q,S$ 的两条线性关系求 $Q$ 和 $S$：

$$
AQ+CS+D=0,
$$

$$
(FP+G+JR)Q+KS+(FQ+JS+L)N+M=0.
$$

所以整个求解流程可以概括为：

1. 先把非线性模型在稳态附近 log-linearize，整理成 $A,B,C,\ldots,N$ 这些矩阵。
2. 猜测线性 policy rules：$x_t=Px_{t-1}+Qz_t$，$y_t=Rx_{t-1}+Sz_t$。
3. 用当期方程把 $R$ 表示成 $P$，把 $S$ 表示成 $Q$。
4. 在 Euler-type 期望方程里，用 $E_tz_{t+1}=Nz_t$ 处理未来冲击。
5. 匹配 $x_{t-1}$ 和 $z_t$ 的系数，先求稳定的 $P$，再求 $Q,R,S$。

直觉上，$P$ 决定内生状态如何从过去延续到现在，是系统稳定性的核心；$Q$ 描述外生冲击如何影响状态；$R,S$ 描述 jump variables 如何立即响应状态和冲击。期望算子并没有神秘消失，而是因为我们已经猜测了未来变量的 policy rule，并且知道外生冲击的条件均值，所以它被转换成了关于当前状态的线性表达式。

### 2.14 附录 2：Blanchard-Kahn 与 Schur 方法

这一节最好先把两个名字分清楚：

**Blanchard-Kahn 条件不是一种具体算法，而是一个“局部线性解是否唯一稳定”的判定标准。** 它回答：在所选稳态附近，这个线性理性预期模型有没有唯一一条局部有界的一阶均衡路径？

**Schur 方法不是一个新的经济理论，而是一种数值求解方法。** 它回答：如果局部稳定解存在，怎么用矩阵分解把这个稳定解算出来？

所以二者的关系是：

$$
\text{BK condition checks existence/uniqueness;}
\qquad
\text{Schur/QZ method computes the solution.}
$$

#### 2.14.1 为什么 DSGE 解会有“稳定性问题”

**<u>线性化</u>**后的 DSGE 模型通常不是普通的 backward-looking 差分方程。它里面既有过去给定的状态，也有对未来变量的预期。例如资本 Euler equation 里会出现 $E_t C_{t+1}$，新凯 Phillips curve 里会出现 $E_t\pi_{t+1}$。

这类模型的变量大致可以分成两类：

- **Predetermined variables**：进入本期时已经被历史决定，不能当期自由跳。例如 $K_t$。
- **Jump variables**：本期观察到状态后可以立刻调整、且具有独立前瞻自由度的变量。例如 RBC 中的 $C_t$，在新凯模型里也常包括 $y_t,\pi_t$。劳动 $H_t$ 这类 control variable 往往由当期静态 FOC 决定，不一定是独立 jump variable。

如果一个模型只有 predetermined variables，今天的初值已经给定，未来路径就直接由方程往前推。但 DSGE 里还有 jump variables，它们的当期值本身也是解的一部分。问题就变成：

> 给定已经无法改变的状态变量，应该选择什么样的 jump variables，才能让未来路径满足线性化后的均衡条件，并始终留在稳态附近的局部有界分支上？

BK 条件就是在回答这个问题。

#### 2.14.2 BK 条件的直觉：jump variables 用来消除爆炸方向

先想一个最简单的线性系统：

$$
X_{t+1}=M X_t.
$$

矩阵 $M$ 的特征根决定线性系统中的动态方向。若某个特征根满足 $|\lambda|<1$，沿着这个方向走，偏离会收敛回稳态；若 $|\lambda|>1$，沿着这个方向走，偏离会持续放大并离开稳态邻域。

一阶扰动法要找的是“始终留在稳态附近”的局部有界路径。因此所有不稳定方向都必须在这个局部线性解中被排除。怎么排除？靠 jump variables。

用消费-资本系统看最清楚。假设线性化后可以写成：

$$
\begin{bmatrix}
c_{t+1}\\
k_{t+1}
\end{bmatrix}
=
M
\begin{bmatrix}
c_t\\
k_t
\end{bmatrix}.
$$

这里 $k_t$ 是 predetermined，进入本期时已经给定；$c_t$ 是 jump variable，可以在本期选择。给定 $k_t$ 后，如果 $c_t$ 选错，$(c_t,k_t)$ 这个初始点就会含有爆炸方向的成分，未来路径会发散。只有一个特定的 $c_t$ 能让初始点刚好落在稳定路径上。

这就是 saddle path 的含义：状态变量给定，跳变量立刻跳到某个唯一值，使系统从此沿着稳定路径走。

因此，稳定解唯一通常要求：

$$
\#\{\text{unstable roots}\}
=
\#\{\text{jump variables}\}.
$$

也可以等价地写成：

$$
\#\{\text{stable roots}\}
=
\#\{\text{predetermined variables}\}.
$$

这就是 Blanchard-Kahn condition 的核心。

这里的 jump variables 要理解为“没有历史给定初值、并且具有独立前瞻自由度的变量”。它不等于所有 control variables。有些 control variables 由当期静态 FOC 或恒等式直接决定，可以先消元或作为静态变量处理；BK 根数条件数的是独立的 forward-looking 自由度。更完整的讨论见 [Schur_method.md](Schur_method.md)。

如果 unstable roots 太多，jump variables 不够，就没有足够的自由度把所有不稳定方向都消掉，通常不存在局部有界解。比如有两个不稳定方向，但只有一个 $c_t$ 能跳，就消不完。

如果 unstable roots 太少，jump variables 太多，那么有多个 jump variable 取值都能使路径局部有界，模型不再唯一决定局部均衡路径。这就是 indeterminacy，也常和 sunspot equilibria 联系在一起。你之前 VAT 报告里说“如果所有特征值都小于 1，那么 $c_t$ 初值怎么选都收敛，路径可能取决于动物精神”，讲的就是这个情形。

#### 2.14.3 为什么 unstable roots 反而要等于 jump variables 数量

这个点第一次看很反直觉：既然 unstable root 会导致爆炸，为什么不是要求 unstable root 越少越好？

原因是 jump variable 的初始值没有被历史钉住，必须由模型自己钉住。如果有一个 jump variable，例如 $c_t$，模型需要一个局部有界性条件来把它唯一确定下来。一个 unstable root 正好提供一个“不能含有这个方向分量”的限制，于是它把一个 jump variable 钉住。

所以可以这样记：

$$
\text{one unstable direction}
\quad\Longleftrightarrow\quad
\text{one restriction on jump variables}.
$$

有几个 jump variables，就需要几个这样的 restrictions，才能把它们唯一确定下来。没有 unstable roots 并不一定好，因为这意味着 jump variables 缺少限制，容易出现多重均衡。

#### 2.14.4 期望项在 BK/Schur 里怎么处理

BK 和 Schur 方法通常处理的是一阶线性化后的系统。在线性系统中，期望算子处理起来比较机械：

$$
E_t[aX_{t+1}+bZ_{t+1}]
=
aE_tX_{t+1}+bE_tZ_{t+1}.
$$

未来 innovation 的条件期望为 0：

$$
E_t\varepsilon_{t+1}=0.
$$

但这不等于把未来状态变量都设成 0。若外生状态满足：

$$
z_{t+1}=Nz_t+\varepsilon_{t+1},
$$

那么：

$$
E_tz_{t+1}=Nz_t.
$$

所以更准确的说法是：**一阶近似下，把未来随机扰动替换为条件期望；若冲击有持久性，未来外生状态的条件期望不是 0，而是由当前状态延续出来。** 这不是原非线性模型中的精确等式，而是一阶 Taylor 近似后的性质。相关推导可以回看 [stochastic_RBC_log_linearization.md](stochastic_RBC_log_linearization.md)。

这也解释了为什么你之前 VAT 报告里“把未来冲击替换为期望，然后当成确定性系统迭代”的说法大体方向是对的，但要补一句：若冲击是 AR(1)，不是把未来 $z$ 全部设为 0，而是按 $E_tz_{t+j}=N^jz_t$ 往前推。

#### 2.14.5 Schur 方法到底是什么

现在再看 Schur 方法就简单多了。Schur/QZ 方法不是在改变模型的经济含义，它只是一个更稳健的矩阵算法，用来完成两件事：

1. 找出线性系统里的 stable roots 和 unstable roots。
2. 如果 BK 条件满足，计算让系统落在局部稳定分支上的 policy rules。

实际 DSGE 线性系统经常不能简单写成：

$$
X_{t+1}=MX_t.
$$

因为有些方程里同时有 $E_tX_{t+1}$ 和 $X_t$，甚至矩阵可能不可逆。更一般地，它会被整理成：

$$
\Gamma_0 E_t s_{t+1}
=
\Gamma_1 s_t+\Gamma_2 z_t.
$$

这时如果强行求 $\Gamma_0^{-1}\Gamma_1$，可能遇到矩阵不可逆或数值不稳定。Generalized Schur decomposition，也叫 QZ decomposition，就是专门处理这种 generalized eigenvalue problem 的工具。它不要求简单地手算 $M=\Gamma_0^{-1}\Gamma_1$，而是直接对矩阵对 $(\Gamma_0,\Gamma_1)$ 做分解，得到 generalized eigenvalues。

得到特征根后，Schur/QZ 方法会把它们按 stable 和 unstable 排序。然后：

- 如果 stable roots 数量不等于 predetermined variables 数量，BK 条件失败。
- 如果数量匹配，就利用“不稳定方向必须为 0”这个限制，解出 jump variables 关于 states 的关系。

这里说的“不稳定方向必须为 0”，直接理由是：在线性化模型里，非零不稳定分量会持续放大，使路径离开稳态邻域，因此它不属于一阶扰动法要寻找的局部有界均衡分支。它和原非线性问题中的 boundedness、no-bubble、TVC 通常在标准凹性 RBC 中指向同一条最优分支，但不能在所有非线性模型中简单等同。TVC 的直觉见 [TVC intuition.md](<TVC intuition.md>)，更完整的局部/全局区分见 [Schur_method.md](Schur_method.md)。

还有一个技术细节：stable / unstable 的判定要看线性系统的写法。如果系统写成 $E_t x_{t+1}=Mx_t$，和写成 $x_t=N E_t x_{t+1}$，对应特征值可能互为倒数。因此实际使用 QZ/Schur 时，不能脱离矩阵铅笔和时点约定机械记“大于 1”或“小于 1”；要看算法采用的是 current-to-future map 还是 future-to-current map。

最终它给出的还是我们想要的 policy rules：

$$
y_t=R x_{t-1}+S z_t,
$$

以及：

$$
x_t=P x_{t-1}+Q z_t.
$$

所以可以把 Schur 方法理解成：**用矩阵分解自动找到局部稳定子空间，然后把 jump variables 选到这个稳定子空间上。**

这里还要避免另一个误解：Schur 不是随便给出“一种可能的近似”。如果 BK 条件满足、变量分类和方程组都正确，那么 Schur 得到的是线性化模型中唯一的局部稳定政策方向。若我们已经知道原非线性模型的真实最优政策从该稳态附近出发时确实属于这条局部稳定分支，那么 Schur 得到的线性 policy rule 就是真实政策函数在该稳态处的一阶系数。反过来说，单靠 BK 条件本身并不能枚举或排除所有远离稳态的全局非线性路径；要把 Schur 分支解释成真实全局最优政策的一阶近似，还需要标准 RBC 中的凹性、最优政策唯一性、政策连续/光滑、小偏离导致小调整等额外结构。Schur 没有刻画的是远离稳态后的全局非线性路径，以及二阶、三阶等高阶项。

#### 2.14.6 和上一节 Uhlig 方法的关系

上一节的 Uhlig-style solution 是通过猜测：

$$
x_t=Px_{t-1}+Qz_t,\qquad y_t=Rx_{t-1}+Sz_t
$$

然后代回方程，手工推出 matrix quadratic equation。这个方法很有教学意义，因为它让你看到 $P,Q,R,S$ 是怎么从模型方程里来的。

Schur/QZ 方法则更像实际软件会用的通用算法。它不一定显式写出 matrix quadratic equation，而是直接对整个线性系统做 generalized eigenvalue decomposition，检查 BK 条件并计算稳定解。

所以三者关系可以这样记：

- **BK 条件**：判断稳定解是否存在且唯一。
- **Uhlig 方法**：一种手工推导 policy matrices 的办法。
- **Schur/QZ 方法**：一种数值上更稳健、更通用的求解办法。

你之前 VAT 报告里的极简 NK 例子，本质上也是在做 BK 检查：把 IS curve、Phillips curve 和 policy rule 联立成线性系统，然后看政策参数是否让特征根数量满足 determinacy condition。VAT 政策如果没有改变决定特征根的关键反馈结构，就可能不改变稳定性条件；如果它改变了对通胀或产出的反馈矩阵，就可能改变 BK 条件。

作者展示 generalized Schur method 解出的 impulse responses。Schur 方法求得的 impulse responses 与前面 Uhlig 方法的结果非常接近：

![Figure 6.9 — Responses for Hansen model solved using Schur](../Figures/Ch06/figure_6_9_schur_irf.png)

这张图的目的不是提供新经济结论，而是验证：不同线性求解技术在这个模型上给出基本一致的动态响应。也就是说，Figure 6.9 不是在说 Hansen 模型又多了一个机制，而是在说“换一种求解算法，得到的 policy rules 和 IRFs 仍然一致”，因此前面的经济结论不是某个特定算法造成的。

### 2.15 Matlab code 在实现什么

本章 Matlab code 分三类：第一类求 basic Hansen model 的 $P,Q,R,S$；第二类用线性系统计算方差和标准差；第三类演示 appendix 中的 Schur / Blanchard-Kahn solution。阅读代码时不需要记住每一行矩阵操作，但需要知道它们实现的数学对象：

- 用校准参数和稳态值构造 log-linear system 的矩阵。
- 解 matrix quadratic equation 或用 Schur decomposition 找稳定根。
- 得到 policy matrices 后，计算 impulse responses 或模拟时间序列。
- 根据模型生成的变量序列计算 second moments，并与数据表比较。

这套流程就是后面 DSGE / RBC 数值分析的基本模板。

## 3. Compact Summary: What You Must Retain

- Hansen basic model 是带随机技术、资本积累和劳动-闲暇选择的 RBC benchmark；核心 FOCs 是资本 Euler equation 和劳动供给条件。
- Stationary state 是 log-linearization 的中心点；本章先用稳态条件确定 $\bar K,\bar H,\bar C,\bar r$ 等变量，再研究稳态附近动态。
- 由于技术冲击是持久随机过程，直接 value function iteration 会面临状态维度问题，因此作者使用 log-linearization。
- Log-linearization 把非线性系统转成线性系统，并寻找 laws of motion：$\tilde K_{t+1}=P\tilde K_t+Q\tilde\lambda_t$ 与 $y_t=R\tilde K_t+S\tilde\lambda_t$。
- Calibration 不是纯统计估计，而是用长期宏观事实、外部研究和目标 moments 选择参数；$A$ 被用来匹配稳态劳动约三分之一。
- Basic Hansen model 能较好匹配消费相对波动，但严重低估劳动和投资波动。
- Indivisible labor 通过固定工作时长和随机工作概率，把劳动调整放到 extensive margin 上，从而提高 hours 和 investment 的相对波动。
- IRFs 展示一次技术冲击如何通过劳动、投资和资本积累传播；indivisible labor 模型相对于 basic model 有更强 amplification。

## 4. Figures, Tables, and Formulas to Check in the Original

本章重要图表已经作为截图放入 `Figures/Ch06/`，并在正文中嵌入。尤其要回看：

- Figure 6.1：用 $A$ 校准稳态劳动。
- Table 6.1 与 Table 6.2：basic model 生成的标准差与 Hansen 数据的比较。
- Figure 6.2：indivisible labor 带来的 nonconvex consumption set。
- Figure 6.3 与 Table 6.3：求 $h_0$ 与 indivisible labor 稳态。
- Table 6.4：indivisible labor model 的标准差。
- Figure 6.4-6.8：技术冲击的 impulse responses，以及两个 Hansen 模型的对比。
- Figure 6.9：Schur method 解出的 IRFs。

需要重点核对的公式：

- Bellman equation：
  $$V(k_t,\lambda_t)=\max_{k_{t+1},h_t}\{\ln(\lambda_tk_t^\theta h_t^{1-\theta}+(1-\delta)k_t-k_{t+1})+A\ln(1-h_t)+\beta E_t[V(k_{t+1},\lambda_{t+1})\mid\lambda_t]\}.$$
- Euler equation：
  $$\frac{1}{c_t}=\beta E_t\left[\frac{r_{t+1}+1-\delta}{c_{t+1}}\right].$$
- Labor FOC：
  $$(1-H_t)(1-\theta)\frac{Y_t}{H_t}=AC_t.$$
- General log-linear system and solution form：
  $$0=A x_t+B x_{t-1}+C y_t+D z_t,$$
  $$0=E_t(Fx_{t+1}+Gx_t+Hx_{t-1}+Jy_{t+1}+Ky_t+Lz_{t+1}+Mz_t),$$
  $$z_{t+1}=Nz_t+\varepsilon_{t+1},$$
  $$x_t=Px_{t-1}+Qz_t,\quad y_t=Rx_{t-1}+Sz_t.$$

> ⚠️【需要回原文看图】本章附录中的矩阵二次方程、Blanchard-Kahn 推导和 generalized Schur decomposition 公式较密集，PDF 文本提取容易丢失矩阵排版。若要写代码复现，应回原文逐项核对矩阵维度、符号和系数。

## 5. Questions and Answers

**Q1：为什么 Hansen 模型不能简单沿用第 5 章的 value function iteration？**  
因为技术过程是持久随机过程，外生状态 $\lambda_t$ 的可能取值会随着时间扩张。直接离散化会让状态空间迅速变大，尤其模型再加入更多状态变量时更严重。

**Q2：log-linearization 为什么围绕 stationary state 做？**  
因为稳态是模型长期均衡位置，变量偏离通常被视为围绕该点的小波动。在这个邻域内，非线性关系可用一阶 log deviation 近似成线性系统。

**Q3：basic Hansen model 的主要失败在哪里？**  
它能较好匹配 consumption 相对于 output 的波动，但 hours worked 和 investment 的相对波动太低，说明模型内部 amplification 不足。

**Q4：indivisible labor 为什么能提高劳动波动？**  
因为劳动调整从“每个人连续调整工作小时”变成“固定工作时长下调整工作人口比例”。在 lottery 和 insurance 下，aggregate hours 可以连续变化，但个体劳动 disutility 的边际结构不同，劳动供给更容易响应冲击。

**Q5：calibration 和 estimation 有什么区别？**  
Calibration 通常用外部研究、长期均值和目标 moments 来选择参数，不一定通过统计似然或回归估计。它强调参数的经济解释和模型能否匹配关键数据特征。

**Q6：IRF 和 simulation 的区别是什么？**  
IRF 研究一次特定冲击后的动态响应路径；simulation 则用随机冲击序列生成长期时间序列并计算 moments。前者看传播机制，后者看总体波动特征。

**Q7：Blanchard-Kahn 条件的直觉是什么？**  
线性理性预期模型中，资本等 predetermined variables 不能当期跳变，而消费、劳动等 jump variables 可以当期调整。稳定唯一解需要 jump variables 的数量刚好足以消除爆炸根。

**Q8：这一章和第 7 章的关系是什么？**  
第 6 章先用 log-linearized first-order conditions 求解 Hansen 模型；第 7 章会介绍另一条路：先把目标函数做 quadratic approximation，再用 linear quadratic dynamic programming 求线性政策函数。
