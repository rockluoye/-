shell：就是将linux命令逻辑化处理 

创建扩展名    touch   命名.sh

写入使用vim打开

执行方式./命名.sh

或/bin/bash 命名.sh

开头语句

#！/bin/bash

变量定义：

如：name=“zhangsan”

输出：echo $name    或   echo ${name}

也可以：echo   “his name  is ${name}”

只读变量

readonly:例

url=“http：//www.baidu.com”

readonly  url

删除变量

unset   例：

unset   url

字符串：

单引号：中任何字符串都会原样输出切字符串中不能出现单引号

双引号：包含除$,\,''之外的任意字符，还可转义

数组：只支持一维数组，，不支持多维数组

下标是从0开始的

定义格式：数组名=（值1 值2 .......）

例：

arr=（1 5 6 9 7）

echo $arr       输出为1

读取数组中的元素

echo   ${arr[2]}

读取数组中全部元素

echo   ${arr[@]}

读取数组中长度

echo   ${#arr[@]}或echo   ${arr[*]}

运算符

例：val=‘expr  1 + 2’

关系运算符:  -eq---等于  -gt---大于   -ne---不等于  -lt---小于   -ge---大于等于  -le---小于等于

例：if [ $a  -eq $b]

then

	echo ""

else  

	echo ""

文件检测：-r例：if[-r $file]

-e   开启转义

\n换行

\c空格

printf

例：printf   “%-10s %-8s %-4s\n”

printf   “%-10s %-8s %-4.2f\n”

%d  %s $f都是格式替换符

-10s为宽度为10

-4.2f为宽度为4，保留小数后两位

数值测试   test

例：if   test  $[num1]  -eq   $[num2]

字符串测试

例：if   test  $[num1]  =   $[num2]

分支语句：

多分支：

if  []

then

​	echo ""

elif   []

then

​	echo ""

elif   []

then

​	echo ""

else

case语句：

read aNum

case   $aNum  in

​	(1)   echo""

​	(2)     echo  “”

​	........

esac

循环

for num in 1 2 3 4 5 

do

​	echo "$num"

done

遍历数组

a=（1 2 3）

for x in ${a[*]}

do

​	echo  ''$x"

done

函数：

定义：

demo（）

{

​	echo “”

​	return  $((1+2+3))

}

调用函数

demo

返回值：

demo

echo $?

传参

demo（）

{

​	echo $1---------- 第一个参数

​	echo $2----------第二个参数

​	echo $#---------参数长度

​	echo $*----------所有参数

}

demo   1  2  3 