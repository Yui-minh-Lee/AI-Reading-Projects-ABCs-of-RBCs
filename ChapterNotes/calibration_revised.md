# calibration.md — 第六章 Hansen RBC 模型参数校准手把手讲解

> 对应章节：Chapter 6 — Hansen's RBC Model  
> 目标：假设模型、FOC、稳态方程和 log-linear system 已经写好，但参数还没有数值。本文件用书中 Hansen RBC 例子，完整演示一次从“参数未知”到“可求解、可模拟、可比较数据矩”的 calibration 流程。  
> 关键词：calibration、stationary state、target moments、Solow residual、shock variance、second moments、indivisible labor

---

## 0. 先说清楚：我们到底在“校准”什么？

拿到一个 RBC / DSGE 模型以后，通常会有三层东西：

第一层是**模型结构**，例如效用函数、生产函数、资本积累、技术冲击过程。它告诉我们经济机制长什么样。

第二层是**最优性条件**，也就是 FOC、Euler equation、劳动供给条件、资源约束等。它告诉我们均衡变量之间必须满足什么关系。

第三层才是**数值版本**，也就是具体给出

$$
\beta,\delta,\theta,A,\gamma,\sigma_\varepsilon,\bar K,\bar H,\bar Y,\bar C,\ldots
$$

这些数字。只有到了第三层，我们才能真正求政策函数、画 impulse response functions、模拟时间序列、计算模型产生的方差与相关性。

所以 calibration 要解决的问题是：

> 模型方程已经写好了，但方程本身不会自动告诉你每个参数该是多少。我们需要用长期数据事实、外部研究结果、稳态目标和模型模拟矩，把这些参数一个个 pin down。

这和 estimation 不完全一样。Estimation 通常会指定似然函数或矩条件，然后用统计方法估计参数。Calibration 则更像是“按经济含义逐个定参数”：有些参数直接来自长期平均或文献，有些参数通过稳态关系反推，有些参数通过模型生成的 moments 去匹配数据 moments。

在第六章 Hansen 模型里，校准的逻辑尤其清楚：

1. $\theta$、$\delta$、$\beta$ 先按季度频率和宏观经验给定；
2. $A$ 用“稳态工作时间约为可用时间的三分之一”来反推；
3. $\gamma$ 用技术残差的自相关来定；
4. $\sigma_\varepsilon$ 要在模型求出 law of motion 之后，用“模型产出波动 = 数据产出波动”来定；
5. 对 indivisible labor 模型，还要用同样的稳态劳动目标反推出 $h_0$ 和 $\bar\alpha$。

下面我们就一步一步做。

---

## 1. 第一步：把模型和未知参数列清楚

### 1.1 Basic Hansen RBC model

书中 basic Hansen model 是一个带随机技术冲击和可变劳动供给的标准 RBC 模型。代表性家庭最大化

$$
\max_{\{c_t,h_t,k_{t+1}\}_{t=0}^{\infty}}
\sum_{t=0}^{\infty}\beta^t\left[\ln c_t + A\ln(1-h_t)\right],
$$

其中 $h_t$ 是劳动，$1-h_t$ 是 leisure。

生产函数是

$$
Y_t=\lambda_t K_t^\theta H_t^{1-\theta}.
$$

资本积累和资源约束可以合并写成

$$
C_t+K_{t+1}=Y_t+(1-\delta)K_t.
$$

技术过程在 log-linear 求解时写成技术偏离的 AR(1)：

$$
\tilde\lambda_t=\gamma \tilde\lambda_{t-1}+\varepsilon_t,
\qquad E\varepsilon_t=0,
\qquad \operatorname{sd}(\varepsilon_t)=\sigma_\varepsilon.
$$

这里 $\tilde\lambda_t$ 是围绕稳态的 log deviation。稳态技术归一化为

$$
\bar\lambda=1.
$$

FOC 可以整理为五条核心均衡关系：

$$
1=\beta E_t\left[\frac{C_t}{C_{t+1}}(r_{t+1}+1-\delta)\right],
$$

$$
(1-H_t)(1-\theta)\frac{Y_t}{H_t}=AC_t,
$$

$$
C_t+K_{t+1}=Y_t+(1-\delta)K_t,
$$

$$
Y_t=\lambda_tK_t^\theta H_t^{1-\theta},
$$

$$
r_t=\theta\frac{Y_t}{K_t}.
$$

现在假设这个模型交到我们手里，未知参数主要是：

$$
\beta,\delta,\theta,A,\gamma,\sigma_\varepsilon.
$$

同时，稳态变量也未知：

$$
\bar K,\bar H,\bar Y,\bar C,\bar r,\bar I,\bar w.
$$

注意：稳态变量不是“参数”，但校准时必须一起算出来，因为 log-linearization 和矩阵求解都要用稳态值。

---

## 2. 第二步：决定数据频率和单位

第六章用的是**季度模型**，所以参数也必须按季度频率理解。

这一步很重要，因为很多初学者会把年化参数和季度参数混在一起。比如：

- $\beta=0.99$ 是季度贴现因子，不是年度贴现因子；
- $\delta=0.025$ 是季度折旧率，大致相当于年化 10% 左右；
- 技术冲击 $\gamma=0.95$ 也是季度自相关；
- 产出标准差 $0.0176$ 是季度数据中 log detrended output 的标准差。

如果你换成年度模型，整套参数都要重新调整。不能直接把季度 Hansen 参数塞进年度模型。

数据单位也要统一。RBC 模型通常不关心 GDP 是以百万美元还是十亿美元计量，因为模型变量可以按比例缩放。真正重要的是这些对象：

1. 长期资本收入份额；
2. 长期折旧率；
3. 长期实际回报率或贴现因子；
4. 平均工作时间占可用时间比例；
5. 技术残差的持久性；
6. business-cycle component 的产出波动。

书中 Hansen 例子采用的核心数据目标是：

$$
\bar H \approx 0.3335,
$$

也就是平均工作时间约为可用时间的三分之一；以及

$$
\operatorname{sd}(\tilde Y_t)=0.0176,
$$

也就是 detrended log output 的标准差约为 1.76%。

---

## 3. 第三步：先给定最有经济含义、最不想让模型自己乱调的参数

校准不要一上来就“所有参数一起调”。标准做法是先把最有直接经济含义的参数固定下来。

第六章给定：

$$
\beta=0.99,
\qquad
\delta=0.025,
\qquad
\theta=0.36.
$$

### 3.1 为什么 $\theta=0.36$？

在 Cobb-Douglas 生产函数

$$
Y_t=\lambda_tK_t^\theta H_t^{1-\theta}
$$

中，$\theta$ 是资本收入份额（capital share）。在完全竞争下，资本的产出弹性等于资本收入占比。因此如果数据中资本收入约占国民收入 36%，就设

$$
\theta=0.36.
$$

这类参数通常不靠模型内部动态来调，因为它在数据里有比较直接的对应物。

### 3.2 为什么 $\delta=0.025$？

$\delta$ 是资本折旧率。季度折旧率 0.025 意味着每季度约 2.5% 的资本折旧，粗略年化约 10%。这也是 RBC 文献中常见的季度校准。

如果我们自己用数据做，也可以用长期平均的投资资本比来辅助判断。稳态下

$$
\bar I=\delta \bar K,
$$

所以

$$
\delta=\frac{\bar I}{\bar K}.
$$

书中直接采用

$$
\delta=0.025.
$$

### 3.3 为什么 $\beta=0.99$？

$\beta$ 是季度贴现因子。它控制家庭如何在今天消费和未来消费之间权衡。季度 $\beta=0.99$ 对应一个比较标准的低频实际回报环境。

在稳态 Euler equation 中，

$$
\frac{1}{\beta}=\bar r+1-\delta,
$$

所以

$$
\bar r=\frac{1}{\beta}-(1-\delta).
$$

代入 $\beta=0.99$、$\delta=0.025$：

$$
\bar r=\frac{1}{0.99}-0.975=0.0351.
$$

这表示季度资本租金约为 3.51%。这个数值后面会用来检查稳态计算是否一致。

---

## 4. 第四步：用稳态劳动目标反推出 $A$

现在最关键的问题来了：效用函数里有一个参数

$$
A.
$$

它表示 leisure 在效用中的权重。$A$ 越大，家庭越重视 leisure，于是稳态劳动越低。可是 $A$ 不是可以从国民账户中直接读出来的。所以第六章用一个稳态事实来校准它：

> 长期平均工作时间约占可用时间的三分之一。

也就是设定目标

$$
\bar H=0.3335.
$$

下面不要跳步，我们从 FOC 推出来。

### 4.1 先从 Euler equation 得到资本回报

稳态下，所有变量不变，所以 Euler equation

$$
1=\beta E_t\left[\frac{C_t}{C_{t+1}}(r_{t+1}+1-\delta)\right]
$$

变成

$$
1=\beta(\bar r+1-\delta).
$$

因此

$$
\bar r=\frac{1}{\beta}-(1-\delta).
$$

代入数字：

$$
\bar r=\frac{1}{0.99}-(1-0.025)=0.0351.
$$

### 4.2 再用资本边际产出得到 $\bar K/\bar Y$

资本租金条件是

$$
\bar r=\theta\frac{\bar Y}{\bar K}.
$$

所以

$$
\frac{\bar K}{\bar Y}=\frac{\theta}{\bar r}.
$$

也可以写成

$$
\frac{\bar Y}{\bar K}=\frac{\bar r}{\theta}.
$$

代入 $\theta=0.36$、$\bar r=0.0351$：

$$
\frac{\bar Y}{\bar K}=\frac{0.0351}{0.36}=0.0975.
$$

这一步的含义是：给定资本份额和稳态资本回报，模型已经确定了长期产出资本比。

### 4.3 算出稳态消费产出比

稳态资源约束是

$$
\bar C+\bar K=\bar Y+(1-\delta)\bar K.
$$

移项得

$$
\bar C=\bar Y-\delta\bar K.
$$

两边除以 $\bar Y$：

$$
\frac{\bar C}{\bar Y}=1-\delta\frac{\bar K}{\bar Y}.
$$

而

$$
\frac{\bar K}{\bar Y}=\frac{\theta}{\bar r}
=\frac{\theta}{\frac{1}{\beta}-(1-\delta)}.
$$

所以

$$
\frac{\bar C}{\bar Y}
=1-\delta\frac{\theta}{\frac{1}{\beta}-(1-\delta)}.
$$

把分母改写一下，得到书中常见形式：

$$
\frac{\bar C}{\bar Y}
=1-\frac{\beta\delta\theta}{1-\beta(1-\delta)}.
$$

我们把这个比例记作

$$
s_C\equiv \frac{\bar C}{\bar Y}.
$$

代入数字：

$$
s_C=1-\frac{0.99\times0.025\times0.36}{1-0.99(1-0.025)}=0.7436.
$$

这一步非常重要，因为后面劳动 FOC 里会出现 $C/Y$。

### 4.4 用劳动 FOC 把 $A$ 和 $\bar H$ 连起来

劳动 FOC 是

$$
(1-H_t)(1-\theta)\frac{Y_t}{H_t}=AC_t.
$$

稳态下：

$$
(1-\bar H)(1-\theta)\frac{\bar Y}{\bar H}=A\bar C.
$$

两边除以 $\bar Y$：

$$
(1-\bar H)\frac{1-\theta}{\bar H}=A\frac{\bar C}{\bar Y}.
$$

也就是

$$
\left(\frac{1}{\bar H}-1\right)(1-\theta)=A s_C.
$$

因此

$$
\frac{1}{\bar H}-1=\frac{A s_C}{1-\theta}.
$$

整理出 $\bar H$：

$$
\bar H=\frac{1}{1+\frac{A}{1-\theta}s_C}.
$$

这就是书中 equation (6.4) 的经济含义：给定 $\beta,\delta,\theta$，$s_C$ 已经确定；因此 $A$ 和 $\bar H$ 是一一对应的。

### 4.5 现在反过来：给定目标 $\bar H$，求 $A$

我们目标是

$$
\bar H=0.3335.
$$

由上式

$$
\frac{1}{\bar H}-1=\frac{A s_C}{1-\theta},
$$

所以

$$
A=(1-\theta)\frac{\frac{1}{\bar H}-1}{s_C}.
$$

代入

$$
\theta=0.36,
\qquad
\bar H=0.3335,
\qquad
s_C=0.7436,
$$

得到

$$
A=0.64\times\frac{1/0.3335-1}{0.7436}=1.7201.
$$

书中取

$$
A=1.72.
$$

这一步就是 Figure 6.1 的含义：横轴是 $A$，纵轴是由稳态方程推出的 $\bar H$。选择 $A=1.72$，是为了让模型稳态劳动接近三分之一。

---

## 5. 第五步：有了 $A$ 以后，完整算出 steady state

现在参数已经有：

$$
\beta=0.99,
\quad
\delta=0.025,
\quad
\theta=0.36,
\quad
A=1.72,
\quad
\bar\lambda=1.
$$

稳态劳动为

$$
\bar H=0.3335.
$$

### 5.1 算稳态资本 $\bar K$

生产函数稳态为

$$
\bar Y=\bar K^\theta \bar H^{1-\theta}.
$$

资本租金条件为

$$
\bar r=\theta\frac{\bar Y}{\bar K}.
$$

把生产函数代入资本租金条件：

$$
\bar r=\theta \bar K^{\theta-1}\bar H^{1-\theta}.
$$

整理得

$$
\bar K
=\bar H\left[\frac{\theta\bar\lambda}{\frac{1}{\beta}-(1-\delta)}\right]^{\frac{1}{1-\theta}}.
$$

由于 $\bar\lambda=1$，代入数字：

$$
\bar K
=0.3335\left[\frac{0.36}{0.0351}\right]^{1/0.64}
=12.6695.
$$

### 5.2 算稳态产出 $\bar Y$

$$
\bar Y=\bar K^\theta\bar H^{1-\theta}.
$$

代入：

$$
\bar Y=(12.6695)^{0.36}(0.3335)^{0.64}=1.2353.
$$

### 5.3 算稳态消费 $\bar C$

稳态资源约束：

$$
\bar C=\bar Y-\delta\bar K.
$$

代入：

$$
\bar C=1.2353-0.025\times 12.6695=0.9186.
$$

### 5.4 算稳态投资 $\bar I$

稳态下资本不变，所以投资刚好补偿折旧：

$$
\bar I=\delta\bar K.
$$

代入：

$$
\bar I=0.025\times12.6695=0.3167.
$$

### 5.5 算稳态工资和资本租金

资本租金：

$$
\bar r=\theta\frac{\bar Y}{\bar K}=0.36\times\frac{1.2353}{12.6695}=0.0351.
$$

工资：

$$
\bar w=(1-\theta)\frac{\bar Y}{\bar H}
=0.64\times\frac{1.2353}{0.3335}=2.3706.
$$

### 5.6 做一致性检查

不要小看这一步。校准时一定要检查稳态是否同时满足 Euler equation 和劳动 FOC。

Euler check：

$$
\frac{1}{\beta}=1.0101,
$$

$$
\bar r+1-\delta=0.0351+0.975=1.0101.
$$

一致。

Labor FOC check：

$$
(1-\bar H)\bar w
=(1-0.3335)\times2.3706=1.5800,
$$

$$
A\bar C=1.7201\times0.9186=1.5800.
$$

一致。

到这里为止，我们已经把 deterministic steady state 全部定下来了。

---

## 6. 第六步：用 Solow residual 校准技术持久性 $\gamma$

现在还剩技术过程：

$$
\tilde\lambda_t=\gamma\tilde\lambda_{t-1}+\varepsilon_t.
$$

这里有两个东西要定：

$$
\gamma
\quad\text{和}\quad
\sigma_\varepsilon.
$$

先定 $\gamma$。

### 6.1 从数据构造技术残差

生产函数是

$$
Y_t=\lambda_tK_t^\theta H_t^{1-\theta}.
$$

两边取 log：

$$
\ln Y_t=\ln\lambda_t+\theta\ln K_t+(1-\theta)\ln H_t.
$$

所以技术残差为

$$
\ln\lambda_t
=\ln Y_t-\theta\ln K_t-(1-\theta)\ln H_t.
$$

实际操作时，你需要季度数据：

- real output $Y_t$；
- capital stock $K_t$；
- hours worked $H_t$；
- 已经校准好的 $\theta=0.36$。

然后逐期算出

$$
\hat a_t=\ln Y_t-0.36\ln K_t-0.64\ln H_t.
$$

这里 $\hat a_t$ 就是估计出来的 log technology residual。

### 6.2 估计 AR(1) 自相关

接着跑一个简单的 AR(1)：

$$
\hat a_t=\rho \hat a_{t-1}+u_t.
$$

在 Hansen 使用的美国季度数据中，一阶自相关大约是

$$
\rho\approx0.95.
$$

所以书中设定

$$
\gamma=0.95.
$$

注意这里的逻辑：$\gamma$ 不是为了让模型看起来更好随便调的，而是从技术残差本身的持久性得到的。它决定技术冲击消退得快还是慢。$\gamma$ 越接近 1，技术冲击越 persistent，变量响应也越持久。

---

## 7. 第七步：先求 law of motion，再校准冲击标准差 $\sigma_\varepsilon$

很多人会在这里卡住：既然技术过程已经有 $\gamma=0.95$，那 $\sigma_\varepsilon$ 能不能直接从 Solow residual 的残差标准差得到？

可以这样做，但第六章书中的做法稍有不同。它把 $\sigma_\varepsilon$ 选成一个值，使得**模型生成的产出标准差等于数据中的产出标准差**。

也就是说，书里先求出线性政策函数，然后再选择 shock size。

### 7.1 为什么必须先求 law of motion？

因为冲击 $\varepsilon_t$ 本身不是产出。技术冲击通过模型内部机制传导到资本、劳动、产出、消费和投资。模型中产出到底波动多少，不仅取决于 $\sigma_\varepsilon$，还取决于政策函数系数。

第六章 basic model 求得的 law of motion 是：

$$
\tilde K_{t+1}=0.9537\tilde K_t+0.1132\tilde\lambda_t,
$$

$$
\tilde Y_t=0.2045\tilde K_t+1.4523\tilde\lambda_t,
$$

$$
\tilde C_t=0.5691\tilde K_t+0.3920\tilde\lambda_t,
$$

$$
\tilde H_t=-0.2430\tilde K_t+0.7067\tilde\lambda_t,
$$

$$
\tilde r_t=-0.7955\tilde K_t+1.4523\tilde\lambda_t.
$$

为了简写，令

$$
a=0.9537,
\quad
b=0.1132,
\quad
c=0.2045,
\quad
d=1.4523,
\quad
\gamma=0.95.
$$

于是：

$$
\tilde K_{t+1}=a\tilde K_t+b\tilde\lambda_t,
$$

$$
\tilde Y_t=c\tilde K_t+d\tilde\lambda_t.
$$

### 7.2 把资本和技术都写成过去冲击的函数

技术过程是

$$
\tilde\lambda_t=\gamma\tilde\lambda_{t-1}+\varepsilon_t.
$$

反复代入可得

$$
\tilde\lambda_t=\varepsilon_t+\gamma\varepsilon_{t-1}+\gamma^2\varepsilon_{t-2}+\cdots
=\sum_{i=0}^{\infty}\gamma^i\varepsilon_{t-i}.
$$

资本也会受过去技术冲击影响。由

$$
\tilde K_{t+1}=a\tilde K_t+b\tilde\lambda_t
$$

和技术过程递推，可以把资本写成过去冲击的加权和。书中给出：

$$
\tilde K_{t+1}
=b\sum_{i=0}^{\infty}\sum_{j=0}^{i}a^j\gamma^{i-j}\varepsilon_{t-i}.
$$

这一步的直觉是：技术冲击今天提高产出和投资，投资改变明天资本；资本又有自己的惯性 $a$，技术也有自己的惯性 $\gamma$，所以每个过去冲击都会通过两条 persistence channel 继续影响当前经济。

### 7.3 由冲击方差推出产出方差

把资本和技术的冲击表示代入

$$
\tilde Y_t=c\tilde K_t+d\tilde\lambda_t,
$$

可以得到产出是当前和过去技术冲击的线性组合。

因为不同期 $\varepsilon_t$ 独立，所以产出方差就是每个冲击系数平方之和乘以 $\operatorname{var}(\varepsilon_t)$。书中写成：

$$
\operatorname{var}(\tilde Y_t)
=\left(
 d^2+
 \sum_{i=0}^{\infty}
 \left[
 cb\sum_{j=0}^{i}a^j\gamma^{i-j}+d\gamma^{i+1}
 \right]^2
\right)
\operatorname{var}(\varepsilon_t).
$$

这个大括号里的系数只由模型政策函数和 $\gamma$ 决定。代入 basic model 的系数后，书中得到

$$
\operatorname{var}(\tilde Y_t)=30.0757\operatorname{var}(\varepsilon_t).
$$

取平方根就是

$$
\operatorname{sd}(\tilde Y_t)=\sqrt{30.0757}\sigma_\varepsilon=5.484\sigma_\varepsilon.
$$

### 7.4 用数据中的产出波动反推 $\sigma_\varepsilon$

Hansen 数据中 detrended log output 的标准差是

$$
\operatorname{sd}(\tilde Y_t)=0.0176.
$$

所以

$$
0.0176=5.484\sigma_\varepsilon.
$$

因此

$$
\sigma_\varepsilon=\frac{0.0176}{5.484}=0.0032.
$$

这就是第六章 basic model 的 technology shock 标准差。

注意这个数的含义：它不是直接从生产函数残差估计出来的残差标准差，而是“为了让模型产出波动等于数据产出波动，技术冲击需要有多大”。

---

## 8. 第八步：用同一个模型计算其他 moments，然后和数据比较

校准完 $\sigma_\varepsilon$ 后，模型就有完整数值版本了。现在可以计算模型生成的 second moments。

第六章 basic model 得到：

| 变量 | 标准差 | 相对产出标准差 |
|---|---:|---:|
| $\tilde Y_t$ | $5.484\sigma_\varepsilon$ | 100% |
| $\tilde C_t$ | $4.065\sigma_\varepsilon$ | 74.12% |
| $\tilde H_t$ | $1.640\sigma_\varepsilon$ | 29.90% |
| $\tilde r_t$ | $3.492\sigma_\varepsilon$ | 63.67% |
| $\tilde I_t$ | $11.742\sigma_\varepsilon$ | 214.1% |

数据中 Hansen 给出的相对标准差是：

| 变量 | 相对产出标准差 |
|---|---:|
| $\tilde Y_t$ | 100% |
| $\tilde C_t$ | 73.30% |
| $\tilde H_t$ | 94.32% |
| $\tilde I_t$ | 488.64% |

这一步就是 RBC 校准论文的经典评价方法。不是看模型能不能逐季预测 GDP，而是看模型能不能生成类似真实经济的 business cycle moments。

Basic Hansen model 的结论是：

- consumption volatility 匹配得不错：模型 74.12%，数据 73.30%；
- hours volatility 明显太低：模型 29.90%，数据 94.32%；
- investment volatility 明显太低：模型 214.1%，数据 488.64%。

所以 basic model 的问题不是“不会动”，而是 amplification 不够，尤其劳动和投资波动太弱。

---

## 9. 第九步：对 indivisible labor 模型再做一次校准

第六章接着引入 indivisible labor。这里校准逻辑很适合练手，因为它不是全部重来，而是在 basic model 基础上增加一个新的劳动结构。

### 9.1 Indivisible labor 的新设定：先把 \(h_t\)、\(H_t\)、\(\alpha_t\)、\(h_0\) 讲清楚

这里是最容易误会的一步。前面的 basic RBC 模型里，家庭直接连续选择劳动时间：

$$
H_t\in(0,1),
$$

效用函数是

$$
u(C_t,H_t)=\ln C_t + A\ln(1-H_t).
$$

这里 \(H_t\) 可以理解为“代表性家庭把多少比例的可用时间拿去工作”。如果

$$
H_t=0.3335,
$$

意思就是平均工作时间约占可用时间的三分之一，剩下

$$
1-H_t
$$

是 leisure。

但是 Hansen 引入 indivisible labor 以后，劳动选择的含义变了。

所谓 indivisible labor，不是说整个经济的总劳动不能连续变化，而是说**单个劳动者不能连续选择工作时间**。单个劳动者不是选择

$$
0.21,\quad 0.32,\quad 0.37
$$

这种连续工时，而是只能在两个状态之间选择：

$$
h_i\in\{0,h_0\}.
$$

其中：

- \(h_i=0\)：这个人本期不工作；
- \(h_i=h_0\)：这个人本期工作固定时长；
- \(h_0\)：一旦就业时的固定工时。

比如 \(h_0=0.583\)，意思是：如果一个人本期被安排工作，他就工作 0.583 个单位的可用时间；如果没被安排工作，他就工作 0。

所以 indivisible labor 的核心不是“宏观劳动不能变”，而是：

> 个体劳动是离散的；宏观劳动通过就业人数比例变化来调整。

---

#### 9.1.1 为什么宏观总劳动还能是连续的？

虽然每个人只能工作 \(0\) 或 \(h_0\)，但是整个经济里有很多人。于是宏观平均劳动可以通过“有多少人工作”来连续变化。

令

$$
\alpha_t
$$

表示本期被雇佣的人口比例，也可以理解为代表性家庭成员被抽中工作的概率。

那么 aggregate hours 是

$$
H_t=\alpha_t h_0.
$$

例如，如果

$$
h_0=0.5,
\qquad
\alpha_t=0.6,
$$

那么宏观平均劳动就是

$$
H_t=0.6\times 0.5=0.3.
$$

所以在 indivisible labor 模型里，\(H_t\) 或书中有时写作 \(h_t\)，更准确地说不是“每个人自己连续选择的工时”，而是：

$$
\text{平均劳动投入}
=
\text{就业概率/就业比例}
\times
\text{固定就业工时}.
$$

也就是：

$$
H_t=\alpha_t h_0.
$$

以后看到 indivisible labor 里的 \(h_t\) 或 \(H_t\)，要优先把它理解为 aggregate hours，而不是每个个体连续选择的 hours。

---

#### 9.1.2 Employment lottery 在这里起什么作用？

Hansen 为了让代表性家庭框架还能继续使用，引入了 employment lottery。

直观说，每一期家庭成员面对一个抽签机制：

- 以概率 \(\alpha_t\) 被抽中工作；
- 被抽中就工作 \(h_0\)；
- 没被抽中就工作 0。

同时，由于存在 insurance / risk sharing，家庭成员事前可以共享这种就业风险，所以我们可以用代表性家庭的**期望效用**来写问题。

如果一个人被抽中工作，那么他的劳动时间是 \(h_0\)，闲暇是

$$
1-h_0,
$$

所以 leisure utility 是

$$
A\ln(1-h_0).
$$

如果一个人没被抽中工作，那么劳动时间是 0，闲暇是

$$
1,
$$

所以 leisure utility 是

$$
A\ln(1)=0.
$$

因此，闲暇部分的期望效用是

$$
\alpha_t A\ln(1-h_0)
+
(1-\alpha_t)A\ln(1).
$$

因为

$$
\ln(1)=0,
$$

所以它简化成

$$
\alpha_t A\ln(1-h_0).
$$

再利用

$$
H_t=\alpha_t h_0,
$$

得到

$$
\alpha_t=\frac{H_t}{h_0}.
$$

代回期望效用：

$$
\alpha_t A\ln(1-h_0)
=
\frac{H_t}{h_0}A\ln(1-h_0).
$$

整理成

$$
A\frac{\ln(1-h_0)}{h_0}H_t.
$$

令

$$
B\equiv A\frac{\ln(1-h_0)}{h_0},
$$

于是 period utility 就可以写成

$$
u(C_t,H_t)=\ln C_t+B H_t.
$$

这就是

$$
u(c_t,h_t)=\ln c_t+B h_t
$$

这个形式的来源。它不是凭空换了一个偏好假设，而是从“个体劳动不可分 + employment lottery + insurance”推出来的等价代表性家庭效用函数。

---

#### 9.1.3 为什么 \(B H_t\) 不是“劳动越多效用越高”？

这个写法非常容易误导，因为它表面上是

$$
+\;B H_t.
$$

但关键在于：

$$
0<h_0<1
\quad\Rightarrow\quad
0<1-h_0<1
\quad\Rightarrow\quad
\ln(1-h_0)<0.
$$

而 \(A>0\)、\(h_0>0\)，所以

$$
B=A\frac{\ln(1-h_0)}{h_0}<0.
$$

因此

$$
u(C_t,H_t)=\ln C_t+B H_t
$$

本质上等价于

$$
u(C_t,H_t)=\ln C_t-\bar A H_t,
\qquad
\bar A\equiv -B>0.
$$

也就是说，劳动依然降低效用。只是 Hansen 这里把劳动负效用写成了一个线性项，而且这个线性项的系数 \(B\) 本身是负的。

所以初学时最好在脑子里把它翻译成：

$$
\text{效用}
=
\text{消费效用}
-
\text{劳动成本}.
$$

---

#### 9.1.4 为什么 indivisible labor 会让劳动项变成线性的？

在 basic divisible labor 模型里，效用是

$$
u(C_t,H_t)=\ln C_t+A\ln(1-H_t).
$$

对 \(H_t\) 求导：

$$
\frac{\partial u}{\partial H_t}
=
-\frac{A}{1-H_t}.
$$

这说明劳动的边际负效用不是常数。劳动越多，剩余闲暇越少，再多工作一点越痛苦。

但在 indivisible labor + employment lottery 后，效用变成

$$
u(C_t,H_t)=\ln C_t+B H_t.
$$

对 \(H_t\) 求导：

$$
\frac{\partial u}{\partial H_t}=B.
$$

由于 \(B\) 是常数，宏观劳动的边际效用成本也变成常数。

这就是 Hansen 模型想强调的机制：宏观劳动调整主要来自就业人数比例 \(\alpha_t\) 的变化，而不是每个工人连续微调自己的工时。因此劳动供给在宏观层面更“容易动”，模型生成的 hours volatility 会比 basic RBC 更大。

这也解释了为什么第六章后面会发现：indivisible labor 模型比 basic model 更能放大劳动和产出的波动。

---

#### 9.1.5 这一节和 calibration 有什么关系？

校准时要分清楚三个对象：

| 符号 | 含义 | 在校准中怎么用 |
|---|---|---|
| \(h_0\) | 一旦就业时的固定工时 | 需要通过稳态劳动目标反推 |
| \(\alpha_t\) | 本期就业概率 / 就业人口比例 | 稳态下由 \(\bar\alpha=\bar H/h_0\) 得到 |
| \(H_t=\alpha_t h_0\) | 宏观平均劳动投入 | 仍然要匹配长期平均工作时间 \(\bar H\approx 1/3\) |
| \(B=A\ln(1-h_0)/h_0\) | 线性劳动项的系数 | 由 \(A\) 和 \(h_0\) 推出，且 \(B<0\) |

所以 indivisible labor 模型的校准逻辑不是“随便给一个 \(B\)”，而是：

1. 沿用 basic model 的 \(A=1.72\)；
2. 要求 indivisible labor 模型的稳态平均劳动仍然满足

   $$
   \bar H\approx 0.3335;
   $$

3. 利用

   $$
   B=A\frac{\ln(1-h_0)}{h_0}
   $$

   和 indivisible labor 的稳态劳动公式反推出 \(h_0\)；
4. 再由

   $$
   \bar\alpha=\frac{\bar H}{h_0}
   $$

   得到稳态就业概率。

这就是为什么下面第 9.3 节要解 \(h_0\)，而不是直接把 \(B\) 当成一个独立参数拍脑袋设定。


### 9.2 哪些参数沿用 basic model？

为了让两个模型可比较，第六章保持：

$$
\beta=0.99,
\quad
\delta=0.025,
\quad
\theta=0.36,
\quad
A=1.72,
\quad
\gamma=0.95.
$$

并且希望 indivisible labor 模型的稳态 aggregate hours 仍然等于 basic model：

$$
\bar H=0.3335.
$$

这样两个模型的长期均值基本一致，差别主要来自劳动供给机制，而不是来自不同稳态。

### 9.3 用同一个 $\bar H$ 目标求 $h_0$

Indivisible labor 模型的稳态劳动公式是

$$
\bar H=-\frac{1-\theta}{B s_C},
$$

其中

$$
s_C=\frac{\bar C}{\bar Y}
=1-\frac{\beta\delta\theta}{1-\beta(1-\delta)}.
$$

同时

$$
B=\frac{A\ln(1-h_0)}{h_0}.
$$

我们希望 indivisible labor 的 $\bar H$ 等于 basic model 的 $\bar H$：

$$
\frac{1}{1+\frac{A}{1-\theta}s_C}
= -\frac{1-\theta}{\left(\frac{A\ln(1-h_0)}{h_0}\right)s_C}.
$$

这一步看起来复杂，但目标很简单：找到一个固定工作时长 $h_0$，使得随机就业概率下的 aggregate steady-state hours 还是 0.3335。

整理可得：

$$
\frac{h_0}{\ln(1-h_0)}
=G,
$$

其中

$$
G=-\frac{A s_C}{(1-\theta)+A s_C}.
$$

代入 $A=1.72$、$\theta=0.36$、$s_C=0.7436$：

$$
G=-0.6665.
$$

所以要解

$$
\frac{h_0}{\ln(1-h_0)}=-0.6665.
$$

这个方程没有方便的闭式解，直接用数值方法求。书中得到

$$
h_0=0.583.
$$

### 9.4 求稳态就业概率 $\bar\alpha$

aggregate hours 是

$$
\bar H=\bar\alpha h_0.
$$

所以

$$
\bar\alpha=\frac{\bar H}{h_0}.
$$

代入：

$$
\bar\alpha=\frac{0.3335}{0.583}=0.572.
$$

解释一下这个数字：每个家庭在一个季度有约 57.2% 的概率工作；一旦工作，就工作 $h_0=0.583$ 的可用时间。聚合起来，平均劳动仍然是 0.3335。

### 9.5 为什么 indivisible labor 的稳态变量和 basic model 接近？

因为我们刻意让

$$
\bar H=0.3335
$$

保持不变，同时 $\beta,\delta,\theta$ 也不变。

于是 Euler equation 决定的 $\bar r$ 不变；资本租金条件决定的 $\bar K/\bar H$ 不变；既然 $\bar H$ 不变，$\bar K$ 也不变；进而 $\bar Y$、$\bar C$、$\bar I$ 都基本不变。

书中 indivisible labor 稳态表给出：

| 变量 | 稳态值 |
|---|---:|
| $\bar H$ | 0.3335 |
| $\bar K$ | 12.6698 |
| $\bar Y$ | 1.2353 |
| $\bar C$ | 0.9186 |
| $\bar w$ | 2.3706 |
| $\bar r$ | 0.0351 |

真正变化的是动态响应和方差，不是长期均值。

---

## 10. 第十步：indivisible labor 下重新求 law of motion 和 shock size

因为劳动 FOC 变了，log-linear system 的矩阵也会变，政策函数会重新求。

书中得到 indivisible labor 模型的 law of motion：

$$
\tilde K_{t+1}=0.9418\tilde K_t+0.1552\tilde\lambda_t,
$$

以及

$$
y_t=R\tilde K_t+S\tilde\lambda_t,
$$

其中

$$
R=\begin{bmatrix}
0.0550\\
0.5316\\
-0.4766\\
-0.9450
\end{bmatrix},
\qquad
S=\begin{bmatrix}
1.9418\\
0.4703\\
1.4715\\
1.9417
\end{bmatrix}.
$$

也就是：

$$
\tilde Y_t=0.0550\tilde K_t+1.9418\tilde\lambda_t,
$$

$$
\tilde C_t=0.5316\tilde K_t+0.4703\tilde\lambda_t,
$$

$$
\tilde H_t=-0.4766\tilde K_t+1.4715\tilde\lambda_t,
$$

$$
\tilde r_t=-0.9450\tilde K_t+1.9417\tilde\lambda_t.
$$

用同样方法计算方差，书中得到：

| 变量 | 标准差 | 相对产出标准差 |
|---|---:|---:|
| $\tilde Y_t$ | $6.431\sigma_\varepsilon$ | 100% |
| $\tilde C_t$ | $4.081\sigma_\varepsilon$ | 63.46% |
| $\tilde H_t$ | $3.444\sigma_\varepsilon$ | 53.55% |
| $\tilde r_t$ | $4.514\sigma_\varepsilon$ | 70.19% |
| $\tilde I_t$ | $15.722\sigma_\varepsilon$ | 244.5% |

仍然匹配数据中的产出标准差：

$$
\operatorname{sd}(\tilde Y_t)=0.0176.
$$

所以

$$
0.0176=6.431\sigma_\varepsilon,
$$

$$
\sigma_\varepsilon=\frac{0.0176}{6.431}=0.0027.
$$

这比 basic model 的 0.0032 更小。原因是 indivisible labor 模型本身 amplification 更强：同样大小的技术冲击会引起更大的产出反应，所以要匹配同样的产出波动，所需的冲击标准差反而更小。

---

## 11. 到这里，我们到底完成了什么？

完整校准后，basic Hansen model 的参数是：

| 参数 | 数值 | 校准来源 / 目标 |
|---|---:|---|
| $\beta$ | 0.99 | 季度贴现因子，文献常用值 / 实际回报环境 |
| $\delta$ | 0.025 | 季度折旧率 |
| $\theta$ | 0.36 | 资本收入份额 |
| $A$ | 1.72 | 匹配 $\bar H\approx1/3$ |
| $\bar\lambda$ | 1 | 技术水平归一化 |
| $\gamma$ | 0.95 | Solow residual 的一阶自相关 |
| $\sigma_\varepsilon$ | 0.0032 | 使模型产出标准差等于 0.0176 |

稳态值是：

| 稳态变量 | 数值 |
|---|---:|
| $\bar H$ | 0.3335 |
| $\bar K$ | 12.6695 |
| $\bar Y$ | 1.2353 |
| $\bar C$ | 0.9186 |
| $\bar I$ | 0.3167 |
| $\bar r$ | 0.0351 |
| $\bar w$ | 2.3706 |

Indivisible labor 模型额外参数是：

| 参数 | 数值 | 校准来源 / 目标 |
|---|---:|---|
| $h_0$ | 0.583 | 使 indivisible labor 模型维持同样的 $\bar H$ |
| $\bar\alpha$ | 0.572 | $\bar\alpha=\bar H/h_0$ |
| $B$ | 约 -2.581 | $B=A\ln(1-h_0)/h_0$ |
| $\sigma_\varepsilon$ | 0.0027 | 使 indivisible labor 模型产出标准差等于 0.0176 |

---

## 12. 把这套方法抽象成“以后你自己校准 DSGE/RBC 模型”的流程

以后你拿到一个新模型，可以按下面顺序做。

### Step 1：列出所有 structural parameters

例如：

$$
\Theta=\{\beta,\delta,\theta,A,\gamma,\sigma_\varepsilon\}.
$$

如果有货币、税收、价格黏性，还会有货币增长率、税率、Calvo 参数、Taylor rule 参数等。

### Step 2：给每个参数找一个“来源”或“目标”

不要让一个参数没有来源。常见来源包括：

| 参数类型 | 常用校准来源 |
|---|---|
| 技术份额、资本份额 | 长期收入份额 |
| 折旧率 | 投资资本比、资本存量数据、文献 |
| 贴现因子 | 长期真实利率、文献常用值 |
| 劳动效用权重 | 平均工作时间 |
| 技术持久性 | Solow residual 的 AR(1) 系数 |
| 冲击标准差 | 产出波动、技术残差波动、或者模型矩匹配 |
| 政策参数 | 制度规则、政策数据、外部估计 |

### Step 3：先定外部参数，再反推内部参数

外部参数是指那些有直接数据对应物或文献共识的参数，例如 $\theta,\delta,\beta$。

内部参数是指那些没有直接观测值、需要用模型关系反推的参数，例如 $A$、$h_0$。

不要反过来做。比如你不能先随便定 $A$，再说模型稳态劳动是多少就接受多少。正确做法是先决定现实中平均劳动是多少，再选择 $A$ 让模型匹配它。

### Step 4：求 steady state，并做 FOC check

求完稳态以后，一定检查：

1. Euler equation 是否成立；
2. 劳动 FOC 是否成立；
3. 资源约束是否成立；
4. 生产函数是否成立；
5. factor price 是否和边际产出一致。

如果这些检查不通过，后面 log-linearization、IRF、simulation 都没有意义。

> **<u>【这里指的 FOC check 不是说 “求出稳态之后” 再做】：</u>**
>
> 1. 第一步我们能够直接根据数据确定一些简单的参数，例如折旧、资本份额、折现率；
>
> 2. 根据 FOC 方程组，直接列出稳态应该满足的方程，然后通过等式变形，将里面的 C、Y、K 等等变成现实数据中有的某个比值，然后代回稳态方程组，然后解出系数；
>
> 3. 因为方程组可能是超定的（现实数据多余剩余未知参数），因此我们解出参数之后，还要代回看看 FOC 是否成立：（并不是说解出了 C、K、Y 这些变量再代回，而是解出参数之后代回）
>
>     比如现实中的数据有很多比值，你用其中一个推导出了某个参数的取值，这个时候你把求出来的参数带到另外一个等式里面去，可能会导致算出来的结果导致等式不相等，这主要是因为现实中的数据很多，导致参数往往是超定的，满足了现实数据中的 C/Y 比值，可能就会导致 K/Y 比值满足不了，因此主要就是防止你用某个比值推导出了某个参数之后，再代入另外一个比值进行参数推导，进而导致矛盾的情况；
>
> 4. 因此总的来说，假设有 k 个参数，你可以用 k 套数据代入进去进行参数推导，推出来一定没问题；但是剩下的数据往往就会作为评价指标，看这个模型与现实数据拟合得好不好；

### Step 5：log-linearize 并求 policy functions

围绕稳态，把模型写成线性系统，求出类似

$$
\tilde K_{t+1}=P\tilde K_t+Q\tilde\lambda_t,
$$

$$
y_t=R\tilde K_t+S\tilde\lambda_t.
$$

这一步不是 calibration 本身，但它是校准 shock size 和计算 moments 的前提。

### Step 6：选择 shock size

常见有两种做法：

第一种，直接用外生冲击残差的标准差。例如估计 Solow residual AR(1)，取残差标准差作为 $\sigma_\varepsilon$。

第二种，像第六章一样，选择 $\sigma_\varepsilon$ 使模型生成的某个核心变量波动等于数据。Hansen 例子里就是匹配

$$
\operatorname{sd}(\tilde Y_t)=0.0176.
$$

这两种做法都可以，但你必须在文章或笔记里说明清楚。

### Step 7：留出一些 moments 不参与校准，用来检验模型

这是 RBC 校准最重要的经验。不能把所有 moments 都拿来调参数，否则模型当然能“拟合”数据，但没有检验意义。

第六章的做法是：

- 用平均工作时间校准 $A$；
- 用产出标准差校准 $\sigma_\varepsilon$；
- 然后看模型是否能匹配 consumption、hours、investment 的相对波动。

因此 consumption、hours、investment 的相对波动就有一定检验意义。

> ### 【My Step】
>
> 1. 列出 FOC 方程组；
> 2. 从中推出稳态 FOC 方程组；
> 3. 利用稳态 FOC 进行参数校准；
> 4. 校准完毕求出稳态变量（C、K、H、Y...）；
> 5. 对数线性化，将 control variable、未来的 state variable 表示成当期的 state variable 的线性方程组；

---

## 13. 一个最小可复现 Python 计算片段

下面这段代码只复现校准中的数值计算，不负责求解完整 log-linear system。政策函数系数直接使用第六章给出的结果。

```python
import math

# 1. Quarterly calibration from Hansen example
beta = 0.99
delta = 0.025
theta = 0.36
H_target = 0.3335
lambda_bar = 1.0

# 2. Steady-state capital return from Euler equation
r_bar = 1 / beta - (1 - delta)

# 3. Consumption-output ratio implied by beta, delta, theta
s_C = 1 - beta * delta * theta / (1 - beta * (1 - delta))

# 4. Choose A to match steady-state hours
A = (1 - theta) * (1 / H_target - 1) / s_C

# 5. Steady-state values
K_bar = H_target * (theta * lambda_bar / r_bar) ** (1 / (1 - theta))
Y_bar = lambda_bar * K_bar ** theta * H_target ** (1 - theta)
C_bar = Y_bar - delta * K_bar
I_bar = delta * K_bar
w_bar = (1 - theta) * Y_bar / H_target

print("A =", A)
print("r_bar =", r_bar)
print("K_bar =", K_bar)
print("Y_bar =", Y_bar)
print("C_bar =", C_bar)
print("I_bar =", I_bar)
print("w_bar =", w_bar)

# 6. Basic model shock size from output volatility
sd_Y_data = 0.0176
mult_Y_basic = 5.484
sigma_eps_basic = sd_Y_data / mult_Y_basic
print("sigma_eps_basic =", sigma_eps_basic)

# 7. Indivisible labor: solve h0 / log(1-h0) = G by bisection
G = - A * s_C / ((1 - theta) + A * s_C)

def f(h):
    return h / math.log(1 - h) - G

lo, hi = 1e-8, 0.999999
for _ in range(200):
    mid = (lo + hi) / 2
    # f(h) is monotone over the relevant interval for this target.
    if f(lo) * f(mid) <= 0:
        hi = mid
    else:
        lo = mid

h0 = (lo + hi) / 2
alpha_bar = H_target / h0
B = A * math.log(1 - h0) / h0

print("G =", G)
print("h0 =", h0)
print("alpha_bar =", alpha_bar)
print("B =", B)

# 8. Indivisible model shock size from output volatility
mult_Y_indivisible = 6.431
sigma_eps_indivisible = sd_Y_data / mult_Y_indivisible
print("sigma_eps_indivisible =", sigma_eps_indivisible)
```

运行后应得到大致结果：

```text
A ≈ 1.7201
r_bar ≈ 0.0351
K_bar ≈ 12.6695
Y_bar ≈ 1.2353
C_bar ≈ 0.9186
I_bar ≈ 0.3167
w_bar ≈ 2.3706
sigma_eps_basic ≈ 0.0032
h0 ≈ 0.5831
alpha_bar ≈ 0.572
B ≈ -2.581
sigma_eps_indivisible ≈ 0.0027
```

---

## 14. 最后用一句话总结第六章校准逻辑

第六章的校准不是“凭感觉给参数”，而是把每个参数绑定到一个经济对象：$\theta$ 绑定资本收入份额，$\delta$ 绑定折旧，$\beta$ 绑定跨期回报，$A$ 绑定平均工作时间，$\gamma$ 绑定技术残差持久性，$\sigma_\varepsilon$ 绑定产出波动，$h_0$ 绑定 indivisible labor 下同样的 aggregate steady-state hours。这样模型才从一组抽象 FOC 变成一台可以求解、模拟、画 IRF、和数据 moments 比较的 RBC 机器。
