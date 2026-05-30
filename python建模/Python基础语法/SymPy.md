
SymPy库用于符号运算

# 定义变量：
用sp.symbols()或者sp.var()或者sp.Function都可以
```python
x,y,z = sp.symbols('x,y,z') #定义符号运算
f,g=sp.symbols('f,g',cls=sp.Function) #创建一个未定义的函数
g=sp.Function('y')#创建一个未定义的函数

sp.var('x,y,z')
sp.var('f,g',cls = sp.Function)

#创建多个变量
x0, x1, x2, x3, x4, x5, x6, x7, x8, x9 = symbols('x:10')
# 或者更简单地
vars = symbols('v:5') # 创建 5 个变量 v0, v1, v2, v3, v4
```

SymPy有数组Matrix，

`sp.Matrix([[0,1],[1,1]])`

将Function数据类型转回能画图的匿名函数

`sp.lambdify(args, expr, modules='numpy')`

|           |                                                                                                                                                                                                               |
| --------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `args`    | 符号变量或变量的列表/元组，决定生成函数的参数顺序。例如 `[x, y]` 对应 `f(x, y)`。                                                                                                                                                           |
| `expr`    | 需要转换的 SymPy 表达式（可以是单个表达式，也可以是列表/元组/字典，表示多个输出）。                                                                                                                                                                |
| `modules` | **关键参数**：指定在生成的函数内部使用哪些数学函数库。常见选项：  <br>- `'numpy'`：使用 `numpy.sin`, `numpy.exp` 等，支持数组运算。  <br>- `'math'`：使用标准库 `math`，仅支持标量（单个数值）。  <br>- `'mpmath'`：使用高精度浮点运算。  <br>- 也可以传入自定义字典，例如 `{'sin': my_sin_func}`。 |
## 解简单的线性方程，非线性方程，代数方程

用solve(f, symbols)
f是符号方程式或者方程组，symbols是变量

例：解$ax^2 +bx +c = 0$

```python
a,b,c,x = sp.symbols('a,b,c,x')
x0 = sp.solve(a*x**2 + b*x + c = 0)
```

## 解特征值，特征向量，对角化


求$a^k$, 可以打包出一个函数：
```python
	a = sp.Matrix([[0,1],[1,1]])
	var = a.eigenvals()
	vec = a.eigenvectors()
	P,D = a.diagonalize() #把A对角化
	ak = P @ (D ** k) (P.inv())
```

## 解线性通项公式(差分方程)

利用`sympy.rsolve()`
```python
sp.rsolve(递推关系, 目标函数, 初始条件)
```
递推关系：
$ak​(n)y(n+k)+ak−1​(n)y(n+k−1)+...+a0​(n)y(n)=f(n)$
目标函数：一个未定义的函数
初始条件：即f(0) = 0, f(1) = 1之类的
写为{f(0): 0, f(1): 1}这样的字典形状

