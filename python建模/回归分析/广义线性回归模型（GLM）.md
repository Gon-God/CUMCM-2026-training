
![[Pasted image 20260615164603.png]]

![[Pasted image 20260615164711.png]]

# Logistic回归模型
对于**0-1因变量**产生的问题，我们对回归模型作改进

1. 回归函数应该限制在[0,1]内，Logistic函数的形式为：
 $$f(x)=\frac{e^x}{1+e^x}=\frac{1}{1+e^{-x}}$$
 2. 将0，1这些离散值改为yi等于1的概率是多少


![[Pasted image 20260616163719.png]]

![[Pasted image 20260616163729.png]]
![[Pasted image 20260616163737.png]]![[Pasted image 20260616163749.png]]


```python
import numpy as np
import statsmodels.api as sm

a = np.lo

```