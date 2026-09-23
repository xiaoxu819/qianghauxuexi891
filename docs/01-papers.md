# Papers / 论文分册

> [← 返回总索引](../README.md)
>
> 本分册收录「无人机抗风 + 航迹规划 + 强化学习」方向**最权威的 35 篇文献**，
> 按 **① 权威期刊 → ② 顶会 → ③ 最新期刊（2025–2026） → ④ 综述与博士论文** 四类归档。
> 标题统一 `English（中文）` 格式，⭐ 表示最推荐精读。

---

## 目录

- [Ⅰ. 权威期刊论文 / Top-Tier Journal Papers](#Ⅰ-权威期刊论文--top-tier-journal-papers)
- [Ⅱ. 顶会论文 / Top Conference Papers](#Ⅱ-顶会论文--top-conference-papers)
- [Ⅲ. 最新期刊论文（2025–2026）/ Latest Journal Papers](#Ⅲ-最新期刊论文20252026--latest-journal-papers)
- [Ⅳ. 综述与博士论文 / Surveys & Theses](#Ⅳ-综述与博士论文--surveys--theses)

---

## Ⅰ. 权威期刊论文 / Top-Tier Journal Papers

> 均为 IEEE 汇刊 / Science Robotics 级别，**中科院一区或顶刊**，是方法论的权威依据。

### ⭐ Neural-Fly Enables Rapid Learning for Agile Flight in Strong Winds（强风环境下敏捷飞行的快速学习方法）
- **Source**: *Science Robotics*（顶级期刊 / Top Journal）, 2022
- **Link**: [论文](https://www.science.org/doi/10.1126/scirobotics.abm6597) · [代码](https://github.com/aerorobotics/neural-fly)
- **说明**: 抗风飞行方向**最顶级的期刊成果**。提出「域适应 + 元学习」的 Neural-Fly 控制器，通过在线线性组合少量基函数实现对新风况的快速自适应；Caltech 风洞实测风速至 12.1 m/s。是本项目「气象特征融合」与「域随机化 sim-to-real」两条技术路线的重要参照。

### ⭐ Deep Reinforcement Learning of UAV Tracking Control Under Wind Disturbances Environments（基于深度强化学习的无人机风扰环境跟踪控制）
- **Source**: *IEEE Transactions on Instrumentation and Measurement (TIM)* · TOP / 中科院一区, 2023
- **Link**: [论文](https://ieeexplore.ieee.org/document/10099019)
- **说明**: 直接把风扰作为环境不确定性纳入 DRL 跟踪控制的代表性工作，给出了观测设计、奖励塑形与风扰工况下的跟踪性能对比范式，可作为「PPO 复现基线」的对标对象。

### ⭐ Anti-Disturbance Compensation for Quadrotor Close Crossing Flight Based on Deep Reinforcement Learning（基于深度强化学习的四旋翼近距离穿越飞行抗干扰补偿）
- **Source**: *IEEE Transactions on Industrial Electronics (TIE)* · TOP / 中科院一区, 2023
- **Link**: [论文](https://ieeexplore.ieee.org/document/9773012)
- **说明**: 面向「近距离穿越」这一强气动干扰极端工况，用 DRL 学习抗扰补偿量。展示了 DRL 相对传统控制在高动态、强耦合扰动下的优势，说明「扰动补偿可被学习」。

### Robust Wind-Resistant Hovering Control of Quadrotor UAVs Using Deep Reinforcement Learning（基于深度强化学习的四旋翼无人机鲁棒抗风悬停控制）
- **Source**: *IEEE Transactions on Intelligent Vehicles (T-IV)*, 2023
- **Link**: [论文](https://ieeexplore.ieee.org/document/10286087)
- **说明**: 聚焦最基础也最关键的**抗风悬停**任务，可作为环境搭建阶段（悬停任务）的第一个对标论文。

### Active Wind Rejection Control for a Quadrotor UAV Against Unknown Winds（四旋翼无人机面向未知风的主动抗风控制）
- **Source**: *IEEE Transactions on Aerospace and Electronic Systems (TAES)*, 2023
- **Link**: [论文](https://ieeexplore.ieee.org/document/10251643)
- **说明**: 强调**未知风**（无风速传感器 / 风场不可测）前提下的主动抑制，对「必须由可观测状态反演风」这一技术问题给出了控制侧解法。

### Adaptive Stabilization Control by Deep Reinforcement Learning for Hovering Drone Surveillance（基于深度强化学习的悬停无人机监视自适应稳定控制）
- **Source**: *IEEE Transactions on Mobile Computing (TMC)*, 2025
- **Link**: [论文](https://ieeexplore.ieee.org/document/10912732)
- **说明**: 把抗风稳定控制放到「监视任务」这一实际应用语境中考察，兼顾任务级指标（覆盖、时长）与底层稳定性，适合讨论「任务-控制」联合优化。

### Physical-Constraint-Embedded Deep Reinforcement Learning Approach for Flight Control of Flying-Wing Vehicle（嵌入物理约束的深度强化学习方法及飞翼飞行器飞行控制）
- **Source**: *IEEE Transactions on Automation Science and Engineering (TASE)*, 2026
- **Link**: [论文](https://ieeexplore.ieee.org/document/11419124)
- **说明**: 把**物理约束嵌入**到 DRL 训练中，与本项目「安全护盾 / 控制屏障函数」路线同源，是安全强化学习在飞行控制上的最新代表。

---

## Ⅱ. 顶会论文 / Top Conference Papers

> 覆盖 IROS / ICRA / CoRL / NeurIPS / IJCAI，多为**方法首创或开源基座**，是复现与改进的直接起点。

### ⭐ NavRL: Learning Safe Flight in Dynamic Environments（动态环境下的安全飞行）
- **Source**: *IEEE RA-L 2025*（IEEE Robotics and Automation Letters）
- **Link**: [论文](https://ieeexplore.ieee.org/document/10904341) · [arXiv](https://arxiv.org/abs/2409.15634) · [代码](https://github.com/Zhefan-Xu/NavRL) · DOI: `10.1109/LRA.2025.3546069`
- **说明**: **PPO 策略 + 基于速度障碍（VO）的安全护盾**，用线性规划约束策略输出；在 NVIDIA Isaac Sim 中构建**数千架四旋翼并行训练管线**，实现零样本 sim-to-real；已完成真机验证并开源 ROS1/ROS2 部署代码与预训练模型。是本项目「PPO 主算法 + 安全约束」路线最直接的对标工作。

### ⭐ Learning to Fly — a Gym Environment with PyBullet Physics for Reinforcement Learning of Multi-agent Quadcopter Control（面向多智能体四旋翼控制强化学习的 PyBullet 物理引擎 Gym 环境）
- **Source**: *IROS 2021*（IEEE/RSJ Int. Conf. on Intelligent Robots and Systems）
- **Link**: [论文](https://ieeexplore.ieee.org/document/9635857) · [代码](https://github.com/utiasDSL/gym-pybullet-drones)
- **说明**: `gym-pybullet-drones` 的**论文出处**。定义了单机 / 多机四旋翼的 Gymnasium 环境、悬停与轨迹跟踪任务、下洗气流建模。本项目环境封装阶段应优先对照该环境接口规范。

### ⭐ Flightmare: A Flexible Quadrotor Simulator（Flightmare：一款灵活的四旋翼仿真器）
- **Source**: *CoRL 2020*（Conference on Robot Learning）
- **Link**: [论文](https://proceedings.mlr.press/v155/song21a.html) · [PDF](https://proceedings.mlr.press/v155/song21a/song21a.pdf) · [代码](https://github.com/uzh-rpg/flightmare)
- **说明**: 提出「渲染与物理解耦」的仿真架构（渲染 230 Hz、物理 20 万 Hz），支持千万级并行采样，是**高性能 RL 训练仿真器**的经典设计参考。

### DATT: Deep Adaptive Trajectory Tracking（四旋翼深度自适应轨迹跟踪）
- **Source**: *CoRL 2023 Oral*
- **Link**: [论文](https://openreview.net/forum?id=XEw-cnNsr6) · [PDF](https://openreview.net/pdf?id=XEw-cnNsr6) · [项目主页](https://sites.google.com/view/deep-adaptive-traj-tracking) · [代码](https://github.com/KevinHuang8/DATT)
- **说明**: 提出学习式「**前馈 + 反馈 + 自适应**」控制结构，仿真中用 RL 训练，真机部署时叠加扰动估计器 L1 在闭环内微调、**无需重新训练策略**。实测跟踪 RMSE：DATT `0.05 m`、MPC `0.11 m`、非线性基线 `0.30 m`，推理时延 < 3.2 ms。是本项目「仿真训练 → 真机迁移」的极佳范本。

### GustPilot: Hierarchical DRL-INDI for Wind-Resistant Quadrotor Navigation（分层 DRL-INDI 抗风四旋翼导航）
- **Source**: *arXiv 预印本*, 2026（`2603.19966`）
- **Link**: [论文](https://arxiv.org/abs/2603.19966) · [PDF](https://arxiv.org/pdf/2603.19966.pdf)
- **说明**: **分层架构**：DRL（PPO）高层输出惯性系速度参考（17 维状态），INDI（增量非线性动态逆）底层做几何非线性增量控制抑制风致扰动；用风扇射流域域随机化 + Gym-PyBullet 环境实现零样本真机迁移。**80 次真机飞行结果：DRL-INDI 平均成功率 94.6%，DRL-PID 基线仅 36.0%；跟踪 RMSE 最高降低 50%；3.5 m/s 风扰下仍维持 1.34 m/s 速度。** 抗风方向最具说服力的实证之一。

### WA-TD3: Wind-Aware Twin Delayed DDPG（极端风场下的扰动感知混合学习）
- **Source**: *IJCAI-26*（Special Track on AI and Robotics）
- **Link**: [论文](https://www.ijcai.org/proceedings/2026/0844.pdf)
- **说明**: 用**深度残差网络**从「状态偏差时序」中**隐式提取风场特征**，构成风感知增强的 RL 框架；强风下跟踪精度比既有 SOTA 提升 **> 62%**，且**全程无需显式风传感器**。对应本项目「网络结构级」气象特征融合方案。

### Disturbance Observer-based Control Barrier Functions with Residual Model Learning for Safe Reinforcement Learning（基于扰动观测器与残差模型学习的控制屏障函数用于安全强化学习）
- **Source**: *IROS 2025*
- **Link**: [论文](https://arxiv.org/abs/2410.06570)
- **说明**: 把**扰动观测器（DOB）+ 残差模型学习**嵌入控制屏障函数（CBF），在保证安全约束的同时补偿未建模扰动。是「安全 + 抗扰」交叉方向的代表性方法。

### Distributed Perception Aware Safe Leader Follower System via Control Barrier Methods（基于控制屏障方法的分布式感知安全领导者-跟随者系统）
- **Source**: *ICRA 2025*
- **Link**: [论文](https://arxiv.org/abs/2409.11394)
- **说明**: 面向**多机编队**的分布式安全控制：用控制屏障方法保证感知感知下的安全跟随。是本项目「单机 → 多机扩展」阶段的编队安全参考。

### ⭐ MAPPO: The Surprising Effectiveness of PPO in Cooperative Multi-Agent Games（PPO 在协作多智能体任务中的惊人有效性）
- **Source**: *NeurIPS 2022*
- **Link**: [论文](https://openreview.net/forum?id=YVXaxB6L2Pl) · [代码](https://github.com/marlbenchmark/on-policy)
- **说明**: 证明 PPO 在 SMAC / MPE 等基准上与 off-policy 方法**持平或更优**，成为 CTDE 范式的多智能体事实标准（MAPPO 官方实现 ⭐2107，MIT 许可）。是本项目「单机 PPO → 多机 MAPPO」扩展路径的理论支撑。

### VolleyBots: A Testbed for Multi-Drone Volleyball Game（多无人机排球对抗测试平台）
- **Source**: *NeurIPS 2025*
- **Link**: [论文](https://openreview.net/forum?id=FRbNGgWqCX) · [代码](https://github.com/thu-uav/VolleyBots)
- **说明**: 2025 年最新的多无人机动态协作测试平台，同样验证了 PPO 在多机高风险动态任务上的竞争力，可作为多机实验的可选环境。

---

## Ⅲ. 最新期刊论文（2025–2026）/ Latest Journal Papers

> 反映**当下最前沿**的做法：风场 + 能耗联合优化、演示引导安全控制、泛化性设计、DRL-MPC 混合。

### A Reinforcement Learning Framework for Energy-Optimal UAV Path Planning in Wind Fields（一种用于风场中无人机能量最优路径规划的强化学习框架）
- **Source**: *Pattern Recognition* · 中科院一区 (CAS Q1), 2026
- **Link**: [论文](https://www.sciencedirect.com/science/article/pii/S0031320325015754)
- **说明**: 关键词组合 **风场 + 能耗 + PRM（概率路线图）+ CNN**。把气象场作为先验融入路径代价，是「气象信息 → 航迹规划」端到端改造的代表作。

### EGP2: A Sample-Efficient and Generalizable Reinforcement Learning Framework for UAV Path Planning（面向无人机路径规划的高样本效率与强泛化强化学习框架）
- **Source**: *Robotics and Autonomous Systems* · JCR Q1, 2026
- **Link**: [论文](https://www.sciencedirect.com/science/article/pii/S0921889026003428)
- **说明**: 直击 RL 路径规划两大痛点——**样本效率**与**风扰下的泛化性**，是评估本项目策略泛化能力的对标基准。

### Safe UAV Control Against Wind Disturbances via Demonstration-Guided Reinforcement Learning（通过演示引导的强化学习实现无人机抗风扰安全控制）
- **Source**: *Drones* · JCR Q1, 2026
- **Link**: [论文](https://www.mdpi.com/2504-446X/10/1/2)
- **说明**: **PPO + PID + CBF** 三件套组合，用演示（demonstration）引导加速训练并保证安全性，面向**阵风抗扰**。是「传统控制先验 → 强化学习」融合的清晰范例。

### Trajectory Planning and Tracking for UAVs with Deep Reinforcement Learning and Adaptive Nonlinear MPC（基于深度强化学习与自适应非线性 MPC 的无人机轨迹规划与跟踪）
- **Source**: *Expert Systems with Applications* · JCR Q1, 2025
- **Link**: [论文](https://www.sciencedirect.com/science/article/pii/S0957417425042642)
- **说明**: **DRL + 自适应非线性 MPC 混合**架构。与本项目「TD-MPC 作为模型+学习中间基线」的对比设计高度契合。

### A CCO-PPO Framework for Autonomous UAV Trajectory Tracking in Complex and Disturbed Environments（CCO-PPO 框架：复杂受扰环境下的无人机自主轨迹跟踪）
- **Source**: *Sensors* · JCR Q1, 2026
- **Link**: [论文](https://www.mdpi.com/1424-8220/26/9/2735)
- **说明**: 针对**复杂受扰环境**对 PPO 做结构化改进（CCO），可作为「PPO 改进版」的直接对照实现思路。

### A Method for UAV Path Planning Based on G-MAPONet Reinforcement Learning（基于 G-MAPONet 强化学习的无人机路径规划方法）
- **Source**: *Drones* · JCR Q1, 2025
- **Link**: [论文](https://www.mdpi.com/2504-446X/9/12/871)
- **说明**: 关键词 **GAT（图注意力网络）+ GRPO**，用图结构建模空间关系。适合参考「网络结构级」改进中的注意力/图结构分支设计。

### Wind Disturbance-Resilient Flight Control for Small and Medium-Sized UAVs in Plateau Canyon Environments Using Deep Reinforcement Learning（基于深度强化学习的中小型无人机高原峡谷环境抗风扰飞行控制）
- **Source**: *Journal of Northwestern Polytechnical University*（西北工业大学学报）· EI, 2026
- **Link**: [论文](https://www.jnwpu.org/articles/jnwpu/abs/2026/01/jnwpu2026441p1/jnwpu2026441p1.html)
- **说明**: **高原峡谷**这一中国特有强风切变地形 + **TD3** 算法，是国内团队在极端地形抗风方向的实证工作，地理场景与本项目高度相关。

---

## Ⅳ. 综述与博士论文 / Surveys & Theses

> 先用综述建立全局地图，再进入具体方法，效率最高。

### ⭐ Drone Deep Reinforcement Learning: A Review（无人机深度强化学习：综述）
- **Source**: *Electronics* (MDPI, Review), 2021
- **Link**: [论文](https://www.mdpi.com/2079-9292/10/9/999)
- **说明**: 无人机 DRL 的**入门首选综述**，系统性梳理任务类型、算法选择与仿真平台，适合作为第一周阅读材料。

### A Review of Reinforcement Learning for Fixed-Wing Aircraft Control Tasks（固定翼飞机控制任务的强化学习研究综述）
- **Source**: *IEEE Access* (Review), 2024
- **Link**: [论文](https://ieeexplore.ieee.org/document/10609369)
- **说明**: 面向**固定翼**的 RL 控制综述，与旋翼方向互补；若后续扩展到固定翼平台，这是最快的切入综述。

### Survey on Path Planning Based on Deep Reinforcement Learning（基于深度强化学习的路径规划研究综述）
- **Source**: *PMLR* (Proceedings of ICMLIC 2025), 2025
- **Link**: [论文](https://proceedings.mlr.press/v278/xu25a.html)
- **说明**: 2025 年最新的 DRL 路径规划综述，覆盖状态表示、奖励设计、泛化与安全性等关键议题。

### Reinforcement Learning Based Control of a Fixed-Wing UAV Under Wind Disturbances（基于强化学习的固定翼无人机风扰下控制）
- **Source**: *ONERA*（法国国立航空航天研究院）/ *Université Paris-Saclay* · PhD Thesis, 2025
- **Link**: [论文](https://theses.hal.science/tel-05467318)
- **说明**: **博士论文**级别系统工作，配套 **JSBSim 高保真气动环境**。论文细节丰富（含完整实验设计），是学习「如何做风扰 RL 控制完整研究」的最佳长文。

### Additional Readings / 补充文献
- **Data-Efficient Deep RL for Attitude Control**（深度强化学习降低小型无人机姿态调整所需传感器数量）— *IEEE TNNLS* 2024 · [记录](https://openalex.org/works/W3212087381)
  - 说明: 关注**传感器降本**——用学习弥补传感器缺失，与「未知风下无风速计仍要抗风」的诉求同源。
- **Gust rejection on a morphing wing**（变形翼阵风抑制）— *Communications Engineering* 2024 · [记录](https://openalex.org/works/W4393039867)
  - 说明: 从**气动结构**侧解决阵风抑制（变体机翼），可作为「控制侧抗风」之外的跨学科对照思路。
- **Empirical Study of TD-MPC for Fixed-Wing UAVs Under Varying Wind Conditions**（基于时间差分模型预测控制的固定翼无人机在不同风况下的实证研究）— *SN Computer Science* 2026 · [论文](https://link.springer.com/article/10.1007/s42979-026-04751-w)
  - 说明: 系统对比 MF-RL / MB-RL / PID：**标称工况 TD-MPC 最优，风扰下标准 RL 框架表现次优且不稳定**。这条结论直接支撑本项目「基线对比必须包含风扰工况，且需引入基于模型的改进」的实验设计原则。
- **Wind-Aware RL: State-Space Wind Estimation + LSTM/GRU**（状态空间级风估计）— arXiv 预印本 2026 · [论文](https://arxiv.org/abs/2607.01528)
  - 说明: 风速 RMSE `0.40 m/s`、风向误差 `3.2°`，跟踪误差较风盲 PD 基线降低 `48%`。对应本项目「状态空间级」气象特征融合方案。
- **Hierarchical LSTM Supervisor + RL for UAV Trajectory**（时序监督 + RL 分层）— *IEEE Access* 2025 · [论文](https://doi.org/10.1109/ACCESS.2025.3645364)
  - 说明: LSTM 监督器输出风场/能量先验，RL 负责航迹与机动决策。较直接配点法方向/高度误差降低 `67%`/`89%`，终端误差 < 0.5 m，计算时间减少 > 93%。对应本项目「监督器级」融合方案。
- **Learning High-Speed Flight in the Wild**（野外高速飞行）— *Science Robotics* 2021 · [论文](https://www.science.org/doi/abs/10.1126/scirobotics.abg5810) · [代码](https://github.com/uzh-rpg/agile_autonomy) · [数据集](https://zenodo.org/records/5517791)
  - 说明: 端到端特权学习策略，仅用机载感知即可在森林等复杂环境中以 5–10 m/s 高速飞行，**零样本跨环境迁移**；优于传统「感知-建图-规划」分步流水线。
- **Champion-level Drone Racing**（冠军级无人机竞速）— *Nature* 2023 · [论文](https://www.nature.com/articles/s41586-023-06419-4) · DOI: `10.1038/s41586-023-06419-4`
  - 说明: RL 策略在真实竞速赛道上**击败人类世界冠军**，证明端到端 RL 控制的性能上限。

---

> [← 返回总索引](../README.md) · [下一篇：开源项目 →](02-open-source-projects.md)