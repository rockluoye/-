面试题：

[http://python.jobbole.com/85231/](http://python.jobbole.com/85231/)

https://zhuanlan.zhihu.com/p/54430650

https://juejin.im/post/5b6bc1d16fb9a04f9c43edc3

https://www.jianshu.com/p/276adac5eb6a

https://github.com/kenwoodjw/python_interview_question



过程：

1.安装

2.创建用户 + 授权

3.连接
	-数据库
		终端创建数据库（字符编码）
	-数据表
		终端
		ORM
		pymysql
			create   。。）engine=innodb
	-数据行
		增，删，改，查
			-limit
			-group by
4.关闭

字符串中：r/R:非转义的原始字符串，b:bytes ，u/U:表示unicode字符串



问题：简述ORM原理

1.什么是ORM

ORM的全称是Object Relational Mapping，即对象关系映射。它的实现思想就是将关系数据库中表的数据映射成为对象，以对象的形式展现，这样开发人员就可以把对数据库的操作转化为对这些对象的操作。因此它的目的是为了方便开发人员以面向对象的思想来实现对数据库的操作

也可以说通过类和对象转化为SQL语句，然后用pymysql来进行连接

2.使用ORM

```python
class User(Model):
    id = IntegerField('uid')
    name = StringField('username')
    email = StringField('email')
    password = StringField('password')

u = User(id=12345, name='Michael', email='test@orm.org',password='my-pwd')
u.save()
```

Http就是无状态的短连接

TCP：不断开

### Web应用（网站）流程：

浏览器（socket客户端）
 	2.  sk.socket()
            sk.connect(“端口”)
             sk.send(数据)
      5.接收
      6.连接断开
      socket服务端（网站）
      1.监听ip和端口
      	while True：
      		3.收到“数据”
      		4.响应：返回数据给用户
      		用户断开

```python
import socket


def f1():
    return b'f1'


def f2():
    return b'f2'

routers = [
    ('/xxxx',f1),
    ('/oooo',f2),
]


def run():
    sock = socket.socket()#创建对象
    sock.bind(('127.0.0.1',8080))#绑定IP和端口
    sock.listen(5)#设置监听数量


    while True：
        conn,addr = sock.accept()#接收数据
        data = conn.recy(8096)
        data = str(data,encoding='utf-8')#转为字符串类型
        bytes('字符串'，encoding='utf-8')#转为字节类型
        headers,bodys = data.split('\r\n\r\n')#以换行符分割
        temp_list = headers.split('\r\n')
        method,url,pprotocal = temp_list[0].split(' ')
		
        func_name = None
        for item in routers:
            if item[0] == url:
                func_name = item[1]
                break
                
        if func_name:
            response = func_name()
        else:
            responese = b'404'
            
         
        conn.send(responese)
        conn.close()
        
if __name__ == '__main__':
    run()
```

Django
1.配置

。模板路径

。静态文件

。CSRF注释

函数：

def index（request）：

	request.method()
	
	request.GET
	
	request.POST
	
	return HttpResponse(..)
	
	return render(request,"模板路径"，{})
	
	return redirect（“URL”）

## Django虚拟环境创建与项目创建：

cd 到env文件夹

执行命令：

virtualenv  --no-site-packages  -p  D:\python3_6_5\python.exe  djangoenv

cd Scripts

activate

pip install django==2.0.7--------安装django2.0.7版本

cd 到要建立项目地址

django-admin  startproject  day01-----创建day01项目

在pycharm中seting中加载虚拟环境

python manage.py runserver----启动django

创建应用：python manage.py  startapp app----创建app应用

ip端口的修改：

python manage.py runserver  0.0.0.0:8080

也可以python manage.py runserver  8080

脚本中：runserver  8080

若为runserver默认端口为8000

数据库的配置

在seting中，写配置

```python
DATABASES ={
    "default":{
        "ENGINE":"django.db.backends.mysql",
        "NAME":"szdjango",#数据库名
        "USER":"root",#账号
        "PASSWORD":"123456",#密码
        "HOST":"127.0.0.1",#ip
        "POST":3306  #端口
    }
}
```

安装包：pip install pymysql

在\_\_init\__中:

import pymysql

pymysql.install_as_MySQLdb()--------------加载mysql数据库驱动

迁移命令：python manage.py migrate----将模型映射成表

python  manage.py  makemigrations  app----应用initial.py生效，强行迁移 

python manage.py migrate-----执行迁移文件

migrate指令是用migrations目录中代码文件和django[数据库](http://lib.csdn.net/base/mysql)djaong_migrations表中的代码文件做对比，如果表中没有，那就对这些没有的文件按顺序及依赖关系做migrate apply，然后再把代码文件名加进migrations表中。



## 创建虚拟环境：

virtualenv  --no-site-packages  -p  D:\python3_6_5\python.exe 环境名称

activate激活虚拟环境

在环境中安装：pip  install  django==2.0.7

在激活的虚拟环境中创建项目，在激活环境的情况下进入存放文件的目录，执行下面命令

django-admin  startproject  项目名称

用pycharm打开文件，选择好虚拟环境

在Terminal中执行以下命令

创建应用：python manage.py startapp  应用名

便可启动文件了，进入服务界面

启动方式：

1.python  manage.py  runserver 端口

2.python manage.py runserver  IP:端口

修改数据库的配置

```python
DATABASES ={
    "default":{
        "ENGINE":"django.db.backends.mysql",
        "NAME":"szdjango",#数据库名
        "USER":"root",#账号
        "PASSWORD":"123456",#密码
        "HOST":"127.0.0.1",#ip
        "POST":3306  #端口
    }
}
```

在工程目录的init文件中导入pymysql

```python
import pymysql
pymysql.install_as_MySQLdb()
```

可以导入自定义模型，便不需要手动去创建模型

进行迁移命令-----python  manage.py  migrate

在数据库中刷新便可以看见表了

创建超级管理员python  manage.py  createsuperuser对表进行修改

可以通过/admin/路由进入管理员后台

### 创建模型

在应用中的models中创建模型

```python
from django.db  import  models

class Article(models.Model):
    title = models.CharField(max_length=10, unique=True, null=False)
    desc = models.TextField(null=False)
    class Meta:
    	db_table = 'article'
```

CharField为可变字符类型，TextField为长文本类型，class Meta：db_table = 'article'为定义表名

创建模型之后进入工程目录的settings中，在INSTALLED——APPS中添加元素“app”

生成迁移中间记录文件----python  manage.py  makemigrations 

生成迁移表----python  manage.py  migrate

模型字段定义

模型字段定义



##### 模型字段定义

IntegerField()---定义数字类型

verbose_name=""---字段别名

default=‘20’-----设置默认值为20

DateTimeField(auto_now_add=True)---定义日期格式字段,创建数据时，默认赋予创建时间

DateTimeField(auto_now=True)修改数据时，默认赋予修改时间

TimeField：时间戳类型

ImageField：图片图片类型

DecimalField：有限制小数点后几位的浮点数类型

FloatField：浮点数类型

BooleanField：布尔类型

AutoField：自增元组类型

DecimalField():精确字段类型

在setting中定义路由：

```python
from django.contrib import admin
from django.urls import path
from app.views import hello

urlpatterns = [
    path('admin/', admin.site.urls),
    path('hello/', hello),
]
```

hello为定义的方法

在views中定义方法

```python
from django.shortcuts import render
from django.http import HttpResponse


def hello(request):
    return HttpResponse('hello django')
```

新增数据操作

```python
from django.shortcuts import render
from django.http import HttpResponse

def aad_stu(request):
    stu = Student()
    stu.s_name = '小明'
    stu.save()
    return HttpResponse('创建学生信息成功')
```

查询数据操作

```python
def sel_stu(request):
    stus = Student.objects.filter(s_name='小明').all()
    stu = stus.first()
    return HttpResponse('查询数据成功')
```

查询的多种用法

```python
def sel_stu(request):
    #filter()
    stus = Student.objects.filter(s_name='小明').all()
    stu = stus.first()
    stu = Student.objects.filter(s_name='小华').first()
    # get(条件)
    #条件必须成立，否则报DoesNotExist的错
    #查询的结果必须唯一，，否则也会报错
    stu = Student.objects.get(id=3)
    #exclude(条件)  查询不满足条件的数据
    stus = Student.objects.exclude(s_age=18).all()
    #exists(条件)：判断查询条件是否有值，有值则返回true
    stus = Student.objects.filter(s_age=20).exists()
    #查询长度len(),count()
    stus = len(stus)
    stus = Student.objects.all().count()
    #values(),通过键值对取值性能较优，一般用此种方法取值
    #取id和s_name的值
    stus = Student.objects.all().values('id', 's_name')
    #order_by():排序
    stus = Student.objects.all().order_by('-id')#按id降序取值
    #模糊查询，contains---包含
    stus = Student.objects.filter(s_name__contains='小').all()
    #startswith---以什么开头
    stus = Student.objects.filter(s_name__startswith='小').all()
    #endswith---以什么结尾
    stus = Student.objects.filter(s_name__endswith='明').all()
    #大于gt  大于等于gte   小于lt   小于等于lte
    #在django中不存在 （>    <   >=   <=）
    stus = Student.objects.filter(s_age__gt=17).all()#大于
    # django  orm:  字段__in
    stus = Student.objects.filter(id__in=[1, 2])
    stus = Student.objects.exclude(id__in=[1, 2])
    #聚合  aggregate()
    stus = Student.objects.all().aggregate(Avg('s_age'))
    return HttpResponse('查询数据成功')
```

删除数据：

第一种：stu = Student.objects.filter(s_name='小明').first()

stu.delete()

第二种：Student.objects.filter(s_name='小明').delete()

#### 模板渲染

在工程项目中的settings文件下的TEMPLATES中的‘DIRS’中设置

[os.path.join(BASE_DIR, 'templates')]-------模板路径

对模板进行渲染---render(request, 'index.html')

挖坑和填坑：{% block  title %}{% endblock %}

继承：{% extends  ‘base.html’ %}

继承父模版中内容： {{  block.super  }}

传参给模板：render(request, 'index.html', { 'stus': stus, 'key':value })

解析参数：  {{ stus }}

循环：{% for  stu  in  stus %}{% endfor %}

判断：{%  if  stu.s_age  >  20  %}{% endif %}

判断相等：{% ifequal  stu.s_name  '小明' %}{% endifequal %}

过滤标签：{{ content_h2  |  safe }}

设置静态文件位置，在settings中的STATIC_URL = '/static/'下，加上

STATICFILES_DIRS = [os.path.join(BASE_DIR, 'static'),]

第一种导入静态文件方法<link rel='stylesheet' href='/static/css/style.css'>

第二种导入文件的方法<link rel='stylesheet' href="{% static 'css/style.css' %}”>

## linux中创建django项目

常见的Web框架的介绍

Flask：微框架

Tornado：支持异步操作

Django：重量级框架

Sanic：python3.6+，使用asyncio的异步web框架

Bottle：超微框架，单文件，4000多行代码

django官网：https://www.djangoproject.com

官方文档：https://docs.djangoproject.com/en/1.11/

1.查看python解释器python3是否存在版本：mkvirtualenv  -p  ~/anaconda3/bin/python3

2.用virtualenv在家目录创建虚拟环境：virtualenv  -p ~/anaconda3/bin/python3.6    ~/.virtualenvs/django

3.激活虚拟环境：source ~/.virtualenvs/django/bin/activate

4.安装django包：pip install django==1.11.20

5.在激活环境的情况下创建工程项目，在激活环境的情况下进入存放文件的目录，执行下面命令

django-admin  startproject  项目名称

6.用pycharm打开并选择好创建的虚拟环境

7.创建迁移文件：python manage.py migrate

8.创建超级用户：python manage.py createsuperuser，然后输入用户名和密码，我创建的是admin，密码：password23

9.创建应用文件：python manage.py startapp myapp---应用名称

10.在settings文件中的INSTALLED_APPS加入'myapp.apps.MyappConfig',   来集成应用

11.在urls文件中的urlpatterns中，注册路由，添加url(r'^hello/$', views.hello),   是注册一个hello的路由

12.在views文件中写函数

```python
from django.shortcuts import render
from django.shortcuts import HttpResponse

def hello(request):
    return HttpResponse('hello django')
```

13.时区问题

USE_TZ = False------表示使用系统设置时区时间作为项目的时间

USE_TZ  = True-------表示使用格林威治时间（UTC）作为项目时间

14.语言设置：LANGUAGE_CODE = 'zh_hans'--------设置为中文简体

15.设置系统时间：TIME_ZONE = 'Asia/Shanghai'----设置为亚洲上海时间

16.根路由问题：2.0以上：

```python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    # path('admin/', admin.site.urls),
    path('user', include('user.urls'), namespace='user'),
]
```

1.11版本：

```python
from django.contrib import admin
from django.urls import url, include

urlpatterns = [
    # path('admin/', admin.site.urls),
    url(r'^user', include('user.urls'), namespace='user'),
]
```



#### 模型的创建

```python
from django.db import models

class Student(models.Model):
    name = models.CharField(max_length=16)
    age = models.IntegerField(default=1)
	created_at = models.DateTimeField(auto_now_add=True)
    def __str__(self):  #函数重写
        return 'student({},{},{})'.format(self.id, self.name, self.age)
	class Meta:
    	db_table = 'syudent'   #设置表名
```
##### 常见字段选项：

verbose_name:字段别名

max_length:最大长度

unique：唯一约束

null：是否为空

default：默认值

auto_now_add：创建时，设置为当前时间

auto_now:更新时，设置为当前时间

##### 字段类型

| 类型                  | 说明                                                         |
| --------------------- | ------------------------------------------------------------ |
| AutoField             | 自增ID字段                                                   |
| BigIntegerField       | 64位有符号整数                                               |
| BinaryField           | 存储二进制数据的字段，对应Python的bytes类型                  |
| BooleanField          | 存储True或False                                              |
| CharField             | 长度较小的字符串                                             |
| DateField             | 存储日期，有auto_now和auto_now_add属性                       |
| DateTimeField         | 存储日期和日期，两个附加属性同上                             |
| DecimalField          | 存储固定精度小数，有max_digits（有效位数）和decimal_places（小数点后面）两个必要的参数 |
| DurationField         | 存储时间跨度                                                 |
| EmailField            | 与CharField相同，可以用EmailValidator验证                    |
| FileField             | 文件上传字段                                                 |
| FloatField            | 存储浮点数                                                   |
| ImageField            | 其他同FileFiled，要验证上传的是不是有效图像                  |
| IntegerField          | 存储32位有符号整数。                                         |
| GenericIPAddressField | 存储IPv4或IPv6地址                                           |
| NullBooleanField      | 存储True、False或null值                                      |
| PositiveIntegerField  | 存储无符号整数（只能存储正数）                               |
| SlugField             | 存储slug（简短标注）                                         |
| SmallIntegerField     | 存储16位有符号整数                                           |
| TextField             | 存储数据量较大的文本                                         |
| TimeField             | 存储时间                                                     |
| URLField              | 存储URL的CharField                                           |
| UUIDField             | 存储全局唯一标识符                                           |

####字段参数(选项)

| 选项           | 说明                                                         |
| -------------- | ------------------------------------------------------------ |
| null           | 数据库中对应的字段是否允许为NULL，默认为False                |
| blank          | 后台模型管理验证数据时，是否允许为NULL，默认为False          |
| choices        | 设定字段的选项，各元组中的第一个值是设置在模型上的值，第二值是人类可读的值 |
| db_column      | 字段对应到数据库表中的列名，未指定时直接使用字段的名称       |
| db_index       | 设置为True时将在该字段创建索引                               |
| db_tablespace  | 为有索引的字段设置使用的表空间，默认为DEFAULT_INDEX_TABLESPACE |
| default        | 字段的默认值                                                 |
| editable       | 字段在后台模型管理或ModelForm中是否显示，默认为True          |
| error_messages | 设定字段抛出异常时的默认消息的字典，其中的键包括null、blank、invalid、invalid_choice、unique和unique_for_date |
| help_text      | 表单小组件旁边显示的额外的帮助文本。                         |
| primary_key    | 将字段指定为模型的主键，未指定时会自动添加AutoField用于主键，只读。 |
| unique         | 设置为True时，表中字段的值必须是唯一的                       |
| verbose_name   | 字段在后台模型管理显示的名称，未指定时使用字段的名称         |

ForeignKey 字段选项

1. limit_choices_to：值是一个Q对象或返回一个Q对象，用于限制后台显示哪些对象。
2. related_name：用于获取关联对象的关联管理器对象（反向查询），如果不允许反向，该属性应该被设置为`'+'`，或者以`'+'`结尾。
3. to_field：指定关联的字段，默认关联对象的主键字段。
4. db_constraint：是否为外键创建约束，默认值为True。
5. on_delete：外键关联的对象被删除时对应的动作，可取的值包括django.db.models中定义的：
   - CASCADE：级联删除。
   - PROTECT：抛出ProtectedError异常，阻止删除引用的对象。
   - SET_NULL：把外键设置为null，当null属性被设置为True时才能这么做。
   - SET_DEFAULT：把外键设置为默认值，提供了默认值才能这么做。

ManyToManyField 字段选项

1. symmetrical：是否建立对称的多对多关系。
2. through：指定维持多对多关系的中间表的Django模型。
3. throughfields：定义了中间模型时可以指定建立多对多关系的字段。
4. db_table：指定维持多对多关系的中间表的表名。

####模型元数据选项

| 选项                  | 说明                                                         |
| --------------------- | ------------------------------------------------------------ |
| abstract              | 设置为True时模型是抽象父类                                   |
| app_label             | 如果定义模型的应用不在INSTALLED_APPS中可以用该属性指定       |
| db_table              | 模型使用的数据表名称                                         |
| db_tablespace         | 模型使用的数据表空间                                         |
| default_related_name  | 关联对象回指这个模型时默认使用的名称，默认为<model_name>_set |
| get_latest_by         | 模型中可排序字段的名称。                                     |
| managed               | 设置为True时，Django在迁移中创建数据表并在执行flush管理命令时把表移除 |
| order_with_respect_to | 标记对象为可排序的                                           |
| ordering              | 对象的默认排序                                               |
| permissions           | 创建对象时写入权限表的额外权限                               |
| default_permissions   | 默认为`('add', 'change', 'delete')`                          |
| unique_together       | 设定组合在一起时必须独一无二的字段名                         |
| verbose_name          | 为对象设定人类可读的名称                                     |
| verbose_name_plural   | 设定对象的复数名称                                           |

##### 数据库的配置

```python
DATABASES ={
    "default":{
        "ENGINE":"django.db.backends.mysql",
        "NAME":"szdjango",#数据库名
        "USER":"root",#账号
        "PASSWORD":"123456",#密码
        "HOST":"127.0.0.1",#ip
        "POST":3306  #端口
    }
}
```

##### 创建数据库

创建数据库时，要用create database  hello  charset  utf8mb4

utf8在mysql中占用3个字节，而utf8mb4在mysql中占用4个字节，是真正的UTF-8,在绘文字中utf8是不能显示出来的，而utf8mb4却能做到

##### 数据库驱动

在使用数据库驱动时mysqlclient性能较高，python3支持，编译安装依赖第三方库，生产环境推荐

pymysql为纯python代码编写，易安装，教学推荐，性能低下

python只支持mysqlclient或者MySQL-python所以在init文件中导入时将MySQL-python的代码改为pymysql

```python
import pymysql
pymysql.install_as_MySQLdb()
```

##### 模型迁移过程：

1.创建迁移文件：python manage.py makemigrations 应用名称--如：app

2.可查看迁移时数据库的创建表的过程：python  manage.py  sqlmigrate 应用名称  版本号--如：0001

3.迁移成表：python manage.py migrate

迁移过程中会自动生成id为主键

##### 数据的增加操作：

第一种方法：

```python
#实例化模型
s = Student()
s.name = 'tom'
s.age = 18
s.save()   #调用 django orm 自动为模型生成的数据库操作 api 来完成保存操作
```

第二种：

```python
Student(name='jake', age='18').save()
```

第三种：

```python
Student.objects.create(name='pony', age=23)
```

##### 数据的修改操作：

第一种：

```python
s = Student.objects.get(pk=1)
print(s.query)#django的sql语句
s.age = 25
s.save()
```

第二种：批量更新不会自动修改auto_now---修改时间

```python
Student.objects.filter(nama__startswith='tom').update(age=18)
```

##### 数据的删除操作：

第一种：

```python
s = Student.objects.get(pk=1)
s.delete()
```

第二种：批量删除

```
Student.objects.filter(age=20).delete()
```

第三种：全部删除

```python
Student.objects.all().delete()
```

#### 数据的查询操作

1.all()

```python
#SELECT * FROM students
s = Student.objects.all()
#SELECT * FROM students LIMIT 5
s = Student.objects.all()[:5]#取前五条数据
#SELECT * FROM students LIMIT 5 OFFSET 5
s = Student.objects.all()[5:10]#从5开始取5条

```

2.get()

```python
#返回存在的唯一一条记录
s = Student.objects.get(pk=1)
s = Student.objects.get(age=100)#取不存在的值会报错
s = Student.objects.get(age=19)#取存在多个值得时候会报错
```

3.filter

```python
s = Student.objects.filter(age=100)#不存在时会返回空列表
first():
s = Student.objects.filter(age=19).first()#返回查询列表的的第一个值
last():
s = Student.objects.filter(age=19).last()#返回查询列表的的最后一个值
#通过下标取值,会报IndexError，不支持-1下标访问
s = Student.objects.filter(age=19).[0]
```

4.exclude:支持下标操作

```python
s = Student.objects.exclude(age=19)#返回age不等于19的所有值

```

5.values():将QuerySet中的对象转换为字典,指定返回的字段

```python
#SELECT id, age FROM students WHERE age != 19
s = Student.objects.exclude(age=19).values('id', 'age')
```

6.执行原生sql语句,返回的是一个class，用for循环遍历来取出数据

```python
s = Student.objects.raw('SELECT id, age FROM students WHERE age != 19')
```

7.count();返回个数

```python
s = Student.objects.filter(age=19)
#取集合的长度，一般不用len()而用count(),len需要循环访问来得知长度性能低下
#SELECT COUNT(id) FROM students WHERE age=19
num = Student.objects.filter(age=19).count()
```

8.ordering:

```python
class Meta:
	db_table = 'students'
    ordering = ['-id']#按id降序排列，默认id升序
```

9.order_by():

```python
s = Student.objects.all().order_by('-created_at')#按创建时间倒序排列
```

10.exists():用于if判断是否存在

11.exact：精确查询与filter一样，get没有这个属性

```python
s = Student.objects.filter(age__exact=18)
s = Student.objects.filter(age=18)#与上面是相等的
```

12.contains:模糊查询中的包含

```python
#SELECT * FROM students WHERE name like '%tom%'
s = Student.objects.filter(name__contains='tom')
```

13.icontains:忽略大小写的模糊查询中的包含

```python
#SELECT * FROM students WHERE name like '%tom%'
s = Student.objects.filter(name__icontains='tom')
```

14.startswith:以什么开头的模糊查询，前面加i忽略大小写

```python
#SELECT * FROM students WHERE name like 'tom%'
s = Student.objects.filter(name__startswith='tom')
```

15.endswith:以什么结尾的模糊查询，前面加i忽略大小写

```python
#SELECT * FROM students WHERE name like '%tom'
s = Student.objects.filter(name__endswith='tom')
```

16.查找时间的时分秒

```python
s = Student.objects.filter(updated_at__minute=47)#查找创建时间为47分钟的记录
s = Student.objects.filter(updated_at__second=47)#查找创建时间为47秒的记录
#year/month/day/week_day/hour等
```

17.range：在两者间范围内的

```python
#SELECT * FROM students BETWEEN 18 AND 20
s = Student.objects.filter(age__range=(18, 20))
```

18.in：在什么中

```python
#SELECT * FROM students WHERE age IN (18, 26,30)
s = Student.objects.filter(age__in=(18, 26, 30))
```

19.gte：大于等于，gt:大于，lte:小于等于，lt：小于

```python
#SELECT * FROM students WHERE age >= 28
s = Student.objects.filter(age__gte=28)
```

20.聚合函数aggregate(Max()):返回的是字典 

```python
#SELECT MAX(age) FROM students
#还有Avg()，Sum()，Count()
max_age = Student.objects.aggregate(Max('age'))
count_age = Student.objects.filter(age__lte=20).aggregate(Count('age'))
```

21.F()对两个不同字段的比较，F('java')将字段取出进行比较，F对象可以进行算数运算

```python
s = Student.objects.filter(python__gt=F('java') + 5)#对python和java进行比较
```

用F对象来更新

```python
Student.objects.all().update(java=F('python') + 1)
```

用F对象来判断时间

```python
s = Student.objects.filter(update_at__gt=F('created_at') + timedelta(days=1))#也可以是minute，second...
```

22.Q():实现关系运算符

- or：|

  ```python
  s = Student.objects.filter(Q(age=18) | Q(python__gt=80))
  ```

- and:  ,   &

  ```python
  s = Student.objects.filter(Q(age=18), Q(python__gt=80) & Q(java__gt=70))
  s = Student.objects.filter(Q(age=18), python__gt=80)
  ```

- not:~

  ```python
  s = Student.objects.filter(~Q(age=18))
  ```


#### 表关系操作

##### 一对一：

模型一：

```python
class Student(models.Model):
    name = models.CharField(verbose_name='姓名'， max_length=16, unique=true, null=True)
    age = models.IntegerField(default=0)
    python = models.IntegerField(default=0)
    java = models.IntegerField(default=0)
    #在记录创建时，自动为 created_at 字段的值设置为当前时间
    created_at = modelsDateTimeField(auto_now_add=True)
    #在记录更新时，自动为 updated_at 字段的值设置为当前时间
    updated_at = modelsDateTimeField(auto_now=True)
    #OneToOneField(关联模型， on_dalete=删除策略)：申明为一对一关系
    #models.CASCADE：级联删除
    #字段名称为：实例名_id,以下字段名为:student_info_id
    student_info = models.OneToOneField('StudentInfo', on_dalete=models.CASCADE, null=True)
    #自定义表名，若无定义，表名为Student
    class Meta:
        db_table = 'student'
        ordering = ['id']
```

模型二：

```python
class StudentInfo(models.Model):
    phone = models.CharField(max_length=11, unique=True)
    class Meta:
        db_table = 'student_infos'
```

将两字段建立关联：

```python
student_info = StudentInfo.objects.create(phone='123')
tom = Student.objects.get(name='tom')
#第一种
tom.student_info = student_info
tom.save()
#第二种：
tom.student_info_id = student_info.id
tom.save()
#第三种：
tom.student_info_id = 1
tom.save()
```

通过表一查表二数据

```python
tom_phone = Student.objects.get(name='tom').student_info.phone
```

通过表二查表一数据

```python
phone_name = StudentInfo.objects.get(phone = '123').student.name
```

修改一对一关系

```python
phone = StudentInfo.objects.get(phone=123)
tom = Student.objects.get(name='tom')
tom.student_info = None
phone.save()

jack = Student.objects.get(name='jack')
jack.student_info = phone
jack.save()
```

在级联删除模式下，删除表一记录或表二记录的影响

```python
#在删除主表（表一）一方数据时，表二数据不受影响
jack = Student.objects.get(name='jack')
jack.delete()
#删除扩展表（表二）一方数据时，主表（表一）数据被级联删除
phone = StudentInfo.objects.get(phone='123')
phone.delete()
```

on_delete=models.SET_NULL策略时：

1.在删除主表（表一）一方数据时，表二数据不受影响

2.删除扩展表（表二）一方数据时，主表（表一）记录中的关系为null

##### 一对多：

表三：

```python
class Grade(models.Model):
    name = models.CharField(max_length=32, unique=True)
    class Meta:
        db_table = 'grades'
```

在表一中加入：grade = models.ForeignKey(Grade, on_delete=models.PROTECT, null=True)--------通过外键方式，声明一对多关系，删除策略为：models.PROTECT

ForeignKey(关联模型，on_delete=删除策略)，注意：ForeignKey定义的字段表示多的对方，只能放在多的模型中

在模板中一查多

quest.choice_set.all

创建一对多关系

通过多的一方建立关联：

```python
jack = Student.objects.get(name='jack')
python = Grade.objects.get(name='python-1902')
jack.grade = python
jack.save()
```

通过少的一方(表三)建立关联：通过一的一方操作多的一方数据， django会自动生成一个管理器，名称格式：one.many_set

```python
jack1 = Student.objects.get(name='jack1')
jack2 = Student.objects.get(name='jack2')
python = Grade.objects.get(name='python-1902')
python.student_set.add(jack1, jack2, jack3)
```

在多的一方为关系起别名：related_name='students'

通过一的一方查数据

```python
python = Grade.objects.get(name='python-1902')
s = python.studets.filter(python__gte=80)
s = python.studets.filter(python_info__phone__endswith="8")
```

修改表与表的关系

```python
python = Grade.objects.get(name='python-1902')
tom = Student.objects.get(name='tom')
python.students.add(tom)
#第二种：
python = Grade.objects.get(name='python-1902')
tom = Student.objects.get(name='tom')
tom1 = Student.objects.get(name='tom1')
#通过set方法，重新建立关联关系，原有的关联关系会被清理
python.students.set(objs=(tom, tom1))
```

创建多的一方记录，并建立关联

```python
python = Grade.objects.get(name='python-1902')
#创建一名学生并加到当前班级
python.students.create(name='jim')
```

在保护删除模式下，删除表一记录或表二记录的影响

```python
python = Grade.objects.get(name='python-1902')
tom = Student.objects.get(name='tom')
#通过remove删除，会将多的一方外键置为null
python.students.remove(tom)
#第二种：
tom.grade = None
tom.save()
#清除关联关系
python.students.clear()
```

on_delete=models.PROTECT策略时：

1.在删除多的一方数据时，一的一方（表三）数据不受影响

2.在删除一的一方数据时，多的一方记录中的关系还存在则直接报错，若不存在关系，则把一的一方数据删除

##### 多对多关系

表四：

```python
class Group(models.Model):
    name = models.CharField(max_length=32, unique=True)
    members = models.ManyToManyField('Student')
    class Meta:
        db_table = 'groups'
```

建立表关系

```python
vue = Group.objects.get(name='Vue 小组')
java = Group.objects.get(name='java 小组')
toms = Student.objects.filter(name__startswith='tom')
vue.members.add(*toms)
#第二种方式，创建学院并加入小组
tom1 = Student.objects.get(name='tom1')
#创建小组并加入到其中
tom1.group_set.create(name='HTML 小组')
#为学员添加新组
tom1.group_set.add(java)
```

查询表数据

```python
tom1 = Student.objects.get(name='tom1')
#tom1加入的所有小组
print(tom1.group_set.all())
vue = Group.objects.get(name='Vue 小组')
#Vue小组下有多少人
print(vue.members.all())
#查询vue小组python成绩大于 60分的
s = vue.members.filter(python__gte=60)
```

修改表数据

```python
tom = Student.objects.filter(name__stratswith='tom')
vue = Group.objects.get(name='vue 小组')
vue.member.set(obj=tom)
```

删除表记录

```python
tom = Student.objects.filter(name__stratswith='tom')
#中间表的相关记录也被删除了
tom.group_set.clear()
#第二种：
vue = Group.objects.get(name='vue 小组')
vue.member.remove(tom)
```

ManyToManyField:会自动生成中间表，ManyToManyField字段可以定义在模型的任何一方，推荐定义在符合人们思维的一方



自定义中间表

```python
class Astudent(models.Model):
    name = model.CharField(max_length=32, unique=True)

class Agroup(models.Model):
    name = models.CharField(max_length=32, unique=True)
    members = models.ManyToManyField(Astudent, through='Membership')
    
class Membership(models.Model):
    student = models.ForeignKey(Astudent)
    group = models.ForeignKey(Agroup)
```

### Django的请求流程

1.选择要使用的根路由，一般情况下由settings的ROOT_URLCONF指定

2.加载可用的urlpatterns

3.依次匹配每个URL模式，直到匹配到第一个和URL对应的模式

4.调用3中匹配到的模式相对应的视图函数

参数：第一个参数HttpRequest对象

第二个参数：使用位置参数或者关键字参数接受URL中匹配到的内容

5.如果没有匹配到任何模式或匹配过程中发生异常，则调用特定的错误处理视图

##### 规划路由

1.为每个djangoapp定义一个urls.py

2.在根路由中include每个app的urls.py

```python
from django.conf.urls import url, include
from django.contrib import admin

urlpatterns = [
    url(r'^admin/', admin.site.urls),
    url(r'^user/', include('user.urls')),
]
```

app中的urls

```python
from django.conf.urls import url

from user import views

urlpatterns = [
    url(r'^login$', views.login),
]
```

3.根路由会把请求转发给相应的app

##### URL配置

1.11和2.0的区别

2.0类似于flask：

path：2.0新增的配置方法

有<转换器：参数名>   path('users/\<int:user_id>/', views.user)

转换器有：int， str，uuid，path

re_path:相当于1.11的url

1.11中转换器的作用用正则来实现：

url(r'^users/(?P<user_id>[0-9]+)/$', views.user)

转换器转过来的都是字符串

HTTP状态码

301-永久跳转，资源永久性的转移到了新的地址

302-临时跳转，资源临时性的转移到了新的地址

视图参数的默认值

```python
def page(request, num=1):
    return HttpResponse('{}'.format(num))
```

自定义错误页面,debug为false，自定义错误页面，设置：ALLOWED_HOSTS = ['*']

错误类型有;

handler400 = views.bad_request---请求错误

handler403 = views.permission_denied----无权限

handler404 = views.page_not_found---找不到页面

handler500 = views.server_error---服务器错误

```python
def error(request):
    
    return HttpResponse('')
```

##### 路由跳转，URL反向解析和命名空间

路由跳转：HttpResponseRedirect(),通过302实现

第一种：硬编码地址（尽量不要使用硬编码，会增加代码维护难度）

HttpResponseRedirect('/user/login/')

第二种：反向解析

需要给app中的url的路由定义名字name参数，相当于给路由起别名

url(r'^login/$', views.login, name='login-page')

在python代码中使用reverse函数

```python
def redirect(request):
    return HttpResponseRedirect(reverse('login-page'))
```

带参数跳转

```python
def redirect(request):
    return HttpResponseRedirect(reverse('login-page', kwargs={'student_id':2}))
```

快捷跳转函数：redirect（'login-page'，student_id=1）



在页面中使用反向解析

在应用中创建文件夹templates

渲染页面和传参给页面

```python
return render(request, 'user_center_info.html', context=context)
```

页面跳转链接加传参

```html
<a href="{% url 'user_center_info' user.id%}"></a>
```

命名空间：应用命名空间 + 实例命名空间

应用命名空间定义：

在app的urls中：app_name = 'user'

```python
app_name = 'user'
urlpatterns = [
    url(r'^login/$', views.login, name='login-page'),
    url(r'^redirect/$', views.redirect),
]
```

实例命名空间定义：

在根路由中进行定义：url(r'^user/', include('user.urls', namespace='user')),



运用名字：redirect（'user:login-page'，student_id=1）

在页面中运用：

```html
<a href="{% url 'user:user_center_info' user.id%}"></a>
```

#### 视图

##### 基于函数的视图/FBV

```python
def login(request):
    if request.method == 'POST':
        return HttpResponse('haha')
    return HttpResponse('lala')
```

##### 基于类的视图/CBV

```python
from django.views import View
class CBV(View):
    def get(self, request, *args, **kwargs):
        return HttpResponse('lala')

    def post(self, request, *args, **kwargs):
        return HttpResponse('haha')
```

使用：url(r'^login/$', views.CBV.as_view()),

#### Request，Response对象

#### 请求：

request.scheme:协议类型，http/https

path；获取路径（不包含域名和协议）

method：主要用于判断请求方式，GET，POST。。。

GET：获取GET请求数据:

s = request.GET.get('page')

POST：获取POST请求数据:

s = request.POST.get('page')

getlist获取多条请求数据:

s = request.POST.getlist('page')

get_host():获取请求原始主机

get_port():获取请求的原始端口

is_ajax():判断请求是否通过ajax机制发送

##### 响应

设置响应头：

response["Access-Control-Allow-Origin"] = "*"------------一般用到跨域请求问题

HttpResponse的子类：

HttpResponseRedirect:临时重定向，返回302状态码，被redirect()替代

HttpResponsePermanentRedirect：永久重定向，返回301状态码

HttpResponseBadRequest：错误的请求，返回400状态码

HttpResponseNotFount：页面不存在，返回404状态码

HttpResponseForbidden：禁止访问，返回403状态码

HttpResponseServerError：服务器错误，返回500状态码

JsonResponse():响应json格式的数据：

要设置非dict对象，必须safe参数False

如果JsonResponse()接受一个列表，则需要设置safe=False

#### 模板设置与语法

定义公用模板路径

在根路由的TEMPLATES中设置：'DIRS': [os.path.join(BASE_DIR, 'templates')],

'context_processors'为全局变量

'BACKEND'为选择的引擎，也可以设置为jinjia2

##### 模板继承

挖坑：{% block title %}{% endblock %}

填坑：{% block title %}{% endblock %}

继承：{% extends ‘base.html’ %}----在同文件夹下

{% block title %}

{{ block.super }}

{% endblock %}

用反向解析的方式导入css文件

第一种方式：

{% load  static %}

\<link rel='stylesheet' href="{% static 'user/css/style.css' %}">

第二种方式：

在TEMPLATES的'OPTIONS'中的'context_processors'设置全局变量'django.template.context_processors.static',

\<link rel='stylesheet' href="{{ STATIC_URL }}  user/css/style.css ">

多行注释：{% comment %}{% endcomment %}

单行注释：{#  #}

对象访问：对象属性student，字典my_dict，列表my_list

对象{{ student.name }}

字典{{ my_dict.name }}

列表{{ my_list.0 }}

Student模型对象

{% for student in grade.students.all  %}{% endfor %}

将子模板渲染并嵌入到当前HTML中的变种方法

{% include “foo/bar.html” %}

if条件：{% if 条件 %}{% elif 条件 %}{% else %}{% endif %}

变种：{% ifequal 变量 值  %}{%  endifequal %}---如果变量等于值

for循环：{% for i in [] %}{% endfor %}

循环下取下标值{{ forloop.counter }}

倒序{{ forloop.revcounter }}

循环使用row1和row2：{% cycle 'row1' 'row2' %}---<tr class="{% cycle 'row1' 'row2' %}"></tr>

过滤器：| safe，| date

date将日期格式化：my_date: {{ my_data | date:"Y-m-d H:i:s" }}--my_date时间格式

自定义过滤器：

在应用中添加python包

在包中新建python文件：mytags.py

```python
from django import template

register = template.Library()


@register.filter()
def myreverse(value):
    return value[::-1]


@register.filter()
def mycut(value, arg):
    return value.replace(arg, '')
```

加载python包

{% load  mytags %}

运用自定义过滤器

{{ hello | myreverse }}

{% hello  |  mycut：‘o’  %}



自定义标签：

在mytags.py中写入;

```python
@register.simple_tag()
def current_time(fmt):
    import datetime
    return datetime.datetime.now().strftime(fmt=fmt)
```

运用自定义标签

{% current_time '%Y-%m-%d %H:%M:%S' %}

#### 模型表单的提交

在form表单中加入{% csrf_token %}防止403错误

Django表单：准备和组织数据用于页面渲染

为数据创建HTML表单元素

接收和处理用户从表单发送过来的数据，对输入数据进行验证

写法类似模型定义，一个字段代表form中的一个input元素

步骤：

1.在app中创建forms.py

2.



#### csrf的在ajax的避免

第一种：

1.通过 cookies 获取 csrftoken

2.设置请求头（“X-CSRFToken”, csrftoken）

第二种：

@csrf_exempt------使用装饰器

第三种：

将setting中的csrf中间件关闭

在需要csrf保护的视图函数加装饰器@csrf_protect

### 缓存系统

##### django中的缓存系统

1.开发用缓存

2.文件缓存

3.数据库缓存

4.memcached

5.缓存整个网站

6.缓存视图

#### 使用Django-redis缓存

目的为django cache/session 提供redis支持

安装：pip install django-redis

##### 在stting中配置：----加在末尾位置

1.配置cache backend

```pytthon
CACHES = {
    "default": {
        "BACKEND":"django_redis.cache.RedisCache",#后端存储引擎
        "LOCATION": "redis://127.0.0.1:6379/1",#设置为那个数据库
        "OPTIONS": {
            "CLIENT_CLASS": "django_redis.client.DefaultClient",#将代码转换为redis命令
            "PASSWORD": "mysecret"  #设置redis密码
            "SOCKET_CONNECT_TIMEOUT": 5,  # 连接超时时间
            "SOCKET_TIMEOUT": 5,  # 获取数据超时时间
        }
    }
}
```

2.配置session backed

SESSION_ENGINE = "django.contrib.sessions.backends.cache"

#### 使用redis缓存的操作

1.导包---from django.core.cache import cache

##### 2.redis操作命令

永不超时：cache.set('key', 'value', timeout=None)

立即失效 ：cache.set('key', 'value', timeout=0)

超时时间为25秒：cache.set('key', 'value', timeout=25)

将key为foo设置为永不超时：cache.persist('foo')

将foo设置一个新的超时时间：cache.expire('foo', timeout=5)

批量获取值：cache.get_many(['a','b','c'])

批量设置值：cache.set_many({'a':1,'b':2,'c':3})

批量删除：cache.delete_many(['a','b','c'])

根据key获取值：get







##### 图片的上传

1.安装库：pip install pillow

2.settings.py 设置公用存储图片路径：

MEDIA_ROOT = os.path.join(BASE_DIR, 'media')

MEDIA_URL = '/media/'

3.创建模型

```python
from django.db import models


class Image(models.Model):
    name = models.CharField(max_length=128)
    #会将图片上传到 media/myform/photo 目录中
    photo = models.ImageField(upload_to='myform/photo')
```

4.迁移模型

5.创建两个路由：一个用来上传图片，一个用来展示图片

6.建立上传和展示的html

上传方法用form表单

```python
<form action="{% url 'app:upload-image' %}" method="post" enctype="multipart/form-data">
#enctype上传方法
	{% csrf_token %}
    <input type="file" name="photo"/>
    <input type="submit" value="Upload"/>
</form>
```

后台的接受

```python
if request.method == 'POST':
    photo = request.FILES.get('photo', None)
    name = photo.name
    _name, _ext = os.path.splitext(photo.name)#_ext为扩展名
    photo.name = '{}-{}{}'.format(_name, str(time.time()), _ext)#将图片名设置唯一
    image = Image() #实例化模型对象
    image.name = name
    image.photo = photo
    image.save()
```

展示html

根路由的配置

```python
from django.conf import settings
from django.conf.urls import url
from django.conf.urls.static import static
from django.contrib import admin

urlpatterns = [
    url('admin/', admin.site.urls),
] + static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT)#配置公用地址
```

##### 公用模板的设置方法

1.设置静态媒体目录

设置静态媒体目录，需要设立存储他们的目录

在工程目录里创建static目录

在settings.py文件中设置两个变量STATICFILES_DIRS 和STATIC_URL

STATIC_URL定义了，当django运行时，django应用寻找静态媒体的地址

django模板中，可以引用{{STATIC_URL}}变量避免把路径写死。通常使用默认设置：STATIC_URL = '/static/'

STATICFILES_DIRS 定义了web服务链接媒体的URL地址

STATICFILES_DIRS = (os.path.join(BASE_DIR, 'static'),)

2.MEDIA_XXX和STATIC_XXX配置项的区别

##MEDIA_XXX配置项用来管理媒体文件。经常由FileFields字段上传，它们被保存在settings.MEDIA_ROOT指定的目录下，通过settings.MEDIA_URL指定的路径访问

##STATIC_XXX配置项用来管理静态文件。它们通过manage.py collectstatic命令汇集到settings.STATIC_ROOT目录，并通过settings.STATIC_URL指定的路径访问。

3.设置媒体文件

```python
MEDIA_ROOT = os.path.join(BASE_DIR, 'media')
MEDIA_URL = '/media/'
```

#### restful架构：

开发模式

1.普通开发模式（前后端放在一起写）

2.前后端分离

面向对象的封装

“**封装**”就是将抽象得到的数据和行为（或功能）相结合，形成一个有机的整体（即类）；封装的目的是增强安全性和简化编程，使用者不必了解具体的实现细节，而只是要通过外部接口，一特定的访问权限来使用类的成员

视图分为方法视图和类视图

类视图

```python
from django.views import View
class StudentsView(View):
    #url->view方法->dispatch方法（反射执行：get，post。。）
    #类视图所继承View的源码
    def dispatch(self, request, *args, **kwargs)
    	func = getattr(self, request.method.lower())#返回对象的属性
        ret = func(request, *args, **kwargs)
        return ret
    
    
    def get(self, request, *args, **kwargs):
        return HttpResponse('')
    def post(self, request, *args, **kwargs):
        return HttpResponse('')
```

**super()** 函数是用于调用父类(超类)的一个方法。

super 是用来解决多重继承问题的，直接用类名调用父类方法在使用单继承的时候没问题，但是如果使用多继承，会涉及到查找顺序（MRO）、重复调用（钻石继承）等种种问题

多继承时左边MyBaseView优先

```python
class MyBaseView(object):
    def dispatch(self, request, *args, **kwargs)
        ret = super(MyBaseView,self).dispatch(request, *args, **kwargs)#super会寻找子类中的继承中的dispatch方法，会逐一按优先级寻找
        return ret

class StudentView(MyBaseView, View):
    pass
```

django会有5个中间键

1、process_request : 请求进来时,权限认证 。

2、process_view : 路由匹配之后,能够得到视图函数

3、process_exception : 异常时执行

4、process_template_responseprocess : 模板渲染时执行

5、process_response : 请求有响应时执行

django中csrf的实现

检查视图是否被@csrf_exempt   (免除csrf认证)

去请求体或cookie中获取token

所以csrf一般在process_view之前使用

加@csrf_exempt   表示不需要csrf的认证

加@csrf_protect 表示需要csrf认证，在中间件注释的情况下

给某特定的get或post等等请求免除csrf

```python
from django.utils.decorators import method_decorator
from django.views.decorators import csrf_exempt, csrf_protect 
class StudentView(View):
    @method_decorator(csrf_exempt)
    def dispatch(self, request, *args, **kwargs)
        return super(StudentView,self).dispatch(request, *args, **kwargs)
    
    def get(self, request, *args, **kwargs):
    	pass
    
    def post(self, request, *args, **kwargs):
        pass
```

##### restful规范

在restful架构中，每一个网址代表一种资源，所以网址中不能有动词，只能有名词，而且所用的名词往往与数据库的表格名对应，一般来说，数据库中的表都是记录的“集合”，所以API中的名词也应该使用复数

RESTFul的核心思想是，客户端发出的数据操作指令是“动词+宾语”的结构

如：get  /articles-----动词一般就是五种HTTP的方法

根据HTTP规范，动词一律大写

宾语必须是名词，如：articles----url中名词一般为复数

避免多级url

如：GET  /authors/12/categories/2-----这种url不利于扩展

一般应该这样写：GET /authors/12？categories=2

这样写GET /articles？published=true要好于GET /articles/published

restful10条规范

```python
1. API与用户的通信协议，总是使用HTTPs协议
    2. 域名  携带域名
        tps://api.example.com ：尽量将API部署在专用域名（会存在跨域问题）
        https://example.org/api/：API很简单(推荐)
    3. 版本  携带版本
        -https://api.example.com/v1/
        -把版本号放在请求头中
        127.0.0.1/book/1

    4. 路径  均使用名词表示（把网络上所有东西都看作资源）   （优先说出）
        -127.0.0.1/get_all_book/ 以前写法
        -127.0.0.1/books/  现在这么写
    5. method  方法 通过请求方式来表示进行的操作          （优先说出）
　　　　get 取(得到资源)
　　　　post  增加
　　　　delete  删除
　　　　put 刷新 客户端提供改变后的完整资源
　　　　patch  刷新 客户端提供的改变后的属性

    6. 过滤  通过在url上传参的形式传递搜索条件
    7. 状态码  返回数据中携带状态码
        1 开头：服务器正在处理
        2 开头：服务器处理成功
        3 开头：重定向
        4 开头：客户端错误
        5 开头：服务器错误
    8  错误处理  返回数据中携带错误信息
    9 返回结果针对不同操作，返回数据格式要求
　  10 返回结果中提供链接     核心:返回结果中提供链接
　　　　{
　　　　　　status:100
　　　　　　msg:成功
　　　　　　url:127.0.0.1/books/1
　　　　}
```

##### MVC和MTV框架模式的区别

MVC是怎么来的：最开始MVC是一种思想，为model—View—Controller

它的核心思想是：分工，解耦，让不同的代码块之间降低耦合度，增强代码的可扩展性和可移植，实现向后兼容，后来这种分工的思想受到越来越多的欢迎成为了一种架构模式

MVC的内容：

M全拼为model，主要封装对数据库的访问，对数据库中的数据进行数据的增，删，改，查

V为view，用于封装结果，生成页面展示的html内容

C为controller，用于接收请求，处理业务逻辑，与model交互，返回结果

MVT的内容：

M为model，负责和数据库交互，进行数据处理

v为View，接受请求，进行业务处理，返回应答

T为Template，负责封装构造要返回的html

注意：很多人认为MVT中的V就是mvc中的c控制器，这种说法是错误的，在django中MVT中V仍然只是View，但是它并不是控制器。

MVT将MVC中控制器的功能进行拆分，也就是说MVT在model，view，template三层之外，还有一个url分发器，它的作用是将一个个url页面请求分发给不同的view处理，让后view才调用相应的Model和Template

这种架构的优势在于，控制器接收用户的输入的部分由框架自行处理，django更加关注的是模型model，视图view，模板template，各组件的松耦合的，每个由django驱动的应用都有着明确的目的，并且可独立更改而不会影响其他部分

我的结论是：django肯定是遵循MVC思想的，但是在具体实现上Django是MVT模式









##### django rest framework框架

通过django的认证重写认证过程

```python
from rest_framework import exceptions

class MyAuthentication(object):
    def authenticate(self, request):
        token = request._request.GET.get('token')
        if not token:
            raise exceptions.AuthenticationFailed('用户认证失败')
    
    def authenticate_header(self, val):
        pass

class DogView(APIView):
    authentication_classes = [MyAuthentication, ]

    def get(self, request, *args, **kwargs):
        print(request)
        pass
```

由于源码中调用的认证的类为api_settings.DEFAULT_AUTHENTICATION_CLASSES下的类，而在api_settings中读的是一个‘REST_FRAMEWORK’的，所以要重写认证类时要在setting中设置认证类的调用路径

```python
#设置为公用配置
REST_FRAMEWORK = {
    "DEFAULT_AUTHENTICATION_CLASSES": ['api.utils.auth.FirstAuthtication', ],#指定认证类的路径
}
```

当不进行认证时可在局部变量域中定义authentication = []

##### 权限

1.使用

类，必须继承：BasePermission，必须实现：has_permission方法

```python
from rest_framework.permissions import BasePermission

class SVIPPermission(BasePermission):
    mmessage = "必须是SVIP才能访问"
    def has_permission(self, request, view):
        if request.user.user_type != 3:
            return False
        return True
```

返回值：True有权访问， False无权访问

局部

```python
class UserInfoVIew(APIView):
    permission_classes = [MyPermission1, ]
    def get(self, request, *args, **kwargs):
        return Httpresponse('用户信息')
```

全局：

```python
REST_FRAMEWORK = {
    "DEFAULT_PERMISSION_CLASSES": ['api.utils.permission.SVIPPermission', ],#指定认证类的路径
}
```

##### 版本设计：

1.版本可以通过url的get传参如：.....user/?version=v1

```python
class ParamVersion(object):
    def determine_version(self, request, *args, **kwargs):
        version = request.query_params.get('version')
        return version
    
class UsersView(APIView):
    versioning_class = ParamVersion
    def get(self, request, *args, **kwargs):
        print(request.version)
        return HttpResponse('用户列表')
```

2.使用内置的版本控制





##### rest_framework 解析器：对请求体数据进行解析

1.一般情况下request.POST中有值的要求：

a.请求头的要求

Content-Type：application/x-www-form-urlencoded

b.数据格式的要求：

name = alex&age=18

2.使用解析器使后端可以获取用户发送json格式的数据既请求头content-type:application/json

```python
from rest_framework.parsers import JSONParser

class ParserView(APIView):
    parser_classes = [JSONParser, ]
    def post(self, request, *args, **kwargs):
        """
        允许用户发送json格式的请求头数据
        	a.content-type:application/json
        	b.{'name':'alex',age:18}
        """
        #获取解析过后的结果
        print(request.data)
        return HttpResponse('')
```

3.都能用

Content-Type：application/x-www-form-urlencoded用FormParser

content-type:application/json用JSONParser

```python
from rest_framework.parsers import JSONParser, FormParser

class ParserView(APIView):
    parser_classes = [JSONParser, FormParser,]
    def post(self, request, *args, **kwargs):
        """
        允许用户发送json格式的请求头数据
        	a.content-type:application/json
        	b.{'name':'alex',age:18}
        """
        #获取解析过后的结果
        print(request.data)
        return HttpResponse('')
```

以上都是在用request.data的时候python才去解析

##### 全局配置解析器

```python
REST_FRAMEWORK = {
    "DEFAULT_PARSER_CLASSES": ['rest_framework.parsers.JSONParser', 'rest_framework.parsers.FormParser],#指定认证类的路径
}
```



#### 序列化类

json.dumps输出的会是中文的ascii 字符码，而不是真正的中文，这是因为json.dumps 序列化时对中文默认使用的ascii编码.想输出真正的中文需要指定ensure_ascii=False

对数据进行序列化的方式：

方式一：

```python
class RolesView(APIView):
    def get(self, request, *args, **kwargs):
        roles = models.Role.objects.all().values('id', 'title')
        roles = list(roles)
        ret = json.dumps(roles, ensure_ascii=False)
        return HttpResponse(ret)
```

方式二：

```python
from rest_framework import serializers
class RolesSerializer(serializers.Serializer):
    id = serializers.CharField()
    title = serializers.CharField() #指定模型中的title字段进行序列化
    
class RolesView(APIView):
    def get(self, *args, **kwargs):
        roles = models.Role.objects.all()
        ser = RolesSerializer(instance=roles, many=True)
        ret = json.dumps(ser.data, ensure_ascii=False)
        return HttpResponse(ret)
```

序列化类:就是将类序列化成字典来返回

单个对象的情况：

```python
from rest_framework import serializers
class RolesSerializer(serializers.Serializer):
    id = serializers.CharField()
    title = serializers.CharField() #指定模型中的title字段进行序列化
    
class RolesView(APIView):
    def get(self, *args, **kwargs):
        roles = models.Role.objects.all().first()
        ser = RolesSerializer(instance=roles, many=False)
        ret = json.dumps(ser.data, ensure_ascii=False)
        return HttpResponse(ret)
```

当序列化类中模型为

```python
class UserInfo(models,Model):
    user_type_choices = (
    	(1,'普通用户'),
        （2,'VIP'）,
        （3,'SVIP'）
    )
    user_type = models.IntegerField(choices=user_type_choices)
```

可以这样调用数字所对应的字符串：source可以指定字段

```python
from rest_framework import serializers
class RolesSerializer(serializers.Serializer):
    uuuuu = serializers.CharField(source="user_type")#调用的是数字
    rrrrr = serializers.CharField(source="get_user_type_display")#调用的是字符串
    
class RolesView(APIView):
    def get(self, *args, **kwargs):
        roles = models.Role.objects.all()
        ser = RolesSerializer(instance=roles, many=True)
        ret = json.dumps(ser.data, ensure_ascii=False)
        return HttpResponse(ret)
```

外键的调用

```python
from rest_framework import serializers
class RolesSerializer(serializers.Serializer):
    #调用的是外键所对应的模型中的id字段
    group = serializers.CharField(source="group.id")
    
class RolesView(APIView):
    def get(self, *args, **kwargs):
        roles = models.Role.objects.all()
        ser = RolesSerializer(instance=roles, many=True)
        ret = json.dumps(ser.data, ensure_ascii=False)
        return HttpResponse(ret)
```

多对多关系的调用：

```python
#模型
class UserInfo(models,Model):
    user_type_choices = (
    	(1,'普通用户'),
        （2,'VIP'）,
        （3,'SVIP'）
    )
    user_type = models.IntegerField(choices=user_type_choices)
    roles = models.ManyToManyField("Role")

from rest_framework import serializers
class RolesSerializer(serializers.Serializer):
    #自定义显示函数返回的值
    rls = serializers.SerializerMethodField()
    def get_rls(self, row):
        role_obj_list = row.roles.all()
        ret = []
        for item in role_obj_list:
            ret.append({'id':item.id, 'title':item.title})
        return ret
    
    
class RolesView(APIView):
    def get(self, *args, **kwargs):
        roles = models.Role.objects.all()
        ser = RolesSerializer(instance=roles, many=True)
        ret = json.dumps(ser.data, ensure_ascii=False)
        return HttpResponse(ret)   
```

另外一种序列化方式

```python
class UserInfoSerializer(serializers.ModelSerializer):
    rrrrr = serializers.CharField(source="get_user_type_display")
	rls = serializers.SerializerMethodField()
    class Meta:
        model = models.UserInfo
        fields = ['id', 'username', 'password', 'rrrrr', 'rls', 'group']
        extra_kwargs = {'group':{'source':'group.title'},}
    def get_rls(self, row):
        role_obj_list = row.roles.all()
        ret = []
        for item in role_obj_list:
            ret.append({'id':item.id, 'title':item.title})
        return ret
```

read_only=True指定 当前字段不能被修改，通常用于pk

required 是否为必填字段，在auto_now，auto_now_add 的字段中设置为False

rm -rf / 删除根目录

rm -rf ~/ 删除home目录

rm -rf ./删除当前目录

rm -rf ./code 删除当前目录下的code文件夹

##### django中写原生sql语句的三种方法：

1.使用extra：查询人民邮电出版社出版并且价格大于50元的书籍 

Book.objects.filter(publisher__name='人民邮电出版社').extra(where=['price>50'])  

2.使用raw 

books=Book.objects.raw('select * from hello_book')   

for book in books:   

   print book   

3.自定义sql 

from django.db import connection   

cursor = connection.cursor()   

cursor.execute("insert into hello_author(name) VALUES ('郭敬明')")   

cursor.execute("update hello_author set name='韩寒' WHERE name='郭敬明'")   

cursor.execute("delete from hello_author where name='韩寒'")   

cursor.execute("select * from hello_author")   

cursor.fetchone()   

cursor.fetchall() 

 