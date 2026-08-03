# 宏观经济学高级数学与计算工具学习清单

> 适用对象：已经掌握基础微观、宏观、计量、动态规划与线性代数，希望继续学习 DSGE、最优政策、HANK、连续时间宏观或理论宏观的学习者。  
> 核心原则：**按研究问题触发学习，不要为了证明一个标准结论而提前学完整套抽象理论。**

---

## 0. 总体分层

### A 级：应用宏观的核心工具——应当真正掌握

- [ ] 动态规划：Bellman equation、policy function、value function
- [ ] Euler equation、costate、Hamiltonian 与 TVC
- [ ] 稳态、局部线性化与对数线性化
- [ ] 状态变量、控制变量、跳跃变量
- [ ] Blanchard–Kahn 条件
- [ ] Schur / generalized Schur（QZ）分解
- [ ] 线性二次控制（LQ）
- [ ] Riccati 方程与最优线性反馈
- [ ] 线性状态空间模型
- [ ] Lyapunov 方程与二阶矩
- [ ] Kalman filter
- [ ] 一阶与二阶 perturbation
- [ ] 基本数值优化、非线性方程求解与模拟

### B 级：做最优政策、非线性 DSGE 或 HANK 时按需学习

- [ ] Ramsey policy 与 commitment / discretion
- [ ] 二阶福利近似
- [ ] stabilizability 与 detectability
- [ ] Hamiltonian / symplectic system
- [ ] completion of squares
- [ ] occasionally binding constraints
- [ ] projection、time iteration、value function iteration
- [ ] endogenous grid method
- [ ] 稀疏矩阵与自动微分
- [ ] 分布动态与 Fokker–Planck / Kolmogorov forward equation
- [ ] sequence-space Jacobian

### C 级：理论宏观、连续时间或无限维模型才需要

- [ ] 泛函分析与 Hilbert space
- [ ] Fréchet / Gâteaux derivative
- [ ] 有界线性算子、自伴算子、强正定与 coercivity
- [ ] Lax–Milgram 定理
- [ ] 无限维动态规划
- [ ] HJB 偏微分方程
- [ ] viscosity solution
- [ ] 无限期随机最大值原理
- [ ] FBSDE / forward-backward stochastic systems
- [ ] operator Riccati equation
- [ ] mean-field games 与 master equation
- [ ] 测度空间上的动态系统

---

# 第一部分：动态优化的基础骨架

## 1. 离散时间动态规划

### 需要掌握

- [ ] Bellman principle
- [ ] value function 与 policy function
- [ ] contraction mapping 的直觉
- [ ] envelope condition
- [ ] Euler equation 与 Bellman FOC 的对应关系
- [ ] deterministic 与 stochastic Bellman equation
- [ ] Markov state 的充分性

### 学到什么程度算够

能够从标准 RBC planner problem 写出：

\[
V(k,z)=\max_{c,k'}\left\{u(c,h)+eta E[V(k',z')\mid z]ight\},
\]

并解释状态、控制、约束、期望与政策函数。

### 什么时候升级

当模型包含不可微点、借贷约束、离散选择或分布状态时，再学习全局动态规划和函数逼近。

---

## 2. 最大值原理、costate 与 TVC

### 需要掌握

- [ ] current-value Hamiltonian
- [ ] state equation
- [ ] control FOC
- [ ] costate equation
- [ ] transversality condition
- [ ] Euler equation 与 costate system 的等价关系
- [ ] 必要条件与充分条件的区别

### 核心用途

- 理解无限期动态优化如何由局部 FOC 与无穷远边界共同确定；
- 理解为什么 Euler 方程本身通常不足以选出唯一最优路径；
- 为 Ramsey policy、连续时间宏观和最优税收打基础。

---

# 第二部分：线性化、稳定性与 DSGE 求解

## 3. 稳态与局部近似

### 需要掌握

- [ ] 求确定性稳态
- [ ] 一阶 Taylor expansion
- [ ] 二阶 Taylor expansion
- [ ] level deviation 与 log deviation
- [ ] 对乘积、比值和期望算子的线性化
- [ ] certainty equivalence 在一阶解中的含义

### 必须分清

\[
	ext{原非线性模型}
\quad
eq\quad
	ext{线性化后得到的新线性系统}.
\]

线性化后的求解可以是这个线性系统的精确解，但仍只是原模型的局部近似。

---

## 4. Blanchard–Kahn、Schur 与 QZ

### 需要掌握

- [ ] predetermined state 与 jump variable
- [ ] stable root 与 unstable root
- [ ] BK existence / uniqueness condition
- [ ] invariant subspace
- [ ] generalized eigenvalue problem
- [ ] Schur decomposition
- [ ] generalized Schur / QZ decomposition
- [ ] policy matrix 的提取

### 学到什么程度算够

能够理解：

\[
\Gamma_0 E_t y_{t+1}=\Gamma_1 y_t+\Psiarepsilon_t
\]

为什么需要按稳定与不稳定广义特征值分块，以及 jump variables 如何被稳定子空间锁定。

### 主要用途

- 标准线性 DSGE；
- Dynare、gensys 等求解器；
- 给定政策规则下的 IRF 与 moments；
- 判断不存在、唯一或多重均衡。

---

# 第三部分：LQ、Riccati 与最优政策

## 5. Linear–Quadratic control

标准形式：

\[
\min E_0\sum_{t=0}^{\infty}eta^t
\left(x_t'Qx_t+2x_t'Nu_t+u_t'Ru_tight)
\]

subject to

\[
x_{t+1}=Ax_t+Bu_t+Carepsilon_{t+1}.
\]

### 需要理解

- [ ] 二次目标与线性约束
- [ ] 二次值函数
- [ ] 线性最优反馈
- [ ] certainty equivalence
- [ ] closed-loop system
- [ ] finite-horizon 与 infinite-horizon 的区别

### 主要用途

- 最优货币政策；
- 最优财政政策；
- 最优动态税率；
- 自动稳定器设计；
- quadratic welfare loss；
- commitment 与 discretion 的基准分析。

---

## 6. Riccati 方程

### 需要掌握

- [ ] Riccati recursion
- [ ] algebraic Riccati equation
- [ ] stabilizing solution
- [ ] 由 \(P\) 得到反馈矩阵 \(F\)
- [ ] 闭环矩阵 \(A+BF\)
- [ ] Riccati 与 Bellman fixed point 的关系
- [ ] Riccati 与 Hamiltonian 稳定子空间的关系

### 学到什么程度算够

能够解释：

\[
P
=
Q+eta A'PA
-
(N+eta A'PB)
(R+eta B'PB)^{-1}
(N'+eta B'PA)
\]

是在求什么，而不是必须手工证明所有存在唯一性定理。

---

## 7. Stabilizability 与 detectability

- **stabilizability**：政策工具是否有能力控制所有危险的不稳定方向；
- **detectability**：目标函数是否能够“看见”那些不稳定且会造成损失的状态方向。

### 什么时候需要认真学习

- 无限期 LQ；
- 最优政策存在唯一性；
- Riccati stabilizing solution；
- 部分状态不受控制或不进入损失函数时。

---

# 第四部分：随机动态、状态空间与二阶矩

## 8. 随机过程基础

- [ ] filtration
- [ ] adapted process
- [ ] conditional expectation
- [ ] martingale difference
- [ ] covariance stationarity
- [ ] AR、VAR、Markov process
- [ ] law of iterated expectations
- [ ] \(L^2\) 随机变量的基本概念

### 宏观用途

技术、偏好、财政与货币冲击；理性预期；状态空间模型；随机控制；Bayesian estimation。

---

## 9. Lyapunov 方程与 second moments

对闭环系统：

\[
x_{t+1}=Gx_t+Carepsilon_{t+1},
\]

平稳协方差满足：

\[
\Sigma_x
=
G\Sigma_xG'
+
C\Sigma_arepsilon C'.
\]

### 需要掌握

- [ ] 无条件方差
- [ ] 协方差与相关系数
- [ ] 自相关
- [ ] 稳定性条件
- [ ] simulation moments 与 analytical moments
- [ ] HP filter 对 moments 的影响

---

## 10. State-space model 与 Kalman filter

\[
x_{t+1}=Ax_t+Barepsilon_{t+1},
\qquad
y_t=Cx_t+D\eta_t.
\]

- [ ] latent state 与 observables
- [ ] prediction step
- [ ] update step
- [ ] Kalman gain
- [ ] filter Riccati equation
- [ ] likelihood evaluation
- [ ] smoothing

### 主要用途

DSGE Bayesian estimation、潜在产出与自然利率估计、nowcasting、宏观金融因子模型。

---

# 第五部分：更高阶扰动与福利分析

## 11. Perturbation methods

### 一阶扰动

- 线性政策函数；
- certainty equivalence；
- 适合 IRF、局部动态和基本 moments。

### 二阶扰动

- [ ] 政策函数的二次项
- [ ] 风险方差对均值和政策的影响
- [ ] precautionary behavior
- [ ] stochastic steady state
- [ ] pruning

### 三阶扰动

通常在研究时变风险溢价、skewness、stochastic volatility、不确定性冲击时使用。

### 触发条件

若研究问题涉及“风险本身改变平均决策”，一阶解通常不够。

---

## 12. 二阶福利近似

- [ ] 为什么一阶效用近似无法完整衡量福利损失
- [ ] quadratic welfare loss
- [ ] policy rule comparison
- [ ] unconditional welfare 与 conditional welfare
- [ ] steady-state distortion
- [ ] timeless perspective

### 主要用途

最优 VAT、Ramsey taxation、最优货币政策、自动稳定器参数选择、政策规则福利排序。

---

# 第六部分：全局非线性解法

## 13. 基础全局数值方法

- [ ] grid discretization
- [ ] value function iteration
- [ ] policy function iteration
- [ ] time iteration
- [ ] projection / collocation
- [ ] Chebyshev polynomial
- [ ] interpolation
- [ ] numerical integration / quadrature
- [ ] Monte Carlo simulation

### 什么时候需要

远离稳态、大冲击、强非线性、风险与预防性行为、约束可能绑定、政策函数存在明显曲率。

---

## 14. Occasionally binding constraints

### 常见情形

- 零利率下限；
- 借贷约束；
- 不可逆投资；
- 税率上下限；
- 财政规则触发阈值。

### 工具

- [ ] piecewise-linear methods
- [ ] OccBin 思路
- [ ] regime switching
- [ ] complementarity problem
- [ ] mixed complementarity solver

---

# 第七部分：异质性主体与 HANK

## 15. 异质性主体模型基础

- [ ] incomplete markets
- [ ] idiosyncratic risk
- [ ] borrowing constraint
- [ ] stationary wealth distribution
- [ ] household policy functions
- [ ] aggregation
- [ ] market clearing

### 数值工具

- [ ] endogenous grid method
- [ ] histogram method
- [ ] lottery method
- [ ] sparse transition matrix
- [ ] stationary distribution computation

---

## 16. 分布动态与 sequence-space methods

- [ ] 分布作为状态变量
- [ ] Jacobian of aggregate outcomes
- [ ] sequence-space Jacobian
- [ ] fake-news algorithm 的思想
- [ ] general equilibrium fixed point
- [ ] impulse responses in HANK

### 什么时候值得学

当代表性家庭 DSGE 无法回答收入分配、财富异质性、MPC 或政策异质性传导问题时。

---

# 第八部分：连续时间宏观

## 17. 连续时间最优控制

- [ ] ordinary differential equations
- [ ] continuous-time Hamiltonian
- [ ] HJB equation
- [ ] costate equation
- [ ] saddle-path stability
- [ ] phase diagram

## 18. 随机微积分

- [ ] Brownian motion
- [ ] Itô lemma
- [ ] stochastic differential equation
- [ ] generator
- [ ] Feynman–Kac
- [ ] change of measure 的基本概念

### 主要用途

连续时间资产定价、连续时间宏观金融、随机增长模型、不确定性与灾难风险。

---

## 19. HJB 与 Kolmogorov / Fokker–Planck

典型连续时间异质性主体模型由两部分构成：

\[
	ext{HJB：个体最优决策},
\qquad
	ext{KFE / Fokker–Planck：分布演化}.
\]

### 什么时候学习

continuous-time HANK、连续时间 Aiyagari、mean-field macro、分布动态研究。

---

# 第九部分：真正高级的理论工具

## 20. 泛函分析与 Hilbert space

- [ ] normed space
- [ ] Banach space
- [ ] Hilbert space
- [ ] orthogonal projection
- [ ] bounded linear operator
- [ ] adjoint operator
- [ ] spectrum
- [ ] compactness
- [ ] coercivity

### 宏观中的用途

无限期控制序列空间、分布或函数作为状态变量、无限维动态规划、operator equation 的存在唯一性。

### 建议

除非进入理论宏观、无限维控制或连续时间异质性主体模型，否则先不系统学习。

---

## 21. Fréchet derivative 与无限维优化

### 需要掌握的场景

- 目标函数的自变量是一整条路径；
- 状态是函数或概率分布；
- 需要对函数空间中的映射求导；
- 研究 sequence-space derivative 的严格基础。

---

## 22. 无限期随机最大值原理与 FBSDE

### 核心对象

- forward state equation
- backward costate equation
- adapted solution
- infinite-horizon boundary condition
- decoupling field
- existence and uniqueness

### 宏观用途

连续时间随机控制、recursive utility、理论化的无限期 LQ 证明、mean-field models。

### 当前优先级

低。知道它们在解决什么问题即可，不需要为了标准 DSGE 而提前学习。

---

## 23. Mean-field games 与 master equation

### 前置知识

- stochastic control
- HJB
- Fokker–Planck
- PDE
- measure derivatives
- fixed-point theory

### 适用方向

大量异质性主体相互作用、分布外部性、连续体主体之间的策略互动、理论宏观与宏观金融前沿模型。

---

# 第十部分：宏观估计与计算

## 24. Bayesian DSGE estimation

- [ ] likelihood
- [ ] prior / posterior
- [ ] Metropolis–Hastings
- [ ] identification
- [ ] Kalman filter likelihood
- [ ] posterior predictive checks
- [ ] marginal likelihood
- [ ] impulse response uncertainty

---

## 25. 数值线性代数与计算工具

### 高优先级

- [ ] sparse matrix
- [ ] eigenvalue / generalized eigenvalue
- [ ] Schur / QZ
- [ ] Kronecker product
- [ ] Sylvester equation
- [ ] Lyapunov equation
- [ ] automatic differentiation
- [ ] numerical conditioning
- [ ] nonlinear root finding
- [ ] constrained optimization

很多 DSGE 难点不是经济学概念，而是矩阵规模、病态性和数值稳定性。

---

# 第十一部分：按研究目标选择路线

## 路线 A：标准 DSGE 与动态 VAT

1. 动态规划、Euler、costate、TVC  
2. 稳态与对数线性化  
3. BK、Schur/QZ  
4. 状态空间、IRF、Lyapunov moments  
5. LQ、Riccati 与 quadratic welfare  
6. Ramsey policy / optimal simple rule  
7. 二阶 perturbation  
8. occasionally binding constraints  

### 暂时不需要

Hilbert space 严格理论、FBSDE、operator Riccati、mean-field games。

## 路线 B：最优财政与货币政策

重点增加：

- LQ regulator
- quadratic welfare approximation
- commitment / discretion
- timeless perspective
- Ramsey planner
- implementability constraint
- stabilizing Riccati solution
- policy rule design

## 路线 C：HANK 与分配效应

重点增加：

- incomplete markets
- heterogeneous households
- EGM
- distribution dynamics
- sparse transition matrix
- sequence-space Jacobian
- automatic differentiation
- occasionally binding constraints

## 路线 D：连续时间宏观金融

重点增加：

- ODE / PDE
- stochastic calculus
- HJB
- Fokker–Planck
- Feynman–Kac
- continuous-time filtering
- FBSDE
- affine models 与 Riccati ODE

## 路线 E：纯理论动态宏观

重点增加：

- real analysis
- measure theory
- functional analysis
- fixed-point theorem
- operator theory
- infinite-dimensional optimization
- stochastic control existence theorems
- viscosity solutions
- ergodic theory

---

# 第十二部分：推荐学习顺序

## 阶段 1：应用 DSGE 核心

- [ ] Bellman / Euler / costate / TVC
- [ ] steady state
- [ ] log-linearization
- [ ] BK / Schur / QZ
- [ ] state-space representation
- [ ] IRF 与 moments
- [ ] Lyapunov equation

## 阶段 2：政策与福利

- [ ] LQ control
- [ ] Riccati equation
- [ ] stabilizability / detectability
- [ ] quadratic welfare
- [ ] Ramsey policy
- [ ] commitment / discretion

## 阶段 3：非线性与风险

- [ ] second-order perturbation
- [ ] pruning
- [ ] global solution methods
- [ ] occasionally binding constraints
- [ ] uncertainty shocks

## 阶段 4：按研究方向分流

- HANK：EGM、分布动态、sequence-space
- 连续时间：Itô、HJB、Fokker–Planck
- 理论宏观：泛函分析、无限维控制、FBSDE
- 宏观估计：Kalman、Bayesian methods、identification

---

# 第十三部分：学习触发器

| 研究问题 | 应补的工具 |
|---|---|
| 给定政策规则，研究 IRF | 一阶线性化、BK、Schur/QZ |
| 比较模型波动率 | Lyapunov 方程、simulation moments |
| 求最优 VAT 或最优利率规则 | LQ、Riccati、二阶福利近似 |
| 风险方差影响决策 | 二阶或三阶 perturbation |
| 税率有上下限 | occasionally binding constraints |
| 离稳态很远 | projection、time iteration、global methods |
| 研究收入与财富分配 | HANK、EGM、分布动态 |
| 状态是一个分布或函数 | sequence-space、泛函分析 |
| 连续时间模型 | Itô、HJB、Fokker–Planck |
| 直接证明无限期随机控制存在唯一性 | Hilbert space、FBSDE、operator theory |
| 研究 mean-field interaction | mean-field games、master equation |

---

# 最后的学习原则

1. **先学能直接解决研究问题的工具。**
2. **先掌握经济含义与矩阵结构，再补存在唯一性证明。**
3. **不要为了证明标准 LQ 的线性政策，提前系统学习整套泛函分析。**
4. **遇到分布状态、连续时间或理论存在性问题时，再进入无限维方法。**
5. **对应用宏观而言，数值线性代数、状态空间和求解器往往比抽象证明更重要。**

对当前的动态 VAT / DSGE 研究，最合理的边界是：

\[
oxed{
	ext{熟练掌握 LQ、Riccati、Schur/QZ、Lyapunov 与福利近似；}
}
\]

\[
oxed{
	ext{知道 Hilbert space、FBSDE 和 operator Riccati 在解决什么问题，但暂不系统深入。}
\]
