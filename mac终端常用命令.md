###ls
ls,list的简写，列出目录的内容。

* -a:显示隐藏文件
* -l:以列表方式显示文件信息
* -h:配合-l，显示更人性化

####配合通配符使用

* ls *.txt:显示所有以.txt结尾的文件
* ls ?.txt:显示‘任意字符.txt’形式的文件
* ls [abc].txt:显示a/b/c任意一个.txt形式的文件

###输出重定向
将任意命令的结果输出到文件中

* ls -alh > 1.txt:将ls -alh输出到1.txt中，会覆盖文件之前内容
* ls -alh >> 1.txt:以追加的方式将ls -alh输出到1.txt中

###cat、more查看文件内容 
* cat 1.txt:一次性显示文件内容
* more 1.txt:分屏显示文件内容
* cat 1.txt > 2.txt:配合重定向使用
* cat 1.txt 2.txt > 3.txt: 通过重定向合并两个文件

###管道
将一个命令的输出作为另外一个命令的输入

`ls -alh | more`

###cd 切换工作目录
* cd: 切换到当前用户的主目录
* cd ~ :切换到当前用户的主目录
* cd . :切换到当前目录
* cd .. :切换到上级目录
* cd - :切换到上次目录

###mkdir:创建目录
* mkdir 1:创建目录1
* mkdir -p 1/2/3:递归创建目录，会依次创1.2.3目录

###rm、rmdir
* rmdir 1:删除目录，目录必须为空目录
* rm 1.txt: 删除文件
* rm -i 1.txt: 以交互方式执行删除
* rm -f 1.txt:强制删除文件，不管是否存在 
* rm -r 2: 以递归方式删除目录

###ln：创建链接文件
* ln 1.txt 1_hard.txt: 创建硬连接，原文件删除后，链接文件仍可用
* ln -s 1.txt 1_soft.txt: 创建软连接，源文件删除后，连接文件不可用。

###grep:文本搜索
grep 选项 '搜索内容' 文件名

* -v：显示不包含搜索内容的行
* -n: 显示匹配的行号
* -i: 忽略大小写
* grep -in 'fS' 1.txt :1.txt搜索含有'fs'文本的行，忽略大小写` 
* grep -n '^s' 1.txt: 搜索以‘s’开头的行
* grep -n 's$' 1.txt: 搜索以‘s’结尾的行
* grep -n 's.f' 1.txt: 搜索文本内容包含s开头，f结尾，中间非换行符的三个字符的字符串，

###find:查找文件
find 目录 选项 文件名

* find ./ -name 1.txt:当前文件夹查找名字为1.txt的文件
* find ./ -name '*.txt':查找当前文件夹后缀名为txt的文件,这种查找方式需要对文件名加引号

###cp:拷贝文件
* -a: 该选项通常在复制目录时使用，它保留链接、文件属性，并递归地复制目录，简单而言，保持文件原有属性。
* -f: 已经存在的目标文件而不提示
* -i: 交互式复制，在覆盖目标文件之前将给出提示要求用户确认
* -r: 若给出的源文件是目录文件，则cp将递归复制该目录下的所有子目录和文件，目标文件必须为一个目录名。
* -v: 显示拷贝进度

###mv:移动文件

###tar:归档
tar只是将文件打包，并没有压缩。通常配合gzip进行压缩。

* -c：生成档案文件，创建打包文件
* -v：列出归档解档的详细过程，显示进度
* -f：指定档案文件名称，f后面一定是.tar文件，所以必须放选项最后
* -t：列出档案中包含的文件
* -x：解开档案文件
* tar -cvf 1.tar 1.txt: 将1.txt打包到1.tar
* tar -xvf 1.tar: 解包1.tar

###gzip:压缩、解压
* -d	解压
* -r	压缩所有子目录

* gzip -rk 1.txt :保留源文件，压缩1.txt
* gzip -d 1.txt.gz:解压缩文件
* tar -zcvf 1.tar.gz *.txt:将以txt结尾的文件压缩到1.tar.gz
* tar -zxvf 1.tar.gz:解压缩文件
* tar -zxvf 1.tar.gz -C /python :将文件解压到指定目录

###zip:压缩、解压缩
zip [-r] 目标文件 源文件

* -r :递归压缩文件
* zip -r 1 *.txt:当前目录下所有txt文件压缩到1.zip
* unzip 1.zip:解压文件

###查看进程命令

* ps aux: 注意，不是ps -aux
* top:动态显示进程
* kill pid: 杀掉进程

###ifconfig: 查看网络状态
ifconfig en1 192.168.0.1 //设置网卡IP地址

###ping:测试网络连通
ping 192.168.0.1
ping www.baidu.com

###du:显示当前路径文件使用情况
du -h

###chmod：修改文件属性
r--4
w--2
x--1

chmod 741 2.txt	//u=rwx, g=r o=x

###vi/vim

插入模式：

* i:当前光标前插入
* I:当前光标行首插入
* a:当前光标后插入
* A:当前光标行尾插入
* o:当前光标下一行插入
* O:当前光标上一行插入
* ^:光标移动到行首
* $:光标移动到行尾


命令：

> 复制黏贴
> 
* yy: 复制
* 4yy:从光标行开始向下复制4行
* p:黏贴
* dd：剪切当前行
* 4dd:从光标行开始向下剪切4行，包含当前行
* D:从光标位置开始剪切，直到行末
* d0:从光标位置开始剪切，直到行首
* dw:剪切一个单词
* u:撤销操作
* ctrl+r:反撤销
* x: 删除当前光标位置后面1个字符
* X: 删除当前光标位置前面1个字符


> 光标移动
> 
* h:光标左移
* j:光标下移
* k:光标上移
* l:光标下移
* H:光标移动到当前屏幕下方
* M:光标移动到当前屏幕中间
* L:光标移动到当前屏幕上方

> 翻页
> 
* ctrl + f:向下翻页
* ctrl + b:向上翻页
* ctrl + d:向下翻半页
* ctrl + u:向上翻半页

>代码定位
>
* 10G:迅速定位到第10行
* G:迅速定位到最后一行
* gg:迅速定位到第一行

> 
* w:向后跳到下一个单词
* b:向前跳到上一个单词

> 移动代码
> 
> * v:从光标当前位置，向后开始选中，通过移动光标可以选择多行
> * V:选择当前行，通过移动光标可以选择多行
> * >:选中文本，向右移动一次
> * >:选中文本，向左移动一次
> * . :重复执行上次指令
> * { :跳到代码段开头
> * } :跳到代码段结尾

> 替换文本
> 
> * r:替换一个字符
> * R:替换多个字符
> 
> 搜索
> 
> * /asd: 搜索asd字符串
> * n:下一个搜索到的asd字符串
> 
> 
> 文本替换
> 
> * 输入':'进入末行模式
> * %s/hello/world/g: 文件中所有的hello 替换为 world
> 1,10s/hello/world/g: 文件中1-10行的hello 替换为 world
> 
> 
> 末行模式
> 
> * w:保存
> * q:退出
> * wq:保存退出