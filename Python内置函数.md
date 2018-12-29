###python内置函数

#### abs()
取绝对值
####all()
用于检测可迭代参数中的所有元素是否都为TRUE，如果是返回True，否则返回False。元素除了是0、空、FALSE外都是TRUE。

注：空元素、空列表返回值也是True。

```
>>> all('0')
True
>>> all([])
True
>>> all([0, 1, 2])
False
>>> all([0, '', 2])
False
```

####any()
用于检测可迭代参数中的所有元素是否全部为FALSE，如果是返回False，否则返回True.只要有一个元素不为0、空、FALSE，就返回True.

```
>>> any('')
False
>>> any([])
False
>>> any({})
False
>>> any([0, '', False])
False
>>> any([0, '', False, 1])
True

```

####bin() 
返回一个整数 int 或者长整数 long int 的二进制表示。

####类型强制转换
bool()、int()、float()、str()

####bytearray() 
方法返回一个新字节数组。这个数组里的元素是可变的，并且每个元素的值范围: 0 <= x < 256。

如果 source 为整数，则返回一个长度为 source 的初始化数组；

```
>>> bytearray(10)
bytearray(b'\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00')
```

如果 source 为字符串，则按照指定的 encoding 将字符串转换为字节序列；

```
>>> bytearray('xiaobai', 'utf-8')
bytearray(b'xiaobai')
```

如果 source 为可迭代类型，则元素必须为[0 ,255] 中的整数；

```
>>> bytearray([1,2,3])
bytearray(b'\x01\x02\x03')
```

如果 source 为与 buffer 接口一致的对象，则此对象也可以被用于初始化 bytearray。
如果没有输入任何参数，默认就是初始化数组为0个元素。

####callable() 
函数用于检查一个对象是否是可调用的。如果返回True，object仍然可能调用失败；但如果返回False，调用对象ojbect绝对不会成功。
对于函数, 方法, lambda 函式, 类, 以及实现了 \_\_call\_\_ 方法的类实例, 它都返回 True。

####chr() 
用一个范围在 range（256）内的（就是0～255）整数作参数，返回一个对应的字符。

####classmethod
classmethod修饰的方法是类方法，不需要self参数，但是第一个参数是表示自身类的cls，可以通过cls访问类属性、实例方法。

```
class A(object):

	food = 'egg'
	def eat(self):
		print('eat %s' % self.food)

	@classmethod
	def eat_egg(cls):
		print('eat %s' % cls.food)


if __name__ == '__main__':
	A.eat_egg()
```

####operator模块
operator模块提供了一系列用来判等、取反、数学运算等函数。

```
import operator
operator.lt(a, b) #return a < b
operator.gt(a, b) #return a > b
operator.add(a,b) #return a + b
operator.mod(a,b) #return a % b
operator.contains(a, b) #return b in a
operator.delitem(a, b) #del a[b]
```

####compile()
compile函数是将字符串或文件编码成字节代码，然后配合exec 或 eval执行.exec执行代码，eval执行表达式。

```
>>> str = 'for i in range(0, 10): print(i)'
>>> c = compile(str, '', 'exec')
>>> exec(c)
0
1
2
3
4
5
6
7
8
9

>>> str = '3 * 2 + 4'
>>> c = compile(str, '', 'eval')
>>> eval(c)
10
>>> 
```

####eval() 
用来执行一个字符串表达式，并返回表达式的值。

####exec()
用来执行字符串代码,或者代码文件

```
>>> str = 'for i in range(0, 3): print(i)'
>>> exec(str)
0
1
2
```

```
#1.txt
for i in range(0, 3): print(i)

#执行1.txt中的代码
file = '../1.txt'
with open(file, 'r', encoding='utf-8') as file:
	exec(file.read())
0
1
2
```

####complex() 
用于创建一个值为 real + imag * j 的复数或者转化一个字符串或数为复数。如果第一个参数为字符串，则不需要指定第二个参数。

```
>>> complex(1, 2)
(1+2j)
## 注意：这个地方在"+"号两边不能有空格，也就是不能写成"1 + 2j"，应该是"1+2j"，否则会报错
>>> complex('1+2j')
(1+2j)
```

####zip()
zip函数用于将可迭代对象中对应元组打包成元组，然后将这些元组组成对象，可以节约内存。
list()可以将zip对象转成列表
zip *:可以将元组解压成列表。

```
#将a,b,c压缩到zipped
>>> zipped = zip(a, b, c)
>>> zipped
<zip object at 0x104217b88>
#将zip对象转成列表
>>> l = list(zipped)
>>> l
[(1, 4, 7), (2, 5, 8), (3, 6, 9)]
#将zip对象解压成元组
>>> a1, b1, c1 = zip(*l)
>>> a1
(1, 2, 3)
>>> b1
(4, 5, 6)
>>> c1
(7, 8, 9)
>>> 
```

####dir() 
不带参数时，返回当前范围内的变量、方法和定义的类型列表；带参数时，返回参数的属性、方法列表。如果参数包含方法\_\_dir\_\_()，该方法将被调用。如果参数不包含\_\_dir\_\_()，该方法将最大限度地收集参数信息。

####divmod() 
把除数和余数运算结果结合起来，返回一个包含商和余数的元组(a/b, a%b)。

####enumerate() 
用于将一个可遍历的数据对象(如列表、元组或字符串)组合为一个索引序列，同时列出数据和数据下标.

```
>>> a
[1, 2, 3]
>>> for index, row in enumerate(a):
...     print(index, row)
... 
0 1
1 2
2 3
```

####filter()
通过指定的方法过滤可遍历对象。filter返回的结果是filter对象，可以转成list

```
new_list = list(filter((lambda x: x % 2 == 0), [1, 2, 3, 4]))
print(new_list)

[2, 4]
```