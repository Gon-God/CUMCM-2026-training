
结合了主成分分析与最小二乘分析

面对**变量多、样本少、变量之间关系复杂**的数据

### 主要优势与适用场景

PLS回归的强大之处在于它能解决很多传统方法的“痛点”[](https://eplat.imau.edu.cn/meol/analytics/resPdfShow.do;jsessionid=E4B2E6837EFAF8DE6AAE9AAF1E448193?resId=143305&lid=11210#2#1)：

- **处理“高维”数据**：当预测变量的数量（p）多于样本观测值数量（n）时，传统的最小二乘法会失效[](https://baike.baidu.com/item/%E5%81%8F%E6%9C%80%E5%B0%8F%E4%BA%8C%E4%B9%98%E6%B3%95/10689650?anchor=1#1)[](https://support.minitab.com/zh-cn/minitab/help-and-how-to/statistical-modeling/regression/how-to/partial-least-squares/before-you-start/overview/)。而PLS回归依然可以有效建模[](https://www.kepuchina.cn/article/articleinfo?business_type=100&classify=0&ar_id=200999)。
    
- **应对“多重共线性”**：当预测变量之间存在高度相关性时，传统回归的系数估计会非常不稳定[](https://eplat.imau.edu.cn/meol/analytics/resPdfShow.do;jsessionid=E4B2E6837EFAF8DE6AAE9AAF1E448193?resId=143305&lid=11210#2#1)。PLS回归能有效消除这种影响。
    
- **一个模型分析多个响应变量**：PLS回归可以同时在单个模型中拟合多个响应变量[](https://support.minitab.com/zh-cn/minitab/help-and-how-to/statistical-modeling/regression/supporting-topics/partial-least-squares-regression/what-is-partial-least-squares-regression/)，这比单独为每个响应变量建模能发现更微妙的关联[](https://support.minitab.com/zh-cn/minitab/help-and-how-to/statistical-modeling/regression/how-to/partial-least-squares/before-you-start/overview/)。
    
- **兼具探索与预测功能**：它不仅能建立预测模型，还能同时实现数据结构简化（类似主成分分析）和变量间相关性分析（类似典型相关分析）。

### 主要缺点与局限

尽管功能强大，PLS回归也有其局限性：

- **成分物理意义模糊**：提取出的潜变量是原始变量的线性组合，其实际含义有时难以直接解释。
    
- **并非万能**：提取的主成分可能无法同时保证方差和相关程度都达到最大。

---
实现：

1. **数据标准化**：对自变量矩阵X和因变量矩阵Y进行标准化处理，消除量纲影响。
    
2. **提取第一个成分**：
    
    - 从X中提取第一个成分 `t1`（X的线性组合），从Y中提取第一个成分 `u1`（Y的线性组合），并使得 `t1` 与 `u1` 之间的协方差最大。
        
3. **建立回归并计算残差**：
    
    - 建立X对 `t1` 和Y对 `t1` 的回归。
        
    - 计算X和Y的残差矩阵，即原始数据中未被当前成分解释的部分。
        
4. **迭代提取后续成分**：用上一步得到的残差矩阵代替原始X和Y，重复步骤2和3，提取第二个成分、第三个成分……直到提取出足够数量的成分或残差矩阵趋近于零[](https://support.minitab.com/zh-cn/minitab/help-and-how-to/statistical-modeling/regression/how-to/partial-least-squares/methods-and-formulas/methods/)。
    
5. **构建最终模型**：基于提取出的所有成分，构建最终的回归模型，并转换为关于原始变量的回归系数[](https://support.minitab.com/zh-cn/minitab/help-and-how-to/statistical-modeling/regression/how-to/partial-least-squares/methods-and-formulas/methods/)。

---

利用`sklearn.cross_decomposition.PLSRegression`进行模型的训练

首先要进行交叉验证，得出n_components的值
```python
import numpy as np
from sklearn.cross_decomposition import PLSRegression
from sklearn.model_selection import train_test_split
from sklearn.metrics import mean_squared_error, r2_score
from sklearn.model_selection import cross_val_predict, GridSearchCV
from sklearn.metrics import make_scorer

# 1. 准备数据 (这里用随机数据作为示例)
# 在实际应用中，你需要从CSV或数据库中加载你的数据[reference:8]
np.random.seed(42)
X = np.random.rand(100, 5)  # 100个样本，5个特征（自变量）[reference:9]
y = np.random.rand(100, 1)  # 100个样本，1个目标变量（因变量）[reference:10]

# 2. 划分训练集和测试集[reference:11]
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)


from sklearn.model_selection import cross_val_predict, GridSearchCV
from sklearn.metrics import make_scorer

# 定义要搜索的参数范围
param_grid = {'n_components': range(1, 16)}  # 测试1到15个成分

# 创建PLS回归模型
pls = PLSRegression()

# 使用网格搜索进行交叉验证
# 这里使用负均方误差作为评分标准，因为GridSearchCV默认是最大化评分
grid_search = GridSearchCV(pls, param_grid, cv=5, scoring='neg_mean_squared_error')
grid_search.fit(X_train, y_train)

# 输出最佳参数
print(f"最佳成分数量: {grid_search.best_params_['n_components']}")
```

最佳成分数量: 2

```python
# 3. 创建PLS回归模型[reference:12][reference:13]
# n_components是关键参数，代表要提取的潜变量（成分）数量[reference:14]
pls = PLSRegression(n_components=2)

# 4. 训练模型[reference:15][reference:16]
pls.fit(X_train, y_train)

# 5. 进行预测[reference:17]
y_pred = pls.predict(X_test)

# 6. 评估模型[reference:18]
mse = mean_squared_error(y_test, y_pred)
r2 = r2_score(y_test, y_pred)
print(f"均方误差 (MSE): {mse:.4f}")
print(f"R² 得分: {r2:.4f}")
```
均方误差 (MSE): 0.1241
R² 得分: -0.6236