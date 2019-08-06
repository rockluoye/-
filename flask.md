# 安装

pip安装虚拟环境：

1.pip install virtualenv

2.cd 目录---------cd到目录，准备建立虚拟环境

3.virtualenv --no-site-packages -p python解释器所在目录  虚拟环境名称

4.cd到你建立的虚拟文件中的Scripts

5.执行activate

6.pip install flask----------------安装flask

7.执行deactivate---------退出虚拟环境，安装成功

run()启动后flask默认端口是5000，而Django是8000

若host为0，或0.0.0.0则可以通过ip访问（其他电脑可以访问该ip）

flask-script插件

1.安装

pip install  flask-script

2.初始化manager = Manager(app=app)--------在命令行输入端口路由信息

3.使用manager.run()启动应用

4.默认虚拟环境使用workon时是在c:\Users\xie\Envs中

manager中-d为调试模式

# flask的基础

```python
import sys
from flask import Flask
#获取flask对象，初始化基础的配置
app = Flask(__name__)

#定义路由地址：’/‘，和处理方法
@aap.route('/')
def hello()：--------路由+视图函数
	return 'hello world'

if __name__ == '__main__':
    
    #用来接收传参------sys.argv
    host = sys.argv[1]
    port = sys.argv[1]
    
    #启动flask程序						
   
app.run(host=host,port=port,debug=True)
#host为ip地址，port为端口，debug为每次修稿时重新运行
    
```

用命令行的方式启动:

执行命令行：python  文件名.py  runserver -h ip地址 -p 8000 -d -r

h------host

p--------port

d---------debug
r--------自动重启

url_for{{ "" ,filename='' }}------反向解析，用来找static中的文件的

render_plament-----模板渲染

#创建蓝图对象blue
blue = Blueprint('first', \__name__)

#注册蓝图，app和blue绑定
app.register_blueprint(blueprint=blue)



路由匹配规则:转换器<转换器：参数名>

如：’/article/\<int:id>/‘--------’/article/2/‘

’/article/\<string:id>/‘-----------’/article/title/‘

转换器无默认string

带参数传参：converter：string  接受任何没有斜杠（‘/’）的文件

<int：id>:整数

\<float:小数>:小数

path：支持/的字符串

uuid：生成唯一的随机数id

any：\<any(movie,dog,cat):like>任意在括号中的一种

```python
import sys
import os
from flask import Flask
from flask_script import Manaher
#获取flask对象，初始化基础的配置
app = Flask(__name__)

#定义路由地址：’/‘，和处理方法
@aap.route('/')
def hello()：
	return 'hello world'

if __name__ == '__main__':
    
   manage = Manager(app)
    
    #启动flask程序						
  
	app.run()
```

返回请求值：request

执行命令行request.args

取值request.args['pk']

```python
import sys
import os
from flask import Flask
from flask_script import Manaher
#获取flask对象，初始化基础的配置
app = Flask(__name__)

#定义路由地址：’/‘，和处理方法
@aap.route('/article/')
def hello()：

	return 'hello world'

if __name__ == '__main__':
    
   manage = Manager(app)
    
    #启动flask程序						
  
	app.run()
```

# request

request.url------完整请求路径url

request.url------去掉get参数的url

request.url------只有主机和端口url

request.method---请求方式

request.path----url中的路由

request.args------get请求的参数-------通过？来传参

request.form-----post请求的参数

request.cookies------请求的cookies

request.remote_addr-----客户端ip

request.files-----上传的文件

request.headers------请求头信息

request.form.get(key):得到key所对应的value值；其中key为字符串方式在括号中

request.form.getlist(key)：得到值后返回的值组装成列表

request.args .get  获取值

getlist（key）     得到key所对应的value值；其中key为字符串方式在括号中

模板语法：render_template('index.html',name="...")------------将变量name=‘’...‘’传进index.html中

##### response：响应

res=make_response('<><>'):创建响应对象

如：res = make_response("hello")

res=Response(‘’)---------与make_response一样

有：str_h=render_template('index.html',name="...")

res=Response(str_h)

redirect:重定向

return redirect('/response/')------重定向到自己的路由

return redirect(url_for('first.set_response'，name=‘lisi’))---反向解析到路由/response/，set_response为函数名，first为蓝图名称，name为参数

反向解析静态资源：

{{ url_for("static",filename="css/base.css") }}

abort(502)-----主动抛出错误

捕获异常：

```python
@blue.errorhandler(404)
	print(e)
    return ''
```

#### cookie:

在使用cookie时必须要用response

render_template():渲染，括号中为要渲染的h5地址，以字符串

设置cookie

res.set_cookies('key','value')

res.set_cookie(”token“，”123456“，max_age=300)------------存入到前端cookie钥匙,其中300为钥匙的时间单位为秒

获取cookie

request.cookies.get('username', ' ')

注销cookie

res.delede_cookie('key')

特点；

不能夸域名

不能跨浏览器

支持过期时间

#### session：

如：设置：session['username'] =‘ coco'

调用：username = session.get('username'，‘’)

在使用时应加密格式如：app.secret_key = 'asjkdfawey6t257er5g87q638erg'-----------字符为随意字符

删除session

session.pop(“key”)

清除session

 session.clear

在做登录页面时使用MD5加密方法

```python
user.password = md5_password(password)#存入表中时进行加密
def md5_password(pwd):
    m = hashlib.md5()
    m.update(pwd.encode())
    return m.hexdigest()

#在进行判断时同样要进行加密再判断
password = md5_password(password)
users = User.query.filter_by(name=username, password=password)
```



### 模板语法

Flask中使用Jinja模板引擎

变量：{{ var }}-------变量不存在，默认忽略

标签：{{% tag %}}

动态加载页面

1.继承原界面------{%  extends  '模板位置'  %}-----将父模板挖的坑填好

如：

```python
{% extends "base.html" %}
{%  block  title  %}
{%  endblock  %}
```

2.挖坑----{%  block  title  %}      {%  endblock  %}

3.{{  super（）  }}语法------继承父类的坑内的内容

4.{% include  ”地址“ %}----导入某个模板

5.{%macro hello(name)%}

	<p>{{ name }}</p>

{%endmacro%}-------宏定义函数，可以调用hello函数

#### 模板语法

标签解析----{%  标签  %}{%  end标签  %}

变量解析----{{  变量  }}

循环-----{%  for  i  in  a  %}{%  else  %}  {%  endfor  %}

可以有range

条件-----{%  if  条件  %}{%  else  %}{%  endif  %}

编号：

{{  loop.index }}:从一开始编号

{{ loop.index0 }}:从0开始编号

{{ loop.revindex }}:倒序开始编号到一结束

{{ loop.revindex0 }}:倒序开始编号到0结束

{{ loop.first }}:如果是第一次循环返回True，其他的返回False

{{ loop.last }}:最后一次循环返回True，其他的返回False

过滤器：

{  变量 | safe }

safe：将不安全的信息过滤掉

abs(value)：返回一个数值的绝对值。示例：-1|abs

default(value,default_value,boolean=false)：如果当前变量没有值，则会使用参数中的值来代替。示例：name|default(‘xiaotuo’)——如果name不存在，则会使用xiaotuo来替代。boolean=False默认是在只有这个变量为undefined的时候才会使用default中的值，如果想使用python的形式判断是否为false，则可以传递boolean=true。也可以使用or来替换。

escape(value)或e：转义字符，会将<、>等符号转义成HTML中的符号。显例：`content|escape`或`content|e`

first(value)：返回一个序列的第一个元素。示例：names|first

format(value,*arags,**kwargs)：格式化字符串。比如：{{ "%s" - "%s"|format('Hello?',"Foo!") }}将输出：Helloo? - Foo!

last(value)：返回一个序列的最后一个元素。示例：names|last。

length(value)：返回一个序列或者字典的长度。示例：names|length。

join(value,d=u”)：将一个序列用d这个参数的值拼接成字符串。

safe(value)：如果开启了全局转义，那么safe过滤器会将变量关掉转义。示例：content_html|safe。

int(value)：将值转换为int类型。

float(value)：将值转换为float类型。

lower(value)：将字符串转换为小写。

upper(value)：将字符串转换为小写。

replace(value,old,new)： 替换将old替换为new的字符串。

truncate(value,length=255,killwords=False)：截取length长度的字符串。

striptags(value)：删除字符串中所有的HTML标签，如果出现多个空格，将替换成一个空格。

trim：截取字符串前面和后面的空白字符。

string(value)：将变量转换成字符串。

wordcount(s)：计算一个长字符串中单词的个数

#### 大量参数传参：

```python
params = {
    "name": "何",
    "age": 24,
    "likes": ["编程", "赌博"]
}
render_template('index.html', **params)
```

过滤器:{ 变量|过滤器| }

capitalize

### 蓝图：

1.导包------from  flask  import  Blueprint

2.生成蓝图对象管理路由-----blue = Blueprint（‘first’， \__name__）

3.使用蓝图对象管理路由----@blue.route('/..../',   methods=['GET', 'POST'])

4.在manage中注册蓝图---app.register_blueprint(blueprint=blue, url_prefix='/app')

5.导包from  app.viwes  import  blue

跳转地址

无参情况

第一种方法：

1.导包----from flask import  redirect

2.直接return redirect('/app/home/')

第二种方法：反向解析

1.导包---from  flask import url_for

2.return redirect('first.home')

有参情况

如：/article/\<int:id>

第一种方法：硬编码地址

return redirect('/app/article/2/')

第二种方法：使用反向解析url_for

return redirect(url_for('first.article', id=3))

静态资源的加载：第一种方式：直接硬编码地址

第二种：通过反向解析静态资源的方式

href=“{{ url_for('static', filename='back/css/style.css')}}”

striptags：将变量中的样式删掉

## 模型

数据库操作：

ORM：Objects  +  Relationship + Mapping-----------对象关系映射

自动转化对应数据库的sql语句

模型和表之间的关系：

类-------表结构

属性------字段

对象------数据

在程序中涉及到复杂sql语句时，还是要自己写sql语句

一般pymysql+ORM

flask中ORM----SQLAlchemy





mysql数据库操作

定义模型：

```python
from flask_sqlalchemy import SQLAlchemy
db = SQLAlchemy()#实例化对象

class Student(db.Model):
    id = db.Column(db.Integer, primary_key=True, autoincrement=True)
	name = db.Column(db.String(10), unique=True)
	age = db.Column(db.Integer, default=18)
    #tablename不写，则表示模型对应的表名称为模型的小写
    __tablename__ = 'stu'   #关联数据库中表名为stu的表
    
```

导包-----pip  install   flask-sqlalchemy

在manage中定义数据库连接信息

```python
from flask_session import Session
#连接配置
#dialect+driver://username:password@host:post/database
#mysql + pymysql://root:密码@127.0.0.1：3306/表名
app.config['SQLALCHEMY_DATABASE_URI'] = 'mysql+pymysql://root:密码@127.0.0.1：3306/表名'
db.init_app(app)#配置数据库的连接信息
```

在本地中创建数据库命名为如：‘stu’等表名

在viwes中创建数据库表

```python
from pymysql import 
@blue.route('/.../', methods=['GET', 'POST'])
def create_db():
    #生成数据库中表
    db.create_all()
    #删除数据库中的所有的表
    db.drop_all()
    return '创建表成功'
```

模型定义

Integer：整型

String(size):varchar

Boolean:布尔

Datetime：日期

Text：长文本

Float：浮点

模型约束：

unique：是否唯一

nullable：是否为空

primary_key:主键

default：默认值

添加数据

```python
#向stu表中插入数据
stu = Student()
stu.name = '小明'
stu.age = 28
#add(对象)：准备向数据库中插入数据insert
db.session.add(stu)
#commit():将准备的insert语句插入到数据库中
db.session.commit()

```

批量添加

```python
for i  in  range(10):
    stu = Student()
    stu.name = '小明' + str(i)
    stu.age = 18 + i
    all_stus.append(stu)
db.session.add_all(all_stus)#添加所有学生对象
db.session.commit()
```

### 查询：

```python
stus = Student.query.filter_by(name='小明').all()[0]#ORM方法
stus = Student.query.filter_by(name='小明').first()
```

方式二：

```python
stus = Student.query.filter_by(Student.name == '小明0').all()
```

方式三：

```python
stu = Student.query.get(3)#括号中只能给主键值，默认查询主键行的信息
```

排序查询：order_by

```python
stus = Student.query.order_by(-Student.id).all()#降序，-去掉为升序
```

分页：offset()为跳过几个参数    limit()截取几个参数

```python
page = 1
stus = Student.query.all()[(page-1)*3:page*3]#前闭后开
stus = Student.query.offset((page-1)*3).limit(3).all()
```

模糊查询,contains()，like ’%小明%‘，endswith()，startswith()：

```python
#filter_by只能精确查询
stus = Student.query.filter(Student.name.contains('小明')).all()
stus = Student.query.filter(Student.name.endswith('明')).all()#以明结束的
stus = Student.query.filter(Student.name.startswith('大')).all()#以大开头的
stus = Student.query.filter(Student.name.like('_明')).all()#下划线为占位
```

查询大于,查询大于gt，大于等于ge，小于lt，小于等于le：

```python
stus = Student.query.filter(Student.age >= 20).all()
stus = Student.query.filter(Student.age.__gt__(20)).all()#不用运算符的写法

```

多过滤条件，且关系

且，或，非操作：

导包from  sqlalchemy  import or_，and\_，not\_

```python
stus = Student.query.filter(or_(Student.name.endswith('4'),Student.age.__gt__(20))).all()
```

not_:

```python
stus = Student.query.filter(Student.name.endswith('4'),not_(Student.age.__gt__(20))).all()
```

定义外键：

```python
grade_id = db.Column(db.Integer,dn.Foreignkey('grade.id'),nullable=True)
```

### 删除：

```python
stu = Student.query.filter_by(name='小明').first()
db.sesion.delete(stu)
db.session.commit()
```

### 修改：

```python
stu = Student.query.filter_by(age=18).first()
stu.age = 20
db.session.add(stu)  #可写可不写
db.session.commit()
```

#### sqlite数据库的操作

项目结构为app(static,templates,\__init__.py，exts.py，models.py，views.py)  +  manager.py

1.配置：

```python
from flask import Flask
from .views import blue
from app.exts import init_exts
def create_app():
    app = Flask(__name__)
    app.config['ENV'] = 'development'   #配置成开发环境
    #数据库配置
    app.config['SQLALCHEMY_DATABASE_URI'] = 'sqlite:///sqlite3.db'  # 配置连接数据库路径DB_URI
    app.config['SQLALCHEMY_TRACK_MODIFICATIONS'] = False  # 禁止对象追踪修改
    #加载Flask插件
    init_exts(app)
    app.register_blueprint(blueprint=blue)
    return app
```

2.创建Flask插件

```python
from flask_sqlalchemy import SQLAlchemy
db = SQLAlchemy()
#初始化插件
def init_exts(app):
    db.init_app(app)  #将插件进行绑定在路由app上，init_app()为flask中的绑定函数
```

3.建立模型model.py

```python
from app.exts import db
class Person(db.Model):
    __tablename__ = "person"   #表名
    id = db.Column(db.Integer, primary_key=True)
    name = db.Column(db.String(20), unique=True)
    age = db.Column(db.Integer, default=18)
```

4.创建视图函数，在调用时创建数据库表

```python
from app.models import Person, db

@blue.route('/cretaedb/')
def create_db():
    db.create_all()#将模型中的转化成表
    return "创建数据库表"
```

5.删除数据库

```python
#删除数据库表
@blue.route('/dropdb/')
def drop_db():
    db.drop_all()

    return "删除"
```

6.为数据库中的表添加纪录，访问一次该路由添加一次数据记录

```python
@blue.route('/addperson/')
def addperson():
    p = Person()#p为表中的记录
    n = random.randint(10, 99)
    p.name = "qiang" + str(n)
    p.age = n
    db.session.add(p)  #执行添加操作
    db.session.commit()  #提交
    return "添加"
```

7.获取数据库中的记录，用persons.html的for循环逐个显示

```python
#获取数据
@blue.route('/getperson/')
def getperson():
    personlist = Person.query.all()
    print(personlist)
    return render_template('persons.html', person_list=personlist)
```

8.数据迁移

安装pip install  flask-migrate

migrate = Migrate()

migrate.init_app(app=app, db=db)------绑定app与指定db数据库

from flask_migrate  import  MigrateCommand

manager.add_command('db', MigrateCommand)--------添加自定义迁移命令

操作：

python manage.py  db init   只调用一次，做初始化

python manage.py  db migrate  生成迁移文件

python manage.py db  upgrade  执行迁移中的升级

python manage.py db downgrade  执行迁移中的降级

#### mysql数据库的操作

1.与sqlite类似，只需将app.config['SQLALCHEMY_DATABASE_URI'] = 'sqlite:///sqlite3.db'

改为app.config['SQLALCHEMY_DATABASE_URI'] = ‘mysql+pymysql://root:rock1204@localhost:3306/flaskdb’

其中root为用户名，rock1204为密码，localhost为地址，3306为端口，flaskdb为数据名

2.用cmd创建数据库，便可以在数据库中创建表，添加数据，修改数据

3.迁移与sqlite一样

迁移指的是在数据库中创建需要的表

添加插件

```python
from flask_sqlalchemy import SQLAlchemy
from flask_migrate import Migrate
db = SQLAlchemy()
migrate = Migrate()#实例化对象
#初始化插件
def init_exts(app):
    db.init_app(app)
    migrate.init_app(app, db)#绑定插件和指定数据库
```

在manager.py中添加自定义命令

```python
from flask_script import Manager
from app import create_app
from flask_migrate import MigrateCommand

app = create_app()
manager = Manager(app)
manager.add_command('db', MigrateCommand)

if __name__ == '__main__':
    manager.run()
```

在Terminal中执行命令

python manager.py  db init   只调用一次，做初始化

在项目目录中生成迁移目录migrations

python manager.py  db migrate  

在versions目录中生成版本号迁移文件

python manager.py db  upgrade  

在迁移文件中添加表

python manager.py db downgrade  

执行迁移文件中的降级，回退

每次修改表结构都需要执行python manager.py  db migrate  和python manager.py db  upgrade 来生成新的版本迁移文件

##### 模型中的类型与约束

创建模型

```python
# 模型：类
class Person(db.Model):
    __tablename__ = 'person'
    id = db.Column(db.Integer, primary_key=True, autoincrement=True)
    name = db.Column(db.String(20), unique=True)
    age = db.Column(db.Integer, default=1)

```

字段类型

| 类型名       | Python类型         | 说 明                                                |
| ------------ | :----------------- | ---------------------------------------------------- |
| Integer      | int                | 普通整数, 一般是 32 位                               |
| SmallInteger | int                | 取值范围小的整数,一般是 16 位                        |
| BigInteger   | int 或 long        | 不限制精度的整数                                     |
| Float        | float              | 浮点数                                               |
| Numeric      | decimal.Decimal    | 定点数                                               |
| String       | str                | 变长字符串                                           |
| Text         | str                | 变长字符串,对较长或不限长度的字符串做了优化          |
| Unicode      | unicode            | 变长 Unicode 字符串                                  |
| UnicodeText  | unicode            | 变长 Unicode 字符串,对较长或不限长度的字符串做了优化 |
| Boolean      | bool               | 布尔值                                               |
| Date         | datetime.date      | 日期                                                 |
| Time         | datetime.time      | 时间                                                 |
| DateTime     | datetime.datetime  | 日期和时间                                           |
| Interval     | datetime.timedelta | 时间间隔                                             |
| LargeBinary  | str                | 二进制文件                                           |

##### 常用约束

| 选项名      | 说 明                                                        |
| :---------- | :----------------------------------------------------------- |
| primary_key | 如果设为 True ,这列就是表的主键                              |
| unique      | 如果设为 True ,这列不允许出现重复的值                        |
| index       | 如果设为 True ,为这列创建索引,提升查询效率                   |
| nullable    | 如果设为 True ,这列允许使用空值;如果设为 False ,这列不允许使用空值 |
| default     | 为这列定义默认值                                             |

##### 删除数据：

```python
p = Person.query.get(1)#找到要删除的数据，1主键id值
try:
    db.session.delete(p)#删除数据
    db.session.commit()#提交
except:
    db.session.rollback()#回滚
    db.session.flush()#刷新
```

db.drop_all删除库中的所有表

##### 添加数据：

```python
 p = Person()#p为表中的一条空记录
 p.name = "qiang" + str(n)#在记录中加数据
 p.age = n
 db.session.add(p)  #执行添加操作
 db.session.commit()  #提交
```

##### 修改数据：

```python
p = Person.query.get(2)
p.name = "haha"
try:
    db.session.commit()
except:
    db.session.rollback()
    db.session.flush()
```

##### 查询数据：

过滤器
        filter()	把过滤器添加到原查询上,返回一个新查询
        filter_by()	把等值过滤器添加到原查询上,返回一个新查询集合
        limit()	  使用指定的值限制原查询返回的结果数量,返回一个新查询
        offset()	偏移原查询返回的结果,返回一个新查询，括号中的内容为表的index
        order_by()	根据指定条件对原查询结果进行排序,返回一个新查询
        group_by()	根据指定条件对原查询结果进行分组,返回一个新查询

    常用查询
        all()	以列表形式返回查询的所有结果,返回列表
        first()	返回查询的第一个结果,如果没有结果,则返回 None
        first_or_404()	返回查询的第一个结果,如果没有结果,则终止请求,返回 404 错误响应
        get()	返回指定主键对应的行,如果没有对应的行,则返回 None
        get_or_404()	返回指定主键对应的行,如果没找到指定的主键,则终止请求,返回 404 错误响应
        count()	返回查询结果的数量
        paginate()	返回一个 Paginate 对象,它包含指定范围内的结果
    
        查询属性
            contains
            startswith
            endswith
            in_
            __gt__
            __ge__
            __lt__
            __le__


    逻辑运算
        与 and_
            filter(and_(条件),条件…)
        或 or_
            filter(or_(条件),条件…)
        非 not_
            filter(not_(条件),条件…)
    
    示例:   
     	查询:
     		person = Person()
            persons = Person.query.all()  # 获取所有
            persons = Person.query.filter(Person.age>22)
    
            # filter功能比filter_by强大
            persons = Person.query.filter(Person.age==22)  # filter(类.属性==值)
            persons = Person.query.filter_by(age=22) # filter_by(属性=值)
    
            persons = Person.query.filter(Person.age.__lt__(22)) # <
            persons = Person.query.filter(Person.age.__le__(22)) # <=
            persons = Person.query.filter(Person.age.__gt__(22)) # >
            persons = Person.query.filter(Person.age.__ge__(22)) # >=
    
            persons = Person.query.filter(Person.age.startswith('宝'))  # 开头匹配
            persons = Person.query.filter(Person.age.endswith('宝'))  # 结尾匹配
            persons = Person.query.filter(Person.age.contains('宝'))  # 包含
            persons = Person.query.filter(Person.age.in_([11,12,22]))  # in_
    
            persons = Person.query.filter(Person.age>=20, Person.age<30)  # and_
            persons = Person.query.filter(and_(Person.age>=20, Person.age<30))  # and_
            persons = Person.query.filter(or_(Person.age>=30, Person.age<20))  # or_
            persons = Person.query.filter(not_(Person.age<30))  # not_
        
        排序:
            persons = Person.query.limit(5)  # 取前5个
            persons = Person.query.order_by('age')  # 升序
            persons = Person.query.order_by(desc('age'))  # 降序
            persons = Person.query.offset(5)  # 跳过前5个
        
        分页:
            # 获取页码page和每页数量num
            page = int(request.args.get('page'))
            num = int(request.args.get('num'))
    
            # 手动做分页
            persons = Person.query.offset((page-1) * num).limit(num)
    
            # 使用paginate做分页
            persons = Person.query.paginate(page, num, False).items
       
        paginate对象的属性：
            items：返回当前页的内容列表
            has_next：是否还有下一页
            has_prev：是否还有上一页
            next(error_out=False)：返回下一页的Pagination对象
            prev(error_out=False)：返回上一页的Pagination对象
            page：当前页的页码（从1开始）
            pages：总页数
            per_page：每页显示的数量
            prev_num：上一页页码数
            next_num：下一页页码数
            query：返回创建该Pagination对象的查询对象
            total：查询返回的记录总数	
钩子函数：中间件
Aop：面向切面编程

before_first_request:处理第一次请求之前执行

before_request:在每次请求之前执行，通常使用这个钩子函数预处理一些变量，实现反爬

after_request:注册一个函数，如果没有未处理的异常抛出，在每次请求之后运行

teardown_appcontext:当app上下文被移除之后执行的函数，可以进行数据库的提交或者回滚

每次路由请求都会调用

```python
@blue.before_request
def before():
    #检测是否是浏览器访问
    ua = request.user_agent-------返回浏览器的代理如：firefox，google
    print(ua)
    if ua.find('python') != -1:
        return '别爬了'
    #如果有return会拦截视图函数的调用
```

防止ip频繁访问

```python
@blue.before_request
def before():
    ip = request.remote_addr  #客户端ip
    if cache.get(ip):
        time.sleep(0.5)
        cache.set(ip, 'aa', timeout=0.5)
        return '别爬了'
    else:
    	#将缓存到内存中，缓存时间为0.5秒
    	cache.set(ip, 'aa', timeout=0.5)
```

常用插件：

##### flask-bootstrap

1.安装   pip  install   flask-bootstrap

2.初始化    from flask_bootstrap  import Bootstrap

3.绑定   Bootstrap(app)

4.使用继承bootstrap父类模板

{% extends  'bootstrap/base.html' %}

{% block navbar %}

.......

{% endblock %}

##### flask-debugtoolbar----调试工具

1.安装  pip install flask-debugtoolbar

2.初始化  from flask_debugtoolbar  import  DebugToolbarExtension

debugtoolbar = DebugToolbarExtension()

debugtoolbar.init_app(app)

##### flask-caching

1.安装   pip  install  flask-caching

2.初始化  from flask_cache  import  Cache

cache  =  Cache(config={'CACHE_TYPE':'simple'})

cache.init_app(app=app)

3.使用

```python
@blue.route('/home/')
@cache.cached(timeout=30)
def home():
    print('加载数据')
    return 'home'      #将数据缓存起来30秒，当页面在30面内再次访问时不再print（'加载数据'），而是直接返回数据
```

##### Flask内置对象

g：global全局对象

如：g.age = 16

可以在其它视图函数位置获取g.age的值

current_app.config----------app的配置信息



jsonify()将字典转化成json对象

```python
@blue.route('/api/')
def api():
    persons = Person.query.all()
    #将列表中的对象转化成成字典
    person_list = list(map(lambda p:p.name,persons))
    return jsonify(person_list)
```

通过请求方式的增删改查

```python
@blue.route('/person/', methods=['get', 'post', 'put', 'dalete'])
def person():
    if request.method == "GET":#查
        persons = Person.query.all()
        person_list = list(map(lambda p:p.name,persons))
        return jsonify(person_list)
    elif request.method == "POST":#增
        name = request.form.get('name')
        age = request.form.get('age')
        p = Person()
        p.name = name
        p.age = age
        #自定义状态码
        data = {
            "status":1,
            "msg":'ok'
        }
        try:
            db.session.add(p)
            db.session.commit()
        except:
            db.session.rollback()
            db.session.flush()
            data["status"] = 0
            data["msg"] = 'fail'
        return jsonify(data)
    elif request.method == "PUT":#改
        name = request.form.get('name')
        newage = request.form.get('newage')
        data = {
            "status":1,
            "msg":'ok'
        }
        p = Person.query.filter_by(name=name).first()
        if p:
            p.age = newage
            db.session.commit()
        else:
            data['status'] = 0
            data['msg'] = 'fail'
        return jsonify(data)
        elif request.method == "PUT":#删
            name = request.form.get('name')
            data = {
                "status":1,
                "msg":'ok'
            }
            p = Person.query.filter_by(name=name).first()
            if p:
                db.session.delete(p)
                db.session.commit()
            else:
                data['status'] = 0
                data['msg'] = 'fail'
            return jsonify(data)

```

在装饰器调用时

在装饰器上加上@wraps(func)表示被装饰的函数还是函数本身，而不是装饰器函数的内函数

```python
def check(func):
    @wraps(func)
    def inner():
        userid = session.get('userid', '')
        if userid != '':
            return render_template('/admin/article.html')
        return func()
    return inner
```



博客项目要求：

1. 博客页面：
     创建连个表： 分类表1，文章表n
     在页面中动态显示分类信息和文章信息
2. 注册登录， 登录成功后才能进入后台管理系统
3. 文章 ： 增删改查 
4. 栏目（分类）：增删改查CURD