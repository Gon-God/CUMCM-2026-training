# 引用 
```python
import pandas as pd
```
#### Pandas提供了3种数据结构
1. Series:带标签的一维数组
2. DataFrame:带标签且大小可变的**二维表格**结构
3. Panel:带标签且大小可变的三维数组

主要用的是DataFrame

# 生成二维数组
语法：
```python
df = pd.DataFrame(data, index, columns, dtype, copy)
```
主要是data要输入进去
index行标签
column列标签

### 1. 从字典创建（键为列名，值为列数据）
```python
data = {'姓名': ['张三', '李四'], '年龄': [25, 30]}
df = pd.DataFrame(data)
```
### 2. 从列表创建（每个内列表为一行）
```python
data = [['张三', 25], ['李四', 30]]
df = pd.DataFrame(data, columns=['姓名', '年龄'])
```
### 3. 从 NumPy 数组创建
```python
arr = np.array([[1, 2], [3, 4]])
df = pd.DataFrame(arr, index=['行1', '行2'], columns=['列A', '列B'])
```
### 4. 也可以直接构建
```python
df = pd.DataFrame(np.random.randn(5), columns = [1,2,3,4,5])
```

# 数据文件写入读取 读写
把DataFrames从Excel和CSV文件读出和写入Excel和CSV文件
#### 写入
利用.to_csv()和.to_excel()
语法：
```python
df.to_csv(path_or_buf, sep=',', encoding=None, index=True, ...)
```

- `path_or_buf`：保存路径
- `sep`：分隔符，默认逗号
- `encoding`：编码，如 `'utf-8'`、`'utf-8-sig'`
- `index`：是否写入行索引，默认 `True`

```python
df = pd.DataFrame({
    '姓名': ['张三', '李四', '王五'],
    '年龄': [25, 30, 28],
    '城市': ['北京', '上海', '广州']
})

# 写入 CSV 文件（相当于“创建”文件）
df.to_csv('人员信息.csv', index=False, encoding='utf-8-sig')

# 写入 Excel 文件
df.to_excel('人员信息.xlsx', index=False)
```

#### 读取
语法：
```python
pd.read_csv(filepath_or_buffer, sep=',', encoding=None)
```

- `filepath_or_buffer`：文件路径
- `sep`：分隔符，默认逗号
- `encoding`：编码，如 `'utf-8'`、`'utf-8-sig'`

```python
# 读取 CSV
df_csv = pd.read_csv('人员信息.csv', encoding='utf-8-sig')

# 读取 Excel（需要安装 openpyxl 或 xlrd）
df_excel = pd.read_excel('人员信息.xlsx')
```

# 数据预处理
