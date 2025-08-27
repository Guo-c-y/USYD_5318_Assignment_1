# README for `COMP5318-assignment1-2025`

### 项目简介
该 Notebook 文件以 `a1-COMP5318-2025-template.ipynb` 为模板，主要实现以下功能：
1. 对稻米分类数据集进行预处理
2. 使用多种机器学习模型进行分类实验，包括：
   - 交叉验证
   - 参数调优
   - 不同分类器性能比较

### 环境配置
通过以下命令安装项目依赖：
```bash
conda env create -f environment.yml -n myenv
conda activate myenv
```

### 文件结构与内容

#### 1. 导入库
- 使用 `pandas`、`numpy` 进行数据处理  
- 使用 `sklearn` 的 `SimpleImputer`、`MinMaxScaler` 进行数据预处理  
- 使用 `sklearn.model_selection` 进行交叉验证 (`StratifiedKFold`、`cross_val_score`、`GridSearchCV`)  
- 使用 `sklearn` 提供的多种分类器，包括：
  - Logistic Regression  
  - Naïve Bayes  
  - Decision Tree  
  - Bagging, AdaBoost, Gradient Boosting  
  - Random Forest  
  - K Nearest Neighbors  

#### 2. 数据加载
- 加载原始数据集（测试为 `test-before.csv`，实际应为 `rice-final2.csv`）。
- 展示前10行数据。

### Part 1

### 3. 数据预处理
- 分离特征与标签。  
- 缺失值填补：用列均值填充缺失值。  
- 特征归一化：缩放到 `[0, 1]` 范围。  
- 标签编码：`class1 -> 0`，`class2 -> 1`。  
- 打印处理后的前十行数据（格式化为小数点后四位）。  
- 保存预处理后的数据集 `rice-final2-preprocessed.csv`。

### 4. 交叉验证与模型训练
- 设置 **10 折分层交叉验证 (StratifiedKFold)**。  
- 定义并评估以下分类器：
  - **Logistic Regression**  
  - **Naïve Bayes**  
  - **Decision Tree (entropy)**  
  - **集成方法**：
    - Bagging + 决策树
    - AdaBoost + 决策树
    - Gradient Boosting  

- 每个模型均通过 `cross_val_score` 计算平均准确率。

### Part 2

### 5. 参数调优 (Grid Search)
- 使用 `GridSearchCV` 对以下模型进行调参：
  - **K Nearest Neighbors (KNN)**  
  - **Random Forest**  
- 调优参数包括邻居数量、树的数量、最大深度等。  
- 使用 **10 折分层交叉验证** 选择最佳参数。

### 6. 模型评估
- 使用准确率 (accuracy) 与 F1 分数 (f1_score) 作为性能指标。  
- 比较不同模型与调优结果的表现。  

### 方法汇总表格

在该 Notebook 的实验部分中，所有分类器通过 **10 折交叉验证** 或 **GridSearchCV** 得到性能结果。以下表格汇总了各模型的表现：

| 模型 | 调参方式 | 交叉验证准确率 | 测试集准确率 | F1 (macro) | F1 (weighted) | 最优参数 |
|------|----------|---------------|--------------|------------|---------------|----------|
| Logistic Regression | 无参数调优 | 平均准确率输出 | - | - | - | 默认参数 |
| Naïve Bayes | 无参数调优 | 平均准确率输出 | - | - | - | 默认参数 |
| Decision Tree (Entropy) | 无参数调优 | 平均准确率输出 | - | - | - | `criterion='entropy'` |
| Bagging + 决策树 | 无参数调优 | 平均准确率输出 | - | - | - | `n_estimators=50, max_samples=100, max_depth=5` |
| AdaBoost + 决策树 | 无参数调优 | 平均准确率输出 | - | - | - | `n_estimators=50, learning_rate=0.5, max_depth=5` |
| Gradient Boosting | 无参数调优 | 平均准确率输出 | - | - | - | `n_estimators=50, learning_rate=0.5` |
| KNN | GridSearchCV | 最优交叉验证准确率 | 对应测试集准确率 | - | - | `n_neighbors=k, p=p` |
| Random Forest | GridSearchCV | 最优交叉验证准确率 | 对应测试集准确率 | `macro F1` | `weighted F1` | `n_estimators, max_leaf_nodes` |

---

### 表格说明
- **无参数调优的模型**：直接报告交叉验证的平均准确率。  
- **Bagging / AdaBoost / Gradient Boosting**：基分类器为决策树，参数在代码中给定。  
- **KNN 与 Random Forest**：通过 `GridSearchCV` 进行参数调优，报告最佳参数及性能。  
- **Random Forest** 额外报告了 F1 (macro 与 weighted)。  
