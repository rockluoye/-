## Tornado引入：

##### python框架种类：

Django框架：重量级

Flask框架：轻量级

Tornado框架：可以做web框架，但不建议。主要用于高并发

sanic框架：高性能框架

##### 4种虚拟环境创建：

1.mkvirtualenv

2.用pycharm

3.使用python中的venv模块：python -m venv  虚拟环境名称

4.virtualenv -p 版本地址  虚拟环境名称

activate：win在cmd中激活虚拟环境

source  activate：mac/ubuntu/centos在cmd中激活虚拟环境

## 创建小应用

```python
import tornado.ioloop
import tornado.web
from tornado.options import options, define, parse_command_line

#设置默认端口，和端口的类型值
define('port', default=8080, type=int)


#定义处理方法
class MainHandler(tornado.web.RequestHandler):
    #定义处理get请求-----http行为方法,GET:用于查询
    #POST：增加数据
    # PUT，PATCH：用于修改
    # DELETE：用于删除
    def get(self):
        #http：//127.0.0.1：8000/
        self.write("Hello,world")

    # 定义处理post请求
    def post(self, *args, **kwargs):
        self.write("Hello,world")

    def put(self, *args, **kwargs):
        self.write('put')

    def patch(self, *args, **kwargs):
        self.write('patch')

    def delete(self, *args, **kwargs):
        self.write('delete')


class ReqHandler(tornado.web.RequestHandler):
    def get(self, *args, **kwargs):
        #get传递参数：request.args
        #post传递参数：request.form
        #tornado中获取请求传递的参数:
        # self.request.argument[key]一个   self.request.arguments[key]多个
        # self.get_argument(key)一个   self.get_arguments(key)多个
        name = self.get_arguments('name')
        self.write(name)

    def post(self, *args, **kwargs):
        #tornado中获取POST请求的参数：
        self.write("获取")


def make_app():
    return tornado.web.Application(handlers=[
        ("/index/", MainHandler),   #/为路由地址 ，MainHandler为处理方法
        ("/req/", ReqHandler),
    ],

    )


if __name__ == '__main__':
    #解析命令行中的参数
    parse_command_line()
    app = make_app()
    #监听端口
    app.listen(options.port)
    #启动一个io事件循环监听端口请求（启动tornado程序）
    tornado.ioloop.IOLoop.current().start()
```

HTTP方式：

GET:用于查询
POST：增加数据
PUT(修改全部字段)，PATCH(修改部分字段)：用于修改
DELETE：用于删除

get：请求的缺陷-----长文本类型超出部分会丢失

##### 获取请求传递的参数

1.获取一个key值self.request.argument[key]，若一个key有多个值可以用self.request.argument(key)获取--------只能get使用

2.self.get_argument(key),self.get_arguments(key)与上同理---get与post可用

3.self.get_body_argument(key), self.get_body_arguments(key)与上同理--除了get请求以外都能用

##### 请求与响应

self.request.method----获取请求方式

self.request.cookies---获取cookies内容

self.request.path----获取请求路由

self.request.files---获取上传文件

修改状态码为500：self.set_status(500)

设置cookies：self.set_cookie(“token”，"123456"，expires_day=1)key为token,值为123456，过期时间为1天

redirect跳转：self.redirect('/index/')跳转到index的路由

render渲染页面：self.render('index.html')渲染index.html的页面

self.write()响应给客户端数据

小应用中的参数：

1.生成Application对象，初始化时定义handlers参数

2.监听端口，Application对象.listen(端口)

3.启动：tornado.ioloop.IOLOOP.current().start()

命令行参数：

1.解析命令行参数：parse_command_line()

2.取参数：option.port

3.定义默认参数值：define('port',default=8000,type=int)

定义行为方法：

def get()

def post()等

##### 路由匹配规则取参数：

在定义路由是定义参数位置

有参数：

第一种：('/day1/(\d+)/(\d+)/(\d+)/')

在取参数时按位置与路由位置一一匹配：

```python
self.write('years:{year} month:{month} day:{day}'.format(
    year=year,
    month=month,
    day=day
))
```

第二种：('/day2/(?<year>\d+)/(?<month>\d+)/(?<day>\d+)/')

取参数时不需要按路由位置取值，一样能得到

```python
self.write('years:{year} day:{day} month:{month}'.format(
    year=year,
    month=month,
    day=day
))
```

#### 模板语法：

##### 1.在路由函数中定义模板路径

```python
template_path=os.path.join(os.path.dirname(os.path.abspath(__file__)), 'templates'),
static_path=os.path.join(os.path.dirname(os.path.abspath(__file__)), 'static'),
```

os.path.abspath(\__file__)指的是当前文件的绝对路径

os.path.dirname()指的是括号中路径的上层文件路径

os.path.join()将参数路径进行拼接形成模板路径

##### 2.静态资源与动态资源的加载

挖坑与填坑：{% block title %}{% end %}

继承父模板：{% extends  ‘base.html’ %}

指定css文件位置：

加载静态资源css资源

<link rel='stylesheet' href='/static/css/style.css'>

反向解析出静态css资源

<link rel='stylesheet' href='{{ static_url('css/style.css') }}'>

注解：{#  #}

循环1：{% for itme in itme1 %}{{ itme }}{% end %}

循环2：{% while  itme %}{{  item.pop()  }}{% end %}直到itme为空时停止，pop（）为弹出

判断：{% if itme == 30  %}{{ itme }}{% else %}<p>haha</p>{% end %}

列表取值：{{ itme[0] }}

试运行：{% try %}{% except %}{% finally %}{% end %}

如果try出异常执行except，finally无论如何都要执行

在模板中定义变量{% set  n = 10 %}{{ n }}

渲染模板：render(模板名称，k=v,k1=v1)

#### 数据库操作

导包：pip install  sqlalchemy

模型定义

```python
from sqlalchemy import Column, String, Integer
class Student():
    #自增的组件id
    id = Column(Integer, primary_key=True, autoincrement=True)
    #长度为32的不能为空的字段
    s_name = Column(String(32), unique=True)
    #默认值为20的int类型的s_age字段
    s_age = Column(Integer, default=20)
    #默认情况下tablename不写，则表名为模型名称
    __tablename__ = 'student'
```

创建包utils，并在其中创建setting.py

在文件中

```python
from sqlalchemy import create_engine
from sqlalchemy.orm import sessionmaker
from sqlalchemy.ext.declarative import declarative_base
import pymysql

#创建连接
url = 'mysql+pymysql://root:rock1204@127.0.0.1：3306/tornadodb'
engine = create_engine(url)

# 创建session（事务的增强版本）
SessionMaker = sessionmaker(bind=engine)
session = SessionMaker()

#指定模型和数据库中表的关联关系的基类
Base = declarative_base(bind=engine)
```

在models文件中创建函数，用来执行迁移操作

```python
from utils.settings import Base


def create_db():
    #迁移模型，映射成表
    Base.metadata.create_all()
    #删除模型对应的表
    #Base.metadata.drop_all()
```

添加操作

```python
#创建学生对象并赋值
stu = Student()
stu.s_name = username
stu.s_age = age
#提交
session.add(stu)
session.commit()
```

查询操作

```python
stus = session.query(Student).filter(Student.s_name == 'coco').all()
#获取主键所在行的数据对象，如果主键值不存在返回None
#Django中：get(条件)，条件必须成立，且结果唯一
stus = session.query(Student).get(id)
```

删除

```python
stu = session.query(Student).get(1)
session.delete(stu)
session.commit()
```

修改

```python
stu = session.query(Student).get(2)
stu.s_age = 30
session.add(stu)
session.commit()
```

#### tornado中的同步与异步爬取源码内容-----进行压力测试

##### 同步获取源码

```python
import tornado.web
import tornado.ioloop
import tornado.httpclient


class SearchHandler(tornado.web.RequestHandler):

    def get(self, *args, **kwargs):
        #获取源码
        wd = self.get_argument('wd')    #获取get传参的参数
        client = tornado.httpclient.HTTPClient()  #获取http客户端，用来实例化发送请求的对象
        response = client.fetch('http://www.baidu.com/s?wd={}'.format(wd))#fetch()方法，获取某个地址的响应结果
        print(response)
        self.write('获取百度搜索某参数源码')


def make_app():
    return tornado.web.Application(
        handlers=[
            ('/search/', SearchHandler),
        ]
    )


if __name__ == '__main__':

    app = make_app()
    app.listen(8000)
    tornado.ioloop.IOLoop.current().start()
```

使用apache的ab进行压力测试

在cmd中cd到ab所在目录

ab -c 10  -n 1000  http://127.0.0.1:8000/search/?wd=ab

用ab程序；-c模拟十个人去执行；-n发送1000个请求

用ab程序模拟10个人每秒发送1000个请求到地址http://127.0.0.1:8000/search/?wd=ab

##### 用异步获取源码

```python
import tornado.web
import tornado.ioloop
import tornado.httpclient


class SearchHandler(tornado.web.RequestHandler):
    #表示io不主动关闭
    @tornado.web.asynchronous
    def get(self, *args, **kwargs):
        #异步获取源码
        wd = self.get_argument('wd')
        client = tornado.httpclient.AsyncHTTPClient()#定义异步客户端
        response = client.fetch('http://www.baidu.com/s?wd={}'.format(wd), callback=self.on_response())  # 异步爬取时的callback回调方法，只要有任何fetch响应了，就会调用回调方法
        print(response)
        self.write('获取百度搜索某参数源码')

    def on_response(self, response):
        print(response)
        print('异步操作结束')
        #主动关闭io
        self.on_finish()


def make_app():
    return tornado.web.Application(
        handlers=[
            ('/search/', SearchHandler),
        ]
    )


if __name__ == '__main__':

    app = make_app()
    app.listen(8000)
    tornado.ioloop.IOLoop.current().start()
```

##### 以同步形式写成异步效果

```python
import tornado.web
import tornado.ioloop
import tornado.httpclient


class SearchHandler(tornado.web.RequestHandler):
    #表示io不主动关闭
    @tornado.web.gen.coroutine
    def get(self, *args, **kwargs):
        #异步获取源码
        wd = self.get_argument('wd')
        client = tornado.httpclient.AsyncHTTPClient()#定义异步客户端
        response = yield client.fetch('http://www.baidu.com/s?wd={}'.format(wd))  #yield的形式进行等待，实现异步操作




def make_app():
    return tornado.web.Application(
        handlers=[
            ('/search/', SearchHandler),
        ]
    )


if __name__ == '__main__':

    app = make_app()
    app.listen(8000)
    tornado.ioloop.IOLoop.current().start()
```

##### 使用putty或Xshell远程连接云服务器并设置远程数据库

输入公网地址，连接

输入用户名，密码登录

python + tab-----查看python版本

更新ubuntu的源---apt   update

安装mysql--------apt  install  mysql-server  mysql-client

修改配置参数

进入到文件夹cd  /etc/mysql/mysql.conf.d

将文件中的mysqld.cnf中的bind-address     =127.0.0.1注释掉

打开数据库，并使用数据库----

进入数据库：mysql  -u  root  -p

切换到mysql数据库：use mysql；

创建root账户：create  user  ‘root‘@’%’  identified  by  ‘密码’；

密码一般为代码中进入数据库的密码

给root用户设置最大权限

grant  all privileges  on \*.*  to 'root'@'%'  identified  by  '密码'；

刷新权限表：flush privileges；

退出数据库并重启

重启数据库----service  mysql  restart

通过以下的命令查找出-添加安全组规则，并打开进行设置

   更多---》网络和安全组----》安全组配置----》配置规则---》添加安全组规则

将端口设置为3306/3306

将授权对象设置为0.0.0.0/0

点击确认

打开可视化工具，建立远程数据连接

ip：设置为服务器公网ip

用户名为root

密码为：刚才设置的’密码‘

建立项目数据库

##### 在服务器的home上建立目录

code，conf，env，logs

code：用来存放执行文件

conf：用来存放uwsgi

env：用来存放虚拟环境

logs：用来存放日志文件

进入env目录安装pip-----apt  install  python3-pip

安装虚拟环境包------pip3   install  virtualenv

virtualenv  环境名称-----当默认为python3时可以使用此命令

virtualenv --no-site-packages blognev  指定python版本安装

也可以用

安装venv模块来安装虚拟环境

aptinstall python3-venv

##### 创建虚拟环境

python3 -m venv blognenv

source  activate-----激活虚拟环境

deactivate----退出虚拟环境

用XShell软件直接将代码拉进code目录下

用putty上传文件：

打开psftp，cd到文件所在目录下，执行命令

pscp 要上传的文件 root@公网ip:/home/code

在code下的blogpro代码目录下创建txt文件用来记录要装的包

以绝对路径安装已经记录的包：/home/env/blogenv/bin/pip3 install -r requirement.txt

在可视化工具中使用数据传输，将本地数据库中的数据传输到云服务数据库中的数据库中

以绝对路径运行manager文件：/home/env/blogenv/bin/python3   /home/code/blogpro/manager.py     runserver   -h  0.0.0.0  -p   80

就可以运行了

当退出时，不能再后台继续运行，但使用的端口依然被占用，需要用杀进程的方式将进程停掉，一般使用：netstat  -lntp查找进程，kill  -9 pid杀进程

使用挂载nohup使程序在后台运行

在代码所在目录建立*.sh文件,我建立为start_blog.sh文件

在文件中写入执行命令：/home/env/blogenv/bin/python3   /home/code/blogpro/manager.py     runserver   -h  0.0.0.0  -p   80

：wq  保存后退出

修改start_blog.sh文件的权限：chmod  -R  777  start_blog.sh

后台挂起启动文件：nohup  ./start_blog.sh  &



##### 第二种使用nginx包进行挂载

1.安装包----apt  install   nginx

2.查看nginx的服务状态---service  nginx  stat

3.若状态为failed重启---service  nginx  restart，启动后nginx会监听80端口

4.在conf中创建blognginx.conf文件，写入以下文件

server {
 listen 80;
 server_name 47.240.0.28;

 location / {
  include uwsgi_params;
  uwsgi_pass 127.0.0.1:8080;

  uwsgi_param UWSGI_CHDIR /home/code/BlogPro;
  uwsgi_param UWSGI_SCRIPT manage:app;

 }
}

其中80为要监听的端口

47.240.0.28为公网ip

uwsgi_pass 127.0.0.1:8080;为将所有的请求都给127.0.0.1：8080来响应

5.编辑nginx下的文件nginx.conf,一般在62行之下导入blognginx.conf文件

------include /home/conf/*.conf;

6.重启service  nginx  restart

7.在conf目录中创建bloguwsgi.ini文件，在文件中写入

[uwsgi]
master=true
socket=127.0.0.1:8080
chdir=/home/code/BlogPro
pythonpath=/home/env/blogenv/bin/python3
callable=app
logto=/home/logs/bloguwsgi.log

启动程序

/home/env/blogenv/bin/uwsgi --ini /home/conf/bloguwsgi.ini &





