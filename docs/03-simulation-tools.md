# Simulation Tools / 仿真软件分册

> [← 返回总索引](../README.md)
>
> 本分册收录本方向**工程落地所需的 10 款仿真软件与工具链**，
> 标题统一 `Tool Name（中文名称）` 格式，每条注明**类型 / 许可协议 / 在强化学习流水线中的定位**。

---

## 选型速查表 / Quick Selection Table

| 工具 | 类型 | 许可 | 最适合的场景 |
|---|---|---|---|
| [NVIDIA Isaac Sim / Isaac Lab](#⭐-nvidia-isaac-sim--isaac-labgpu-并行强化学习训练平台) | GPU 并行 RL 训练 | BSD-3 | 上千架并行训练、零样本 sim-to-real |
| [PyBullet](#⭐-pybulletpython-物理引擎) | 物理引擎 | zlib | **入门首选**，轻量、启动快 |
| [Gazebo (gz-sim)](#gazebo-gz-sim机器人仿真平台) | 机器人仿真 | Apache-2.0 | PX4/ArduPilot 软件在环、硬件在环 |
| [MuJoCo](#mujoco高保真物理引擎) | 物理引擎 | Apache-2.0 | 高保真接触动力学、控制算法验证 |
| [Flightmare](#flightmare四旋翼高性能仿真器) | 四旋翼专用仿真 | MIT | 高吞吐采样、视觉观测 |
| [AirSim](#airsim高保真视觉传感器仿真) | 高保真仿真 | MIT | 逼真视觉/传感器、域随机化 |
| [JSBSim](#jsbsim飞行动力学模型) | 气动仿真 | LGPL | 固定翼高保真气动 |
| [PX4 SITL](#px4-sitl--gazebo飞控软件在环) | 飞控 SITL | BSD-3 | 工业级飞控 + RL 联调 |
| [ArduPilot SITL](#ardupilot-sitl飞控软件在环) | 飞控 SITL | GPL-3.0 | 另一套工业级飞控在环 |
| [ROS 2](#ros-2机器人中间件) | 机器人中间件 | Apache-2.0 | 真机部署、软硬件集成 |

> **一句话选型建议**：**入门用 PyBullet（gym-pybullet-drones），规模化训练用 Isaac Sim，要真机部署接 PX4 + ROS 2，需要真实气动上 JSBSim。**

---

## ⭐ NVIDIA Isaac Sim / Isaac Lab（GPU 并行强化学习训练平台）
- **Type**: GPU 并行 RL 训练平台 / High-fidelity simulation
- **License**: BSD-3
- **Link**: [Isaac Lab 代码](https://github.com/isaac-sim/IsaacLab) · [官网](https://developer.nvidia.com/isaac/lab)
- **说明**: NVIDIA 的 **GPU 并行机器人仿真与 RL 训练框架**，可在单机上并行运行**上千个环境实例**。NavRL（IEEE RA-L 2025）正是在其中并行训练**上千架四旋翼**，从而获得可零样本迁移到真机的策略。
- **在本项目中的定位**: **规模化训练阶段**的主力平台。当 PPO 需要上千万步采样时，Isaac Lab 的吞吐量比 CPU 仿真相差一到两个数量级。

## ⭐ PyBullet（Python 物理引擎）
- **Type**: 物理仿真 / Physics simulation
- **License**: zlib
- **Link**: [官网](https://pybullet.org/) · [代码](https://github.com/bulletphysics/bullet3)
- **说明**: 轻量级 **Python 物理引擎**，安装简单、启动快，是 `gym-pybullet-drones`、`safe-control-gym`、GustPilot 等环境的**底层引擎**。
- **在本项目中的定位**: **入门与快速迭代首选**。环境封装、PPO 复现、奖励塑形调参等高频迭代实验都建议先在 PyBullet 上完成。

## Gazebo (gz-sim)（机器人仿真平台）
- **Type**: 机器人仿真 / Robot simulation
- **License**: Apache-2.0
- **Link**: [代码](https://github.com/gazebosim/gz-sim)
- **说明**: 机器人领域主流仿真平台，**RotorS、PX4 硬件在环（HITL）** 的标准载体，支持复杂世界建模与多传感器。
- **在本项目中的定位**: 与 **PX4 / ArduPilot 软件在环**配套使用，是「从 RL 策略走向真实飞控」的桥梁。

## MuJoCo（高保真物理引擎）
- **Type**: 物理仿真 / Physics simulation
- **License**: Apache-2.0
- **Link**: [官网](https://mujoco.org/) · [代码](https://github.com/google-deepmind/mujoco)
- **说明**: DeepMind 维护的**高保真物理引擎**，以**接触动力学精度与仿真速度**著称，是机器人强化学习的常用后端。
- **在本项目中的定位**: 当需要高精度接触/碰撞建模（如近距离穿越、着陆）时的备选引擎。

## Flightmare（四旋翼高性能仿真器）
- **Type**: 四旋翼专用仿真 / Quadrotor simulator
- **License**: MIT
- **Link**: [代码](https://github.com/uzh-rpg/flightmare) · [论文 (CoRL 2020)](https://proceedings.mlr.press/v155/song21a.html)
- **说明**: ETH Zurich 出品，**渲染（230 Hz）与物理（20 万 Hz）解耦**，可支撑千万级并行采样。
- **在本项目中的定位**: 需要**大规模采样**或**视觉观测**时的性能型选择；`agile_autonomy` 项目即基于它。

## AirSim（高保真视觉/传感器仿真）
- **Type**: 高保真仿真 / High-fidelity simulation
- **License**: MIT
- **Link**: [官网](https://microsoft.github.io/AirSim/) · [代码](https://github.com/microsoft/AirSim)
- **说明**: 微软基于 **Unreal Engine** 的仿真平台，提供**逼真视觉 + 物理 + 多传感器**，并支持**风扰**与传感器噪声注入。
- **在本项目中的定位**: **域随机化**与**感知类**实验平台；若后续引入视觉观测，这是首选。

## JSBSim（飞行动力学模型）
- **Type**: 气动仿真 / Aerodynamics simulation
- **License**: LGPL
- **Link**: [代码](https://github.com/JSBSim-Team/jsbsim)
- **说明**: 开源**飞行动力学模型（FDM, Flight Dynamics Model）**，提供固定翼**高保真气动**计算，含 C++ / Python 接口。
- **在本项目中的定位**: **固定翼扩展**方向的气动底座，`gym-jsbsim` 即封装于此。

## PX4 SITL / Gazebo（飞控软件在环）
- **Type**: 飞控仿真 / Flight controller simulation
- **License**: BSD-3
- **Link**: [官网](https://px4.io/)
- **说明**: PX4 开源飞控的**软件在环（SITL）** 仿真，与 Gazebo 物理引擎配合，可接入强化学习策略，属**工业级**方案。
- **在本项目中的定位**: **真机部署前的最后一关**。策略在 PyBullet/Isaac 训好后，需经 PX4 SITL 验证再上真机。

## ArduPilot SITL（飞控软件在环）
- **Type**: 飞控仿真 / Flight controller simulation
- **License**: GPL-3.0
- **Link**: [文档](https://ardupilot.org/dev/docs/sitl-simulator-software-in-the-loop.html)
- **说明**: ArduPilot 开源飞控的 SITL 仿真，与 PX4 并列的另一套工业级飞控在环方案。
- **在本项目中的定位**: 若硬件平台采用 ArduPilot 生态，则以此为主。

## ROS 2（机器人中间件）
- **Type**: 机器人中间件 / Robot middleware
- **License**: Apache-2.0
- **Link**: [文档](https://docs.ros.org/)
- **说明**: **机器人操作系统 2**，是无人机软硬件集成的事实标准，负责话题通信、节点编排与实时控制。
- **在本项目中的定位**: **真机部署的通信骨架**。NavRL、agile_autonomy 的真机代码均以 ROS 组织，策略推理节点通过 ROS 话题接收状态、发布控制指令。

---

## 推荐组合 / Recommended Stacks

| 阶段 | 推荐组合 | 理由 |
|---|---|---|
| **① 入门复现** | PyBullet + gym-pybullet-drones + Stable-Baselines3 | 环境秒级启动，PPO 当天可跑通 |
| **② 规模化训练** | Isaac Sim / Isaac Lab + PPO | 千级并行环境，采样吞吐最高 |
| **③ 固定翼 / 真实气动** | JSBSim + gym-jsbsim | 高保真 FDM，学术背书 |
| **④ 真机部署** | PX4 SITL + ROS 2 + Gazebo | 工业级链路，降低上机风险 |

---

> [← 返回总索引](../README.md) · [上一篇：开源项目](02-open-source-projects.md) · [下一篇：数据集与风场模型 →](04-datasets-and-models.md)