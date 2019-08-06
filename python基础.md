# python基本数据类型：

1，number类型

a,int类型

b,float类型

c,复数，complex（a,b）

2，字符串类型

用单引号或者双引号括起来的任意字符

3，bool类型

只有Ture和False两种类型

4，None类型

None是python中特殊的类型，表示一个空值

5，list类型

本质上是一个有序的集合

6，tuple类型

本质上是一个有序的集合，一旦初始化就不能改变，当tuple中只有一个元素的时候需要在这个元素后加个逗号消除歧义

7，dict字典类型

在其他语言中称为map集合，以key—value的方式储存

key不可变，value可变

8，set集合

不存在重复的值；

值不可变，在set集合中不可能出现list，dict，set

# 方法：

type（）查看变量的数据类型

id（）查看变量的地址

python特有赋值方法交叉赋值

如：name，age = “lili”，18

name，age = age，name

类型转换：

1，int（）

2，float（）

3，str（）

4，set（）

5

常用方法：

1，abs（）返回绝对值

2，max（）返回最大值

3，min（）返回最小值

4，pow（x，y）返回x的y次幂

5，round（x，n）返回浮点数的四舍五入小数的n位数默认为0

6，range（x，y，z）从x以步长为z到y的可迭代对象

### 7，字符串方法

字符串的编码：

u/U:表示unicode字符串 
不是仅仅是针对中文, 可以针对任何的字符串，代表是对字符串进行unicode编码。 
一般英文字符在使用各种编码下, 基本都可以正常解析, 所以一般不带u；但是中文, 必须表明所需编码, 否则一旦编码转换就会出现乱码。 
建议所有编码方式采用utf8

r/R:非转义的原始字符串 
与普通字符相比，其他相对特殊的字符，其中可能包含转义字符，即那些，反斜杠加上对应字母，表示对应的特殊含义的，比如最常见的”\n”表示换行，”\t”表示Tab等。而如果是以r开头，那么说明后面的字符，都是普通的字符了，即如果是“\n”那么表示一个反斜杠字符，一个字母n，而不是表示换行了。 
以r开头的字符，常用于正则表达式，对应着re模块。

b:bytes 
python3.x里默认的str是(py2.x里的)unicode,  bytes是(py2.x)的str, b”“前缀代表的就是bytes 

python2.x里, b前缀没什么具体意义， 只是为了兼容python3.x的这种写法





1，“，”逗号位置会产生空格

2，“+”数据必须相同

3，“%”格式化输出

4，“”.join(l) 序列中的元素必须为字符串

5，str*n将str重复输出n次

6，str[x:y:z]截取字符串x默认为0，y默认为末尾，z默认为1

x不写默认为0，y必须写，z默认为1

7，evel（）将str类型转为有效的表达式并计算结果

8，len（）返回字符长度



常用数学模块math

ceil（）向上取整

floor（）向下取整

modf（）返回小数部分和整数部分以元组的方式返回

sqrt（）开平方

常用数学模块random

choice（序列）随机返回一个序列（元组或列表）中的元素

randrange（x，y，z）随机返回一个从x开始以步长为z到y（取不到y）结束序列的元素默认为1

random返回[0,1)的浮点数

shuffle（序列）；打乱序列的次序

uniform（m，n）；返回一个从[m，n]的浮点数

# 运算符：

%：取模，返回除法余数

x**y：返回x的y次幂

//；取整

比较运算符

==，！=，<，>，<=,>=

赋值运算符

+=，-=，*=，/=，%=，**=，//=，

逻辑运算符

and，or，not

位运算符

&，|，^，~，<<，>>

进行运算时转为二进制进行

成员运算：

in是否存在于序列

not in

身份运算符：

is是否引用于同一对象

not is

分支语句：

单分支：

if 条件：

	语句块

双分支

if  条件：

	语句块1

else：

	语句块2

多分支语句

if  条件1:

	语句块1

elif  条件2：

	语句块2

..........

else:

	语句块

在判断过程中取值为假的：0，False，None，“”，[]，{}，（）

循环：

1.while  条件：

	循环体

2.for  i   in   可迭代对象：

	循环体

3.for  i in 可迭代对象：

	循环体

else：------非正常结束

	语句块

在循环中用break为结束循环，continue跳出本次循环



迭代器：

通过iter()方法获得了list的迭代器对象，然后就可以通过next()方法来访问list中的元素了。当容器中没有可访问的元素后，next()方法将会抛出一个StopIteration异常终止迭代器

生成器：

如果列表元素可以按照某种算法推算出来，那我们是否可以在循环的过程中不断推算出后续的元素呢？这样就不必创建完整的list，从而节省大量的空间。在Python中，这种一边循环一边计算的机制，称为生成器（Generator）

闭包概念：

一个函数定义中引用了外函数定义的变量，并且该函数可以在其定义环境外被执行。这样的一个函数我们称之为闭包。实际上闭包可以看做一种更加广义的函数概念。因为其已经不再是传统意义上定义的函数

一般情况下，如果一个函数结束，函数内部所有的东西都会被释放掉，还给内存，局部变量也会消失，但是闭包是一种特殊情况，如果外函数在结束时发现有自己的临时变量将来还会在内函数中用到，就把这个临时变量绑定给内函数，然后再自己结束

python魔法命令：

```python
1.__new__(cls):有一个参数self,就是这个`__new__(cls)`返回来的实例,所以我们可以很好的理解，调用`__new__()`方法来进行创建对象，这个new方法可以是object的，也可以是自己重写的，最后必须要return这个创建好的对象的引用既：return object.__new__(cls)而__new__()只负责创建对象，__init__()对创建好的对象进行初始化。
2.__init__(self[, ...])：构造器，当一个实例被创建的时候调用的初始化方法
3.__del__(self)：析构器，当一个实例被销毁的时候调用的方法
4.__call__(self[, args...])：允许一个类的实例像函数一样被调用：x(a, b) 调用x.__call__(a, b),一般在类装饰器中常用
5.__getattr__(self, name)：定义当用户试图获取一个不存在的属性时的行为，_getattr__是python里的一个内建函数，可以很方便地动态返回一个属性；当调用不存在的属性时，Python会试图调用__getattr__(self,'key')来获取属性，并且返回key；
6.__getattribute__(self, name)：定义当该类的属性被访问时的行为
7.__setattr__(self, name, value)：定义当一个属性被设置时的行为
8.__delattr__(self, name)：定义当一个属性被删除时的行为
9.__set__(self, instance, value)：定义当描述符的值被改变时的行为
10.__get__(self, instance, owner)：定义当描述符的值被取得时的行为
```

python的常用原生库：

```python
pickle,os,time,urllib,re,socket,thread,math,datetime,sys
```

--init--,--new--,--del--,--str--,--call--,--getattr--,--setattr--,--get--,--set--,--delattr--

os,sys,random,math,re,socket,urllib,time,datetime,threading,multiprocessing,asyncio

ls,mkdir,rm,mv,touch,cat,vim,unzip,gzip,zip,chmod,kill,ps,grep,rename,pwd,who,tar,rmdir,head,less,more

列表合并：extend

字典如何删除键和合并两个字典：删除键del dict['a']    合并字典dict1.update(dict2)

python的垃圾回收机制

引用计数，标记清除，分代回收

分代回收：将数据分为三类，

类装饰器

```python
class log():
    def __init__(self,func):
        print('__init__')
        func()
        self.func = func
	def __call__(self):
        #self.func(*args,**kwargs)
		print('__call__')
@log
def foo(x,y):
    print('Hi')
    return ''
foo()
# 执行结果
# __init__
# Hi
# __call__
```

数据优化

```python
数据库优化方案
1 查询的时候不要使用select *
2.尽量使用limit 1 取得唯一的一行
3.尽量使用索引字段进行查询
4 可以使用覆盖索引加速查询  （一个索引包含了查询结果中所有的字段）
5 尽量少用like 或者or
6 不要使用全文索引，如果非要使用可以把全文索引独立出来，建立全文索引服务器
7 关联查询的时候，关联的字段都应该有索引
8 不要使用!=操作，不使用索引
9 查询的时候类型不匹配不使用索引
10 联合索引不带左前缀，不使用索引
11 尽量减少子查询，可以使用关联查询代替子查询
    select count(*) from article where uid in(select uid from user where id=10)
    select count(*) from aticle,user where user.id = aticle.uid   and user.id=10
    select count(*) from aticle join user on user.id=article.uid  where userid.id=10
12 尽量多试验不同sql语句，比较他们的效率，采用最少
13 不要在where中，运算符左边运算,只要是计算，不采用索引
    select username from user where age/2>10
14 不要在where中，运算符左边不要出现任何函数,否则不采用索引
   select COUNT(*) from user where year(birthday) == 1993;
15 不要对null判断 ，否则不使用索引
16 避免默认排序
    select cid,count(*) from bbs group by cid
    select cid,count(*) from bbs group by cid order by null #不排序
在应用层面可以nosql技术，把数据保存redius、memcached中加速查询
从架构方面：读写分离
可以使用mysql分区技术，把一个表分为多个文件
分库分表分机器
把表进行垂直切分，或水平切分
```

sort与sorted的区别

sort修改原列表

sorted不修改原列表

```python
foo = [{'name':'ss','age':22},{'name':'zs','age':21}]
a = sorted(foo,key=lambda x:(x["age"],x["name"]),reverse=True) # reverse=True从大到小,当年龄一样时按字母排序
```

字典和json相互转化的方法

```python
dic = {'name':'sz'}
res = json.dumps(dic)--->json
ret = json.loads(res)---->dict
```

求两个列表的交集，差集，并集

```python
a = [1,2,3,4]
b = [3,4,5,6]
jj1 = list(set(a).intersection(set(b))) # 交集
jj2 = list(set(a).union(set(b))) # 并集
jj3 = list(set(a).difference(set(b))) # a中有而b中没有的 ，差集
```

py2和py3最主要的区别

1.打印语句的不同

py2 print ‘aaa’

py3 print('aaa')

2.编码的不同

py2默认采用ASCII编码，在编码中文时会带来编码错误问题

py3默认采用utf-8编码

3.True和False的改变

py2 True和False为全局变量可以随意赋值

py3 True和False为两个关键字不能随意赋值

如何引用上级目录

```bash
import sys
sys.path.append("/test/test") # 使用append修改环境变量的目录，为上一级目录
import t1
print t1.t1()
```

##### 使用生成器读取文件

```python
def readmylines(f,newline):
    buf = ""
    while True:
        while newline in buf:
            pos = buf.index(newline)#找到字符的位置
            yield buf[:pos]
            buf = buf[pos+len(newline):]

        chunk = f.read(4096*5)#读取相应的字符长度
        if not chunk:
            #说明已经读到文件结尾
            yield buf
            break
        buf += chunk
# type(readmylines(f,'||'))
with open("./data.csv",encoding='utf-8') as f:
    #假设以||分割段落
    for line in readmylines(f,' '):
        print('aa')
        print(line)
```

#### 单例模式（Singleton Pattern）

是一种常用的软件设计模式，该模式的主要目的是确保**某一个类只有一个实例存在**。当你希望在整个系统中，某个类只能出现一个实例时，单例对象就能派上用场。

实现单例模式的几种方法

##### 1.使用模块

```python
其实，Python 的模块就是天然的单例模式，因为模块在第一次导入时，会生成 .pyc 文件，当第二次导入时，就会直接加载 .pyc 文件，而不会再次执行模块代码。因此，我们只需把相关的函数和数据定义在一个模块中，就可以获得一个单例对象了。如果我们真的想要一个单例类，可以考虑这样做
class Singleton(object):
    def foo(self):
        pass
singleton = Singleton()
将上面的代码保存在文件 mysingleton.py 中，要使用时，直接在其他文件中导入此文件中的对象，这个对象即是单例模式的对象
from a import singleton
```

##### 2.使用装饰器

```python
python解释器的运行规则：
1.先定义一切类与变量与函数
2.运行py文件中的所有代码
由上可知：
运行路径为:python是解释器语言所以先定义类A()与类中的变量与函数，既执行了print(a)--》运行所有代码既先执行装饰器中的print('s')----》用A实例化对象为a1，运行装饰器既执行Singleton(A(object))中的_singleton函数，然后将类赋值给a1
def Singleton(cls):
    _instance = {}
    print('s')
    def _singleton(*args, **kargs):
        if cls not in _instance:
            _instance[cls] = cls(*args, **kargs)
            print(_instance)
        return _instance[cls]

    return _singleton

@Singleton
class A(object):
    a = 1
    print(a)

    def __init__(self, x=0):
        self.x = x
        print(x)

a1 = A(2)
a2 = A(3)
```

函数传参时：传可变参数为引用，不可变参数为拷贝

##### 进程，线程和协程

进程是程序最小的执行单位，资源占用大(M)，数据通信不方便，操作系统按时间片进行切换，不够灵活

线程是最小的调度单位，资源占用小(k) , 数据通信非常方便，按时间片切换，不够灵活，比较快

协程是微线程 ，资源占用非常小(bytes) , 非常方便, 根据事件IO进行切换，能更加有效的利用cpu

##### python的自省函数：

1、help()

用来查看很多Python自带的帮助文档信息。

2、dir()

可以列出对象的所有属性。

3、type()

返回对象的类型。

4、id()

返回对象的“唯一序号”。对于引用对象来说,返回的是被引用对象的id()。

5、hasattr()和getattr()

分别判断对象是否有某个属性及获得某个属性值。

6、callable()

判断对象是否可以被调用。

7、isinstance()

可以确认某个变量是否有某种类型



##### WSGI,uWSGI,ngnix,uwsgi

Django 是一个 Web 框架，框架的作用在于处理 request 和 reponse，其他的不是框架所关心的内容。所以怎么部署 Django 不是 Django 所需要关心的。Django 所提供的是一个开发服务器，这个开发服务器，没有经过安全测试，而且使用的是 Python 自带的 simple HTTPServer 创建的，在安全性和效率上都是不行的,而uWSGI 是一个全功能的 HTTP 服务器，他要做的就是把 HTTP 协议转化成语言支持的网络协议。比如把 HTTP 协议转化成 WSGI 协议，让 Python 可以直接使用。
uwsgi 是一种 uWSGI 的内部协议，使用二进制方式和其他应用程序进行通信

WSGI是一种WEB服务器  ==网关接口==。 是一个Web服务器（如nginx）与应用服务器（如uWSGI）通信的一种规范（协议）。

uWSGI实现了WSGI的所有接口，是一个快速、自我修复、开发人员和系统管理员友好的服务器。uWSGI代码完全用C编写，效率高、性能稳定。

