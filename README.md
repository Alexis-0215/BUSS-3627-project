# 基于销售数据的随机过程建模与仿真分析

> **课程项目：随机过程（BUSS-3627）**  
> 小组成员：程彧博、叶芷晴、黄章真  
> 学号：522021910090 / 522120910214 / 522120910023  
> 提交日期：2025年6月11日  

## 📌 项目简介

本项目基于英国某电商公司的真实交易数据（Online Retail II 数据集），通过随机过程理论对客户购买行为进行建模与分析。主要研究内容包括：

- 客户订单间隔是否符合泊松过程；
- 客户消费金额状态转移是否服从马尔可夫链；
- 使用生存分析方法预测客户流失；
- 探索客户购买行为的非时齐泊松过程建模；
- 可视化分析与模型验证。

项目旨在揭示客户行为背后的随机性规律，为企业实现精细化运营和客户生命周期管理提供理论支持与实践指导。

## 📊 数据来源与预处理

- **数据集名称**：Online Retail II
- **时间范围**：2009年12月1日至2011年12月9日
- **字段说明**：
  - `Invoice`: 发票编号（唯一标识）
  - `StockCode`, `Description`: 商品编号及描述
  - `Quantity`, `UnitPrice`: 购买数量与单价
  - `InvoiceDate`: 交易时间戳
  - `CustomerID`: 客户唯一标识
  - `Country`: 客户所在国家

### 预处理步骤：
- 剔除取消订单（Invoice以 C 开头）
- 合并同一发票编号的数据
- 统一时间格式并提取时间特征
- 删除缺失 CustomerID 的记录
- 新增 TotalPrice 字段：`TotalPrice = Quantity × UnitPrice`

最终获得约 36,975 条有效交易记录用于建模分析。

## 🧪 主要建模方法

### 1. 泊松过程建模
- 分析客户订单间隔与每日订单间隔是否符合泊松过程
- 使用 K-S 检验判断是否服从指数分布
- 结果显示：81.26% 的客户 和 81.46% 的日期 符合泊松过程假设

### 2. 马尔可夫链建模
- 将客户消费金额划分为三个状态：Low (L), Medium (M), High (H)
- 构建状态转移矩阵并计算平稳分布
- 稳态分布为：`π = [0.34, 0.33, 0.33]`，表明长期来看三类消费状态趋于均衡

### 3. 生存分析
- 使用 Cox 比例风险模型 + Kaplan-Meier 曲线分析客户流失风险
- 流失定义：连续 200 天无购买行为
- RFM 客户分层结果显示：高价值客户仅占 15.97%，流失客户占比高达 35.95%

### 4. 非时齐泊松过程建模
- 使用核密度估计方法估计强度函数 λ(t)
- 对比不同函数形式（均匀、线性、二次）拟合效果
- 结果显示：二次函数在拟合误差上表现最佳

## 📁 项目结构

```
BUSS-3627-project/
├── data/               # 原始数据文件
├── code/               # Python/R 代码文件
│   ├── poisson_model.py    # 泊松过程建模
│   ├── markov_chain.py     # 马尔可夫链建模
│   ├── survival_analysis.py # 生存分析
│   └── nhpp_model.py       # 非时齐泊松过程建模
├── report/             # 报告文档
│   └── 随机过程期末报告.pdf
├── README.md           # 项目说明文档
└── requirements.txt    # Python 依赖包列表
```

## 🔗 相关链接

- 📘 项目报告：[查看 PDF](https://latex.sjtu.edu.cn/read/jvvzxbmjsqjc#8dcffb)
- 💻 GitHub 仓库地址：[https://github.com/Alexis-0215/BUSS-3627-project](https://github.com/Alexis-0215/BUSS-3627-project)

## 👥 小组分工

- **程彧博**：负责项目总体框架设计，并撰写第1章（引言）、第2章（数据来源与预处理）、第3章（泊松过程建模）
- **叶芷晴**：撰写第4章（马尔可夫链建模）和第5章（生存分析）
- **黄章真**：撰写第6章（非时齐泊松过程建模）和第7章（总结与展望）
