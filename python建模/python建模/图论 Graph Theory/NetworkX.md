Python库，可以存储网络

# 引入
```python
import networks as nx
```

---

# 图的生成

network 提供了四种基本图类型
1. Graph: 无向图
	创建：`G = nx.Graph()`
2. DiGraph: 有向图
	创建：`G = nx.DiGraph()`
3. MultiGraph:多重无向图：允许两个顶点之间条数多于1条，允许环
4. MultiDiGraph:多重有向图

