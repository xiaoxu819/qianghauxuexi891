# Algorithms & Baselines / 算法库与基线分册

> [← 返回总索引](../README.md)
>
> 本分册收录**强化学习算法库（6 个）与环境接口标准（含在库内）** 以及**传统控制基线工具（2 个）**，
> 并给出本项目「**PPO 主算法 + SAC 对照 + PID/MPC 基线**」的选型理由与落地建议。
> 标题统一 `Library Name（中文名称）` 格式。

---

## 目录

- [Ⅰ. 强化学习算法库 / RL Algorithm Libraries](#Ⅰ-强化学习算法库--rl-algorithm-libraries)
- [Ⅱ. 环境接口标准 / Environment Interface Standards](#Ⅱ-环境接口标准--environment-interface-standards)
- [Ⅲ. 传统控制基线工具 / Classical Control Baseline Tools](#Ⅲ-传统控制基线工具--classical-control-baseline-tools)
- [Ⅳ. 主算法与基线选型 / Algorithm & Baseline Selection](#Ⅳ-主算法与基线选型--algorithm--baseline-selection)

---

## Ⅰ. 强化学习算法库 / RL Algorithm Libraries

### ⭐ Stable-Baselines3 (SB3)（稳定基线3）
- **Stars / License**: ⭐13.7k · MIT
- **Link**: [代码](https://github.com/DLR-RM/stable-baselines3) · [官方文档](https://stable-baselines3.readthedocs.io/en/master/)
- **这个仓库里是什么**: **PyTorch 实现的 PPO / SAC / TD3 / DQN** 等主流算法，**Gymnasium 兼容**，API 统一、文档完善、社区活跃。
- **为什么推荐**: 本项目**主算法 PPO 的首选实现**。上手快、超参默认值合理，可把精力集中在环境设计与奖励塑形上。

### ⭐ CleanRL（单文件高质量强化学习实现）
- **Stars / License**: ⭐10.3k · MIT
- **Link**: [代码](https://github.com/vwxyzjn/cleanrl)
- **这个仓库里是什么**: 把 PPO / SAC / DQN 等算法写成**单个独立文件**，**去抽象、全透明**，所有细节（GAE、裁剪、优势归一化）都在一个文件里能读完。
- **为什么推荐**: **调试与改算法的利器**。当你要改 PPO 的裁剪目标、GAE 或奖励结构时，改 CleanRL 比改 SB3 直观得多；也便于复现论文细节。

### SKRL（多后端强化学习库）
- **Stars / License**: ⭐1.1k · MIT
- **Link**: [代码](https://github.com/Toni-SM/skrl)
- **这个仓库里是什么**: 支持 **PyTorch / JAX 双后端**的 RL 库，兼容多种环境接口（含 Isaac Lab），模块化程度高。
- **为什么推荐**: 若走 **Isaac Lab 大规模并行训练**路线，SKRL 是官方推荐的算法库之一。

### Ray RLlib（分布式强化学习框架）
- **License**: Apache-2.0
- **Link**: [代码](https://github.com/ray-project/ray)
- **这个仓库里是什么**: 基于 **Ray** 的**分布式 RL 训练框架**，支持大规模并行采样与多智能体场景。
- **为什么推荐**: 当训练规模超出单机（多机多卡、海量环境实例）时的**扩展方案**。

---

## Ⅱ. 环境接口标准 / Environment Interface Standards

> 环境封装是整个项目的**第一步**，这两个库定义了「合规」的标准。

### ⭐ Gymnasium（强化学习环境标准 API）
- **Stars / License**: ⭐12.4k · MIT
- **Link**: [代码](https://github.com/Farama-Foundation/Gymnasium) · [官方文档](https://gymnasium.farama.org/api/env/)
- **这个仓库里是什么**: **Farama 基金会维护的 RL 环境标准 API**（OpenAI Gym 的官方后继者）。
- **关键接口规范**（调研报告「关键技术基础①」）:
  - `reset(*, seed, options) → (观测, 附加信息)`；`step(动作) → (观测, 奖励, terminated, truncated, 附加信息)`
  - `action_space` / `observation_space` 必须是 `Space` 对象，`Box` 支持**逐维上下界**
  - 用 `gym.register()` 注册、`make()` 创建；**`EnvChecker` 自动校验接口合规性**
  - 自定义环境首行须调用 `super().reset(seed=seed)`
  - **`terminated` 与 `truncated` 必须分离**（Gymnasium 0.26 起）：前者是 MDP 定义的终止态，后者是超时/越界的截断
- **为什么推荐**: 本项目「按 Gymnasium 规范封装风扰无人机环境，通过 EnvChecker 校验」的**直接依据**。

### PettingZoo（多智能体强化学习标准 API）
- **Stars / License**: ⭐3.5k · MIT
- **Link**: [代码](https://github.com/Farama-Foundation/PettingZoo)
- **这个仓库里是什么**: 与 Gymnasium 同门的**多智能体 RL 标准 API**，定义多智能体环境的统一交互范式。
- **为什么推荐**: 本项目**多机协同阶段**的环境接口标准，`PyFlyt` 亦提供 PettingZoo 接口。

---

## Ⅲ. 传统控制基线工具 / Classical Control Baseline Tools

> **强化学习的增益只有在与传统控制基线同工况对比时才可信**（调研报告「关键技术基础④」）。

### ⭐ do-mpc（模型预测控制 Python 库）
- **License**: LGPL-3.0
- **Link**: [代码](https://github.com/do-mpc/do-mpc)
- **这个仓库里是什么**: **MPC（模型预测控制）的 Python 库**，支持线性/非线性 MPC、滚动时域优化与显式约束处理。
- **为什么推荐**: 搭建 **MPC 基线**的最省力选择。可给出预测时域与权重配置，满足「基线需调至最优，避免稻草人对比」的公平性要求。

### PythonRobotics（机器人路径规划与控制算法集合）
- **License**: MIT
- **Link**: [代码](https://github.com/AtsushiSakai/PythonRobotics)
- **这个仓库里是什么**: 机器人**路径规划 + 控制算法**的经典集合，含 **MPC / LQR / PID** 等实现，每个算法配可视化动画。
- **为什么推荐**: 快速获得**PID / LQR 基线**实现与调参直觉，也可用于对比传统规划器与本项目 RL 规划器的轨迹形态差异。

---

## Ⅳ. 主算法与基线选型 / Algorithm & Baseline Selection

> 依据调研报告「关键技术基础②③④」，本项目的算法矩阵如下。

### 为什么主算法选 PPO
- **on-policy（在策略）方法**：策略更新方向可控、训练过程稳定，**便于与安全护盾类约束模块叠加**；
- 相比 **TRPO**（信赖域策略优化）**只需一阶梯度**，实现简单、易与 PyTorch 生态集成；
- 在 **MAPPO（NeurIPS 2022）** 与 **VolleyBots（NeurIPS 2025）** 等工作中，PPO 在多智能体与无人机任务上与 off-policy 方法**持平或更优**。

**风扰场景下的实现要点**:
- **观测归一化**：风速、姿态、角速度量纲差异大，需**按维归一化**；
- **奖励塑形**：`位置误差 + 姿态稳定 + 动作平滑 + 能耗惩罚`，风扰下需**提高姿态项权重**；
- **域随机化**：训练中随机化风场参数，是**零样本 sim-to-real 的关键**。

**关键超参建议**（调研报告「关键技术基础②」）:

| 超参 | 建议取值 | 说明 |
|---|---|---|
| 裁剪系数 ε | `0.1 ~ 0.3` | 越大越激进、越小越保守 |
| 学习率 | `3e-4` 量级 | **与 batch 规模耦合** |
| GAE-λ | `0.95` | 在偏差与方差之间折中 |
| 折扣因子 γ | `0.99` 及以上 | 长航程任务需要更长视野 |
| KL 散度监控 | `0.01 ~ 0.02` | 衡量新旧策略差异，超出需调小学习率 |
| 熵系数 | 随训练衰减 | 前期维持探索，后期收敛 |

### 算法矩阵 / Algorithm Matrix

| 角色 | 算法 | 实现 | 选择的理由 |
|---|---|---|---|
| **主算法** | **PPO** | [SB3](https://github.com/DLR-RM/stable-baselines3) / [CleanRL](https://github.com/vwxyzjn/cleanrl) / [NavRL](https://github.com/Zhefan-Xu/NavRL) | 训练稳定、与安全约束模块兼容、可复用现成实现 |
| **对照算法** | **SAC** | [SB3](https://github.com/DLR-RM/stable-baselines3) | 验证「**样本效率 vs 稳定性**」的权衡；适合采样成本高的真实平台 |
| **中间基线** | **TD-MPC** | 论文方法 | 「模型 + 学习」的中间形态，风扰下通常比标准 RL 更稳 |
| **多机扩展** | **MAPPO** | [marlbenchmark/on-policy](https://github.com/marlbenchmark/on-policy) | 单机 PPO → 多机最自然的路径（CTDE 范式） |
| **传统基线 ①** | **级联 PID** | [PythonRobotics](https://github.com/AtsushiSakai/PythonRobotics) | 姿态内环 + 位置外环，工业默认方案 |
| **传统基线 ②** | **线性/非线性 MPC** | [do-mpc](https://github.com/do-mpc/do-mpc) | 滚动时域优化 + 显式约束处理 |

### 对比实验的公平性原则
- **同一动力学模型、同一风场序列、同一评价指标**；
- 指标至少含：**位置 RMSE、姿态误差、超调量、控制能耗、推理时延**；
- 基线需**调至最优**（PID 用整定后的增益，MPC 给出预测时域与权重），**避免「稻草人」对比**；
- **必须包含风扰工况**——若只在标称（无风）工况比较，RL 的优势会被高估。

> **实证支撑**：*SN Computer Science* 2026 在变化风况固定翼无人机上系统对比 MF-RL、MB-RL 与 PID，发现**标称工况 TD-MPC 最优，而风扰下标准 RL 框架表现次优且不稳定**。 [论文](https://link.springer.com/article/10.1007/s42979-026-04751-w)

---

> [← 返回总索引](../README.md) · [上一篇：数据集与风场模型](04-datasets-and-models.md)