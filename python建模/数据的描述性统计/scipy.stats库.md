
# 连续性概率分布

对于连续性随机变量，都有以下函数

| 方法   | 作用             |
| :--- | -------------- |
| rvs  | 产生随机数          |
| pdf  | 概率密度函数         |
| cdf  | 分布函数           |
| sf   | 生存函数           |
| ppf  | 反函数            |
| stat | 期望与方差          |
| fit  | 极大似然估计法，估计未知参数 |

常用分布函数

| 名称         | 关键字         | 调用方式                                      |
| :--------- | ----------- | ----------------------------------------- |
| 均匀分布       | uniform.pdf | uniform.pdf(x,a,b),[a,b]区间的均匀分布           |
| 指数分布       | expon.pdf   | expon.pdf(x,sacle=theta),期望为theta的指数分布    |
| 正态分布       | norm.pdf    | norm.pdf(x,mu,sigma),均值为mu,标准差为sigma的正态分布 |
| 卡方分布       | chi2.pdf    | chi2.pdf(x,n),自由度为n                       |
| t分布        | t.pdf       | t.pdf(x,n),自由度为n                          |
| F分布        | f.pdf       | f.pdf(x,m,n)，自由度为m,n的F分布                  |
| $\Gamma$分布 | gamma.pdf   | gamma.pdf(x,a=A,scale=B)                  |
|            |             |                                           |


正态分布的函数

| 函数     | 调用方式                                                         |
| ------ | ------------------------------------------------------------ |
| 概率密度   | norm.pdf(x, mu, sigma)：均值 mu，标准差 sigma 的正态分布概率密度函数           |
| 分布函数   | norm.cdf(x, mu, sigma)：均值 mu，标准差 sigma 的正态分布的分布函数            |
| 分位数    | norm.ppf(alpha, mu, sigma)：均值 mu，标准差 sigma 的正态分布 alpha 分位数   |
| 随机数    | norm.rvs(mu, sigma, size=N)：产生均值为 mu，标准差 sigma 的 N 个正态分布的随机数 |
| 最大似然估计 | norm.fit(a)：假设数组 a 来自正态分布，返回 mu 和 sigma 的最大似然估计              |

---

# 离散型随机变量

| 分布名称 | 关键字         | 调用方式                             |
| ---- | ----------- | -------------------------------- |
| 二项分布 | binom.pmf   | binom.pmf(x, n, p) 计算 x 处的概率     |
| 几何分布 | geom.pmf    | geom.pmf(x, p) 计算第 x 次首次成功的概率    |
| 泊松分布 | poisson.pmf | poisson.pmf(x, lambda) 计算 x 处的概率 |
|      |             |                                  |

---

# 可视化

```python
from scipy.stats import expon,gamma
import pylab as plt

x = plt.linspace(0,3,20)

plt.plot(x,expon.pdf(x,scale=1),'*-',label = 'e(1)')
plt.plot(x,expon.pdf(x,scale=1/3),'*-', label = 'e(1/3)')
plt.plot(x,gamma.pdf(x, 2, 2),'*-',label = 'gamma')

plt.legend()
plt.show()
```

![[Pasted image 20260614150023.png]]


