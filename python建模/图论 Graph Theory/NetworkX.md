Python库，可以存储网络

# 引入
```python
import networks as nx
```

---

# 图的生成

networkx 提供了四种基本图类型
1. Graph: 无向图
	创建：`G = nx.Graph()`
2. DiGraph: 有向图
	创建：`G = nx.DiGraph()`
3. MultiGraph:多重无向图：允许两个顶点之间条数多于1条，允许环
4. MultiDiGraph:多重有向图

**Grow()函数**

```python
nx.draw(G)
```

G是要绘制的图对象

| 类别  | 参数名           | 作用简介                                           | 常用示例                                                                                                                  |
| --- | ------------- | ---------------------------------------------- | --------------------------------------------------------------------------------------------------------------------- |
| 整体  | `G`           | **要绘制的图对象**                                    | `nx.draw(G)`                                                                                                          |
| 布局  | `pos`         | 指定节点位置 (布局算法)。若未指定，**默认使用弹簧布局(spring_layout)** | `pos = nx.circular_layout(G)`顶点在一个圆环上均匀分布<br>`pos = nx.random_layout(G)`单位正方形随机分布<br>pos = nx.shell_layout:顶点在多个同心圆分布 |
| 节点  | `node_size`   | 控制节点大小                                         | `node_size=200` (值越大节点越大，默认300)                                                                                       |
| 节点  | `node_color`  | 控制节点颜色                                         | `node_color='blue'`, `node_color='#FF5733'` (默认红色)                                                                    |
| 节点  | `node_shape`  | 控制节点形状                                         | `node_shape='s'` (方形，默认圆形'o')                                                                                         |
| 节点  | `with_labels` | 是否显示节点标签                                       | `with_labels=True`                                                                                                    |
| 节点  | `font_size`   | 控制节点标签字体大小                                     | `font_size=12` (默认12)                                                                                                 |
| 节点  | `font_color`  | 控制节点标签字体颜色                                     | `font_color='black'` (默认黑色)                                                                                           |
| 边   | `width`       | 控制边的粗细                                         | `width=2.0` (默认1.0)                                                                                                   |
| 边   | `edge_color`  | 控制边的颜色                                         | `edge_color='gray'` (默认黑色)                                                                                            |
| 边   | `style`       | 控制边的样式                                         | `style='dashed'` (虚线)                                                                                                 |
| 通用  | `alpha`       | 控制颜色透明度                                        | `alpha=0.6` (值为0到1)                                                                                                   |
| 其他  | `ax`          | 指定 Matplotlib 坐标轴对象                            | `fig, ax = plt.subplots(); nx.draw(G, ax=ax)`                                                                         |



```python
import networkx as nx
import pylab as plt

G = nx.cubical_graph() #生成一个3正则图
plt.subplot(121)
nx.draw(G, with_labels=True)

pt.subplot(122)
s = ['v'+ str(i) for i in range (1,9)] #str(i)，这样能创建一个由v1到v9的数组
s = dict(zip(range(8),s)) #将vi转化为了字典形式

nx.draw(G, pos = nx.`pos = nx.circular_layout(G),labels=s)
plt.show()
```
![[Pasted image 20260611212219.png]]

---
# 数据储存结构

```python
G=nx.Graph()
G.add_node(1) #添加编号为1的顶点
G.add_nodes_from(['A','B']) #同时添加多个顶点
G.add_edge('A','B') #添加A和B之间的无向边
G.add_edge(1,2,weight=0.5) #顶点1和2之间权重为0.5的无向边
e=[('A','B',0.3),('B','C',0.9),('A','C',0.5),('C','D',1.2)]
G.add_weighted_edges_from(e) #添加多个权重无向边
print(G.adj)#显示邻接表的字典数据
print(list(G.adjacency()))#显示邻接表的列表数据
```

---

# 图数据的导出

```python

W1 = nx.to_numpy_matrix(G) #导出G的权重邻接矩阵
W2 = nx.get_edge_attributes(G,'weight') #导出赋权边的字典数据
np.savetxt('data.txt',W1,fmt = '%d')#把矩阵数据保存在一个文本文件里面
```

---

# 算法

求最短路径:
`dijkstra_path(G, source, target, weight = 'weight')`

求最短距离
`dijkstra_path_length(G, source, target, weight = 'weight')`

source是源节点，target是目标节点，weight默认