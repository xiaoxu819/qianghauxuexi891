# Open-Source Projects / 开源项目分册

> [← 返回总索引](../README.md)
>
> 本分册收录「无人机抗风 + 航迹规划 + 强化学习」方向**最顶尖的 19 个 GitHub 项目**，
> 每条标注 ⭐Star 数 与 许可协议，并说明「**这个仓库里大概是什么**」，便于你快速判断是否值得深入。
> 标题统一 `Repository Name（中文名称）` 格式。

---

## 目录

- [Ⅰ. 仿真环境基座 / Simulation Environment Foundations](#Ⅰ-仿真环境基座--simulation-environment-foundations)
- [Ⅱ. 抗风与抗扰控制 / Wind & Disturbance Rejection Control](#Ⅱ-抗风与抗扰控制--wind--disturbance-rejection-control)
- [Ⅲ. 安全飞行与高速敏捷 / Safe & Agile Flight](#Ⅲ-安全飞行与高速敏捷--safe--agile-flight)
- [Ⅳ. 多机协同与多智能体 / Multi-UAV & Multi-Agent RL](#Ⅳ-多机协同与多智能体--multi-uav--multi-agent-rl)
- [Ⅴ. 资源汇总清单 / Curated Awesome Lists](#Ⅴ-资源汇总清单--curated-awesome-lists)

---

## Ⅰ. 仿真环境基座 / Simulation Environment Foundations

> 这几个仓库是本方向**动手的第一站**：装好环境、跑通 PPO 悬停/跟踪，再谈改算法。

### ⭐ gym-pybullet-drones（PyBullet 四旋翼强化学习环境 · 官方维护版）
- **Stars / License**: ⭐2144 · MIT
- **Link**: [代码](https://github.com/learnsyslab/gym-pybullet-drones) · [原组织仓库](https://github.com/utiasDSL/gym-pybullet-drones) · [论文 (IROS 2021)](https://ieeexplore.ieee.org/document/9635857)
- **这个仓库里是什么**: 本方向**事实标准的入门仿真环境**。基于 PyBullet + Gymnasium，支持**单机 / 多机**四旋翼，内置**悬停、轨迹跟踪、下洗气流（downwash）**等任务，附带 **PPO 训练示例**，并可对接 Betaflight / Crazyflie 的 SITL。原仓库在 UTIAS-DSL 组织下，现重定向至 `learnsyslab` 组织。
- **为什么推荐**: 环境接口规范、任务定义清晰、与 Stable-Baselines3 无缝衔接，是「环境封装 + PPO 复现」阶段最高性价比的起点。

### gym-pybullet-drones（PyBullet 四旋翼环境 · 极简重构版）
- **Stars / License**: ⭐2144（共享）· MIT
- **Link**: [代码](https://github.com/learnsyslab/gym-pybullet-drones)
- **这个仓库里是什么**: 官方仓库的**极简重构版**，兼容 Gymnasium + Stable-Baselines3 2.0 + SITL，**更新更活跃**。
- **为什么推荐**: 若官方版依赖较旧，优先用这个版本，可减少环境配置摩擦。

### ⭐ PyFlyt（无人机飞行仿真 · Gymnasium/PettingZoo 接口）
- **Stars / License**: ⭐261 · MIT
- **Link**: [代码](https://github.com/jjshoots/PyFlyt)
- **这个仓库里是什么**: 无人机飞行仿真库，提供 **Gymnasium 与 PettingZoo 双接口**（单智能体 + 多智能体），覆盖**四旋翼 / 固定翼 / 火箭**三类平台，内置多种任务环境，配套 arXiv 论文。
- **为什么推荐**: 若后续要从旋翼扩展到**固定翼**，或需要 PettingZoo 风格的多机任务，这是最省力的环境。

### Gym-JSBSim（固定翼无人机 + JSBSim 高保真气动环境）
- **Stars / License**: ⭐260 · MIT
- **Link**: [代码](https://github.com/Gor-Ren/gym-jsbsim) · [相关博士论文](https://theses.hal.science/tel-05467318)
- **这个仓库里是什么**: 把**固定翼无人机**与 **JSBSim 高保真飞行动力学模型（FDM）**接入强化学习循环，环境随一篇博士论文发布。
- **为什么推荐**: 需要**真实气动特性**（而非简化质点模型）时，这是最有学术背书的选择。

### ⭐ Flightmare（四旋翼高性能仿真器）
- **Stars / License**: ⭐（ETH Zurich RPG 出品）
- **Link**: [代码](https://github.com/uzh-rpg/flightmare) · [论文 (CoRL 2020)](https://proceedings.mlr.press/v155/song21a.html)
- **这个仓库里是什么**: ETH Zurich 的四旋翼仿真器，**Unity 渲染 + 物理解耦架构**，渲染 230 Hz、物理可达 20 万 Hz，支持千万级并行采样。
- **为什么推荐**: 当你需要**高吞吐训练**或**视觉观测**（相机输入）时，性能优于 PyBullet 系列。

### AirSim（高保真无人机/车辆仿真 · Microsoft）
- **Stars / License**: ⭐（Microsoft 官方）· MIT
- **Link**: [代码](https://github.com/microsoft/AirSim) · [官网](https://microsoft.github.io/AirSim/)
- **这个仓库里是什么**: 基于 **Unreal Engine** 的高保真**视觉 + 物理 + 传感器**仿真平台，支持**风扰、传感器噪声**，面向研究级 Sim-to-Real。
- **为什么推荐**: 需要**逼真视觉/传感器**（相机、激光雷达、IMU 噪声）时首选；也是「域随机化」的丰富噪声源。

---

## Ⅱ. 抗风与抗扰控制 / Wind & Disturbance Rejection Control

> 本分册**最贴合你课题**的一类：如何在强风、未知风、阵风下保持稳定与跟踪精度。

### ⭐ aerorobotics/neural-fly（强风下快速自适应飞行控制）
- **Stars / License**: ⭐221
- **Link**: [代码](https://github.com/aerorobotics/neural-fly) · [论文 (Science Robotics 2022)](https://www.science.org/doi/full/10.1126/scirobotics.abm6597)
- **这个仓库里是什么**: **Science Robotics 论文的官方配套代码**。核心是「域适应 + 元学习」：学习一组气动基函数，在线线性组合即可快速适应新风况。Caltech 风洞实测风速至 **12.1 m/s**，并**开源了训练数据**。
- **为什么推荐**: 抗风方向**权威性最高**的开源实现，且提供真实风洞数据，是验证「气象特征融合」效果的黄金参照。

### ⭐ muellerlab/xadapt_ctrl（学习型底层控制器 · 极端自适应与扰动抑制）
- **Stars / License**: ⭐90
- **Link**: [代码](https://github.com/muellerlab/xadapt_ctrl) · [论文 (IEEE T-RO 2025)](https://arxiv.org/abs/2409.12949) · [PDF](https://arxiv.org/pdf/2409.12949.pdf)
- **这个仓库里是什么**: 一种**基于学习的四旋翼控制器**，主打**极端环境适应能力与扰动抑制**（论文发表于 IEEE T-RO 2025）。
- **为什么推荐**: 若你想在**底层控制**（而非高层决策）做学习型抗扰改进，这是最新且代码完整的参考实现。

### hersh500/occam（含气动学与风扰的多旋翼仿真）
- **Stars / License**: ⭐310 · MIT
- **Link**: [代码](https://github.com/hersh500/occam) · [项目主页](https://hersh500.github.io/occam/)
- **这个仓库里是什么**: 一个**含气动学模型与风扰**的多旋翼仿真环境，专门面向强化学习的 **sim-to-real**。
- **为什么推荐**: 相比纯刚体模型，它把**气动效应**显式建模，是「域随机化 + 气动不确定性」实验的合适平台。

### DTUWindEnergy/WindGym（风电场强化学习控制环境）
- **Stars / License**: ⭐（DTU 风能系出品）
- **Link**: [代码](https://github.com/DTUWindEnergy/WindGym)
- **这个仓库里是什么**: **风电场**层面的强化学习控制环境，Gymnasium 兼容，内置 **Mann 湍流模型**。
- **为什么推荐**: 任务对象是风电场而非无人机，但其**湍流建模与风场生成方式**可直接借鉴到无人机风扰工况构造。

### ruppikha/uav-wind-estimation-control（无人机风估计与控制 · Manipal 数据集配套）
- **Stars / License**: ⭐
- **Link**: [代码](https://github.com/ruppikha/uav-wind-estimation-control)
- **这个仓库里是什么**: 配套 **Manipal 无人机飞行数据集**（变风况/地形飞行，17 路同步特征，面向风估计，IEEE Access 2025）的代码实现。
- **为什么推荐**: 想做**显式风估计**（由可观测状态反演风速风向）时，这里有现成的数据 + 代码闭环。

---

## Ⅲ. 安全飞行与高速敏捷 / Safe & Agile Flight

### ⭐ Zhefan-Xu/NavRL（动态环境下安全飞行 · PPO + 安全护盾）
- **Stars / License**: ⭐1623 · MIT
- **Link**: [代码](https://github.com/Zhefan-Xu/NavRL) · [论文 (IEEE RA-L 2025)](https://ieeexplore.ieee.org/document/10904341) · [arXiv](https://arxiv.org/abs/2409.15634)
- **这个仓库里是什么**: **PPO 策略 + 基于速度障碍（VO）的安全护盾**，用线性规划约束策略输出；在 **NVIDIA Isaac Sim** 中构建**数千架四旋翼并行训练管线**，实现零样本 sim-to-real。仓库开源了 **ROS1/ROS2 部署代码与预训练模型**。
- **为什么推荐**: 本方向**工程完成度最高**的开源项目之一，从训练到真机部署全链路打通，是「PPO + 安全约束 + sim-to-real」的最佳范本。

### ⭐ uzh-rpg/agile_autonomy（野外高速飞行策略学习）
- **Stars / License**: ⭐811 · GPL-3.0
- **Link**: [代码](https://github.com/uzh-rpg/agile_autonomy) · [论文 (Science Robotics 2021)](https://www.science.org/doi/abs/10.1126/scirobotics.abg5810) · [数据集](https://zenodo.org/records/5517791)
- **这个仓库里是什么**: **Science Robotics 论文配套**。端到端**特权学习（privileged learning）** 策略，仅用机载感知即可在森林等复杂环境以 **5–10 m/s** 高速飞行，零样本跨环境迁移。仓库内含 **Flightmare 仿真配置与公开数据集**。
- **为什么推荐**: 「仿真中学、真机中飞」的教学级完整案例，训练管线与数据都开源，可直接复用其**特权学习 + 蒸馏**范式。

### KevinHuang8/DATT（深度自适应轨迹跟踪 · CoRL 2023 Oral）
- **Stars / License**: ⭐98
- **Link**: [代码](https://github.com/KevinHuang8/DATT) · [论文](https://openreview.net/forum?id=XEw-cnNsr6) · [项目主页](https://sites.google.com/view/deep-adaptive-traj-tracking)
- **这个仓库里是什么**: CoRL 2023 Oral 工作。学习式「**前馈 + 反馈 + 自适应**」控制结构，仿真中用 RL 训练，真机部署时叠加 **L1 扰动估计器**在闭环内微调，**无需重新训练策略**。
- **为什么推荐**: 实测跟踪 RMSE `0.05 m`（优于 MPC `0.11 m`），推理时延 < 3.2 ms。是「在非平稳风场中打败 MPC」的强证据。

---

## Ⅳ. 多机协同与多智能体 / Multi-UAV & Multi-Agent RL

### ⭐ marlbenchmark/on-policy（MAPPO 官方实现）
- **Stars / License**: ⭐2107 · MIT
- **Link**: [代码](https://github.com/marlbenchmark/on-policy) · [论文 (NeurIPS 2022)](https://openreview.net/forum?id=YVXaxB6L2Pl)
- **这个仓库里是什么**: **MAPPO（Multi-Agent PPO）的官方实现**，支持 **SMAC、MPE** 等多智能体基准环境，是 CTDE（集中训练-分散执行）范式的事实标准代码库。
- **为什么推荐**: 本项目「单机 PPO → 多机 MAPPO」扩展路径的**直接落地代码**，接口成熟、社区活跃。

### thu-uav/VolleyBots（多无人机排球对抗测试平台）
- **Stars / License**: ⭐（清华 UAV 组出品）
- **Link**: [代码](https://github.com/thu-uav/VolleyBots) · [论文 (NeurIPS 2025)](https://openreview.net/forum?id=FRbNGgWqCX)
- **这个仓库里是什么**: NeurIPS 2025 的**多无人机动态协作测试平台**（排球对抗），考察高风险动态环境下的多机协同。
- **为什么推荐**: 2025 年最新的多机基准，适合验证多机协同策略在**高动态对抗**下的鲁棒性。

### henbudidiao/UAV-path-planning（基于 MASAC 的多无人机协同路径规划）
- **Stars / License**: ⭐
- **Link**: [代码](https://github.com/henbudidiao/UAV-path-planning)
- **这个仓库里是什么**: 基于 **MASAC（Multi-Agent Soft Actor-Critic）** 的多无人机协同路径规划实现。
- **为什么推荐**: 若选择 **SAC 路线**做多机扩展（而非 MAPPO），这是可直接对照的中文社区实现。

---

## Ⅴ. 资源汇总清单 / Curated Awesome Lists

### ⭐ shield09/awesome-RL-for-UAVs（无人机强化学习论文+代码收录列表）
- **Stars / License**: ⭐
- **Link**: [列表](https://github.com/shield09/awesome-RL-for-UAVs)
- **这个仓库里是什么**: 无人机强化学习的**论文 + 代码精选列表**，按固定翼、旋翼、空战等分类整理。
- **为什么推荐**: 作为**广度检索**的入口，可快速发现本清单之外的补充文献。

### ZJU-FAST-Lab/VID-Dataset（视觉-惯性-动力学数据集）
- **Stars / License**: ⭐
- **Link**: [数据集](https://github.com/ZJU-FAST-Lab/VID-Dataset)
- **这个仓库里是什么**: 包含**外力/扰动真值**的视觉-惯性-动力学数据集，可用于**扰动辨识与残差学习**。
- **为什么推荐**: 若走「残差驱动的隐式风感知」路线（如 WA-TD3），这是少见的带**扰动真值标签**的公开数据。

---

> [← 返回总索引](../README.md) · [上一篇：论文](01-papers.md) · [下一篇：仿真软件 →](03-simulation-tools.md)