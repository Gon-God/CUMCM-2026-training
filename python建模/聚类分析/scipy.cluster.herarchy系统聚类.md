
1. linkage

`Z=linkage(y,method='single',metric='euclidean')`

各参数详解如下：

- **`y`** (**必需**): 输入数据。可以是：
    
    - 一个 `n x m` 的观测向量矩阵（即样本数据点），其中 `n` 是样本数，`m` 是特征数
        
    - 一个**压缩距离矩阵** (condensed distance matrix)您可以先用 `scipy.spatial.distance.pdist` 函数计算样本间的成对距离，再将结果传入`linkage`函数。

|方法 (`method`)|簇间距离的定义|特点与别名|
|---|---|---|
|**`'single'`**|不同簇中**最近**两点间的距离[](https://docs.scipy.org.cn/doc/scipy-1.14.0/reference/generated/scipy.cluster.hierarchy.linkage.html#scipy.cluster.hierarchy.linkage)[](https://docs.scipy.org/doc/scipy-1.14.1/reference/generated/scipy.cluster.hierarchy.linkage.html#scipy.cluster.hierarchy.linkage)|最近点算法，易形成链状簇，对噪声敏感|
|**`'complete'`**|不同簇中**最远**两点间的距离[](https://docs.scipy.org.cn/doc/scipy-1.14.0/reference/generated/scipy.cluster.hierarchy.linkage.html#scipy.cluster.hierarchy.linkage)[](https://docs.scipy.org/doc/scipy-1.14.1/reference/generated/scipy.cluster.hierarchy.linkage.html#scipy.cluster.hierarchy.linkage)|最远点算法，倾向于生成紧凑的球形簇|
|**`'average'`**|不同簇间**所有点对**的平均距离[](https://docs.scipy.org.cn/doc/scipy-1.14.0/reference/generated/scipy.cluster.hierarchy.linkage.html#scipy.cluster.hierarchy.linkage)[](https://docs.scipy.org/doc/scipy-1.14.1/reference/generated/scipy.cluster.hierarchy.linkage.html#scipy.cluster.hierarchy.linkage)|又称UPGMA算法，是两者间的折中|
|**`'weighted'`**|两个被合并簇与另一簇距离的加权平均[](https://docs.scipy.org.cn/doc/scipy-1.14.0/reference/generated/scipy.cluster.hierarchy.linkage.html#scipy.cluster.hierarchy.linkage)[](https://docs.scipy.org/doc/scipy-1.16.2/reference/generated/scipy.cluster.hierarchy.linkage.html#scipy.cluster.hierarchy.linkage)|又称WPGMA算法，赋予两合并簇相同权重|
|**`'centroid'`**|两个簇**质心**间的欧氏距离[](https://docs.scipy.org/doc/scipy-0.10.1/reference/generated/scipy.cluster.hierarchy.linkage.html#scipy.cluster.hierarchy.linkage)[](https://osgeo.cn/scipy/reference/generated/scipy.cluster.hierarchy.linkage.html#scipy.cluster.hierarchy.linkage)|又称UPGMC算法，质心代表簇的中心|
|**`'ward'`**|最小化合并后簇的**方差**增量[](https://docs.scipy.org/doc/scipy-0.10.1/reference/generated/scipy.cluster.hierarchy.linkage.html#scipy.cluster.hierarchy.linkage)|方差最小化算法，倾向于生成大小相近的簇|
- **`metric`** (**可选**, 默认 `'euclidean'`): 当输入 `y` 是数据矩阵时，用于计算样本间距离的度量，如 `'euclidean'`(欧氏距离)、`'minkowski'`(闵可夫斯基距离)、`'cityblock'`(曼哈顿距离)等[](https://tinycool.blog.csdn.net/article/details/135651401#comments_31437312)。
- ###  返回值 (`Z`)：连接矩阵

函数返回一个 `(n-1) x 4` 的 NumPy 数组 `Z`，记录了层次聚类的完整过程[](https://tinycool.blog.csdn.net/article/details/135651401#comments_31437312)[](https://browse.library.kiwix.org/content/stackoverflow.com_en_all_2023-11/questions/37712465/what-is-the-meaning-of-the-return-values-of-the-scipy-cluster-hierarchy-linkag)。对 `Z` 的每一行（`i` 从 `0` 到 `n-2`）：

- **`Z[i, 0]` & `Z[i, 1]`** (整数): 在第 `i` 次合并中，被聚在一起的**两个簇的索引**。索引小于 `n` 表示原始数据点（叶节点），大于等于 `n` 则表示之前合并生成的簇（内部节点）[](https://docs.scipy.org.cn/doc/scipy-1.14.0/reference/generated/scipy.cluster.hierarchy.linkage.html#scipy.cluster.hierarchy.linkage)[](https://docs.scipy.org.cn/doc/scipy-1.16.0/reference/generated/scipy.cluster.hierarchy.linkage.html)。
    
- **`Z[i, 2]`** (浮点数): 这两个簇在合并时的距离[](https://docs.scipy.org.cn/doc/scipy-1.14.0/reference/generated/scipy.cluster.hierarchy.linkage.html#scipy.cluster.hierarchy.linkage)[](https://browse.library.kiwix.org/content/stackoverflow.com_en_all_2023-11/questions/37712465/what-is-the-meaning-of-the-return-values-of-the-scipy-cluster-hierarchy-linkag)。
    
- **`Z[i, 3]`** (整数): 这个新形成的簇中所包含的**原始数据点的总数**（即该子树的叶子节点数）



例子
```python
from scipy.cluster.hierarchy import dendrogram, linkage
import matplotlib.pyplot as plt

X = [[i] for i in [2, 8, 0, 4, 1, 9, 9, 0]]
Z = linkage(X, method='ward')

print("连接矩阵 Z:")
print(Z)
# dendrogram(Z)
# plt.show()
```
[[ 5.          6.          0.          2.        ]
 [ 2.          7.          0.          2.        ]
 [ 0.          4.          1.          2.        ]
 [ 1.          8.          1.15470054  3.        ]
 [ 9.         10.          2.12132034  4.        ]
 [ 3.         12.          4.11096096  5.        ]
 [11.         13.         14.07183949  8.        ]]




`sch.dendrogram(c)`提供了将linkage的复杂归类图示化为树状图的方法

plt.show()即可
![[Pasted image 20260616172259.png]]
