###数组
shell数组用括号表示，元素用空格符分隔。

获取数组元素： ${array[index]}
获取数组所有元素： ${array[*]}
获取数组长度：${#array[*]}

###grep:查找文件中是否包含字符串
### ！取反
shell中取反操作使用 ！ 号，！号前后要有空格

###cat 命令
cat用来查看文件，当cat不跟参数时，cat从标准输入STDIN读取数据，即输入什么，显示什么。如果把标准输入重定向到文件，那cat输出的结果就是文件的每一行数据。

###命令替换：将命令的输出赋值给变量
反引号括起来的是命令，命令的结果会传递给currentTime变量
currentTime= \`date \`

或者
`currentTime = $(date)`

###重定向
* 输出重定向
`ls -l > 1.log  #将ls -l的结果输出到1.log`

* 输入重定向：将文件内容作为指令的输入
`wc < 1.log  #将1.log作为wc指令的参数`

* 内联输入重定向：指定文本当做输入数据开始和结束标志，以获得更多输入，直到输入了结束标志

```
wc << EOF
> 111
> 222
> 333
> EOF
3       3      13
```

###管道：一个命令的输出当做另一个命令的输入
```
ls -l | sort > 1.log #将ls -l的结果排序，然后重定向到1.log中
ls -l | more #将ls的结果分屏显示
```

###数学运算： 
将数学表达式放在$[]中，可执行数学表达式，但是缺点是不能进行浮点数运算.

`$[数学表达式] `

```
$[1+2]
$[3*4]
```

###脚本中使用bash 计算器,可以进行浮点运算

```
value=$(echo “options; expression” | bc)
val=$(echo “scale=4; 4 / 5” | bc) #scale是设置bc的小数点位数，然后执行4/5
```

###通过内联输入重定向
```
#!/bin/bash
var1=10.46
var2=43.67
var3=33.2
var4=71
var5=$(bc << EOF
scale=4
a1=$var1*$var2
b1=$var3*$var4
a1+b1
EOF
)
echo value=$var5
~               
```   

###简易计算器
支持输入多个数字及运算符，调用方式 ./test1 1+2*3

```
#!/bin/bash
value=$(echo "scale=4; $1" | bc)
echo value=$value
```

### `$?` 查看命令的退出状态码

```
126代表没有权限
设置脚本的退出码  exit 5  #脚本执行完后，以退出码5返回，退出码范围0-255
```

### if语句
```
if command1
then 
	command2
else
   	command3
fi
```
如果command1指令返回的状态码为0，执行command2，否则执行command3.else语句可选.

```
if command1
then
	command2
elif command3
then
	command4
fi
```

if语句无法判断数值或字符串比较，需要借助test表达式

```
#!/bin/bash
a=10
if test a > 5
then
    echo "a > 5"
elif test a > 10
then
    echo "a > 10"
fi
```
或使[]表达式，[]两边必须要有空格,test表达式无法比较浮点数

####数值比较

* -eq :相等
* -ge:大于等于
* -gt:大于
* -le:小于等于
* -lt:小于
* -ne:不等于

```
#!/bin/bash
if [ $1 -gt $2 ]
then
    echo "$1 >= $2"
elif [ $1 -lt $2 ]
then
    echo "$1 < $2"
elif [ $1 -eq $2 ]
then
    echo "$1 = $2"
fi
```

####字符串比较
* str1 > str2 str1是否大于str2
* str1 < str2 str1是否小于str2
* str1 = str2 str1是否等于str2
* str1 != str2 str1是否不等于str2
* -n str1: str1长度是否非0
* -z str1: str1长度是否为0

当比较大于和小于的时候，需要对运算符进行转义，否则会当做重定向处理

```
name1=jermy
name2=xiaobai
if [ $name1 = $name2 ]
then
    echo "=="
fi

if [ $name1 != $name2 ]
then
    echo "!="
fi

if [ $name1 \> $name2 ]
then
    echo ">"
fi
if [ $name1 \< $name2 ]
then
    echo "<"
fi
if [ -n $name1 ]
then
    echo "not 0"
fi
if [ -z $name1 ]
then
    echo "=0"
fi
```

####文件比较

* -d file: 检查file是否存在，并且是目录
* -e file: 检查file是否存在
* -f file：检查文件是否存在且是文件
* -r file: 检查file是否存在且可读
* -s file:检查file是否存在且非空
* -w file:检查file是否存在且可写
* -x file:检查file是否存在且可执行
* -O file：检查file是否存在且属于当前用户
* -G file：检查file是否存在且默认组与当前用户相同
* file1 -nt file2 ：检查file1是否比file2新
* file1 -ot file2 ：检查file1是否比file2旧

### 组合运算符

```
if [ condition1 ] && [ condition2 ]
then
       echo
fi

if [ condition1 ] || [ condition2 ]
then
       echo
fi
```

### 双括号表达式
test表达式只能使用简单的算术操作，双括号提供了更多的数学符号，和其他语言里面的if语句可使用的数学符号相同。也可以用来赋值

```
a=10
b=20
if (( $a > $b ))
then
	echo “”
fi

c=(( $a++ ))
```

###双方括号表达式：用于字符串的模式匹配。双括号前后必须有空格

```
#!/bin/bash
if [[ $USER == j* ]]
then
    echo "$USER start with j"
else
    echo "not start with j"
fi
检查用户名是否j开头。== 将右边的字符串视为一个模式，并应用模式匹配规则
```

###case

case语句会将制定变量与不同模式匹配，如果匹配，则只需该模式的命令。可以使用竖线在一行中分隔多个模式。

```
#!/bin/bash
case $USER in
xiaobai | xiaohei)
    echo "xiaobai";;
xiaohong)
    echo "xiaohong";;
jermy)
    echo "jermy";;
esac
```

### for循环

```
for var in list
do
	commands
done

#读取列表的值
for name in xiaobai xiaohei xiaohong jermy
do
	echo $name
done
```

### 更改字段分隔符
系统默认的字段分隔符是空格 制表符 换行符，存储在IFS(内部字段分隔符)中，在处理字段时，可能需要忽略某些分隔符，此时可以通过修改IFS来达到目的。

```
#!/bin/bash
OLDIFS=$IFS	#保存IFS
IFS=$'\n'  	#设置新的IFS
for item in $(ls -l)
do
    echo $item
done
IFS=$OLDIFS    #还原IFS

#!/bin/bash
OLDIFS=$IFS
IFS=:;	#修改IFS为冒号、分号
for i in "this:is:test:message"
do 
    echo $i
done
IFS=$OLDIFS
```

### 使用通配符读取目录

```
#!/bin/bash
for file in ./*
do
    if [ -d $file ]
    	then echo “$file is a directory”
    elif [ -f $file ]
	then echo “$file is a file”
    fi
done
```

###C语言格式的for循环
使用C语言的for循环，需要使用双括号

```
#!/bin/bash
for (( i=0;i<10;i++ ))
do
	echo $i
done
```

###while命令

循环开始执行test command，如果test command返回状态码0，执行other command，继续while循环，否则退出循环

```
while test command
do
	other command
done
```

```
#!/bin/bash
a=10
while [ $a -gt 0 ]
do
    echo $a
    a=$[ $a - 1 ]
done
```

### until命令
只有 test command不返回状态0时，才会执行other command，如果返回0，循环退出

```
until test command
do
	other command
done
```

```
#!/bin/bash
a=10
until [ $a -eq 0 ]
do
    echo $a
    a=$[ $a - 1 ]
done
```

###循环处理文件数据

```
#!/bin/bash
IFSOLD=$IFS
IFS=$'\n'
for line in $(cat 1.txt)	#以换行为分隔读取每一行数据
do
    IFS=:		#以冒号为分隔，分隔每行数据
    for text in $line
    do
	echo $text
    done
done
IFS=$IFSOLD
```

###跳出循环
* break:当有嵌套循环时，break只会跳出内部循环，外部循环并未停止。break后可以跟参数，break 2跳出第二层级循环。
* continue：终止某次循环命令，但并不会完全终止整个循环。
continue也可以跟层级，continue 2 终止第二层级当前循环

###处理循环的输出
循环执行后，通过管道命令，可以对循环结果进行重定向或其他处理

```
#!/bin/bash
IFSOLD=$IFS
IFS=$'\n'
for line in $(cat 1.txt)	#以换行为分隔读取每一行数据
do
    IFS=:		#以冒号为分隔，分隔每行数据
    for text in $line
    do
	echo $text
    done
done > 1.txt	#对循环结果重定向，
# done | sort   #对循环结果排序
IFS=$IFSOLD
```

##处理用户输入
###位置参数
* $0 程序名,根据执行脚本命令的不同，输出不同。
* $1 第一个参数
* $2 第二个参数，直到$9
* 参数多于9个，引用是需要通过 ${10}的方式引用

`$0`会根据执行脚本的命令不同，输出不同，可以使用basename获取脚本名称

```
JermydeMacBook-Pro:shell jermy$ test2
./test2
JermydeMacBook-Pro:shell jermy$ ./test2
./test2
JermydeMacBook-Pro:shell jermy$ /Users/jermy/Desktop/shell/test2
/Users/jermy/Desktop/shell/test2

```

```
#!/bin/bash
name=$(basename $0)
echo $name

JermydeMacBook-Pro:shell jermy$ test2
test2
JermydeMacBook-Pro:shell jermy$ ./test2
test2
JermydeMacBook-Pro:shell jermy$ /Users/jermy/Desktop/shell/test2
test2
```

###检测命令行参数
如果命令需要用户输入参数，但实际调用时没有加参数，指令执行会报错，所有需要在脚本中添加检查参数的判断。

```
#!/bin/bash
if [ -n "$1" ]
then echo "hello $1"
else
echo "invalid parameter"
fi
```

###参数统计
当命令需要的参数过多时，检查每个参数比较麻烦，$#可以统计脚本运行时携带的参数个数。

```
#!/bin/bash
if [ $# -ne 2 ]
then
    echo
    echo Usage: test2.sh a b
    echo
else
    total=$[ $1+$2 ]
    echo $total
fi
```

```
JermydeMacBook-Pro:shell jermy$ test2

Usage: test2.sh a b

JermydeMacBook-Pro:shell jermy$ 
JermydeMacBook-Pro:shell jermy$ test2 1

Usage: test2.sh a b

JermydeMacBook-Pro:shell jermy$ test2 1 2
3

```

获取最后一个参数

```
echo $#     #显示参数个数
echo ${!#}	#获取最后一个参数
```

###获取所有数据
* $* 将命令行的所有参数当做一个单词保存，变成一个整体
* $@ 将命令行的所有参数当做一个字符串中多个独立的单词，可以通过for遍历。

在mac上测试。这两个指令没什么区别。都可以通过for遍历

```
echo $*
for item in $*
do
    echo $item
done

echo $@
for item in $@
do
    echo $item
done
```

```
test2 aaaa bbbbb cccc

aaaa bbbbb cccc
aaaa
bbbbb
cccc
aaaa bbbbb cccc
aaaa
bbbbb
cccc
```

###移动变量 shift

shift命令会将每个参数的位置左移一个位置，变量$2会一道$1中，$1的值会被删除。$0的值是脚本名称，不会变。

如果需要一次性移动多个位置，需要给shift命令提供一个参数。
shift 2:移动2个位置，跳过不需要的参数。

```
//在不知道参数个数的情况下，通过shift，输出所有参数
n=1
while [ -n "$1" ]
do
    echo "index $n, value $1"
    n=$[ $n+1 ]
    shift
done
```

###处理选项
命令行选项和参数一样，可以像处理命令行参数一样处理命令行选项。

####处理简单选项
使用case语句，匹配选项，单独处理

```
#!/bin/bash
while [ -n "$1" ]
do
    case $1 in
    -a)
    echo "get -a";;
    -b)
    echo "get -b";;
    -c)
    echo "get -c";;
    esac
    shift
done
```

```
test2 -c -b -a

get -c
get -b
get -a
```

####分离选项和参数
shell会使用“--”来分隔选项和参数，“--”之前是选项，之后是参数.

```
#!/bin/bash
while [ -n "$1" ]
do
    case $1 in
	-a) echo "get -a";;
	-b) echo "get -b";;
	-c) echo "get -c";;
	--) shift
	    break;;
	*) echo "not an option"
    esac
    shift
done

count=1
for parma in $@
do
    echo "parma$count: $parma"
    count=$[ $count + 1 ]
done
```

```
test2 -a -b -c -- aaa bbb ccc

get -a
get -b
get -c
parma1: aaa
parma2: bbb
parma3: ccc
```

####带值的选项

```
while [ -n "$1" ]
do
    case $1 in
	-a) echo "find option -a";;
	-b) param=$2
	    echo "find option -b, param=$param"
	    shift;;
        -c) param=$2
            echo "find option -c, param=$param"
            shift;;
	*) echo "invalid input"
    esac
    shift
done
```

```
test2 -a -b eeeee -c rrrrr

find option -a
find option -b, param=eeeee
find option -c, param=rrrrr
```

###使用getopt命令
如果使用组合选项，比如-ab，上面列出的三种方式无法处理，这时就需要使用getopt命令。

getopt命令可以接收一系列任意形式的命令行选项和参数，并自动将他们转换成适当的格式。

`getopt optstring parameters`
你需要在optstring中列出每个命令行选项字母，在需要选项的字母后加冒号。

当指定了一个不在optstring的选项时，getopt会产生一个错误，如果想忽略这个错误，可以在命令后加-q选项。(这个选项在MAC上无效，会导致设置getopt失败)

```
set -- $(getopt ab:cd "$@")	#设置选项abcd,选项b带参数

while [ -n "$1" ]
do
    case "$1" in
	-a) echo "find option -a";;
	-b) param="$2"
            echo "find option -b,param=$param"
	    shift;;
	-c) echo "find option -c";;
	-d) echo "find option -d";;
    esac
    shift
done
```

getopt的缺点是选项参数有空格的话，会识别失败。

###getopts
getopts相比getopt，能识别带空格的参数。

getopts会用到两个环境变量，OPTARG会保存参数值。OPTIND保存了参数列表正在处理的参数位置。

```
while getopts :ab:c opt		
//:ab:c 是命令行选项形式，第一个冒号表示忽略找不到选项的错误。b后面的冒号表示选项b带参数。 opt保存getopts定义的参数。相比getopt，case语句中不需要加"-"
do
    case "$opt" in
	a) echo "find -a option";;
	b) echo "find -b option ,with value $OPTARG";;
	c) echo "find -c option";;
	*) echo "unknown option $opt"
    esac
done
```

optstring中未定义的选项字母会以问号形式发送给代码。

getopts命令知道何时停止处理选项，并将参数留给你处理。在getopts处理每个选项时，

它会将OPTIND环境变量值增一。在getopts完成处理时，你可以使用shift命令和OPTIND值来 移动参数。

```
while getopts :ab:c opt
do
    case "$opt" in
	a) echo "find option -a";;
	b) echo "find option -b, with parma $OPTARG";;
	c) echo "find option -c";;
	*) echo "uknow option" ;;
    esac
done

#OPTIND保存了当前处理的选项位置，要获得后面的参数，需要左移参数
shift $[ $OPTIND -1 ]
count=1
for param in "$@"
do
    echo "param $count: $param"
    count=$[ $count+1 ]
done

```

```
test2 -a -b 111 -c ad sfwf wfn w

find option -a
find option -b, with parma 111
find option -c
param 1: ad
param 2: sfwf
param 3: wfn
param 4: w
```

###获取用户输入

####基本读取
获取用户输入使用read命令，read param ，将用户输入保存到param中

```
// echo -n :不会在字符串末尾输出换行符，让提示信息和用户输入在一行显示
echo -n "please input your nane"
read name
echo "your name is $name"
```

####使用read -p 读取输入
read -p选项允许在命令行中指定提示符

```
read -p "please input your name: " name
echo "your name is $name"
```
如果需要用户输入多个数据时，read命令需要指定多个变量，如果变量数据不够，剩余的数据会保存到最后一个变量中。

如果read命令不指定变量，read会将收到的数据都放在REPLY环境变量中。

```
read -p "please input data: "
n=1
for data in $REPLY
do
    echo "index: $n, data:$data"
    n=$[ $n+1 ]
done 

test2

please input data: ff sf wek wkfsdf 
index: 1, data:ff
index: 2, data:sf
index: 3, data:wek
index: 4, data:wkfsdf
```

####输入超时 -t
-t选项可以指定输入超时时间，当计时器过期后，read指令会返回非0退出状态码

```
if read -t 5 -p "please input: " data
then
    echo "your input is: $data"
else
    echo "timeout"
fi
```

####指定输入字符个数 -n
-n 选项可以指定read指令输入字符个数，当用户输入指定字符个数后，read自动退出，将数据传递给变量

```
//当输入1个字符后，read指令自动退出
read -n1 -p "please input: "
echo
echo "your input is $REPLY"
```

####隐藏读取 -s
当用户输入密码时，不希望密码显示在屏幕上，可以使用-s选项，实际上数据会显示，只是文字颜色被设成跟背景色一致。

```
read -s -p "please input: "
echo 
echo "data: $REPLY"
```

####读取文件
read可以读取文件数据，每次调用read命令，会从文件中读取一行文本，当读取到文件末尾时，read会退出病房非0退出状态码。

```
count=1
cat 1.txt | while read line
do
    echo "line $count: $line"
    count=$[ $count+1 ]
done
echo "finish read file"
```

##呈现数据
###标准文件描述符
Linux系统对每个对象当做文件处理，使用文件描述符标识每个对象。

* 0 :STDIN 标准输入，键盘输入或输入重定向
* 1 :STDOUT 标准输出，终端显示器
* 2 :STDERR 标准错误输出

默认情况下STDOUT和STDERR文件描述符会执行同一个位置，即终端显示器。当对STDOUT重定向后，STDERR不会发生改变，即STDERR的消息还是会显示在屏幕上。

###重定向错误数据

####只重定向错误数据

```
//将错误数据重定向到1.log中
ls -l 1.fff 2> 1.log
```

####重定向数据和错误

```
//将正确的数据重定向到1.log,错误的数据重定向到2.log 
ls -l 1.fff 1> 1.log 2> 2.log
```

```
//将数据和错误数据都重定向到1.log
ls -l 1.fff $> 1.log
```

###脚本中重定向输出
####临时重定向

```
//这行会在脚本的STDERR文件描述符所指向的位置显示文本，而不是通常的STDOUT
echo "this is an error" >$2

//运行脚本时，如果重定向了STDERR，上面的错误信息会重定向到指定文本中
test 2> 1.log
```

####永久重定向
使用exec命令，可以告诉shell在脚本执行期间重定向某个特定文件描述符.

```
exec 1>1.log	//将STDOUT重定向到1.log
exec 2>2.log //将STDERR重定向到2.log
```

####重定向输入
exec命令允许将STDIN重定向到文件中

```
//设定1.txt为标准输入，从1.txt中读取数据
exec 0< 1.txt

while read line
do
    echo "data is : $line"
done
```

###创建自己的重定向

####创建输出文件描述符

```
//将文件描述符3重定向到3.log
exec 3> 3.log
echo "this is test1"
echo "this is test2"
echo "this is test3" >&3 //这条语句输出在文件3中
```

####重定向文件描述符

```
exec 3>&1			//将文件描述符3重定向到1中，即STDOUT
exec 1>1.log	    //将STDOUT重定向到1.log
echo "this is test"  //标准输出，会输出到1.log
echo "this is test" >&3 //因为文件描述符3现在定向在STDOUT，所以这个语句会显示在屏幕上
exec 1>&3        //将文件描述符1重定向到STDOUT
```

####创建输入文件描述符
可以先将STDIN重定向到其他文件描述符，读取完文件后再将STDIN还原。

```
exec 6<&0  	//将STDIN重定向到文件描述符6
exec 0<1.log //将文件描述符0重定向到1.log，即1.log是数据输入源
n=1
while read line	//通过read命令从输入源读数据
do
    echo "line$n: $line"
    n=$[ $n+1 ]
done

exec 0<&6	//还原文件描述符

read -n1 -p "is done? Y|N :" flag //从标准输入源输入数据
echo
case $flag in
y | Y)
    echo "done!!!";;
n | N)
    echo "not done!!!"
esac

```

####关闭文件描述符

```
exec 3>&-		//关闭文件描述符3
```

####列出打开的文件描述符
lsof 命令会列出整个Linux系统打开的所有文件描述符。

* -p: 指定进程ID
* -d: 指定文件描述符编号

```
// -a 表示逻辑与运算
// $$ 获取当前的PID 
/usr/sbin/lsof -a -p $$ -d 0,1,2
```

####阻止命令输出
当脚本作为后台进程运行时，不需要显示脚本输出。可以将STDERR重定向到一个叫null文件的特殊文件。

路径：/dev/null

重定向到null文件的任何数据都会被丢掉，不会显示。

```
ls -al xxx 2> /dev/null 	//将STDERR重定向到null文件，会忽略所有错误输出
```

null文件另外一个功能是清空文件中的数据

```
cat /dev/null > test  //将null文件重定向到test中，清空test数据
```

###临时文件
Linux系统下/tmp目录存放不需要永久保存的文件，mktemp命令可以在当前脚本目录下创建一个临时文件。

####创建本地临时文件

```
mktemp testing.XXXXXX   //参数格式：文件名.XXXXXX，系统会自动补全6个字符

mktemp -d test.XXXX //创建临时文件夹
```

```
tempFile=$(mktemp test.XXXXXX)	//创建临时文件
exec 3>$tempFile		//文件描述符3输出到临时文件

echo "this is test1" >&3 
echo "this is test2" >&3

exec 3>&- //关闭文件描述符
echo "content is :"
cat $tempFile

rm -f $tempFile >/dev/null //删除临时文件
```

####在系统临时目录下创建临时文件
mktemp是在脚本所在的目录创建临时文件，使用-t选项，可以在系统的临时目录创建文件

`mktemp -t test.XXXX`

###记录消息
将输出同时发送给显示器和日志文件，需要使用tee命令。tee命令将从STDIN过来的数据同时发给STDOUT和tee指定的文件名。由于tee会重定向来自STDIN的视乎，可以配合管道命令重定向输出。

```
date | tee 1.log  //在显示器和文件同时显示date命令的结果,默认会覆盖输出文件的内容

date | tee -a 1.log //以追加的方式输出，不覆盖输出文件的内容
```

##控制脚本

###处理信号
Linux通过信号和系统中的进程进行通信。

* Ctrl+C 中断进程，发送SIGINT信号
* Ctrl+Z 暂停进程，发送SIGTSTP信号

###捕获信号
`trap commands signals`

```
//捕获Ctrl+C中断退出信号
trap "echo i got signal Ctrl+C" SIGINT
echo start
n=1
while [ $n -lt 10 ]
do
    echo $n
    sleep 1
    n=$[ $n+1 ]
done
```

###捕获脚本退出的信号

```
//脚本退出的信号是EXIT，脚本执行完就会发出EXIT信号。
trap "echo exit signal" EXIT
echo start
n=1
while [ $n -lt 5 ]
do
    echo $n
    sleep 1
    n=$[ $n+1 ]
done
```

###移除捕获
trap -- SIGINT //移除捕获SIGINT信号

###后台模式运行脚本
后台模式运行脚本，只需要在命令后加个`&`就可以了.脚本会在后台运行，并显示作业号和PID。但后台进程仍然会共享STDIN和STDOUT，所有会在屏幕输出数据。当终端被关闭时，后台脚本也会停止。

```
test2 &	//后台模式运行test2
```

###非控制台下运行脚本
让脚本一直在后台执行，直到结束。即使退出终端，脚本也不会停止。需要使用nohup命令。

`nohup test2 & `

nohup命令会解除终端与进程的关联，进程也就不再与STDOUT和STDERR联系在一起。nohup命令会自动将STDOUT和STDERR消息重定向到名为nohup.out文件中。

###作业控制
jobs命令 查看当前进程的所有作业，作业前面带加号的代表当前默认作业，带减号的作业将成为下一个默认作业。

* bg:以后台模式重启暂停的作业。
作业通过Ctrl+Z暂停后，通过jobs能获取暂停的作业号，通过bg 作业号，将对应的作业在后台继续运行。
* fg:以前台模式重启暂停的作业。

###调度谦让度
Linux系统进程优先级由高到第为 -20~19.数值越大，优先级越低。

nice指令设置优先级： 
`nice -n 10 test2 > 1.log &` 设置test2优先级为10，输出重定向到1.log ，并且在后台运行。

renice：调整优先级：
`renice -p 5055 -n 0` 调整PID为5055的作业的优先级为0

###定时运行作业

####at命令执行作业
at -f filename time

##函数

###创建函数
函数定义必须放在函数调用之前，否则会找不到方法。

```
//方式一
function name {
}    //定义函数

//方式二
test2() {
}

name  //调用函数
test2
```

###函数返回值
####使用return命令
return命令允许指定一个整数值来定义函数的退出状态码。执行完函数后需要使用$?指令获取返回码，返回码必须是0~255.

####使用函数输出

```
function test {
    read -p "input a number :" num
    echo $[ $num*2 ]	//这里不是通过return返回，而是通过echo输出
}

n=$(test) //获取test的输出
echo "double value: $n"
```

###函数中使用变量

####向函数传递参数
函数内部也可以使用$0 $1等环境变量，但是函数内部的环境变量和脚本的环境变量是不同的环境。在函数内部获得的环境变量是传递给函数的参数。

```
function test {
    echo $[ $1+$2 ]
}

ret=$(test $1 $2)
echo "res=$ret"
```

local:函数的内部变量如果和全局变量同名，会使用全局变量。如果需要使用局部变量，使用local指令。

####函数传递数组

```
function testit {
    local newarray
    newarray=$(echo $@)	//需要把数组元素分解成单个值，然后重新组合成新对象
    echo "the new array is: ${newarray[*]}"
}

myarray=(1 2 3 4 5)
echo "the original array is ${myarray[*]}"
testit ${myarray[*]}
```

####从函数返回数组

```
function arraydblr {
    local originarray
    local newarray
    local elements
    local i

    originarray=($(echo $@))
    newarray=($(echo $@))
    elements=$#

    for(( i=0;i<elements;i++ ))
    {
	newarray[$i]=$[ ${originarray[$i]}*2 ]
    }
    echo ${newarray[*]}
}

arr=(1 2 3 4 5)
echo "the original array is: ${arr[*]}"
arg1=$(echo ${arr[*]})
result=($(arraydblr $arg1))
echo "the new array is: ${result[*]}"
```

###函数递归

```
function factorial {
    if [ $1 -eq 1 ]
    then
	echo 1
    else
	value=$(factorial $[ $1-1 ])
	echo $[ $value * $1 ]
    fi	
}

read -p "please input a number: " num
res=$(factorial $num)
echo "res is: $res"
```