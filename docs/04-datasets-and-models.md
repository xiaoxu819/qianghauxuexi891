# Datasets & Wind Models / 数据集与风场模型分册

> [← 返回总索引](../README.md)
>
> 本分册收录**气象风场数据集（7 个）、真实飞行数据集（5 个）与湍流模型（2 套）**，
> 并说明如何把它们用于**域随机化（domain randomization）** 与**风扰测试工况生成**。
> 标题统一 `Dataset Name（中文名称）` 格式。

---

## 目录

- [Ⅰ. 气象风场数据集（全球/区域再分析）/ Global & Regional Meteorological Reanalysis](#Ⅰ-气象风场数据集全球区域再分析--global--regional-meteorological-reanalysis)
- [Ⅱ. 真实飞行与扰动数据集 / Real Flight & Disturbance Datasets](#Ⅱ-真实飞行与扰动数据集--real-flight--disturbance-datasets)
- [Ⅲ. 风场与湍流模型 / Wind Field & Turbulence Models](#Ⅲ-风场与湍流模型--wind-field--turbulence-models)
- [Ⅳ. 在本项目中的用法 / How to Use in This Project](#Ⅳ-在本项目中的用法--how-to-use-in-this-project)

---

## Ⅰ. 气象风场数据集（全球/区域再分析）/ Global & Regional Meteorological Reanalysis

### ⭐ ERA5 (ECMWF Reanalysis v5)（欧洲中期天气预报中心全球再分析数据）
- **Link**: [数据集](https://cds.climate.copernicus.eu/datasets/reanalysis-era5-single-levels)
- **说明**: ECMWF 全球再分析数据，**0.25° 空间分辨率、逐小时时间分辨率**，含**风速、风向、温度、气压**等变量。是**最权威的气象数据集**，气象领域论文的标准数据源。
- **用途**: 提取目标区域的**历史风场序列**，构造训练与测试用的风扰工况；也可作策略输入的**气象先验特征**。

### MERRA-2 (NASA)（NASA 全球再分析数据）
- **Link**: [数据集](https://gmao.gsfc.nasa.gov/gmao-products/merra-2/)
- **说明**: NASA 的全球再分析产品，与 ERA5 **时间覆盖与同化方案互补**，同样含风场数据。
- **用途**: 与 ERA5 做**交叉验证**，避免单一数据源偏差；也便于构造**跨数据集泛化**测试。

### HRRR (NOAA)（美国高分辨率快速刷新气象模型）
- **Link**: [数据集](https://rapidrefresh.noaa.gov/hrrr/)
- **说明**: NOAA 的高分辨率快速刷新模型，**3 km 分辨率、逐小时更新**，适合**局地强对流与阵风**场景。
- **用途**: 生成**短时强阵风**工况，比全球再分析更能刻画突发扰动。

### PLUSWIND (DOE Wind Data Hub)（美国风电场级多模型小时风速数据集）
- **Link**: [数据集](https://wdh.energy.gov/project/pluswind)
- **说明**: 面向美国风电场的**场级多模型小时风速数据集**，**融合 ERA5 / MERRA-2 / HRRR** 三源。
- **用途**: 学习「**多源气象融合**」的特征工程范式，可迁移到无人机的多源风场输入设计。

### Texas / North America Weather Data (TAMU)（北美网格气象数据）
- **Link**: [数据集](https://electricgrids.engr.tamu.edu/weather-data/)
- **说明**: 北美 **0.25° 网格气象数据，覆盖 1940 年至今**，含风速、风向、**100 m 高度风速**等。
- **用途**: **长时段、大范围**的风场建模与统计特性分析（风切变、季节变化）。

### NOAA National Weather Service（美国国家气象局站点观测）
- **Link**: [数据集](https://www.weather.gov/)
- **说明**: 美国国家气象局**站点实测**气象数据（逐时风速/风向、气温等）。
- **用途**: 作为**实测基准**校验再分析数据在目标区域的代表性。

### China Meteorological Data Service Centre (CMA)（中国气象数据服务中心）
- **Link**: [数据集](http://data.cma.cn/)（需注册）
- **说明**: 中国地面气象站**逐时/逐日观测**数据。
- **用途**: 若研究区域在国内，这是**最贴近本土**的实测数据来源。

---

## Ⅱ. 真实飞行与扰动数据集 / Real Flight & Disturbance Datasets

### ⭐ CMU DJI Matrice 100 Wind Dataset（CMU 大疆 M100 风场数据集）
- **Link**: [论文 (Scientific Data 2021)](https://doi.org/10.1038/s41597-021-00930-x) · DOI: `10.1038/s41597-021-00930-x`（元数据 CC0）
- **说明**: **209 架次真实飞行**，机载**超声风速仪实测风场**，发表于 *Scientific Data*。
- **为什么推荐**: 少见的**「飞行状态 + 实测风」同步配对**数据，是验证「由状态反演风」与「抗风策略」的**黄金真实基准**。

### ⭐ Manipal UAV Flight Dataset（Manipal 无人机飞行数据集）
- **Link**: [代码与数据](https://github.com/ruppikha/uav-wind-estimation-control) · [论文 (IEEE Access 2025)](https://doi.org/10.1109/ACCESS.2025.3645364)
- **说明**: **变风况 / 变地形**飞行数据，**17 路同步特征**，面向**风估计**任务（IEEE Access 2025）。
- **为什么推荐**: 特征维度丰富且明确面向风估计，配套代码可直接跑通「数据 → 风估计 → 控制」闭环。

### ⭐ VID Dataset (Vision-Inertial-Dynamics)（视觉-惯性-动力学数据集）
- **Link**: [数据集](https://github.com/ZJU-FAST-Lab/VID-Dataset)
- **说明**: 包含**外力 / 扰动真值**的视觉-惯性-动力学数据集。
- **为什么推荐**: 带**扰动真值标签**的公开数据集非常稀缺，适合**扰动辨识与残差学习**（如 WA-TD3 的残差分支）训练。

### Fixed-Wing Benchmark Telemetry（固定翼基准遥测数据）
- **Link**: DOI: `10.5281/zenodo.16992975`（Zenodo）
- **说明**: **240 架次 PX4 / INAV 遥测**数据，面向**风感知导航**。
- **为什么推荐**: 固定翼方向的**现成遥测语料**，适合做风感知导航的离线预训练与验证。

### Agile Autonomy Dataset（野外高速飞行数据集）
- **Link**: [数据集](https://zenodo.org/records/5517791) · [代码](https://github.com/uzh-rpg/agile_autonomy)
- **说明**: Science Robotics 2021「Learning High-Speed Flight in the Wild」配套数据，含**森林等复杂环境的高速飞行**数据。
- **为什么推荐**: 若要研究**复杂环境下的高速机动**，这是权威论文配套的公开数据。

---

## Ⅲ. 风场与湍流模型 / Wind Field & Turbulence Models

> 湍流模型是**仿真侧风场生成**的标准工具，也是**域随机化**的参数来源。

### ⭐ Dryden Turbulence Model（Dryden 湍流模型）
- **Link**: [参考](https://en.wikipedia.org/wiki/Continuous_gusts)
- **说明**: 1952 年提出，以**有理谱（rational spectrum）近似湍流功率谱**，**工程实现简单**，是仿真中**最常用的连续湍流模型**。
- **用途**: 作为基础风场扰动生成器，参数（湍流尺度、强度）可直接作为**域随机化的采样维度**。

### ⭐ von Kármán Turbulence Model（von Kármán 湍流模型）
- **Link**: [参考](https://en.wikipedia.org/wiki/Continuous_gusts) · 权威出处：**MIL-STD-1797A**（美国飞行品质军标）
- **说明**: NACA 1957 年提出，**DoD（美国国防部）/ FAA（美国联邦航空管理局）首选**的连续湍流模型，**频谱拟合更贴近实测**。
- **用途**: 当需要**更高物理保真度**的风扰工况时替换 Dryden；建议两者都实现并对比。
- **工程实现参考**: **MathWorks Aerospace Blockset** 同时提供 Dryden 与 von Kármán 湍流模块的标准实现。

---

## Ⅳ. 在本项目中的用法 / How to Use in This Project

> 对应调研报告「关键技术基础⑤：气象时序特征融入 RL 策略网络」与「第四步：域随机化训练」。

| 环节 | 用什么 | 怎么用 |
|---|---|---|
| **风场序列生成** | Dryden / von Kármán 湍流模型 | 生成含**风切变与阵风**的风场序列，作为仿真环境的扰动输入 |
| **域随机化（训练）** | 湍流模型参数 + ERA5 统计特性 | 训练时随机化风场参数（强度、尺度、方向），是**零样本 sim-to-real 的关键** |
| **风扰测试工况** | ERA5 / MERRA-2 / HRRR | 用真实再分析数据构造**贴近实际**的测试工况，避免只在标称工况评估 |
| **显式风估计** | CMU M100 / Manipal / VID | 用带**风的真值**数据训练风估计器（LSTM/GRU），拼入观测向量（**状态空间级**融合） |
| **残差隐式风感知** | VID Dataset（扰动真值） | 用扰动真值监督「预测动力学 − 实际动力学」的残差时序（**网络结构级**融合） |
| **泛化性评估** | MERRA-2 vs ERA5 跨源 | 用不同数据源/不同区域的风场测试策略泛化能力 |

> **三类融合方案的实证效果参照**（详见 [论文分册](01-papers.md)）：
> - 状态空间级：风速 RMSE `0.40 m/s`、风向误差 `3.2°`，跟踪误差降 `48%`
> - 网络结构级：WA-TD3 强风下跟踪精度提升 **> 62%**
> - 监督器级：方向/高度误差降 `67%`/`89%`，计算时间减 **> 93%**

---

> [← 返回总索引](../README.md) · [上一篇：仿真软件](03-simulation-tools.md) · [下一篇：算法库与基线 →](05-algorithms-and-baselines.md)