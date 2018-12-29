https://www.w3cschool.cn/python3/python3-os-file-methods.html

####解释器

在Linux/Unix系统中，你可以在脚本顶部添加以下命令让Python脚本可以像SHELL脚本一样可直接执行：

```
#! /usr/bin/env python3.4
```

然后修改脚本权限，使其有执行权限，命令如下：

```
$ chmod +x hello.py
```

执行以下命令：

```
./hello.py
```

####基础类型
* Python中变量不需要声明。每个变量在使用前必须赋值，变量赋值以后该变量才会被创建。
* "/"除法运算符总是返回浮点数，要获取证书使用"//"运算符。

####字符串
* python中的字符串不能改变,可以使用字符串拼接的方式产生新字符串。
* 字符串使用单引号或双引号括起来，使用反斜杠转义特殊字符。
* 如果不想让反斜杠发送转义，可以在字符串签名加r，

```
>>> print('this is tom\'s food')
this is tom's food

>>> print(r'this is tom\'s food')
this is tom\'s food
```
* 字符串可以使用"+"运算符连接，使用“*”运算符表示重复

```
>>> print("this is " + "mine " * 3)
this is mine mine mine 
```

* 字符串有两种索引方式：从左向右，从0开始增加；从右向左，从-1开始减少。Python没有单独的字符类型，字符就是长度为1的字符串。

```
>>> str = "this is tom"
>>> print(str[0])
t
>>> print(str[-1], str[-2])
m o
>>> 
```

* 获取子串，用冒号分隔两个索引，截取的范围是前闭后开,索引可以省略。

```
>>> print(str[0:5])
this 
>>> print(str[0:6])
this i
>>> print(str[3:])
s is tom
>>> print(str[:6])
this i
```

* 字符串长度：len()

```
>>> print(len(str))
15
```

####列表

* 列表类似数组，列表中的元素类型可以不相同。列表中元素可以改变。
* 列表同样支持分切割、拼接(+)运算

```
>>> arr = [1, "a", 10]
>>> arr2 = [2, "b"]
>>> print(arr + arr2)
[1, 'a', 10, 2, 'b']
>>> print(arr[:2])
[1, 'a']
>>> arr[0] = 20
>>> print(arr)
[20, 'a', 10]
```

* list.append(x)：追加元素
* list.extend(L):添加指定列表的所有元素来扩充列表
* list.insert(i, x):在指定位置插入元素
* list.remove(x):删除值为x的第一个元素，如果不存在，返回错误
* list.pop(i):删除并返回指定位置的元素，i是可选的，如果没有指定索引，将删除最后一个元素
* list.clear():清空所有元素
* list.index(x):返回列表中第一个值为x的元素的索引。
* list.count(x):返回列表中值为x的元素的个数
* list.sort():对列表元素排序
* list.reverse():列表中元素倒序
* list.copy():列表浅复制

* 替换、删除元素

```
>>> arr[1: 3] = [33, 55]	#将下标为1、2的元素分别替换成33 55
>>> print(arr)
[20, 33, 55, 30]
>>> arr[0: 2] = []	#删除下标为0、1的元素
>>> print(arr)
[55, 30]
>>> arr = []	#清空列表
>>> print(arr)
[]
```

* len：返回列表长度
* 嵌套列表

```
>>> a, b = [1, 2, 3], [4, 5, 6]
>>> c = [a, b]
>>> print(c)
[[1, 2, 3], [4, 5, 6]]
>>> print(c[0][0])
1
>>> print(c[1][0:3])
[4, 5, 6]
```

####元组
* 元组写在小括号之间，元素可以不相同。但是元组的元素不能修改。
* 元组只有一个元素时，需要在元素后加逗号,如果不加逗号，会被当做对应的数据类型

```
>>> tup1, tup2 = (), (10,)
>>> print(tup1)
()
>>> print(tup2)
(10,)
```

* 元组同样支持分切割、拼接(+)运算
* 元组无法修改元素，可以通过拼接创建新元组

```
>>> tup = (1, 2, "a", "b")
>>> print(tup[1: 3])
(2, 'a')
>>> tup[0: 2] = ()	#无法修改元组
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: 'tuple' object does not support item assignment
>>> tup1 = tup[0: 2]
>>> print(tup1)
(1, 2)
>>> del tup #删除元组之后再使用元组，会报错
>>> print(tup)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: name 'tup' is not defined
``` 

* 元组同样支持+号和*号运算

```
>>> tup = (1, 2, "a", "b")
>>> print(len(tup))
4

>>> tup1 = (44,)
>>> print(tup1 + tup)
(44, 1, 2, 'a', 'b')

>>> print(tup1 * 4)
(44, 44, 44, 44)

>>> print(33 in tup)
False
```

* 内置函数

```
>>> tup = ("a", "b", "c")
>>> print(max(tup))	#返回最大元素，要求元素类型必须相同
c
>>> print(min(tup))
a
>>> arr = [1, 2, 3]

>>> print(tuple(arr))	#列表转成元组
(1, 2, 3)
```
####集合
* 集合是一个无序不重复元素的集，基本功能是进行成员关系测试和消除重复元素。
* 可以使用大括号或set()函数创建集合，创建空集合必须用set(),因为 { }用来创建空字典。

```
>>> set1 = {1 ,2, 4 ,2}
>>> set2 = set("xiaobai")	#从字符串创建集合
>>> set2
{'o', 'b', 'a', 'i', 'x'}
>>> set3 = set("xiaohei")
>>> set3
{'e', 'h', 'o', 'a', 'i', 'x'}
>>> set2 - set3	#返回只存在set2的元素
{'b'}
>>> set3 - set2
{'e', 'h'}

>>> set3 | set2
{'e', 'h', 'o', 'a', 'i', 'b', 'x'}

>>> set3 & set2
{'x', 'o', 'i', 'a'}
>>> set3 ^ set2
{'e', 'b', 'h'}

#集合也支持推导式
>>> {x for x in "abadfadfb" if x not in "abc"}
{'d', 'f'}
```

####字典

* 字典的键值必须不可变，可以使用数字、字符串、元组，不可以使用列表

```
#定义字典
>>> dic = {"name": "xiaobai", "age": 20, "height": 175}

#根据键获取值
>>> print(dic["name"])
xiaobai

#修改键对应的值
>>> dic["age"] = 22
>>> print(dic["age"])
22

#添加新的键值
>>> dic["weight"] = 70
>>> print(dic["weight"])
70

#删除字典中的键值对
>>> del dic["weight"]
>>> print(dic)
{'name': 'xiaobai', 'age': 22, 'height': 175}

#删除字典，字典将不再存在，访问字典会发生错误
>>> del dic
>>> print(dic)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: name 'dic' is not defined

>>> dic = {"name": "xiaobai"}
>>> print(dic)
{'name': 'xiaobai'}

#清空字典所有的键值对，清空后字典还存在，会变成空字典，还可以添加元素
>>> dic.clear()
>>> print(dic)
{}
>>> dic["name"] = "xiaobai"
>>> print(dic)
{'name': 'xiaobai'}

```

* 遍历字典

```
#在字典中遍历时，关键字和对应的值可以使用 items() 方法同时解读出来
dic = {"name": "xiaobai", "age": 10}
for k, v in dic.items():
	print(k, v)
	
```

* 内置函数

> len:获取字典键值个数 

> str:输出字典可以打印的字符串表示

> type:返回变量类型

```
>>> dic = {"name": "xiaobai", "age": 20}

>>> str(dic)
"{'name': 'xiaobai', 'age': 20}"

>>> len(dic)
2

>>> type(dic)
<class 'dict'>

```

* 内置方法

> dic.clear(): 清空字典所有值，不会删除字典，清空后字典会变成空字典，但是仍然可以添加元素
> 
> dic.copy():返回字典的浅复制副本
> 
> dic.fromkeys()：以序列中的值做为键创建新字典，序列可以是元组或者列表，值为键对应的初始值，也可以设置默认值

```
>>> dic = {}
>>> dup = ("name", "age", "height")    
>>> dic = dic.fromkeys(dup)
>>> dic
{'name': None, 'age': None, 'height': None}
>>> dic.clear()
>>> dic.fromkeys(dup, 20)
{'name': 20, 'age': 20, 'height': 20}

```
> dic.get(key, defaultValue):获取键对应的值，如果键不存在，返回defaultValue

```
>>> dic
{'name': 20, 'age': 20, 'height': 20}
>>> dic.get("name", "NA")
20
>>> dic.get("sex", "NA")
'NA'
>>> 
```
> key in dic: 如果字典中包含键值key,返回True，否则返回False
> 
> dic.items():以列表返回可遍历的(键, 值) 元组数组

```
>>> dic
{'name': 20, 'age': 20, 'height': 20}
>>> dic.items()
dict_items([('name', 20), ('age', 20), ('height', 20)])
```

> dic.keys():以列表的形式返回字典所有的KEY
> 
> dic.values():以列表的形式返回字典所有值

```
>>> dic
{'name': 20, 'age': 20, 'height': 20}
>>> dic.keys()
dict_keys(['name', 'age', 'height'])

>>> dic.values()
dict_values([20, 20, 20])
```

> dic.setdefault(key, defaultvalue):获取key对应的值，如果key不存在，会添加键，并设置值为defaultvalue

```
>>> dic
{'name': 20, 'age': 20, 'height': 20}

>>> dic.setdefault("name")
20

>>> dic.setdefault("sex", "male")
'male'
>>> dic
{'name': 20, 'age': 20, 'height': 20, 'sex': 'male'}
```

> dic.update(dic1):把dic1的键值更新到dic中,如果dic和dic1有相同的键，dic中的值会被覆盖。

```
>>> dic = {"name": "xiaobai", "age": 20}
>>> dic1 = {"name": "xiaohei", "height": 175}
>>> dic.update(dic1)
>>> dic
{'name': 'xiaohei', 'age': 20, 'height': 175}
```

####Python逻辑运算符
与其他语言不一样，Python的逻辑运算符使用 "and"、“or”、“not”

* and:布尔与，如果x为False，x and y返回False，否则返回y的计算值
* or:布尔或，如果x为True,返回x的值，否则返回y的值
* not:布尔非，如果x为True，返回False，如果x为False，返回True

```
>>> a ,b, c = False, 10, 20
>>> print(a and b)
False
>>> print(b and c)
20
>>> print(b or c)
10
>>> print(c or b)
20
>>> print(a or b)
10
>>> print(not a)
True
>>> print(not b)
False
```

####成员运算符
* in:如果在指定的序列中找到值，返回True，否则返回False
* not in:如果在指定的序列中找不到值，返回True，否则返回False

```
>>> str = "abcd1234"
>>> print("a" in str)
True
>>> print("b" not in str)
False
```

####身份运算符
* is:判断两个对象是否引用自于同一对象，如果id(x)==id(y)，返回True
* is not:判断两个标识符是不是引用自不同对象。

```
>>> a, b, c = 20, 20, 15
>>> print(a is b)
True
>>> print(b is c)
False
```

####if语句

* 每个条件后面都有使用冒号
* 使用缩进来划分语句块，相同缩进的语句在一起组成一个语句块
* Python中使用elif代替else if
* Python中没有switch语句

```
a = 10
if a > 10:
	print("a > 10")
elif a > 20:
	print("a>20")
else:
	print("a <=10")
```

####while循环

* while条件后需要跟冒号
* Python中没有do...while

```
i = 0
sum = 0

while i < 100:
	sum += i
	i = i + 1

print("sum = %d" % (sum))
```

####for循环
for循环可以遍历任何序列，比如列表、元组、字典、字符串等.

```
balls = ["football", "basketball", "pingpangball"]

for ball in balls:
	if ball == "basketball":
		print("i like %s" %(ball))
		break
	print("this is %s" %(ball))
else:
	print("no basketball")

print("done")
```

####range()函数
* 如果要遍历数字序列，可以使用内置range()函数，它会生成数列
* range是左闭右开区间

```
#输出0 - 4
for i in range(5):
	print(i)
```

* 使用range指定区间

```
for i in range(4, 9):
	print(i)
```

* 使用range指定区间，并指定不同的增量

```
#输出 0 3 6 9
for i in range(0, 10, 3):
	print(i)
```

* 使用range()和len()遍历序列

```
arr = ["xiaobai", "xiaoming", "xiaohong"]

for i in range(len(arr)):
	print(str(i), arr[i])
```

* 使用range()生成序列

```
#列表
print(list(range(5)))

#元组
tup = tuple(range(5))
print(tup)

#字典
dic = {}
dic = dic.fromkeys(range(5), 15)
print(dic)
```

####else语句
for、while循环可以有else语句，它在穷尽列表或条件为假时，被执行。但循环被break终止时不执行。

####pass语句
pass语句什么都不做，只在语法上需要一条语句，但程序不需要任何操作时使用。

####迭代器
* 迭代器是一个能记住遍历的位置的对象。
* 迭代器两个基本方法：iter()和 next()
* 字符串、列表、元组都可以用于创建迭代器

```
list = [1, 2, 3, 4]
it = iter(list)	#创建迭代器对象
print (next(it))	#输出迭代器下一个元素
print (next(it))
```

* 使用for语句遍历迭代器

```
list = [1, 2, 3, 4]
it = iter(list)

for x in it:
	print(x, end=" ")	#每输出一个元素，后面都跟一个空格
```

* 使用next()遍历迭代器

```
import sys

list = [1, 2, 3, 4]
it = iter(list)

while True:
	try:
		print(next(it))
	except StopIteration:
		sys.exit()
```

####生成器

* 在 Python 中，使用了 yield 的函数被称为生成器（generator）。
* 跟普通函数不同的是，生成器是一个返回迭代器的函数，只能用于迭代操作，更简单点理解生成器就是一个迭代器。
* 在调用生成器运行的过程中，每次遇到 yield 时函数会暂停并保存当前所有的运行信息，返回yield的值。并在下一次执行 next()方法时从当前位置继续运行。

```
#!/usr/bin/python3

import sys

def fibonacci(n): # 生成器函数 - 斐波那契
    a, b, counter = 0, 1, 0
    while True:
        if (counter > n): 
            return
        yield a
        a, b = b, a + b
        counter += 1
f = fibonacci(10) # f 是一个迭代器，由生成器返回生成

while True:
    try:
        print (next(f), end=" ")
    except StopIteration:
        sys.exit()
```

####函数
* 函数定义使用def关键字。
* 参数列表可以有默认值
* 函数可以有返回值，使用return语句，也可以返回空值
* 可变参数列表，这些参数会被包装进元组。

```
def info(name, age = 0, height = 0):
	print("name is", name)
	print("age is", age)
	print("height is", height)
	return
	
res = info("xiaobai")
#res的值是空值，None

#可变参数列表
def sum(*args):
	num = 0
	for i in args:
		num += i
	print(num)

sum(1,2,3,4)
```

####数据结构

* 队列

```
from collections import deque
queue = deque(["aaa", "bbb", "ccc"])
queue.append("ddd")
queue.append("eee")
print(queue.popleft())
print(queue)
print(queue.popleft())
print(queue)
```

* 堆栈
堆栈可以直接使用队列实现

```
stack = ["aaa", "bbb"]
stack.append("ccc")	#入栈
print(stack)
stack.pop()	#出栈
print(stack)
```

####列表推导式
将一些操作应用于某个序列的每个元素，用其获得的结果作为生产新列表的元素。或者根据确定的判定条件创建子序列。

```
#列表中每个元素都乘2
>>> [2*x for x in list]
[6, 4, 4]

//计算列表中每个元素的长度，生成新列表
>>> list = ["aaa", "vvvvv", "ddddddd"]
>>> [len(x) for x in list]
[3, 5, 7]

//计算列表中长度大于4的元素的长度，生成新列表
>>> [len(x) for x in list if len(x) > 4]
[5, 7]
```

####del 语句
del语句删除列表中对应索引的元素，或者是删除整个列表

```
>>> arr = [1, 2, 3]
>>> del arr[0]	#删除索引为0的元素
>>> arr
[2, 3]

>>> arr.extend([4, 5, 6])
>>> arr
[2, 3, 4, 5, 6]
>>> del arr[2:4]	#根据切割删除元素
>>> arr
[2, 3, 6]
>>> del arr[:]
>>> arr
[]
>>> del arr	#删除列表，列表将不再存在，使用时会报错
>>> arr
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: name 'arr' is not defined
```

####序列遍历

* enumerate():在序列的遍历时，索引位置和对应值可以使用enumerate()函数得到

```
arr = [1 ,2, 3]
for i, v in enumerate(arr):
	print(i, v)

dic = {"name": "xiaobai", "age": 20}
for i, v in enumerate(dic):
	print(i, v)

str = "xiaobai"
for i, v in enumerate(str):
	print(i, v)

dup = (1, 2, 3, 4)	
for i, v in enumerate(dup):
	print(i, v)
```

* zip():同时遍历两个或多个序列，可以使用zip()组合

```
questions = ["name", "age"]
answers = ["xiaobai", 20]
for q, a in zip(questions, answers):
	print("what is your {0}? It is {1}.".format(q, a))
```

* reversed():反向遍历序列

```
for i in reversed(range(1, 10, 2)):
	print(i)
```

* sorted():返回一个已排序的队列

```
basket = ["apple", "orange", "pair"]
for f in sorted(basket):
	print(f)
```

###模块
模块就是后缀名为.py的Python文件，模块可以被其他程序引入，以使用其中的函数。

#### import语句
导入模块需要用import语句，解释器会搜索所有的目录列表查找指定模块。被导入模块的名称将放到当前模块的符号表中。

```
# support.py
def print_func(par):
    print("hello:", par)
    return
    
#test.py
import support
support.print_func("xiaobai")
```
调用模块里的函数，需要使用模块.函数名()的形式调用，如果模块的函数使用频繁，可以赋一个本地名称

```
info = support.print_func
info("xiaobai")
```

#### from...import...
从模块导入指定的部分，会把模块内的指定的函数名称导入到目标模块的符号表中，而不是把模块名称导入，所以使用这种方式导入模块的函数，在使用函数时，不需要使用"模块名.函数名"的方式调用，直接通过函数名调用。

```
#从support模块导入showInfo函数，调用showInfo函数时不需要加模块名
from support import showInfo
showInfo("hello")
```

#### from...import
一次性把模块内的函数、变量都导入到目标模块的符号表中。

#### \_\_name\_\_属性

* 当一个模块被另一个程序第一次引入时，其主程序将运行。如果想让模块被引入时，不执行模块的程序，可以用\_\_name\_\_属性来让程序块仅在该模块自身运行时执行。
* 每个模块都有一个\_\_name\_\_属性，当其值是'\_\_main\_\_'时，表明该模块自身在运行，否则是被引入。

```
#support.py
if __name__ == "__main__":
	print("自身运行")
else:
	print("其他模块引用")

def print_func(par):
    print("hello:", par)
    return

def showInfo(info):
	print("showInfo", info)
	return
	
	
#自身执行
>> python3 support.py
>> 自身运行

#其他程序引用
>> python3 test.py
>> 其他模块引用
```

####dir()
内置函数dir()可以找到模块内定义的所有名称。以字符串列表的形式返回。

####包
包含\_\_init\_\_.py文件的文件夹就是一个包。\_\_init\_\_.py可以是空文件，也可以加初始化代码，或为\_\_all\_\_变量赋值。

导入包内子模块的方法：

* import package.mod1.mod2: 导入mod2子模块，调用时也需要使用全名：package.mod1.mod2.func()
* from package.mod1 import mod2:导入mod2子模块，调用时不需要使用全名：mod2.func()
* from package.mod1.mod2 import info:直接导入mod2的info()函数，调用：info();
* 当使用from package import item这种形式的时候，对应的item既可以是包里面的子模块（子包），或者包里面定义的其他名称，比如函数，类或者变量。
* 如果使用形如import item.subitem.subsubitem这种导入形式，除了最后一项，都必须是包，而最后一项则可以是模块或者是包，但是不可以是类，函数或者变量的名字。

####from...import *
导入包时如果使用from...import \*的方式，会把包里面的所有子模块全部导入。为了解决这个问题，引入了\_\_all\_\_。如果在\_\_init\_\_.py文件中存在\_\_all\_\_列表变量，在使用from...import \*的方式导入时，只会导入\_\_all\_\_中声明的模块。

###输入输出
####输出
* str.format():格式化输出
* str():输出值转成字符串，用户易读的形式
* repr():输出值转成字符串，解释器易读的形式

```
#repr()函数可以转义字符串中的特殊字符
>> s = "hello world \n"
>> print(s)	#输出hello world，同时还有换行
>> hello world
>> 
>> print(str(s))	#输出hello world，同时还有换行
>> hello world
>>
>> repr(s)	//#会将"\n"转义成"\\n"
>> "'hello world\\n'"
>> print(repr(s)) #输出转义的字符串
>>'hello world\n'
```

####rjust()、ljust()
* rjust(n, "c"):字符串右对齐，左边填充
* ljust(n, "c"):字符串左对齐，右侧填充
* center(n, "c"):字符串居中对齐，两侧填充
* zfill(n):字符串左侧填充0
n表示字符串填充后的长度，“c”表示用来填充的字符串,"c可省略，默认用空格填充"。如果字符串长度大于n,不会填充任何字符。
这三个方法会返回新的字符串。

```
>>> s = "hello"
>>> print(s.rjust(10, "*"))	#右侧对齐，左侧填充"*"
*****hello
>>> print(s.rjust(10)) 	#右侧对齐，左侧填充空格
     hello
>>> print(s.ljust(10)) #左侧对齐，左侧填充空格
hello     
>>> print(s.ljust(10, "X")) #左侧对齐，左侧填充"X"
helloXXXXX

>>> s.center(10, "*")
'**hello***'

>>> s.zfill(10)	#字符串左侧填充0
'00000hello'
```

####str.format()

* 格式字符串中的{}会被format()中的参数替换。

`print("name is {}, age is {}".format("xiaobai", 20))`

* {}中可以指定参数在format中的位置，下标从0开始.注：如果有一个参数使用了下标表示法，那其他参数都必须使用下标表示法。
`print("name is {0}, age is {1}".format("xiaobai", 20))`

* 如果format使用了关键字参数，嘛呢它的值会指向使用该名字的参数
`print("name is {name}, age is {age}".format(name = "xiaobai", age = 20))`

* '!a' (使用 ascii()), '!s' (使用 str()) 和 '!r' (使用 repr()) 可以用于在格式化某个值之前对其进行转化:
`print("name is {!s}, age is {!r}".format("xiaobai", 20))`

* 可选项":"后面可以跟字段名，可以对值进行更好的格式化。

注：需要注意的是如果参数是字符串，那":"后不能有空格，否则会报错。比如{1:10} 和 {1: 10}，当下标1对应的参数是字符串时，第二种写法会报错。(不知道为啥，反正会报错)

```
#数字后面保留3位小数
print("name is {}, age is {:.3f}".format("name", 20))

#设置name和age的宽度
table = {"xiaobai": 20, "xiaohong": 30}
for name, age in table.items():
	print("{0:10} - {1:10}".format(name, age))
```

* 如果你有一个很长的格式化字符串, 而你不想将它们分开, 那么在格式化时通过变量名而非位置会是很好的事情。
最简单的就是传入一个字典, 然后使用方括号 '[]' 来访问键值 :

```
table = {'Sjoerd': 4127, 'Jack': 4098, 'Dcab': 8637678}
print('Jack: {0[Jack]:d}; Sjoerd: {0[Sjoerd]:d}; '
          'Dcab: {0[Dcab]:d}'.format(table))
          
# 也可以通过在 table 变量前使用 '**' 来实现相同的功能：
table = {'Sjoerd': 4127, 'Jack': 4098, 'Dcab': 8637678}
print('Jack: {Jack:d}; Sjoerd: {Sjoerd:d}; Dcab: {Dcab:d}'.format(**table))

```

####旧式字符串格式化
% 操作符也可以实现字符串格式化。 它将左边的参数作为类似 sprintf() 式的格式化字符串, 而将右边的代入, 然后返回格式化后的字符串. 

```
print("name is %s, age is %d" % ("name", 20))
```

###文件操作

####打开文件
> open(filename, mode)

* filename:文件名.
* mode:文件打开方式,是可选的，默认是只读。
* 'r'：只读； 
* 'w':只写(如果存在同名文件，会删除之前文件)。
* 'a'：追加文件内容，数据会自动添加到文件末尾。
* 'r+':读写。

文件打开成功后，会返回文件对象
`f = open('\tmp\file', 'w')`

####f.read()
读取文件内容，以字符串或字节对象返回。f.read(size)：读取指定长度内容，如果size为空或负值，将会读取全部内容。

####f.readline()
从文件读取单独的一行。以换行符'\n'为结束依据。如果f.readline()返回一个空字符串，说明已经读取到最后一行。

```
f = open("/Users/jermy/Desktop/python/test.py")
while 1:
	str = f.readline()
	if len(str) == 0:
		break
	print(str)
```

####f.readlines()
返回文件中包含的所有行。如果设置可选参数sizehint，则读取指定长度的字节，并且将这些字节按行分隔。

```
>>> f = open("/Users/jermy/Desktop/python/test.py")
>>> f.readlines(30)
['#! /usr/bin/env python3.6\n', '\n', "table = {'Sjoerd': 4127, 'Jack': 4098, 'Dcab': 8637678}\n"]
```

另外一种方式是迭代一个文件对象，然后读取每行

```
>>> f = open("/Users/jermy/Desktop/python/test.py")
>>> for line in f:
...     print(line, end=" ")
... 
#! /usr/bin/env python3.6
 
 table = {'Sjoerd': 4127, 'Jack': 4098, 'Dcab': 8637678}
 print("Jack: {0[Jack]:d}; Sjoerd: {0[Sjoerd]:d}; Dcab: {0[Dcab]:d}".format(table))
 >>> 
```

####f.write(string)
将String写入到文件，然后返回写入的字符数

```
#使用'w'方式打开文件，如果文件存在，会先删除 然后创建文件
>>> f = open("/Users/jermy/Desktop/python/test.py", 'w')
>>> f.write("this is test")
12
>>> f = open("/Users/jermy/Desktop/python/test.py")
>>> f.readlines()
['this is test']
>>> 
```

####f.tell()
返回文件对象当前所处的位置，是从文件开头开始算的字节数。

```
>>> f = open("/Users/jermy/Desktop/python/test.py")
>>> f.tell()
0
>>> f.read(3)
'thi'
>>> f.tell()
3
>>> 
```

####f.seek()
f.seek(offset,from_what):改变文件对象当前位置。
offset是偏移位置，from_what默认值是0。

* seek(x,0) ： 从起始位置即文件首行首字符开始移动 x 个字符
* seek(x,1) ： 表示从当前位置往后移动x个字符
* seek(-x,2)：表示从文件的结尾往前移动x个字符



>注：
在使用seek（）函数时，有时候会报错为  “io.UnsupportedOperation: can't do nonzero cur-relative seeks”，这是因为，在文本文件中，没有使用b模式选项打开的文件，只允许从文件头开始计算相对位置，从文件尾计算时就会引发异常。将  f=open("aaa.txt","r+")  改成
f = open("aaa.txt","rb")   就可以了

```
>>> f = open("/Users/jermy/Desktop/python/test.py", 'rb')
>>> f.seek(3,0)
3
>>> f.seek(3,1)
6
>>> f = open("/Users/jermy/Desktop/python/test.py", 'r+')
>>> f.seek(3,0)
3
>>> f.seek(3,1)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
io.UnsupportedOperation: can't do nonzero cur-relative seeks
```

####f.close()
关闭文件，并释放资源。

####with
当处理一个文件对象时, 使用 with 关键字是非常好的方式。在结束后, 它会帮你正确的关闭文件。 而且写起来也比 try - finally 语句块要简短:

```
>>> with open('/tmp/workfile', 'r') as f:
...     read_data = f.read()
>>> f.closed
True
```

####方法操作汇总

* file.close() 关闭文件。关闭后文件不能再进行读写操作。
* file.flush() 刷新文件内部缓冲，直接把内部缓冲区的数据立刻写入文件, 而不是被动的等待输出缓冲区写入。
* file.fileno() 返回一个整型的文件描述符(file descriptor FD 整型), 可以用在如os模块的read方法等一些底层操作上。
* file.isatty() 如果文件连接到一个终端设备返回 True，否则返回 False。
* file.next()返回文件下一行。
* file.read([size])从文件读取指定的字节数，如果未给定或为负则读取所有。
* file.readline([size]) 读取整行，包括 "\n" 字符。
* file.readlines([sizehint])读取所有行并返回列表，若给定sizeint>0，返回总和大约为sizeint字节的行, 实际读取值可能比sizeint较大, 因为需要填充缓冲区。
* file.seek(offset[, whence]) 设置文件当前位置
* file.tell() 返回文件当前位置。
* file.truncate([size]) 截取文件，截取的字节通过size指定，默认为当前文件位置。
* file.write(str)将字符串写入文件，返回的是写入的字符长度。
* file.writelines(sequence)向文件写入一个序列字符串列表，如果需要换行则要自己加入每行的换行符。

###pickle
python通过pickle实现了数据序列化和反序列化。通过pickle模块的序列化操作，可以将数据保存到文件中去。通过反序列化操作能够从文件中读取数据。
```
#序列化
import pickle
data1 = {"a":[1,2,3,4],"b":("name", "age"),"c":None}
selfref_list=[1,2,3]
selfref_list.append(selfref_list)

output = open("/Users/jermy/Desktop/python/test.py","wb")

pickle.dump(data1, output)
pickle.dump(selfref_list, output, -1)

output.close()

#反序列化
import pprint, pickle

pkl_file = open("/Users/jermy/Desktop/python/test.py","rb")

data1 = pickle.load(pkl_file)
pprint.pprint(data1)

data2 = pickle.load(pkl_file)
pprint.pprint(data2)

pkl_file.close()
```