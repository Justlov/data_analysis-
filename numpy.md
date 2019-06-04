

# numpy

## 创建数组

创建数组最简单的方法就是使用array函数。它接收一切序列型的对象（包括其他数组），然后产生一个新的含有传入数据的Numpy数组。

### 1. array函数创建数组

* ```python
  ndarray1 = np.array([1, 2, 3, 4])
  ndarray2 = np.array(list('abcdefg'))
  ndarray3 = np.array([[11, 22, 33, 44], [10, 20, 30, 40]])
  ```

### 2. zeros和zeros_like创建数组

* ```
  ndarray4 = np.zeros(10)
  ndarray5 = np.zeros((3, 3))
  ndarray6 = np.zeros_like(ndarray5) 
  ```

### 3. ones和ones_like创建数组

* ```
  # 创建数组，元素默认值是1
  ndarray7 = np.ones(10)
  ndarray8 = np.ones((3, 3))
  # 修改元素的值
  ndarray8[0][1] = 999
  ndarray9 = np.ones_like(ndarray5)  # 按照 ndarray5 的shape创建数组
  ```

### 4. empty和empty_like创建数组

用于创建空数组，空数据中的值并不为0,而是未初始化的随机值

* ```python
  ndarray10 = np.empty(5)
  ndarray11 = np.empty((2, 3))
  ndarray12 = np.empty_like(ndarray11)
  ```

### 5. arange创建数组

arange函数是python内置函数range函数的数组版本

* 

```python
# 产生0-9共10个元素
ndarray13 = np.arange(10)
# 产生从10-19共10个元素
ndarray14 = np.arange(10, 20)
# 产生10 12 14 16 18, 2为step
ndarray15 = np.arange(10, 20, 2)
# ndarray15的形状
print('ndarray14的形状:', ndarray14.shape)
# 将其形状改变为(2, 5)
ndarray14.reshape((2, 5))
```

### 6. eys创建对角矩阵数组

该函数用于创建一个N*N的矩阵，对角线为1，其余为0.

* ```python
  ndarray16 = np.eye(5)
  ```

## 数据类型

我们可以通过ndarray的dtype来打印数组中元素的类型. ndarray常见的数据类型如下:

| 类型          | 类型代码 | 说明                                        |
| ------------- | -------- | ------------------------------------------- |
| int8、uint8   | i1、u1   | 有符号和无符号的8位(1个字节长度)整型        |
| int16、uint16 | i2、u2   | 有符号和无符号的16位(2个字节长度)整型       |
| int32、uint32 | i4、u4   | 有符号和无符号的32位(4个字节长度)整型       |
| float16       | f2       | 半精度浮点数                                |
| float32       | f4或f    | 标准单精度浮点数                            |
| float64       | f8或d    | 双精度浮点数                                |
| bool          | ?        | 布尔类型                                    |
| object        | O        | Python对象类型                              |
| unicode_      | U        | 固定长度的unicode类型，跟字符串定义方式一样 |

* ```python
  import numpy as np
  
  ndarray1 = np.array([1, 2, 3, 4])
  ndarray1.dtype
  ndarray2 = np.array(list('abcdefg'))
  ndarray2.dtype
  ndarray3 = np.array([True, False, False, True])
  ndarray3.dtype
  class Person(object):
      pass
  ndarray4 = np.array([Person(), Person(), Person()])
  ndarray4.dtype
  ```

### 使用astype函数转换数组类型

* ```python
  ndarray5 = np.array([1, 2, 3, 4, 5])
  # 类型转换完毕返回新的数组
  ndarray6 = ndarray5.astype(np.float32)
  
  # 如果浮点数转换为整数，则小数部分将会被截断
  ndarray7 = np.array([1.1, 2.2, 3.3, 4.4])
  ndarray8 = ndarray7.astype(np.int32)
  
  # 如果某些字符串数组表示的全是数字，也可以用astype将其转换为数值类型
  ndarray9 = np.array(['10', '20', '30', '40'])
  ndarray10 = ndarray9.astype(np.int32)
  ```

## 数组运算

不需要循环即可对数据进行批量运算，叫做矢量化运算. 不同形状的数组之间的算数运算，叫做广播.

* ```python
  import numpy as np
  
  ndarray1 = np.array([1, 2, 3, 4, 5])
  ndarray2 = np.array([3, 4, 5, 6, 7])
  
  # 数组和数组之间的运算
  ndarray3 = ndarray1 * ndarray2
  ndarray4 = ndarray1 + ndarray2
  
  # 数组和数字值之间的运算
  ndarray5 = ndarray1 + 100
  ndarray6 = 5 / ndarray1
  
  # 多维数组和多维数组之间的运算
  ndarray7 = np.arange(9).reshape((3, 3))
  ndarray8 = np.arange(9).reshape((3, 3))
  ndarray9 = ndarray7 + ndarray8 
  
  # 一维数组和多维数组之间运算
  ndarray10 = np.arange(3)
  ndarray11 = np.arange(6).reshape((2, 3))
  ndarray12 = ndarray10 + ndarray11
  ```

## 数组索引和切片

### 数组索引和切片基本用法

类似列表的索引 切片

* ```python
  import numpy as np
  
  ndarray1 = np.arange(10)
  ndarray1[1]
  ndarray1[1:2:3]
  ndarray2 = np.arange(15).reshape((3, 5))
  ndarray2[2,3]
  ```

###  数组花式索引

* ```python
  import numpy as np
  ndarray1 = np.empty((8, 4))
  for i in range(8):
      ndarray1[i] = np.arange(i, i + 4)
  
  # 选取特定的子集,参数为列表
  ret1 = ndarray1[[0, 1, 6, 7]]
  
  # 使用负数索引会从末尾开始选取行
  ret2 = ndarray1[[-1, 0, -2]]
  
  # 一次传入多个数组
  ret3 = ndarray1[[1, 3, 5], [1, 2, 3]]
  ret4 = ndarray1[[1, 3, 5]][[1, 2]]
  
  # 获取选区数据
  ret5 = ndarray1[[1, 3, 5]][:, [1, 2, 3]]
  ret6 = ndarray1[np.ix_([1, 2, 4], [1, 2, 3])]
  ```

### 布尔型索引

* ##### 1. 布尔类型基本用法：

* ```python
  import numpy as np
  
  names = np.array(['aaa', 'bbb', 'ccc', 'ddd', 'eee', 'fff', 'ggg'])
  data = np.arange(35).reshape((7, 5))
  # 数组中每一个元素都进行==运算，返回一个数组
  mask = names == 'aaa'
  
  ```

* ##### 2. 布尔类型数组跟切片、整数混合使用

* ```python
  import numpy as np
  
  names = np.array(['aaa', 'bbb', 'ccc', 'ddd', 'eee', 'fff', 'ggg'])
  data = np.arange(35).reshape((7, 5))
  
  ret1 = data[names == 'ccc']
  
  # 布尔类型数组和整数混合使用
  ret2= data[names == 'ccc', 2]
  
  # 布尔类型数组和切片混合使用
  ret3= data[names == 'ccc', 1:]
  ```

* ##### 3. 使用不等于!=，使用(~)对条件否定

* ```python
  import numpy as np
  
  names = np.array(['aaa', 'bbb', 'ccc', 'ddd', 'eee', 'fff', 'ggg'])
  data = np.arange(35).reshape((7, 5))
  
  ret1 = data[names != 'ccc']
  ret2 = data[~(names == 'ccc')]
  ret3 = data[~(names > 'ccc')]
  ```

* ##### 4. 使用&(和)、|(或)组合多个布尔条件

* 

```python
import numpy as np

names = np.array(['aaa', 'bbb', 'ccc', 'ddd', 'eee', 'fff', 'ggg'])
data = np.arange(35).reshape((7, 5))

# 注意，Python的关键字and、or在布尔数组中无效
ret1 = data[(names == 'aaa') | (names == 'ccc')]
ret2 = data[(names > 'ddd') | (names == 'aaa')]
ret3 = data[(names < 'eee') & (names > 'bbb') ]
```

* ##### 5. 使用布尔类型数组设置值是一种经常用到的手段

* ```python
  import numpy as np
  
  ndarray1 = np.arange(5)
  ndarray2 = np.arange(16).reshape((4, 4))
  names = np.array(['aaa', 'bbb', 'ccc', 'ddd'])
  
  # 将数组ndarray1中所有大于5的元素设置成666
  ndarray1[ndarray1 > 2] = 8
  
  # 将ndarray2的aaa这一行所有的元素设置为0
  ndarray2[names == 'aaa'] = 0
  # 将ndarray2的bbb这一行2位置往后所有的元素设置为1
  ndarray2[names == 'bbb', 2:] = 1
  # 将ndarray2的ccc ddd这2行所有的元素设置为2
  ndarray2[(names == 'ccc') | (names == 'ddd')] = 2
  ```

* ##### 6. np.where用法

* > 已知有两个数组: ndarray1 = np.array([6, 7, 8, 6, 8, 3, 4, 5, 8, 7]) ndarray2 = np.array([3, 5, 3, 7, 2, 1, 2, 2, 7, 4]) 以此对比数组中对应位置的值，取出大的值，组成新的数组.

  ```python
  import numpy as np
  
  # 创建两个数组
  ndarray1 = np.array([6, 7, 8, 6, 8, 3, 4, 5, 8, 7])
  ndarray2 = np.array([3, 5, 3, 7, 2, 1, 2, 2, 7, 4])
  # 比较条件
  result1 = [ n1 if c else n2 for n1, n2, c in zip(ndarray1, ndarray2, ndarray1 > ndarray2) ]
  # 这里也可以使用numpy提供的where函数
  # 使用格式为: result = np.where(条件, 值1, 值2)
  result2 = np.where(ndarray1 > ndarray2, ndarray1, ndarray2)
  ```

## 数组函数

### 通用元素级数组函数

