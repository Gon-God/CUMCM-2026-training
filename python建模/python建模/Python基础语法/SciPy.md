# 功能模块表
| 模块名                     | 功能描述                                                                 |     |
| ----------------------- | -------------------------------------------------------------------- | --- |
| **`scipy.cluster`**     | 提供聚类算法                                                               |     |
| **`scipy.constants`**   | 包含大量物理和数学常数，如光速、普朗克常数等                                               |     |
| **`scipy.fft`**         | 用于执行快速傅里叶变换 (FFT) 及其逆变换                                              |     |
| **`scipy.integrate`**   | 提供数值积分（如 `quad` 函数）和常微分方程（ODE）求解器（如 `odeint` 函数）                     |     |
| **`scipy.interpolate`** | 用于**插值**和平滑样条，支持一维和多维插值，如线性、样条和径向基函数插值                               |     |
| **`scipy.io`**          | 用于**数据的输入和输出**，支持多种文件格式，如MATLAB (`.mat`)、`.wav`、`.arff`              |     |
| **`scipy.linalg`**      | 扩展 `numpy.linalg` 的**线性代数**模块，提供矩阵分解（如LU、SVD）、特征值求解等功能               |     |
| **`scipy.ndimage`**     | 提供**N维图像处理功能**，包括滤波、几何变换、形态学操作等。                                     |     |
| **`scipy.odr`**         | **正交距离回归**（Orthogonal Distance Regression），用于在自变量和因变量都存在误差的情况下进行回归分析 |     |
| **`scipy.optimize`**    | 包含多种**优化**算法，用于函数最小化（标量和多元）、曲线拟合、求根和线性规划等                            |     |
| **`scipy.signal`**      | 提供全面的**信号处理**工具，如滤波、卷积、频谱分析和波形生成等                                    |     |
| **`scipy.sparse`**      | 专用于处理大型稀疏矩阵（大部分元素为零的矩阵），提供多种存储格式和线性代数运算                              |     |
| **`scipy.spatial`**     | 提供**空间数据结构和算法**，如 `Delaunay` 三角剖分、`KDTrees` 最近邻搜索和 `ConvexHull` 计算等  |     |
| **`scipy.special`**     | 收录了大量特殊数学函数，如贝塞尔、伽马、椭圆函数等                                            |     |
| **`scipy.stats`**       | 提供广泛的统计函数和概率分布（包括连续和离散），用于描述性统计、假设检验和回归分析                            |     |

## 求解非线性方程

利用scipy.optimize.fsolve 和 scipy.optimize.root

**给定一个函数 `func(x)`，`fsolve` 会尝试找到一个 `x` 使得 `func(x) = 0`**。如果方程组有多个变量，`x` 就是一个数组

语法
```python
def equation(x):
    return x**2 - 4
root = scipy.optimize.fsolve(equation, x0=1.5)  # 第一个参数是方程函数，x0 是初始猜测
print(root)  # 输出 [2.]

root1 = scipy.optimize.root(equation, x0=1.5)
print(root1)

```

## 积分


利用scipy.inergrate模块
```python
scipy.inergrate.quad(func,a,b,args)
```

func是函数方程，a是下限，b是上限，args是提供不需要的变量，防止误认，是一个元组

```python
def integrand(x,a,b)
	return a*x**2+b*x
	
result = integrand(integrand, 1, 2, args = (a，b))#保留a,b，只对x积分
result = integrand(integrand, 1, 2, args = (1，2))#把a=1,b=2传入函数，对x积分
```

此外，对于多重积分，我们有
```python
dblquad(func,a,b,gfun,hfun,args) #二重数值积分
tplquad(func,a,b,gfun,hfun,qfun,rfun) #计算三重数值积分
nquad(func,ranges,args) #计算多变量积分，n重积分
```

nquad()函数，我们阅读先对第一个变量积分，然后第二个...


$$∫01​(∫01(x2+y2)dy)dx$$
```python
def integrand(y, x):
    return x**2 + y**2
# ranges 列表依次为 (y的边界), (x的边界)
result, err = nquad(integrand, [(0, 1), (0, 1)])
print(result)  # 输出应为 2/3 ≈ 0.666666666666...
```

对于依赖边界的二重积分

```python
def integrand(y, x):
    return x**2 + y**2
# 第二个变量 x 的边界 (0,1)
# 第一个变量 y 的边界为 (0, x)，其中 x 是外层变量（第二个参数）
def y_bounds(x):
    return (0, x)
result, err = nquad(integrand, [y_bounds, (0, 1)])
print(result)  # 应该等于 7/15 ≈ 0.46666...
```

## 最小二乘解

利用函数scipy.optimize.least_squares

`least_squares` 的核心是找到一组参数 **x**，使得系统输出的**残差** **f(x)** 的加权平方和最小

语法：
```python
least_squares(fun,x0)
```
fun是函数，x0是x的初始值


## 最大模特征值与特征向量

1. 利用 `numpy.linalg.eig`
语法：
```python
numpy.linalg.eig(a)
```
  
  **参数**

- `a` : 形状为 `(M, M)` 的方阵（稠密数组或类似数组对象）。
    

**返回值**

- `w` : 一维数组，长度为 `M`，特征值（可能为复数）。
    
- `v` : 形状为 `(M, M)` 的矩阵，**列** `v[:, i]` 是对应特征值 `w[i]` 的特征向量。
  
```python
A = np.array([[1, 2], [3, 4]])

# 1. 计算所有特征值和特征向量
eigenvalues, eigenvectors = np.linalg.eig(A)

print(f"最大模特征值: {eigenvalues}")
print(f"对应的特征向量: {eigenvectors}")
```
2. 使用 `scipy.sparse.linalg.eigs`
语法：
```python
scipy.sparse.linalg.eigs(A, k=6,which='LM'')
```
A是矩阵，k是求几个，which有一下参数：
`'LM'`（最大模），`'SM'`（最小模），`'LR'`（最大实部），`'SR'`（最小实部），`'LI'`（最大虚部），`'SI'`（最小虚部）

**一般求最大模就是用'LM'**

```python
from scipy.sparse.linalg import eigs
import numpy as np

A = np.array([[1, 2], [3, 4]])

# k=1 表示只计算 1 个特征值/特征向量
# which='LM' 表示选择模（Magnitude）最大的那个[reference:6]
eigenvalues, eigenvectors = eigs(A, k=1, which='LM')
```







