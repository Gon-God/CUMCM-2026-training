# 导入
```python
import numpy as np
```

---
# 数组创建

### array()函数：创建自定义数组
把各种对象转化为ndarry多维数组
一般是把列表传入，转化为数组
```python
语法：
numpy.array(object)

#example
arr1 = np.array([1, 2, 3, 4])
print(arr1)  # 输出：[1 2 3 4]

arr3 = np.array([[[1, 2, 3], [4, 5, 6]], [[7, 8, 9], [10, 11, 12]]])
print(arr3)
# 输出：
# [[[ 1  2  3]
#   [ 4  5  6]]
# 
#  [[ 7  8  9]
#   [10 11 12]]]
```


### arange()函数：创建等差数列

```python
arange(start, stop, step, dtpye)
```
start默认为0
stop必须填，如果只填一个，默认为stop
step默认为1
dtpye自动推断

```python
# 1. 一个参数：只有 stop，start=0, step=1
print(np.arange(5))      # 输出：[0 1 2 3 4]
# 2. 两个参数：start, stop
print(np.arange(2, 7))   # 输出：[2 3 4 5 6]
# 3. 三个参数：start, stop, step
print(np.arange(1, 10, 2))   # 输出：[1 3 5 7 9]
# 4. 浮点数步长
print(np.arange(0, 1, 0.2))  # 输出：[0.  0.2 0.4 0.6 0.8]
# 5. 负步长（递减序列）
print(np.arange(10, 4, -1))  # 输出：[10  9  8  7  6  5]

np.arange(6).reshape(2,3) #指定形状
```


### linspace()函数：给定范围，创建等距数组

```python
numpy.linspace(start, stop, num=50, endpoint=True)
```
endpoint:默认为True
True：列表包含stop值
False:不包含stop值

```python
#从 0 到 1，生成 5 个点
print(np.linspace(0, 1, 5))
# 输出：[0.   0.25 0.5  0.75 1.  ]

同时返回步长
arr, step = np.linspace(0, 1, 5, retstep=True)
print(arr)   # [0.   0.25 0.5  0.75 1.  ]
print(step) # 0.25
```

### logsapce()函数：生成等比数组
```python
 numpy.logspace(start, stop, num=50, endpoint=True)
```

stop是次数，如果为3，就是3次方

```python
a = np.logspace(0, 3, 4)
print(a)  # 输出: [   1.   10.  100. 1000.]
```

#### 随机数数组：numpy.random.randn()
```python
# 生成一维数组（5个元素）
arr1d = np.random.randn(5)
print(arr1d)    # [-0.982  0.341  1.232 -0.511  0.721]
# 生成 2x3 的二维数组
arr2d = np.random.randn(2, 3)
print(arr2d)
# [[ 0.124 -0.853  0.547]
#  [ 0.984 -1.234  0.231]]
```
### 其他指定生成函数

#### ones():值全为1
```python
a = np.ones((数组大小形状))

a = np.ones(4) #-->[1,1,1,1]
a = np.ones((4,2)) #-->[[1,1,1,1][1,1,1,1]]
```
#### zeros(): 用法同ones()
#### empty():同ones()
#### eye():生成单位矩阵，对角矩阵
```python
a = np.eye(3) #生成3阶单位矩阵
a = np.eye(3, 2)#3阶，对角线元素为2
```
#### zeros_like():生成与某个矩阵同维度的全0数组

---
# 数组元素索引
语法：
```python
列表名[start, end, step]

#example
a = np.arrange(16).reshape(4,4)
b = a[1, 2]#第二行第三列，为7
c = arr2d[:2, 1:3] # 前2行，第1~2列,为一个数组
c = arr2d[:1, :1] #返回[[1]]
```

### 布尔索引

```python
arr = np.array([1, 2, 3, 4, 5])
mask = arr > 3
print(mask)            # [False False False  True  True]
print(arr[mask])
```

---
# 矩阵的合并

**vstack([A, B])函数：上下合并**
**hstack([A, B])函数：左右合并**

```python
a = np.array([[1, 2], [3, 4]])   # 形状 (2,2)
b = np.array([[5, 6], [7, 8]])   # 形状 (2,2)
c = np.vstack((a, b))
print(c)
# 输出：
# [[1 2]
#  [3 4]
#  [5 6]
#  [7 8]]

a = np.array([[1, 2], [3, 4]])   # 形状 (2,2)
b = np.array([[5, 6], [7, 8]])   # 形状 (2,2)
c = np.hstack((a, b))
print(c)
# 输出：
# [[1 2 5 6]
#  [3 4 7 8]]
```

---

# 矩阵的分割

**vsplit(a.m)** 把a平均分为m个**行**数组
**hsplit(a.m)** 把a平均分为m个**列**数组

```python
arr = np.arange(12).reshape(6, 2)  # 6行2列
print(arr)
# [[ 0  1]
#  [ 2  3]
#  [ 4  5]
#  [ 6  7]
#  [ 8  9]
#  [10 11]]
# 分割成 3 个等高的子数组（每个包含 2 行）
result = np.vsplit(arr, 3)
print(result[0])  # [[0 1], [2 3]]
print(result[1])  # [[4 5], [6 7]]
print(result[2])  # [[8 9], [10 11]]


arr = np.arange(12).reshape(3, 4)  # 3行4列
print(arr)
# [[ 0  1  2  3]
#  [ 4  5  6  7]
#  [ 8  9 10 11]]
# 水平分割成 2 个等宽的子数组（每个 2 列）
result = np.hsplit(arr, 2)
print(result[0])  # [[0 1], [4 5], [8 9]]
print(result[1])  # [[2 3], [6 7], [10 11]]
# 按列位置分割：在列索引 1 和 3 处切分
result2 = np.hsplit(arr, [1, 3])
# 产生: 第0列, 第1-2列, 第3列
print(result2[0].shape)  # (3,1)
print(result2[1].shape)  # (3,2)
print(result2[2].shape)  # (3,1)
```

---

# 矩阵运算

### 求和

全部求和
```python
np.sum(matrix)
matrix.sum()

matrix = np.array([[1, 2, 3],
                   [4, 5, 6]])
total = np.sum(matrix)   # 或者 matrix.sum()
print(total)  # 输出: 21 (1+2+3+4+5+6)
```

按行求和
```python
matrix = np.array([[1, 2, 3],
                   [4, 5, 6]])
                   
row_sums = np.sum(matrix, axis=1)
print(row_sums)  # 输出: [ 6 15]
```
按列求和
```python
matrix = np.array([[1, 2, 3],
                   [4, 5, 6]])
                   
                
col_sums = np.sum(matrix, axis=0)
print(col_sums)  # 输出: [5 7 9]
```

### 逐个元素运算

各个元素
加减乘除就可以

### 矩阵乘法
符号为@
```python
a = b @ c
```

### 逐元素四舍五入
```python
np.round(a, decimals=0)#decimals，保留的小数位数
```

---

# 矩阵运算与线性代数

全都是利用numpy,linalg模块

### norm()求范数
语法：
```python
np.linalg.norm(x, ord=None, axis=None, keepdims=None)
```
x是矩阵，
ord=n 第n范数,默认为2，
axis按行按列, 没有就是求整个矩阵的
keepdims是否保持二维特性

```python
a = np.array([0,3,4],[1,6,4])
b = np.linalg.norm(a, axis=1) #求行向量2范数
c = np.linalg.norm(a, axis=0) #求列向量2范数
b = np.linalg.norm(a) #求矩阵2范数

print(np.round(b, 4))#输出结果保留四位小数
```

### 求线性方程组的唯一解

方程Ax=b
利用函数np.linalg.solve(A, b)
```python
A = np.array([[3, 1], 
              [1, 2]])
b = np.array([9, 8])
# 求解
x = np.linalg.solve(A, b)
print(x)   # 输出: [2. 3.]  即 x=2, y=3
```

### 求线性方程组的最小二乘解

方程Ax=b
利用函数np.linalg.lstsq(A, b)
输出的是四个值
```python
A = np.array([[1, 2],
              [3, 4],
              [5, 6]])
b = np.array([3, 7, 11])
# 求解最小二乘解
x, residuals, rank, s = np.linalg.lstsq(A, b, rcond=None)
print(x)          # 最小二乘解
print(residuals)  # 残差平方和（仅当 m>n 且满秩时有效）
print(rank)       # 矩阵 A 的秩
print(s)          # 奇异值数组
```

### 求矩阵逆
利用函数np.linalg.inv()
```python
# 定义一个方阵
A = np.array([[1, 2],
              [3, 4]])
# 求逆矩阵
A_inv = np.linalg.inv(A)
print(A_inv)
# 输出：
# [[-2.   1. ]
#  [ 1.5 -0.5]]
```

### 求矩阵广义逆
利用函数np.linalg.pinv()

### 求行列式
利用函数np.linalg.det()

### 求特征值
注意输入的必须为方阵
利用np.linalg.eig()
```python
eigenvalues, eigenvectors = np.linalg.eig(A)
```


### 求奇异值分解
```python
# 创建一个任意矩阵 (m x n)
A = np.array([[1, 2, 3],
              [4, 5, 6]])
U, s, Vh = np.linalg.svd(A, full_matrices=True)
print("U 的形状:", U.shape)   # (m, m) 或 (m, k)
print("奇异值 s:", s)         # 长度为 min(m, n) 的一维数组
print("Vh 的形状:", Vh.shape) # (n, n) 或 (k, n)
```

### 求QR分解
```python
A = np.array([[1, 2], [3, 4], [5, 6]])   # 形状 (m, n)
Q, R = np.linalg.qr(A, mode='reduced')
print(Q.shape)   # (m, n) 或 (m, m) 取决于 mode
print(R.shape)   # (n, n) 或 (m, n)
```

