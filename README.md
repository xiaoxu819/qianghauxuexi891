# UAV Wind-Resistance & Path Planning with Reinforcement Learning
# 无人机抗风与航迹规划 · 强化学习资源库

> **一句话说明 / One-line Summary**
> 本仓库系统收录「无人机抗风 + 航迹规划 + 强化学习」方向的**权威论文、开源项目、仿真软件、数据集与算法库**，
> 内容源自《徐荣超--强化学习算法方向调研报告》与《其他权威期刊论文、数据集、仿真软件推荐.xlsx》两份原始资料，
> 并在其基础上做了去重、分级与可访问性校验。
>
> This repository curates **authoritative papers, open-source projects, simulators, datasets and RL algorithm libraries**
> for *UAV wind-resistance and path planning with reinforcement learning*.

---

## 阅读约定 / How to Read

| 约定 | 说明 |
|---|---|
| **标题格式** | 统一采用 `English Title（中文标题）`，**英文在前、中文在后**，便于与论文原文、GitHub 仓库名一一对应 |
| **链接格式** | 所有长链接一律写成短超链接，如 `[论文](...)` `[代码](...)` `[官网](...)`，保持界面整洁 |
| **分级标记** | ⭐ = 最权威 / 最顶尖 / 最推荐，**优先精读**；无标记 = 有价值的补充与扩展 |
| **语言** | 说明文字中英混排，关键术语附中文解释 |

---

## 仓库文件说明 / Repository Contents

> 本节逐条解释本仓库**每一个新建文件**的用途，方便你随时回溯「这里放了什么、为什么放」。

| 文件 / 路径 | 中文名称 | 内容详解 |
|---|---|---|
| [`README.md`](.) | **总索引（本文件）** | 全仓库导航入口。包含阅读约定、目录导航、精选 Top 榜单、缩略语对照表，以及这份文件说明表。建议从这里出发，再点进 `docs/` 各分册。 |
| [`docs/01-papers.md`](docs/01-papers.md) | **论文分册** | 收录 **35+ 篇**权威文献，按四类归档：① 权威期刊论文（IEEE TIM / TIE / TAES / T-IV / TMC / TASE、Science Robotics）② 顶会论文（IROS / ICRA / CoRL / NeurIPS / IJCAI）③ 最新期刊论文（2025–2026，Pattern Recognition / Drones / RAS / ESWA / Sensors）④ 方向综述与博士论文。每条含期刊等级、年份、核心方法与直达链接。 |
| [`docs/02-open-source-projects.md`](docs/02-open-source-projects.md) | **开源项目分册** | 收录 **19 个** GitHub 项目，按五大类归档：① 仿真环境基座 ② 抗风 / 抗扰控制 ③ 安全飞行与竞速 ④ 多机协同与多智能体 ⑤ 资源汇总清单。每条标注 ⭐Star 数与开源许可协议，并说明「这个仓库里大概是什么」。 |
| [`docs/03-simulation-tools.md`](docs/03-simulation-tools.md) | **仿真软件分册** | 收录 **10 款**仿真与工具链：Isaac Sim / Isaac Lab、Gazebo（gz-sim）、PyBullet、MuJoCo、AirSim、JSBSim、Flightmare、PX4 SITL、ArduPilot SITL、ROS 2。每条注明类型、许可协议与在强化学习流水线中的定位。 |
| [`docs/04-datasets-and-models.md`](docs/04-datasets-and-models.md) | **数据集与风场模型分册** | 收录 **12 个**气象 / 飞行数据集（ERA5、MERRA-2、HRRR、PLUSWIND、TAMU、CMA、CMU Matrice 100 风场数据集、Manipal、VID、固定翼遥测等）与 **2 套湍流模型**（Dryden / von Kármán，MIL-STD-1797A），并说明如何用于域随机化与风扰测试工况生成。 |
| [`docs/05-algorithms-and-baselines.md`](docs/05-algorithms-and-baselines.md) | **算法库与基线分册** | 收录 **8 个**强化学习与环境接口库（Stable-Baselines3、CleanRL、Gymnasium、PettingZoo、SKRL、Ray RLlib）与传统控制基线工具（do-mpc、PythonRobotics），并给出本项目「PPO 主算法 + SAC 对照 + PID/MPC 基线」的选型理由。 |
| [`assets/`](assets/) | **原始资料归档** | 存放两份调研原始文件，便于日后回溯与二次查阅：<br>• `其他权威期刊论文、数据集、仿真软件推荐.xlsx` —— 11 个工作表的分类链接清单；<br>• `徐荣超--强化学习算法方向调研报告.pptx` —— 24 页完整调研报告（含技术基础、论文精读、开源生态、技术路线）。 |

---

## 目录导航 / Navigation

| # | 分册 | 内容概要 | 直达 |
|---|---|---|---|
| 01 | **Papers / 论文** | 权威期刊 · 顶会 · 最新期刊 · 综述 | [docs/01-papers.md](docs/01-papers.md) |
| 02 | **Open-Source Projects / 开源项目** | 仿真环境 · 抗风控制 · 安全飞行 · 多机协同 | [docs/02-open-source-projects.md](docs/02-open-source-projects.md) |
| 03 | **Simulation Tools / 仿真软件** | Isaac Sim · Gazebo · PyBullet · MuJoCo · JSBSim | [docs/03-simulation-tools.md](docs/03-simulation-tools.md) |
| 04 | **Datasets & Wind Models / 数据集与风场模型** | ERA5 · MERRA-2 · HRRR · 真实飞行数据集 · 湍流模型 | [docs/04-datasets-and-models.md](docs/04-datasets-and-models.md) |
| 05 | **Algorithms & Baselines / 算法库与基线** | SB3 · CleanRL · Gymnasium · MAPPO · PID/MPC | [docs/05-algorithms-and-baselines.md](docs/05-algorithms-and-baselines.md) |

---

## ⭐ 精选 Top Picks / 最值得先看的 8 条

> 如果只看少量资料，建议按下面顺序：**先看综述定方向 → 再看顶尖论文定方法 → 最后跑开源环境动手。**

| 序 | 条目 | 类型 | 为什么最值得看 |
|---|---|---|---|
| 1 | **Neural-Fly Enables Rapid Learning for Agile Flight in Strong Winds**（强风下敏捷飞行快速学习） | Science Robotics 2022 | 抗风飞行领域**最顶级的期刊成果之一**，Caltech 风洞实测至 12.1 m/s，提出域适应 + 元学习范式。 [论文](https://www.science.org/doi/10.1126/scirobotics.abm6597) · [代码](https://github.com/aerorobotics/neural-fly) |
| 2 | **Learning High-Speed Flight in the Wild**（野外高速飞行） | Science Robotics 2021 | 端到端特权学习，仅靠机载感知即可 5–10 m/s 穿越森林，**零样本跨环境迁移**。 [论文](https://www.science.org/doi/abs/10.1126/scirobotics.abg5810) · [代码](https://github.com/uzh-rpg/agile_autonomy) |
| 3 | **Champion-level Drone Racing**（冠军级无人机竞速） | Nature 2023 | RL 策略在真实赛道**击败人类世界冠军**，证明端到端 RL 控制的性能上限。 [论文](https://www.nature.com/articles/s41586-023-06419-4) |
| 4 | **NavRL: Learning Safe Flight in Dynamic Environments**（动态环境下的安全飞行） | IEEE RA-L 2025 | **PPO + 速度障碍安全护盾**，Isaac Sim 千架四旋翼并行训练，零样本 sim-to-real 并开源 ROS 部署代码。 [论文](https://ieeexplore.ieee.org/document/10904341) · [代码](https://github.com/Zhefan-Xu/NavRL) |
| 5 | **gym-pybullet-drones**（PyBullet 四旋翼 RL 环境） | ⭐2144 · MIT | 本方向**事实标准**的入门仿真环境，单机/多机、悬停/轨迹跟踪/下洗气流，无缝对接 Stable-Baselines3。 [代码](https://github.com/learnsyslab/gym-pybullet-drones) |
| 6 | **Drone Deep Reinforcement Learning: A Review**（无人机深度强化学习综述） | Electronics 2021 | 最快建立**领域全局地图**的综述，适合作为第一篇入门读物。 [论文](https://www.mdpi.com/2079-9292/10/9/999) |
| 7 | **ERA5 (ECMWF) Reanalysis**（ERA5 全球再分析气象数据） | 最权威气象数据集 | 0.25° / 小时级全球风场，**气象特征融合方向的标准数据源**，可直接构造风扰工况。 [数据集](https://cds.climate.copernicus.eu/datasets/reanalysis-era5-single-levels) |
| 8 | **Stable-Baselines3 (SB3)** | ⭐13.7k · MIT | PPO / SAC / TD3 的**首选 PyTorch 参考实现**，本方向主算法 PPO 的最佳落地点。 [代码](https://github.com/DLR-RM/stable-baselines3) |

---

## 缩略语对照 / Abbreviations

| 缩写 | 全称（English） | 中文 |
|---|---|---|
| RL / DRL | (Deep) Reinforcement Learning | （深度）强化学习 |
| PPO | Proximal Policy Optimization | 近端策略优化 |
| SAC | Soft Actor-Critic | 软演员-评论家 |
| TD3 | Twin Delayed Deep Deterministic Policy Gradient | 双延迟深度确定性策略梯度 |
| MARL | Multi-Agent Reinforcement Learning | 多智能体强化学习 |
| MAPPO | Multi-Agent PPO | 多智能体近端策略优化 |
| CTDE | Centralized Training with Decentralized Execution | 集中训练-分散执行 |
| PID | Proportional-Integral-Derivative | 比例-积分-微分 |
| MPC | Model Predictive Control | 模型预测控制 |
| CBF | Control Barrier Function | 控制屏障函数 |
| VO | Velocity Obstacle | 速度障碍法 |
| INDI | Incremental Nonlinear Dynamic Inversion | 增量非线性动态逆 |
| GAE | Generalized Advantage Estimation | 广义优势估计 |
| MDP | Markov Decision Process | 马尔可夫决策过程 |
| RMSE | Root Mean Square Error | 均方根误差 |
| SITL | Software-In-The-Loop | 软件在环仿真 |
| FDM | Flight Dynamics Model | 飞行动力学模型 |

---

## 资料溯源 / Provenance

- **原始调研报告**：[`assets/徐荣超--强化学习算法方向调研报告.pptx`](assets/)（24 页，含技术基础 ①–⑤、论文精读 ①–⑤、开源生态、技术路线四步走）
- **原始链接清单**：[`assets/其他权威期刊论文、数据集、仿真软件推荐.xlsx`](assets/)（11 个工作表分类整理）
- **收录原则**：只保留**最权威、最顶尖、最有效**的链接；每条附中英文说明，长链接统一超链接化。

> ⚠️ 本仓库仅收录**外部链接与简介**，不转载论文全文与第三方源码，版权归原作者所有。请通过各条目的官方链接访问与引用。