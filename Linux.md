# Linux

## 

## 一键配置vim:

wget -q0-  https://raw.github.com/ma6174/vim/master/setup.sh | sh -x

截图：Shift + PrtScr

```
登入数据库：mysql -h rm-2zecm564n8yf006m3125010.mysql.rds.aliyuncs.com -u yuzhendi -p mysql
```

#!/bin/bash    编辑方式 -->bash

单行注释:  #

多行注释：  

​	:<<!

​	语句

​	！

执行  bash  a.sh   或者  直接加执行的权限

## 课下积累

### Linux xargs 命令

xargs 是给命令传递参数的一个过滤器，也是组合多个命令的一个工具。

xargs 可以将管道或标准输入（stdin）数据转换成命令行参数，也能够从文件的输出中读取数据。

xargs 也可以将单行或多行文本输入转换为其他格式，例如多行变单行，单行变多行。

xargs 默认的命令是 echo，这意味着通过管道传递给 xargs 的输入将会包含换行和空白，不过通过 xargs 的处理，换行和空白将被空格取代。

xargs 是一个强有力的命令，它能够捕获一个命令的输出，然后传递给另外一个命令。

之所以能用到这个命令，关键是由于很多命令不支持|管道来传递参数，而日常工作中有有这个必要，所以就有了 xargs 命令，例如：

```shell
find /sbin -perm +700 |ls -l       #这个命令是错误的
find /sbin -perm +700 |xargs ls -l   #这样才是正确的
```

xargs 一般是和管道一起使用。

命令格式

```shell
somecommand |xargs -item  command
```

参数：

-a file 从文件中读入作为sdtin
-e flag ，注意有的时候可能会是-E，flag必须是一个以空格分隔的标志，当xargs分析到含有flag这个标志的时候就停止。
-p 当每次执行一个argument的时候询问一次用户。
-n num 后面加次数，表示命令在执行的时候一次用的argument的个数，默认是用所有的。
-t 表示先打印命令，然后再执行。
-i 或者是-I，这得看linux支持了，将xargs的每项名称，一般是一行一行赋值给 {}，可以用 {} 代替。
-r no-run-if-empty 当xargs的输入为空的时候则停止xargs，不用再去执行了。
-s num 命令行的最大字符数，指的是 xargs 后面那个命令的最大命令行字符数。
-L num 从标准输入一次读取 num 行送给 command 命令。
-l 同 -L。
-d delim 分隔符，默认的xargs分隔符是回车，argument的分隔符是空格，这里修改的是xargs的分隔符。
-x exit的意思，主要是配合-s使用。。
-P 修改最大的进程数，默认是1，为0时候为as many as it can ，这个例子我没有想到，应该平时都用不到的吧。

### Linux wc命令

Linux wc命令用于计算字数。

利用wc指令我们可以计算文件的Byte数、字数、或是列数，若不指定文件名称、或是所给予的文件名为"-"，则wc指令会从标准输入设备读取数据。

语法

```shell
wc [-clw][--help][--version][文件...]
```

参数：

```shell
-c或--bytes或--chars 只显示Bytes数。
-l或--lines 只显示行数。
-w或--words 只显示字数。
--help 在线帮助。
--version 显示版本信息。
```

```shell
使用 wc统计，结果如下：
$ wc testfile           # testfile文件的统计信息  
3 92 598 testfile       # testfile文件的行数为3、单词数92、字节数598 
```

### Linux chmod命令

Linux/Unix 的文件调用权限分为三级 : 文件拥有者、群组、其他。利用 chmod 可以藉以控制文件如何被他人所调用。

使用权限 : 所有使用者

语法

```shell
chmod [-cfvR] [--help] [--version] mode file...
```

参数说明
mode : 权限设定字串，格式如下 :

参数说明
mode : 权限设定字串，格式如下 :

```shell
[ugoa...][[+-=][rwxX]...][,...]
```


其中：

u 表示该文件的拥有者，g 表示与该文件的拥有者属于同一个群体(group)者，o 表示其他以外的人，a 表示这三者皆是。
+ 表示增加权限、- 表示取消权限、= 表示唯一设定权限。
r 表示可读取，w 表示可写入，x 表示可执行，X 表示只有当该文件是个子目录或者该文件已经被设定过为可执行。
其他参数说明：

-c : 若该文件权限确实已经更改，才显示其更改动作
-f : 若该文件权限无法被更改也不要显示错误讯息
-v : 显示权限变更的详细资料
-R : 对目前目录下的所有文件与子目录进行相同的权限变更(即以递回的方式逐个变更)
--help : 显示辅助说明
--version : 显示版本

实例
将文件 file1.txt 设为所有人皆可读取 :

```shell
chmod ugo+r file1.txt
```


将文件 file1.txt 设为所有人皆可读取 :

```shell
chmod a+r file1.txt
```


将文件 file1.txt 与 file2.txt 设为该文件拥有者，与其所属同一个群体者可写入，但其他以外的人则不可写入 :

```shell
chmod ug+w,o-w file1.txt file2.txt
```


将 ex1.py 设定为只有该文件拥有者可以执行 :

```shell
chmod u+x ex1.py
```


将目前目录下的所有文件与子目录皆设为任何人可读取 :

```shell
chmod -R a+r *
```



## shell变成基础

### 变量和局部变量

变量的定义：（弱类型语言）

```shell
	a=12 	a=helloword		a=`pwd`	
	a=$a:a 	#字符串拼接，可以判断a是否为空
```



局部变量

```shell
local a=12
```

### 特殊变量

```shell
$0:获取当前执行shell脚本的文件名，包括路径；
$n:获取当前执行脚本的第n个参数，n=0-9,当n大于9使，要用大括号；
$*:获取当前执行脚本的所有参数，将所有命令行参数视为单个字符串，相当于"$1$2$3";
$#:得到执行脚本的参数个数；
$@:获取这个程序所有参数，并保留参数之间的空白，相当于"$1" "$2" "$3",这是将参数传给其他程序的最好的办法。
```

状态变量

```shell
$?:判断上一指令是否成功执行，0为成功执行，非零则不成功；
$$:取当前进程的PID；
$!:上一个指令的PID；
```

### 变量，参数展开

```shell
${parameter:-word}如果变量未定以，则表达式的值为word;
${parameter:=word}如果变量未定以，设置变量的值为word，表达式的值也是word;
${parameter:?word}用于捕捉由于变量未定以而导致的错误并退出程序；
${parameter:+word}如果变量已经定义，返回word，也就是真
```

### 字符串展开

```shell
${#parameter}:输出字符串的长度
${parameter:offset}:从第offset字符开始截取；
${parameter:offset:length}:从offset字符截length长度的字符；
${parameter#pattern}:从头删除最短匹配
${parameter##pattern}：最长
${parameter%pattern}:从尾删除最短
${parameter%%pattern}:从尾部删除最长
```

### 函数

```shell
function _printf_ {
	echo $1
	return
}
```

```shell
_printf_ {
	echo $1
	return
}
```

```shell
function _printf_() {
	echo $1
	return
}
```

### 流程控制 

#### IF

```shell
if [[ condition ]];then #if空格[[空格 判断 空格]]

	#statements

fi
if [[ condition ]];then
	#statements
	else
		#statements
fi
if [[ condition ]];then
	#statements
elif [[ condition ]];then
	#statements
fi
```

```shell
&1 -eq $2 #判断两个整数相当
$[${min}] -ge $1 #-ge 是大于等于（整数），${}中的括号表示$的约束，$[]表示整数
$1 -gt $2 #整数1大于整数2
$1 -le $2 #小于等于
$1 -lt $2 #小于
$1 -ne $2 #不等于
字符串用  =  ！=    -z 是否为空 或者用拼接的方式:${str}:x = x
```

#### FOR

```shell
for i in words;do
	#srarements
done
for (( i = 0; i < 10; i++));do
	#statements
done
```

#### WHILE

```shell
while [[ condition ]];do

	#statements

done
```

#### CASE

```shell
case word in
	pattern )
	;;
esac
```

### 数组

```shell
declare -a a
	name[subscript]=value
	name=(value1 value2)
```



## 命令系统

Linux帮助系统

man	#命令全名，简单的说明及用法

tldr	#too long don't read 联网使用手册，简洁

### shell通配符

* ```shell
  ? 	代表单个任意字符
  例如： ls ?.sh
  	ls ??.sh #两个字符
  * 代表任意几个字符
  例如： ls *ld #包含ld的任意个字符的文件
  [list]	匹配list中的任意一个字符
  例如：a[xyz]c 及axc,ayc,azc
  [!list]	匹配除list中的任意字符
  例如：a[!0-9a-z]
  [c1-c2]	匹配c1-c2中的任一字符
  [string1,string2...]	匹配string1、string2或更多其中之一的字符串
  ```

  ### 任务管理

```shell
1.&
在命令的后面加上 & 表示后台执行的意思
command &
fg 回到前台
```

```
2.;
command;command 表示命令顺序执行
```

```
3.&&
语句1 && 语句2 1成功部执行后面
```

```
4.||
```

```shell
5.``
命令中如果包含另一个命令，则用``括起来，在执行的时候系统优先执行``中的子命令，然后将其结果带入父命令继续执行
command1 `command2`
```

```shell
6.ctrl+z
将程序暂时挂起（jobs可以看状态,fg回前台bg将挂起的命令后台执行）
```

### 管道、重定向

```shell
|
#将前面的命令通过管道，将输入流到下一个命令
例如：
ls | cat
man ls | cat -n | head -n 120 | tail -n 20
```



```shell
1.>
重定向符
```

```shell
2.>>
作用与>基本相同，不同的是>>将内容追加到文件的末尾，而>内容覆盖原来文件
```

```shell
3.<
与>相反，是文件到命令的重定向。
例如： ./a.out < a.txt
```

```shell
4.<<
例如：cat >> a.log <<EOF
```

### 系统信息的获取

|  命令  | 功能                       |  命令  |               功能               |
| :----: | -------------------------- | :----: | :------------------------------: |
| uptime | 打印系统运行时长和平均负载 |   w    | 当前登陆用户及列表正在执行的任务 |
|  who   | 显示当前登陆系统的用户信息 | whoami |      打印当前有效的用户名称      |
|  last  | 显示用户最近登陆信息       | uname  |         打印当前系统信息         |
|  date  | 显示或设置系统时间与日期   |  cal   |             显示日历             |

date [dsu] <参数> ：

选项：

1. ​	-d "string":显示字符串所指的日期
2. ​    -s  "string": 设置时间

参数：

​	<+日期格式>:显示使用的日期格式

```shell
date +"%H:%M:%s"
```

### 文件及目录操作

| 命令  | 功能         | 命令  | 功能         |
| :---: | ------------ | ----- | ------------ |
|  cd   | 切换当前目录 | pwd   | 打印当前目录 |
| mkdir | 创建目录     | rmdir | 删除目录     |

pwd [-LP] :

​	L	显示逻辑工作目录

​	P	显示物理工作目录

mkdir	[pm] <dir>

​	-p	自动创建父母录

​	-m	设置权限

|   命令   |        功能        |  命令   |   功能   |
| :------: | :----------------: | :-----: | :------: |
|    ls    | 显示文件及目录信息 |   cp    |   拷贝   |
|    rm    |        删除        |   mv    |   移动   |
| basename |      取文件名      | dirname | 取目录名 |

#### cp拷贝：

cp [irapdslu] <sour> <des>

1. -i：	若文件存在，询问用户
2. -r：    递归复制
3. -a：   pdr的集合
4. -p:      连同文件属性一起拷贝
5. -d:      若源文件为连接文件的属性，则复制连接文件的属性
6. -s:       拷贝为软连接(相当于两个文件)
7. -l:        拷贝为硬连接（相当于一个文件，但删除一个另外一个还存在）软硬连接，一改都改
8. -u:       源文件比目的文件新才拷贝

#### rm删除

rm [irf] <dir_or_file>

1. -i:    互动模式
2. -r:    递归删除
3. -f:    强制删除

### 文件内容的查阅

| 命令 |           功能           | 命令 |          功能          |
| :--: | :----------------------: | :--: | :--------------------: |
| cat  |        正向连续读        | tac  |       反向连续读       |
|  nl  |     输出行号显示文件     | more | 一页一页的显示文件内容 |
| less | 与more相似，但是可上下看 | head |       只看头几行       |
| tail |       只看末尾几行       |  od  |    以二进制内容查看    |

```shell
head: 

head [-n num] file

	-n num :显示文件前面num行

	-n -num: 除了最后num行，其余显示

tail：

tail [-n num] file

	-n num: 显示文件后面num行

	-n +num： 除了前面num行，其余显示
```



### 数据提取操作

| 命令  |       说明       | 命令  |         说明         |
| :---: | :--------------: | :---: | :------------------: |
|  cut  |       切分       | grep  |         检索         |
| sort  |       排序       |  wc   | 统计字符、字数、行数 |
| uniq  |       去重       |  tee  |      双向重导向      |
| split |     文件切分     | xargs |       参数代换       |
|  tr   | 替换、压缩和删除 |       |                      |

#### TR对标准输入的字符替换、压缩和删除

```shell
tr [cdst] <字符集> <字符集>
参数：
-c, --complement：反选设定字符。也就是符合 SET1 的部份不做处理，不符合的剩余部份才进行转换
-d, --delete：删除指令字符
-s, --squeeze-repeats：缩减连续重复的字符成指定的单个字符
-t, --truncate-set1：削减 SET1 指定范围，使之与 SET2 设定长度相等
```

**语法**

```shell
tr [-cdst][--help][--version][第一字符集][第二字符集]  
tr [OPTION]…SET1[SET2] 
例如：
cat testfile |tr a-z A-Z 
```

#### CUT切分

Linux cut命令用于显示每行从开头算起 num1 到 num2 的文字。

**语法**

```shell
cut  [-bn] [file]
cut [-c] [file]
cut [-df] [file]
```

**使用说明:**

cut 命令从文件的每一行剪切字节、字符和字段并将这些字节、字符和字段写至标准输出。

如果不指定 File 参数，cut 命令将读取标准输入。必须指定 -b、-c 或 -f 标志之一。

**参数:**

-b ：以字节为单位进行分割。这些字节位置将忽略多字节字符边界，除非也指定了 -n 标志。
-c ：以字符为单位进行分割。
-d ：自定义分隔符，默认为制表符。
-f ：与-d一起使用，指定显示哪个区域。
-n ：取消分割多字节字符。仅和 -b 标志一起使用。如果字符的最后一个字节落在由 -b 标志的 List 参数指示的
范围之内，该字符将被写出；否则，该字符将被排除
实例
当你执行who命令时，会输出类似如下的内容：

```shell
$ who
rocrocket :0           2009-01-08 11:07
rocrocket pts/0        2009-01-08 11:23 (:0.0)
rocrocket pts/1        2009-01-08 14:15 (:0.0)
如果我们想提取每一行的第3个字节，就这样：

$ who|cut -b 3
c
c
```

#### GREP检索

**语法**

```shell
grep [-acinv] <string> <file>
```

**参数**

-a	:将以二进制文件以普通文件的形式搜索数据

-c	:统计搜寻到的次数

-i	:忽略大小写

-n	:顺序输出行号

-v	:反向输出（输出没有找到的）

#### SORT排序

语法

```shell
sort [-bcdfimMnr][-o<输出文件>][-t<分隔字符>][+<起始栏位>-<结束栏位>][--help][--verison][文件]
```

参数说明：

参数说明：

-b 忽略每行前面开始出的空格字符。
-c 检查文件是否已经按照顺序排序。
-d 排序时，处理英文字母、数字及空格字符外，忽略其他的字符。
-f 排序时，将小写字母视为大写字母。
-i 排序时，除了040至176之间的ASCII字符外，忽略其他的字符。
-m 将几个排序好的文件进行合并。
-M 将前面3个字母依照月份的缩写进行排序。
-n 依照数值的大小排序。
-u 意味着是唯一的(unique)，输出的结果是去完重了的。
-o<输出文件> 将排序后的结果存入指定的文件。
-r 以相反的顺序来排序。
-t<分隔字符> 指定排序时所用的栏位分隔字符。
+<起始栏位>-<结束栏位> 以指定的栏位来排序，范围由起始栏位到结束栏位的前一栏位。
--help 显示帮助。
--version 显示版本信息。
实例
在使用sort命令以默认的式对文件的行进行排序，使用的命令如下：

```shell
sort testfile 
```


sort 命令将以默认的方式将文本文件的第一列以ASCII 码的次序排列，并将结果输出到标准输出。

使用 cat命令显示testfile文件可知其原有的排序如下：

$

```shell
 cat testfile      #testfile文件原有排序  
test 30  
Hello 95  
Linux 85 
```

使用sort命令重排后的结果如下：

```shell
$ sort testfile #重排结果  
Hello 95  
Linux 85  
test 30 
```

### 文件时间和隐藏属性

#### *文件的三个时间：

mtime :内容数据改动时才更新这个时间（一般不和说明时就是这个时间）

ctime :文件的权限、属性改动的时候更新这个时间

atime : 文件的内容被取用access时，更新这个时间

```shell
ls -l --time=ctime etc/hostname
```

修改文件时间与新建文件

touch [-acdmt] <file>

参数：

​	-a : 仅修改访问时间

​	-c : 仅修改文件的时间，若文件不存在，不创建

​	-d : 修改文件日期

​	-m : 仅修改mtime

​	-t : 修改文件时间[yymmddhhmm]

#### 文件隐藏属性

chattr [+-=] [ASacdistu] <file_or_dir>

参数：

​	A : 不修改atime

​	S ： 同步写入

​	a : 只增加数据

​	c ：自动压缩、解压

​	d : 不会被dump程序备份

​	i : 不能删除、修改、建立连接

​	s : 文件删除时，直接从硬盘删除

​	u ： 文件删除时，数据内容存在磁盘中 

### 文件的特殊权限

|    权限    |      |      作用的对象      |                 效果                 |
| :--------: | :--: | :------------------: | :----------------------------------: |
|  *set_uid  |  s   |    二进制程序文件    | 用户在执行该程序时获取程序所有者权限 |
|  *set_gid  |  s   | 目录和二进制程序文件 | 用户在该目录里，有效组变为目录所属组 |
| sticky bit |  s   |         目录         | 在目录下，用户只能删除自己创建的内容 |

此处添加图片说明：

### 命令与文件的查询

|  命令  |          功能          |  命令   |      功能      |
| :----: | :--------------------: | :-----: | :------------: |
| which  |      寻找执行文件      | whereis |  寻找特定文件  |
| locate | 搜索文件（可部分查找） |  find   | 多样化高级查找 |

## 用户管理

### 用户管理的重要配置文件

|   配置文件   |                   内容                   |
| :----------: | :--------------------------------------: |
| /etc/passwd  | 用户名 密码位 用户编号 姓名 $HOME $SHELL |
| /etx/shadow  | 用户名 已加密密码 密码改动信息 密码策略  |
|  /etc/group  |     群组名 密码位 群组编号 组内用户      |
| /etc/gshadow |             群组密码相关文件             |
| /etc/sudoers |       用户名 权限定义 权限（sudo）       |

![](/home/yuzhendi/图片/2020-03-18 09-39-57 的屏幕截图.png)

![](/home/yuzhendi/图片/2020-03-18 09-41-59 的屏幕截图.png)

![](/home/yuzhendi/图片/2020-03-18 09-43-54 的屏幕截图.png)

![](/home/yuzhendi/图片/2020-03-18 09-44-58 的屏幕截图.png)

（如果要给一个组密码，则需要添加管理员使其可以修改密码）

### CHSH 更改用户SHELL

```shell
chsh -s Shell <username>
```

![butuijian](/home/yuzhendi/图片/2020-03-18 09-48-23 的屏幕截图.png)

（不推荐直接到passwad文件里直接修改文件）

### 用户管理相关的命令

|  命令   |     说明      |  命令   |        说明        |
| :-----: | :-----------: | :-----: | :----------------: |
|   su    |   切换用户    |  sudo   | 临时切换成root用户 |
| passwd  | 设定用户密码  | gpasswd |    设定群组密码    |
|  chsh   | 更改用户shell | usermod |    修改用户账号    |
| useradd |   新建用户    | userdel |      删除用户      |
|   id    | 显示用户信息  |         |                    |

SU 切换用户

```shell
su [-lmpfc] <username>
```

```
- | -l :重新登陆
-m | -p :不更改环境变量
-c comand: 切换后执行命令
```

