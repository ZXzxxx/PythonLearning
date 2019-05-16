## 1. list和array

​	python中的list是python的内置数据类型（就是基本数据类型的意思），list中的存储的数据的类型不必相同的，如 [1, 2, 3, ‘a’, 4]。array是numpy中封装好的一种数据类型，其中存储的类型必须全部相同，如 [1, 2, 3, 4]。

​	在list中的数据类型保存的是存放数据的地址，简单的说就是指针而并非数据，这样保存一个list时是很麻烦的。例如list1=[1,2,3,'a']，需要4个指针和四个数据，增加了存储和CPU的消耗。

```python
list1=[1,2,3,'a']
print(list1)

a=np.array([1,2,3,4,5])
b=np.array([[1,2,3],[4,5,6]])
c=list(a)   # array到list的转换
print a,np.shape(a)
print b,np.shape(b)
print c,np.shape(c)

### 输出
[1, 2, 3, 'a'] #元素数据类型不同，且用逗号隔开
[1 2 3 4 5] (5L,) #一维数据，类型用tuple表示
[[1 2 3]
 [4 5 6]] (2L,3L) #二维数组
[1, 2, 3, 4, 5] (5L,)
```

#### 1.1 array的创建

​	numpy中的数组就像python中的列表，但是numpy可以让事情变得更有效率，特别是对于更大的数组。和python列表不同，numpy数组只能包含一种类型的成员，创建数组的方法如下：

```python
import numpy as np
```

```python
ar = np.array([1, 2, 3])
ar
--- array([1, 2, 3]) ---
print(ar) #输出的是数组，不是列表，没有逗号哦！！ 此处是3行一列的一维数组
--- [1 2 3] ---
```

​	如果初始化列表中有不同类型的数据，Numpy会尝试把它们全部转化为最通用的类型。例如，整数int将转化为float类型。（小的转大的）

```python
np.array([3.1, 4, 5, 6])
--- array([3.1, 4. , 5. , 6. ]) ---
```

​	也可以手动设置类型

```python
np.array([1, 2, 3], dtype = 'float32')
--- array([1., 2., 3.], dtype=float32) ---
```

​	用 array（） 函数创建数组时，里面可以列表、元组或者它们的组合，最后都会变成数组。

```python
arr1 = np.array(range(5)) #整型
arr2 = np.array([1.2,3.4,5.6]) #浮点
arr3 = np.array([[1,2,3],('a','b','c')]) #既有列表又有元组，且元素个数相同，最终都变成数组
arr4 = np.array([[1,2,3],('a','b','c','d')]) #列表和元组内元素个数不同，相当于数组里有两个元素，列表和元组，数据类型都是object
print(arr1, type(arr1), arr1.dtype)
print(arr2, type(arr2), arr2.dtype)
print(arr3, arr3.shape, arr3.ndim, arr3.size, arr3.dtype)# 数组、结构、维度、大小、类型
print(arr4, arr4.shape, arr4.ndim, arr4.size, arr4.dtype)
```

```
[0 1 2 3 4] <class 'numpy.ndarray'> int32
[1.2 3.4 5.6] <class 'numpy.ndarray'> float64
[['1' '2' '3']
 ['a' 'b' 'c']] (2, 3) 2 6 <U11
[list([1, 2, 3]) ('a', 'b', 'c', 'd')] (2,) 1 2 object
```

​	数组的转置

```python
yw = np.array([1,2,3]) #一维数组转置是不变的
print(yw, yw.shape, yw.ndim)
ywT = yw.T
print(ywT, ywT.shape, ywT.ndim)
ew = np.array([[1,2],[3,4],[5,6]])
print(ew, ew.shape, ew.ndim)
ewT = ew.T
print(ewT, ewT.shape, ewT.ndim)
```

```
[1 2 3] (3,) 1
[1 2 3] (3,) 1
[[1 2]
 [3 4]
 [5 6]] (3, 2) 2
[[1 3 5]
 [2 4 6]] (2, 3) 2
```

​	可以连接两个或多个数组

```python
a = np.array([1, 2, 3])
b = np.array([3, 2, 1])
c = np.array([7, 8, 9])
np.concatenate([a, b, c])
```

```
array([1, 2, 3, 3, 2, 1, 7, 8, 9])
```

#### 1.2 创建特殊数据

​	numpy有几个函数，可以直接创建数组，对于大型数组的创建时很有效的.

```python
np.empty(5)
```

```
array([0.2, 0.4, 0.6, 0.8, 1. ])
```



```python
np.zeros(10, dtype = int)
```

```
array([0, 0, 0, 0, 0, 0, 0, 0, 0, 0])
```



```python
np.ones((3, 5), dtype = float)
```

```
array([[1., 1., 1., 1., 1.],
       [1., 1., 1., 1., 1.],
       [1., 1., 1., 1., 1.]])
```



```python
np.full((3, 5), 3.14)
```

```
array([[3.14, 3.14, 3.14, 3.14, 3.14],
       [3.14, 3.14, 3.14, 3.14, 3.14],
       [3.14, 3.14, 3.14, 3.14, 3.14]])
```



```python
np.arange(0, 20, 2) #[0,20) 间隔是2
```

```
array([ 0,  2,  4,  6,  8, 10, 12, 14, 16, 18])
```



```python
np.linspace(0, 1, 5) #[0,1] 5个数
```

```
array([0.  , 0.25, 0.5 , 0.75, 1.  ])
```



```python
np.linspace(0, 1, 7)
```

```
array([0.        , 0.16666667, 0.33333333, 0.5       , 0.66666667,
       0.83333333, 1.        ])
```



```python
np.eye(3) # 单位数组
```

```
array([[1., 0., 0.],
       [0., 1., 0.],
       [0., 0., 1.]])
```



```python
np.eye(4)
```

```
array([[1., 0., 0., 0.],
       [0., 1., 0., 0.],
       [0., 0., 1., 0.],
       [0., 0., 0., 1.]])
```

#### 1.3 array数组属性

​	每个numpy创建的数组都有一些比较通用的属性。

​	numpy.random.randint(low,high=None,size=None,dtype) . 
​	生成在半开半闭区间[low,high)上离散均匀分布的整数值;若high=None，则取值区间变为[0,low) 

```python
np.random.seed(0) #如果不设置seed的值，每次就会生成不同的随机数，设置了之后就是生成相同的随机数了，而且这个值是起始值
x1 = np.random.randint(10, size = 6)
print("数组x1：",x1)
print("数组x1的维度：",x1.ndim)
print("数组x1的结构（就是几行几列）：", x1.shape)
print("数组x1的元素个数：", x1.size)
print("数组的元素类型：", x1.dtype)
```

```
数组x1： [5 0 3 3 7 9]
数组x1的维度： 1
数组x1的结构（就是几行几列）： (6,)
数组x1的元素个数： 6
数组的元素类型： int32
```

##### 1.3.1 一维访问

​	访问数组的一个或者多个元素

```python
print(x1[0])
--- 5 ---
```

```python
print(x1[-1]) #-1指的最后一个元素
--- 9 ---
```

```python
print(x1[-2]) #-2指的倒数第二个元素，以此类推，就x1来说，-7开始就不行了，就越界了
--- 7 ---
```

```python
x1[1] = 3.14 #都变成int32类型
print(x1)
```

```
[5 3 3 3 7 9]
```

```python
print(x1[0:5]) # 逗号前是行索引，没有逗号说明包括所有的列。冒号是第几行(列)到第几行(列) [前闭后开]
```

```
[5 3 3 3 7]
```

```python
print(x1[:5])
```

```
[5 3 3 3 7]
```

```python
print(x1[5:])
```

```
[9]
```

```python
print(x1[::2]) #每两个输出一次
```

```
[5 3 7]
```

##### 1.3.2 二维访问

​	二维数组的元素访问。

```python
x2 = np.random.randint(10, size=(3, 4))
print(x2)
```

```
[[3 5 2 4]
 [7 6 8 8]
 [1 6 7 7]]
```

```python
print(x2[0:])
```

```
[[3 5 2 4]
 [7 6 8 8]
 [1 6 7 7]]
```

```python
print(x2[0,1]) # 逗号前是行索引，逗号后是列索引
--- 5 ---
```

```python
print(x2[0:1])
```

```python
print(x2[:,1]) #取第一列
```

```
[5 6 6]
```

```python
print(x2[0:2,2]) #第0行和第1行的第2列
```

```
[2 8]
```

​	**实例：**

```python
def reverse_calculation(values):
    output = np.empty(len(values))
    for i in range(len(values)):
        output[i] = 1.0/values[i]
    return output

values = np.random.randint(1, 10, size = 5)
print(reverse_calculation(values))
```

```
[0.11111111 0.5        0.16666667 0.11111111 0.2       ]
```

#### 1.4 array相关运算

##### 1.4.1 一维

```python
x = np.arange(4)
print("x = ", x)
```

```
x =  [0 1 2 3]
```

```python
print("x + 5 = ", x + 5)
```

```
x + 5 =  [5 6 7 8]
```

```python
print("x - 5 = ", x - 5)
```

```
x - 5 =  [-5 -4 -3 -2]
```

```python
print("x * 2 = ", x * 2)
```

```
x * 2 =  [0 2 4 6]
```

```python
print("x / 2 = ", x / 2)
```

```
x / 2 =  [0.  0.5 1.  1.5]
```

```python
print("x // 2 = ", x // 2)
```

```
x // 2 =  [0 0 1 1]
```

```python
x = [-6, -3, 2, 5]
print("x = ", x)
print("取绝对值：", np.abs(x))
```

```
x =  [-6, -3, 2, 5]
取绝对值： [6 3 2 5]
```

```python
print("求指数：", np.exp(x)) #e的几次方
```

```
求指数： [2.47875218e-03 4.97870684e-02 7.38905610e+00 1.48413159e+02]
```

```python
print("求对数：", np.log(np.abs(x))) #求以e为底的对数,也可以指明以谁为底：log10这样
```

```
求对数： [1.79175947 1.09861229 0.69314718 1.60943791]
```

```python
x = np.random.rand(4,4) 
print("x = ", x)
```

```
x =  [[0.31542835 0.36371077 0.57019677 0.43860151]
 [0.98837384 0.10204481 0.20887676 0.16130952]
 [0.65310833 0.2532916  0.46631077 0.24442559]
 [0.15896958 0.11037514 0.65632959 0.13818295]]
```

```python
>>> x > 0.7
```

```
array([[False, False, False, False],
       [ True, False, False, False],
       [False, False, False, False],
       [False, False, False, False]])
```

##### 1.4.2 二维

```python
xx = np.full((2, 3), 3)
print("xx = ", xx)
```

```
xx =  [[3 3 3]
 [3 3 3]]
```

```python
print("xx + 5 = ", xx + 5)
```

```
xx + 5 =  [[8 8 8]
 [8 8 8]]
```

```
x =  [-6, -3, 2, 5]
取绝对值： [6 3 2 5]
```



```python
print("求指数：", np.exp(x)) #e的几次方
```

```
求指数： [2.47875218e-03 4.97870684e-02 7.38905610e+00 1.48413159e+02]
```



```python
print("求对数：", np.log(np.abs(x))) #求以e为底的对数,也可以指明以谁为底：log10这样
```

```
求对数： [1.79175947 1.09861229 0.69314718 1.60943791]
```



```python
x = np.random.rand(4,4) 
print("x = ", x)
```

```
x =  [[0.31542835 0.36371077 0.57019677 0.43860151]
 [0.98837384 0.10204481 0.20887676 0.16130952]
 [0.65310833 0.2532916  0.46631077 0.24442559]
 [0.15896958 0.11037514 0.65632959 0.13818295]]
```



```python
x > 0.7
```



```
array([[False, False, False, False],
       [ True, False, False, False],
       [False, False, False, False],
       [False, False, False, False]])
```



```python
x = np.random.randint(10, size = 5)
print("x = ", x)
```

```
x =  [1 2 4 2 0]
```



```python
x > 2
```



```
array([False, False,  True, False, False])
```



#### 1.5 numpy的运算

##### 1.5.1 点积运算

```python
xar = np.array([[1,2],[3,4]])
yar = np.array([[5,6],[7,8]])
v = np.array([9,10])
w = np.array([11,12])
```

```python
# 9x11 + 10x12 = 219
print(v.dot(w))
print(np.dot(v, w))
```

```
219
219
```

```python
# 就是矩阵的相乘运算
print(xar.dot(yar))
print(np.dot(xar, yar))
```

```
[[19 22]
 [43 50]]
[[19 22]
 [43 50]]
```

##### 1.5.2 求和运算

```python
xxAr = np.array([[1,2],[3,4]])
print(np.sum(xxAr)) #默认求和 把所有的元素都加起来
print(np.sum(xxAr, axis=0)) #=0的时候，计算每列的和
print(np.sum(xxAr, axis=1)) #=1的时候，计算每行的和
```

```
10
[4 6]
[3 7]
```

## 2. list

​	集合，用 [] 表示。

#### 2.1 增

​	append(e) 添加到尾部，insert(index, e)添加到指定位置。

#### 2.2 删

​	pop()删除尾部元素，pop(index)删除指定元素

## 3. tuple

​	元组，可看作是不可变的list，用 () 表示。

​	也没有pop()、insert()、append()方法。

​	tuple的不可变性，是不能做tuple[0] = e这种操作。但是如果tuple中包含一个列表元素，然后把列表元素取出来赋给某个变量，然后改变该列表中元素的值。最终打印的元组的值也是被改变的，例如：

```python
>>> t = (3.14, 'China', 'Jason', ['A', 'B'])
>>> print t
(3.14, 'China', 'Jason', ['A', 'B'])
>>> L = t[3]
>>> L[0] = 122
>>> L[1] = 233
>>> print t
(3.14, 'China', 'Jason', [122, 233])
```

## 4. dict

​	字典，可以存储键值对，相当于Java中的hashMap，用 {} 表示。

​	Dict是无序的，不能存储有序集合。

​	key不可变，value可变。一旦一个键值加到dict里面，那它对应的key就不能再变了。所以List不能作为dict的key。另外，key也不能重复。

#### 4.1 dict合并

```python
>>> d1 = {'mike':12, 'jack':19}
>>> d2 = {'jone':22, 'ivy':17}
>>> dMerge = dict(d1.items() + d2.items())
>>> print dMerge
{'mike': 12, 'jack': 19, 'jone': 22, 'ivy': 17}
```

或者

```python
>>> dMerge2 = dict(d1, **d2)
>>> print dMerge2
{'mike': 12, 'jack': 19, 'jone': 22, 'ivy': 17}
```

方法2比方法1速度快很多，方法2等同于：

```python
>>> dMerge3 = dict(d1)
>>> dMerge3.update(d2)
>>> print dMerge
{'mike': 12, 'jack': 19, 'jone': 22, 'ivy': 17}
```

## 5. set

​	set类似于一个list，但是内容不能重复，通过调用set()方法创建：

```python
>>> s = set(['A', 'B', 'C'])
```

​	就像dict是无序的一样，set也是无序的，也不能包含重复的元素。

 	对于访问一个set的意义就仅仅在于查看某个元素是否在这个集合里面，元素大小写是敏感的：

```python
>>> print 'A' in s
True
>>> print 'D' in s
False
```

#### 5.1 增删

​	通过add和remove来添加、删除元素（保持不重复），添加元素时，用set的add(e)方法：

```python
>>> s = set([1, 2, 3])
>>> s.add(4)
>>> print s
set([1, 2, 3, 4])
```

​	如果添加的元素已经存在于set中，add(e)不会报错，但是不会加进去了：

```python
>>> s = set([1, 2, 3])
>>> s.add(3)
>>> print s
set([1, 2, 3])
```

​	删除set中的元素时，用set的remove(e)方法，注意传进去的是元素值，因为set是无序的所以不能通过下标找元素。

```python
>>> s = set([1, 2, 3, 4])
>>> s.remove(4)
>>> print s
set([1, 2, 3])
```

​	如果删除的元素不存在set中，remove()会报错：

```python
>>> s = set([1, 2, 3])
>>> s.remove(4)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
KeyError: 4
```

#### 5.2 应用

所以如果我们要判断一个元素是否在一些不同的条件内符合，用set是最好的选择，下面例子：

```python
months = set(['Jan','Feb','Mar','Apr','May','Jun','Jul','Aug','Sep','Oct','Nov','Dec',])
x1 = 'Feb'
x2 = 'Sun'

if x1 in months:
    print 'x1: ok'
else:
    print 'x1: error'

if x2 in months:
    print 'x2: ok'
else:
    print 'x2: error'

>>>
x1: ok
x2: error
```

