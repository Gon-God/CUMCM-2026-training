
pylab,pyplot提供了类似MATLAB的绘图接口
一般来说，我们用Matplotlib.pylab

# 引入
```python
import matplotlib.pyplot as plt
```

### 显示中文符号
```python
rcParams['font.sans-serif'] = ['SimHei'] #正常显示中文标签
rcParams['axes.unicode_minus'] = False #用来正常显示负号
```

### 设置字体大小
```python
plt.rc('font', size = 16)
```

---

# 显示图例

```python
plt.legend()
```
如果不加东西, 就是自动

| 参数               | 说明                | 示例                                                          |
| ---------------- | ----------------- | ----------------------------------------------------------- |
| `loc`            | 图例的位置             | `'upper right'`, `'lower left'`, `'center'`, `'best'`（自动选择） |
| `ncol`           | 图例显示的列数           | `ncol=2`（两列并排）                                              |
| `fontsize`       | 图例文字大小            | `'small'`, `'large'`, 整数（如 `12`）                            |
| `title`          | 为图例添加标题           | `title='曲线类型'`                                              |
| `shadow`         | 是否添加阴影            | `shadow=True`                                               |
| `frameon`        | 是否显示图例边框          | `frameon=False`（去掉边框）                                       |
| `bbox_to_anchor` | 将图例放置在坐标系外部（高级定位） | `(1.05, 1)`（放在图表右侧）                                         |
### 位置 `loc` 的常用值

| 字符串              | 含义           |
| ---------------- | ------------ |
| `'best'`         | 自动选择最优位置（默认） |
| `'upper right'`  | 右上角          |
| `'upper left'`   | 左上角          |
| `'lower left'`   | 左下角          |
| `'lower right'`  | 右下角          |
| `'right'`        | 右侧中间         |
| `'center left'`  | 左侧中间         |
| `'center right'` | 右侧中间         |
| `'lower center'` | 底部中间         |
| `'upper center'` | 顶部中间         |
| `'center'`       | 正中央          |

自定义图例外观

```python
plt.legend(
    loc='lower right',      # 位置
    ncol=1,                 # 列数
    fontsize='large',       # 字号
    title='Legend Title',   # 标题
    shadow=True,            # 阴影
    fancybox=True,          # 圆角边框
    framealpha=0.5          # 边框透明度
)
```

---
# 标签，标题

```python
plt.xlabel('') #x轴标签
plt.ylabel('') #y轴标签
plt.title('') #标题
```

## 常用参数（可同时用于三个函数）

| 参数           | 说明                                       | 示例                  |
| ------------ | ---------------------------------------- | ------------------- |
| `fontsize`   | 文字大小（整数或字符串如 'large'）                    | `fontsize=14`       |
| `fontweight` | 粗细（'normal', 'bold'）                     | `fontweight='bold'` |
| `color`      | 文字颜色（名称、十六进制或RGB）                        | `color='red'`       |
| `loc`        | 标签位置（`title` 专用：'center','left','right'） | `loc='left'`        |
| `labelpad`   | 标签与轴/图的间距（点数）                            | `labelpad=10`       |
| `style`      | 字体样式（'normal','italic'）                  | `style='italic'`    |

示例：
```python
plt.plot(x, y, label='sin(x)')

plt.xlabel("时间 (秒)", fontsize=12, color='blue', labelpad=8)
plt.ylabel("振幅", fontsize=12, fontweight='bold')
plt.title("正弦函数图像", fontsize=16, fontweight='bold', loc='left', color='darkgreen')

plt.legend()
plt.show()
```

---

# 折线图

格式：
```python
pylab.plot(x, y, s)
```
s为指定的线条的字符串

| 关键字参数                     | 说明                          |     |
| ------------------------- | --------------------------- | --- |
| `color` / `c`             | 设置线条颜色                      |     |
| `linestyle` / `ls`        | 设置线条样式                      |     |
| `linewidth` / `lw`        | 设置线条宽度（浮点数）                 |     |
| `marker`                  | 设置数据点的标记样式                  |     |
| `markersize` / `ms`       | 设置标记的大小                     |     |
| `markerfacecolor` / `mfc` | 设置标记内部的填充颜色                 |     |
| `markeredgecolor` / `mec` | 设置标记边缘的颜色                   |     |
| `alpha`                   | 设置线条或标记的透明度                 |     |
| `label`                   | 为图线设置标签，与 `legend()` 函数一同使用 |     |
|                           |                             |     |
### color
| 颜色名称         | 缩写    |
| ------------ | ----- |
| 蓝色 (blue)    | `'b'` |
| 绿色 (green)   | `'g'` |
| 红色 (red)     | `'r'` |
| 青色 (cyan)    | `'c'` |
| 品红 (magenta) | `'m'` |
| 黄色 (yellow)  | `'y'` |
| 黑色 (black)   | `'k'` |
| 白色 (white)   | `'w'` |
### linestyle
| 样式名称 | 字符串缩写            | 完整字符串       | 示例效果    |
| ---- | ---------------- | ----------- | ------- |
| 实线   | `'-'`            | `'solid'`   | ━━━━━   |
| 虚线   | `'--'`           | `'dashed'`  | ━ ━ ━   |
| 点划线  | `'-.'`           | `'dashdot'` | ━ ‧ ━ ‧ |
| 点线   | `':'`            | `'dotted'`  | ‧ ‧ ‧ ‧ |
| 无线条  | `'None'` 或 `' '` | `'none'`    | (无)     |
### marker 数据点形状

| 描述       | 标记代码             | 示例效果   |
| -------- | ---------------- | ------ |
| 点 (小圆点)  | `'.'`            | •      |
| 像素点      | `','`            | █ (极小) |
| 圆圈       | `'o'`            | ○      |
| 下三角形     | `'v'`            | ▼      |
| 上三角形     | `'^'`            | ▲      |
| 左三角形     | `'<'`            | ◀      |
| 右三角形     | `'>'`            | ▶      |
| 正方形      | `'s'`            | ■      |
| 菱形 (宽)   | `'D'`            | ◆      |
| 细菱形      | `'d'`            | ◇      |
| 五边形      | `'p'`            | ⬟      |
| 星形       | `'*'`            | ★      |
| 六边形1 (横) | `'h'`            | ⬢      |
| 六边形2 (竖) | `'H'`            | ⬣      |
| 加号       | `'+'`            | +      |
| 叉号       | `'x'`            | ×      |
| 竖线       | `'\|'`           | \|     |
| 横线       | `'_'`            | _      |
| 无标记      | `'None'` / `' '` | (无)    |

---

# 其他类型的图

| 图表名称    | 主要函数                               | 简要说明                                                                                      | 核心代码示例                                                  |
| ------- | ---------------------------------- | ----------------------------------------------------------------------------------------- | ------------------------------------------------------- |
| **散点图** | `plt.scatter()`                    | 显示两个变量之间的关系，也常用来展示数据的分布或聚类。                                                               | `plt.scatter(x, y, s=area, c=colors, alpha=0.5)`        |
| **条形图** | `plt.bar()` (垂直) `plt.barh()` (水平) | 适用于比较不同类别的数值大小。                                                                           | `plt.bar(categories, values, width=0.8)`                |
| **直方图** | `plt.hist()`                       | 将数据分组（bins），观察数据的频率分布情况。                                                                  | `plt.hist(data, bins=30, edgecolor='black', alpha=0.7)` |
| **箱线图** | `plt.boxplot()`                    | 用一种标准化的方式展示数据的分布特征，包括中位数、四分位数和异常值[](https://developer.baidu.com/article/details/2793881)。 | `plt.boxplot(data, notch=True, vert=True)`              |
| **饼图**  | `plt.pie()`                        | 展示各部分占整体的比例关系。                                                                            | `plt.pie(sizes, labels=labels, autopct='%1.1f%%')`      |
| **填充图** | `plt.fill_between()`               | 突出显示两条曲线之间的区域                                                                             | `plt.fill_between(x, y1, y2, color='blue', alpha=0.3)`  |
晚点一个一个弄

---

## 绘图DataFrame
Pandas 中的DataFrame对象，可以通过plot方法直接绘制

```python
df.plot(kind= '图表类型', title = "")
df.plot.图表类型()
```

==kind参数对照表==

| 图表类型     | `kind` 参数                    | 适用场景                                                                                                                       | 核心参数（除通用外）                  |
| -------- | ---------------------------- | -------------------------------------------------------------------------------------------------------------------------- | --------------------------- |
| **柱状图**  | `'bar'` (垂直) / `'barh'` (水平) | 对比不同**类别**的数据（如各产品销售、地区人口）。                                                                                                | `stacked`: 是否堆叠显示。          |
| **直方图**  | `'hist'`                     | 查看单列数据的**数值分布**（如年龄、收入分布）[](https://cloud.tencent.cn/developer/information/python%20pandas%20dataframe.plot\(\))。          | `bins`: 柱子数量；`alpha`: 透明度。  |
| **箱线图**  | `'box'`                      | 展示数据的分布和**异常值**（四分位数、中位数等）[](https://cloud.tencent.cn/developer/information/python%20pandas%20dataframe.plot\(\))。         |                             |
| **密度图**  | `'kde'` 或 `'density'`        | 观察数据的**概率密度分布**，是直方图的平滑版本。                                                                                                 |                             |
| **散点图**  | `'scatter'`                  | 分析两个**数值变量**间的**关系**（如相关性）[](https://cloud.tencent.cn/developer/information/python%20pandas%20dataframe.plot\(\))。         | `x`, `y`: 指定 x 轴和 y 轴对应的列名。 |
| **面积图**  | `'area'`                     | 显示数据序列的**变化趋势**，并强调其累积贡献。                                                                                                  | `stacked`: 是否堆叠（默认 True）。   |
| **饼图**   | `'pie'`                      | 展示各部分的**占比**关系（如市场份额）[](https://cloud.tencent.cn/developer/information/python%20pandas%20dataframe.plot\(\))。              | `y`: 指定用于做饼的列。              |
| **六边形图** | `'hexbin'`                   | 处理海量数据点的**密度散点图**，通过六边形分箱避免重叠[](https://pandas.ac.cn/docs/reference/api/pandas.DataFrame.plot.html#pandas.DataFrame.plot)。 |                             |

### 常用定制参数

你可以在 `plot()` 函数中加入参数来美化图表：

| 参数                  | 说明            | 示例                |
| ------------------- | ------------- | ----------------- |
| `title`             | 图表标题          | `title='My Plot'` |
| `xlabel` / `ylabel` | X/Y轴标签        | `xlabel='日期'`     |
| `figsize`           | 图表尺寸，如 (宽, 高) | `figsize=(10, 6)` |
| `grid`              | 是否显示网格线       | `grid=True`       |
| `legend`            | 是否显示图例        | `legend=True`     |
| `xlim` / `ylim`     | 轴的范围          | `ylim=(0, 200)`   |

---

# 子图

利用 plt.subplots()
语法：
```python
fig, axes = plt.subplots(nrows, ncols, figsize=(w, h))
```

- `nrows`, `ncols`：行数和列数
    
- `figsize`：画布尺寸（英寸）
    
- 返回：`fig` (Figure 对象) 和 `axes` (Axes 对象或二维数组)

调用
`axes[横向位置，纵向位置].plot()
`axes[0, 0].set_title('设置子图标题')`

**创建2x2子图**
```python
x = np.linspace(0, 2*np.pi, 100)
#创建等距线性数组
y1 = np.sin(x)
y2 = np.cos(x)
y3 = np.sin(x)**2
y4 = np.cos(x)**2

fig, axes = plt.subplots(2, 2, figsize=(10, 8))
#2x2,尺寸为10x8英寸

axes[0, 0].plot(x, y1, 'r-')
axes[0, 0].set_title('sin(x)')

axes[0, 1].plot(x, y2, 'b--')
axes[0, 1].set_title('cos(x)')

axes[1, 0].plot(x, y3, 'g-.')
axes[1, 0].set_title('sin²(x)')

axes[1, 1].plot(x, y4, 'm:')
axes[1, 1].set_title('cos²(x)')

plt.tight_layout()  # 自动调整间距，防止重叠
plt.show()
```

---

# 三维绘图

### 通用设置

|函数/属性|说明|示例|
|---|---|---|
|`ax.set_xlabel()`, `.set_ylabel()`, `.set_zlabel()`|坐标轴标签|`ax.set_xlabel('X')`|
|`ax.set_title()`|图表标题|`ax.set_title('3D Plot')`|
|`ax.view_init(elev, azim)`|设置视角 (仰角, 方位角)|`ax.view_init(30, 45)`|
|`fig.colorbar(mappable)`|添加颜色条|`fig.colorbar(surf)`|
|`ax.set_xlim()`, `.set_ylim()`, `.set_zlim()`|设置坐标轴范围|`ax.set_zlim(-1, 1)`|

### 三维曲线图

用`plot(x,y,z，“”)`传入三个参数绘制折线图即可
```python
# 在同一个坐标系中绘制两条曲线
t = np.linspace(0, 4 * np.pi, 100)
x1, y1, z1 = np.sin(t), np.cos(t), t
x2, y2, z2 = np.sin(t + np.pi), np.cos(t + np.pi), t  # 另一条相位偏移的螺旋线

ax.plot(x1, y1, z1, label='Curve 1', color='r')
ax.plot(x2, y2, z2, label='Curve 2', color='b', linestyle='--')
```

核心参数

|参数|说明|示例|
|---|---|---|
|`xs, ys, zs`|三个一维数组（或单个标量）|`x, y, z`|
|`color` / `c`|线条颜色|`'b'`, `'red'`|
|`linestyle` / `ls`|线型|`'-'`, `'--'`, `':'`|
|`linewidth` / `lw`|线宽|`2.5`|
|`marker`|数据点标记形状|`'o'`, `'^'`, `'.'`|
|`markersize` / `ms`|标记大小|`5`|
|`label`|图例标签|`'my curve'`|
|`alpha`|透明度|`0.8`|
### 三维曲面图
设置：
```python
import matplotlib.pyplot as plt
from mpl_toolkits.mplot3d import Axes3D
import numpy as np

fig = plt.figure()
ax = fig.add_subplot(111, projection='3d')
```

###  工具1：`plot_surface`（规则网格数据）

如果你的数据点排列成规则的**网格**（如矩阵形式），这是最合适的选择。

`ax.plot_surface(X, Y, Z)` 需要 X, Y, Z 三个**二维数组**作为输入，它们定义了每个网格点上的坐标

下面是一个经典示例，它使用网格数据绘制了一个三维的“波纹”曲面：
```python
# 1. 生成数据：创建网格坐标并计算 Z 值
x = np.linspace(-5, 5, 100)
y = np.linspace(-5, 5, 100)
X, Y = np.meshgrid(x, y)
Z = np.sin(np.sqrt(X**2 + Y**2))
# 2. 绘制曲面
surf = ax.plot_surface(X, Y, Z, cmap='viridis')
# 3. 添加颜色条、标签并显示
fig.colorbar(surf)
ax.set_xlabel('X Axis'); ax.set_ylabel('Y Axis'); ax.set_zlabel('Z Axis')
plt.show()
```

核心参数

| 参数                 | 说明                       | 常用值/示例                                             |
| ------------------ | ------------------------ | -------------------------------------------------- |
| `X, Y, Z`          | **必填**，二维数组，定义网格点的坐标     | 由 `np.meshgrid` 生成                                 |
| `cmap`             | 颜色映射方案                   | `'viridis'`, `'plasma'`, `'coolwarm'`, `'rainbow'` |
| `norm`             | 颜色映射的归一化方式               | `Normalize()`, `LogNorm()`                         |
| `rstride, cstride` | 行/列采样步长（控制分辨率）           | `rstride=1, cstride=1` (最高)                        |
| `rcount, ccount`   | 行/列最大采样点数（替代 stride，更直观） | `rcount=100, ccount=100`                           |
| `color`            | 单一颜色（当不需要 `cmap` 时）      | `'red'`, `'#FF5733'`                               |
| `alpha`            | 透明度 (0-1)                | `alpha=0.7`                                        |
| `antialiased`      | 是否抗锯齿                    | `antialiased=True` (默认)                            |
| `shade`            | 是否光照阴影                   | `shade=True` (默认)                                  |
| `linewidth`        | 网格线宽度                    | `linewidth=0` (不显示网格线)                             |
| `edgecolor`        | 网格线颜色                    | `edgecolor='black'`                                |
|                    |                          |                                                    |

### 工具2：`plot_trisurf`（非规则网格数据）

如果你的数据点是**随机分布或散乱的**（如测量得到的离散点），无法形成规则网格，就需要使用 `plot_trisurf`。

- `ax.plot_trisurf(x, y, z)` 接受三个**一维数组**作为输入，然后通过三角剖分算法自动生成曲面

下面的代码用随机生成的100个点来演示，它会自动将这些散点连接成一个连续的曲面：
```python
# 1. 生成非规则数据点
n_points = 1000
x = np.random.uniform(-5, 5, n_points)
y = np.random.uniform(-5, 5, n_points)
z = np.sin(np.sqrt(x**2 + y**2)) + np.random.normal(0, 0.1, n_points)
# 2. 绘制曲面
ax.plot_trisurf(x, y, z, cmap='viridis', edgecolor='none')
ax.set_xlabel('X'); ax.set_ylabel('Y'); ax.set_zlabel('Z')
plt.show()
```

核心参数

| 参数          | 说明                 | 常用值/示例                                             |
| ----------- | ------------------ | -------------------------------------------------- |
| `x, y, z`   | **必填**，一维数组，散点坐标   | 长度相等的三个数组                                          |
| `triangles` | 自定义三角剖分（通常省略，自动计算） | `triangles` (三角索引数组)                               |
| `cmap`      | 颜色映射方案             | `'viridis'`, `'plasma'`, `'coolwarm'`, `'rainbow'` |
| `shade`     | 光照阴影               | `shade=True`                                       |
| `edgecolor` | 三角形边缘颜色            | `'none'` (不描边)                                     |
