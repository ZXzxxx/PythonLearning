（参考）<https://blog.csdn.net/yjk13703623757/article/details/77918633>

## `if __name__ == '__main__'`

​	通俗的理解`__name__ == '__main__'`：假如你叫小明.py，在朋友眼中，你是小明`(__name__ == '小明')`；在你自己眼中，你是你自己`(__name__ == '__main__')`。

`	if __name__ == '__main__'`的意思是：当.py文件被直接运行时，`if __name__ == '__main__'`之下的代码块将被运行；当.py文件以模块形式被导入时，`if __name__ == '__main__'`之下的代码块不被运行。

## 程序入口

​	Python属于脚本语言，不像编译型语言那样先将程序编译成二进制再运行，而是动态的逐行解释运行。也就是从脚本第一行开始运行，没有统一的入口。

​	一个Python源码文件（.py）除了可以被直接运行外，还可以作为模块（也就是库），被其他.py文件导入。不管是直接运行还是被导入，.py文件的**最顶层代码都会被运行**（Python用缩进来区分代码层次），而当一个.py文件作为模块被导入时，我们可能希望一部分代码不被运行。

#### 一个.py文件被其他.py文件引用

​	假设有一个const.py文件，内容如下：

```python
PI = 3.14

def main():
    print("PI:", PI)

main()

# 运行结果：PI: 3.1412345678
```

​	现在写一个用于计算圆面积的area.py文件，area.py文件需要用到const.py文件中的PI变量。从const.py中，把PI变量导入area.py：

```python
from const import PI

def calc_round_area(radius):
    return PI * (radius ** 2)

def main():
    print("round area: ", calc_round_area(2))

main()

'''
运行结果：
PI: 3.14
round area:  12.56
'''
```

#### `if __name__ == "__main__"`

​	const.py中的main函数也被运行了，实际上不希望它被运行，因为const.py提供的main函数只是为了测试常量定义。这时`if __name__ == '__main__'`派上了用场。

​	把const.py改一下，添加`if __name__ == "__main__"`：

```python
PI = 3.14

def main():
    print("PI:", PI)

if __name__ == "__main__":
    main()1234567
```

​	运行const.py，输出如下：

```python
PI: 3.141
```

​	运行area.py，输出如下：

```python
round area:  12.561
```

​	如上可以看到`if __name__ == '__main__'`相当于Python模拟的程序入口，Python本身并没有这么规定，这只是一种编码习惯。由于模块之间相互引用，不同模块可能有这样的定义，而程序入口只有一个。到底哪个程序入口被选中，这取决于`__name__`的值。 

