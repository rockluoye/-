# 目录结构

 sudo su root：切换到超级管理员

cd  /:切换到根目录

tree：以树形结构显示内容

/：根目录

/home 家目录，用来存放普通用户

/root 超级用户目录

/lib : 目录是根文件系统上的程序所需的共享库，存放了根文件系统程序运行所需的共享文件。这些文件包含了可被许多程序共享的代码，以避免每个程序都包含有相同的子程序的副本，故可以使得可执行文件变得更小，节省空间。

/bin ：存放常用的程序文件

/dev : 存放设备文件 

/etc 存放一些系统配置信息，如用户名密码

/var 可以存放日志，数据文件等

/temp 存放临时文件，定期清除

/usr ：在这个目录下，你可以找到那些不适合放在/bin或/etc目录下的额外的工具。比如游戏、打印工具等。用到的文件和应用程序几乎都在这个目录

## 常用命令

ls：列出指定目录下的所有文件

-a 包含隐藏文件（开头的文件）

-l 显示文件详细信息

ll相当于ls-al： 包含隐藏文件和显示文件的详细信息

-lht按时间降序排序出隐藏文件和显示文件的详细信息

-lhtr按时间升序排序出隐藏文件和显示文件的详细信息

ls -a：显示当前目录下的所有文件夹，包括隐藏文件



cat：查看文件的内容

head：查看文件内容，头10行

head -3 ：查看文件内容，头3行

tail：查看文件内容，尾10行

tail -3 ：查看文件内容，尾3行

more：more命令和cat的功能一样都是查看文件里的内容，但有所不同的是more可以按页来查看文件的内容，还支持直接跳转行等功能

less：less 与 more 类似，但使用 less 可以随意浏览文件，而 more 仅能向前移动，却不能向后移动，而且 less 在查看之前不会加载整个文件。

wc：显示文件行数，字节数以及文件名信息

stat：查看文件详细信息，可以获取文件的名，大小，权限

file：查看文件类型

echo：用于在终端输出字符串或者是变量的值

|：管道，作用：将一个命令的输出作为另一个命令的输入

\>：输出重定向，允许执行结果重定向到另一个文件中

\>>:如上但追加不清空

还可以有：cat a   b   >   c

less  c

more   c



cd：切换工作目录

	cd  切换到当前家目录
	cd ~切换到家目录
	cd /切换到根目录
	cd .切换到当前目录
	cd .. 切换到上一层目录
	cd - 切换到上一次的目录
	cd #切换到当前家目录

tree -l 2：用树结构显示两层

tree -f：显示树结构的绝对地址



 mv 重命名文件或者移动目录或者覆盖其他文件



cp 复制

-i：在目标文件存在的时候询问是否覆盖

-r：若给出的源文件是一目录文件，此时cp将递归复制目录下的文件

-a：复制时保持原有的属性

-f：对于已经存在的目标文件不提示

-v：显示拷贝进度



mkdir 创建目录 -p可以递归创建多层文件

递归创建文件：mkdir -p a/b/c/d

mkdir -p aa/{bb，cc}/{dd，ff}

mkdir .c：创建隐藏文件夹



clear：清除控制台

touch 创建空文件

atime：最后一次访问文件或目录的时间

mtime：最后一次修改内容的时间

ctime：最后一次改变属性的时间



vim filename:打开文件，并将光标置于第一行首

vim +n  filename：打开文件并将光标置于第n行首

vim  +   filename ：打开文件，并将光标置于最后一行首

vim：文本编辑器

```linu
i--------进入插入模式，在光标前
I--------在当前行首
a-------在光标后
A------在当前行尾
o------在当前行之下新开一行
O------在当前行之上新开一行
r------替换当前字符
R------替换当前字符及其以后的字符，直至按esc键
esc-----退出插入模式
：w-----保存	
：q------退出
：wq------先保存后退出
：q！-----强制退出
：w！----执行强制存盘
```


删除操作：

x：删除光标处的单个字符

dd：删除光标所在行

d^：删除当前字符到行首的所有字符

u：取消最近的一次操作，并恢复操作结果

ctrl  +  r 对使用u命令撤销的操作进行恢复库

### 文件类型

-代表是文件

d代表目录

b代表块设备文件

c代表字符设备文件

l代表链接文件

p代表管道文件

s代表socket文件



cat ：查看文件内容

history：查看历史记录



rmdir：删除给定的目录，只能是空文件夹

rm 删除文件或目录

  	-r 可以删除目录

	-ri：交互式删除，每次删除都会询问
	
	-rf 强制删除



ln 创建链接文件

	软链接：ln -s 源文件 目标文件
	
	硬链接：ln 源文件 目标文件

硬链接：硬连接指通过索引节点来进行连接。在Linux的文件系统中，保存在磁盘分区中的文件不管是什么类型都给它分配一个编号，称为索引节点号(Inode Index)。在Linux中，多个文件名指向同一索引节点是存在的。一般这种连接就是硬连接。硬连接的作用是允许一个文件拥有多个有效路径名，这样用户就可以建立硬连接到重要文件，以防止“误删”的功能。其原因如上所述，因为对应该目录的索引节点有一个以上的连接。只删除一个连接并不影响索引节点本身和其它的连接，只有当最后一个连接被删除后，文件的数据块及目录的连接才会被释放。也就是说，文件真正删除的条件是与之相关的所有硬连接文件均被删除。

软链接：另外一种连接称之为符号连接（Symbolic Link），也叫软连接。软链接文件有类似于Windows的快捷方式。它实际上是一个特殊的文件。在符号连接中，文件实际上是一个文本文件，其中包含的有另一文 件的位置信息。

软链接的特点：

1.软链接是存放另外一个文件的路径的形式存在

2.软链接可以跨文件系统，硬链接不可以、

3.软链接可以对一个不存在的文件进行链接，硬链接必须要有源文件

4.软链接可以对目录进行链接

硬链接的特点：

1.硬链接，以文本副本的形式存在，但不占用实际空间

2.不允许给目录创建硬链接

3.硬链接只有在同一文件系统中才能创建

4.删除其中一个硬文件并不影响其他相同的inode号文件

区别：

1.硬链接原文件/链接文件公用一个inode号，说明他们是同一个文件，而软链接原文件/链接文件拥有不同的inode号，软连接是独立的文件，类似于快捷方式，存储着源文件的位置信息便于指向，表明他们是两个不同的文件；
2.在文件属性上软链接明确写出了是链接文件，而硬链接没有写出来，因为在本质上硬链接文件和原文件是完全平等关系；
3.链接数目是不一样的，软链接的链接数目不会增加；
4.文件大小是不一样的，硬链接文件显示的大小是跟原文件是一样的。而这里软链接显示的大小与原文件就不同了

查看

cat  文件  |  grep  -cinv aaa

-c：显示aaa字符在文件中的数量

-i：显示有aaa字符的行

-n：显示有aaa字符的行，并显示是第几行

-v：显示出含有aaa字符之外的所有行



| grep：筛选，检索

find：按条件查找

-name：精准匹配

-size;匹配文件大小

find -size  +1k：查找文件大于1k的

find -size  -1k：查找文件小于1k的

-empty：查找空文件

-perm：查找指定权限的



locate：查找数据

-i：忽略 大小写

-c：不输出找寻结果，仅计算结果数

sort：给文件内容进行排序

-f：忽略大小写差异

-b：忽略空格部分

-r;反向排序

-n：使用纯数字排序

cut：可以从一个文本文件或者文本流中提取文本序列

-c：按字符取值

tee：读取标准输入的数据，并将其内容输出成文件



which查找其他命令所在位置

如：which ls，which  cd ..........

type 寻找命令所在位置包括命令别名

# 压缩

tar【参数】打包文件名 文件

	-c 生成档案文件，创建打包文件
	-v  列出归档解档的详细过程，显示进度
	-f  指定档案文件名称，f后面一定是.tar文件，所以必须放选项最后
	-t 列出档案中包含的文件
	-x 解开档案文件，拆包

gzip：

	解压   gzip【选项】待解压文件
	压缩    gzip【选项】被压缩文件 压缩后文件名
	选项  -r 压缩所有子目录   gzip -r 1.tar 1.tar.gz
		-d  解压             gzip -d 1.tar.gz

结合tar使用：

			压缩   tar -cvzf 1.tar.gz 文件（*.txt）
			解压   tar -xvzf 1.tar.gz解压到当前目录
			tar -xvzf 1.tar.gz -C   /temp   解压到指定目录

bzip与gzip类似：用法是将gzip中-z改为-j

zip与unzip：通过zip压缩文件的目标文件不需要扩展名，默认为zip

压缩格式：     zip【-r】目标文件    源文件

解压：            unzip -d 解压后目录文件   压缩文件

# 用户和组

root：超级管理员，通常用于系统的管理和维护，对linux系统具有不受任何限制的操作权限

whoami：查看当前系统当前用户的用户名

who：查看当前所有登录系统的用户信息

exit：退出

如果切换后的用户，则返回上一个登录的账号

su：切换用户

useradd：添加用户

如：sudo useradd -m -s /bin/bash  lisi

userdel：删除用户

如：sudo userdel -rf  lisi

passwd：设置密码

如：sudo passwd lisi

一般存在/home目录中

添加过程：

	进入root的home目录后
	1.useradd zahngsan----------添加用户
	2.mkdir  /home/zhangsan-----在home目录下创建一个和用户同名的目录
	3.sudo chown zhangsan：zhangsan /home/zhangsan---将新建的用户和新建的用户目录联系起来
	4.sudo passwd zhangsan------设置密码
	5.ls -a /home/rock/.bash*------进入其他用户家目录查看其他用户的配置信息
	6.ls -a /etc/skel/----------查看配置文件
	7.cp /etc/skel/.bash* .----进入新建用户home目录，拷贝配置文件

第二种方式：

	1.sudo useradd -m -s /bin/bash lisi-----添加用户
	2.sudo passwd lisi-------设置密码

第三种方式：

	sudo useradd -m wangwu--------添加用户，然后设置密码

建议使用第二种方式

-m 强制建立用户主文件夹，并将/etc/skel/当中的配置复制过来，自动建立用户的登入目录； 

-s shell。用户登录所使用的shell

删除用户：

sudo userdel -rf 用户名

组：

作用：将多个用户管理在同一个组下，方便管理，可以让不同用户享用同种权限

将用户加到root1组中：

useradd -g root1 zhangsan

查看组--------cat /etc/group

添加组 sudo groupadd python1901

sudo useradd -m -s /bin/bash  -g python1901 zhaoliu------创建用户并添加到组python1901中

usermod：修改用户的基本信息

-g 修改用户所属的组

-l 修改用户账号名称

如：sudo usermod -g python1901 wangwu

sudo usermod -l wangba wangwu----修改用户名

创建用户并分组

sudo useradd –m –s /bin/bash –g root lisi

删除组：

sudo userdel -rf  wangwu-----删除组内的用户

sudo groupdel python1901----删除组

sudo：让当前用户暂时以管理员的身份root来执行命令

权限：

chmod ：修改文件权限

drwxr-xr-x  4 root root 4096 6月   9  2018 .WebStorm2018.1/

rwx：当前用户的权限

r-x：同组内其他用户的权限

r-x ：其他组内用户的权限

r 读取权限，数字代号为4

w 写入权限，数字代号为2

x执行权限，数字代号为0

— 不具备任何权限，数字代号为0

0     不可读 不可写 不可执行

1      不可读 不可写 可执行

2     不可读 可写 不可执行

3     不可读 可写 可执行

4     可读 不可写 不可执行

5      可读 不可写 可执行

6      可读 可写 不可执行

7      可读 可写 可执行

修改时：例：

数字法：

chmod 751 file

文件所有者：读写执行权限

同组用户：读执行的权限

其他用户；执行的权限

字母法：

chmod u/g/o/a    +/-/= rwx   文件

u：user表示该文件的所有者

g：group表示与该文件的所有者属于同一组者

o：other表示其他以外的

a：表示三者皆是

+：表示增加权限

-：表示撤销权限

=：设定权限

例：chmod u+x filname

 chmod u=rwx,g=rx,o=r filename

修改文件所有者

格式：chown 新的用户名     文件名

charp     新的组     文件名

# 进程

ps：查看进程信息

-a   显示终端上的所有进程，包括其他用户的进程

-u   显示进程的详细状态

-x    显示没有控制终端的进程

-w    显示加宽，以便显示更多的信息

-r      只显示正在运行的进程

top 动态显示进程

M      根据内存使用量来排序

P         根据CPU占有率来排序

T         根据进程运行时间的长短来排序

U        可以根据后面输入的用户名来筛选进程

K         可以根据后面输入的PID来杀死进程

q退出

查pid号：sudo ps -aux | grep 程序名

kill：终止进程

格式   kill   -9   PID

df 显示磁盘上的可使用情况

du 检测目录所占磁盘空间

reboot：重启

shutdown -h  now：立即关机



ping    测试远程主机的连通性

ifconfig 显示网卡信息，ip地址

wget  www.baidu.com将网站中的东西爬下来存到index.html中

curl ww.baidu.com  中的直接显示在终端黑屏中

安装：

1.apt	

sudo apt-get  install  package------安装包

sudo apt-get  remove  package------安装包

sudo apt-get  update

# git

## 本地仓库

#### 1.安装git

pip install git

#### 2.创建版本库

mkdir hello------创建目录，在hello目录下创建

cd hello----进入hello文件夹

git init---------将普通目录变成版本库

#### 3.把文件添加到版本库

touch  a.txt----创建文件

git add a.txt------将文件添加到缓存区

git status------查看git状态

git comfig  --global  user.email  “you @example.com”---第一次使用

git comfig  --global  user.name “Rock”---第一次使用

git commit  -m  ‘创建了新文件...’------提交并写日志信息

git reset HEAD 文件名---------取消文件的暂存

git diff--------查看文件的区别

#### 4.版本回退

git log----修改的日志信息

git log --pretty=oneline-------一行显示日志信息

git reset  --hard  HEAD^------回退到上一个版本

git reset  --hard  HEAD^^------回退到上一个的上一个版本

git reset  --hard  HEAD~100------回退到上100个版本

git reset  --hard  版本号(如:566280d)---回退到版本号位置

git reflog----显示所有历史操作

#### 5.文件删除

git rm c.txt-----删除c.txt文件

git remote  rm origin：移除远程仓库的关联

## 远程仓库

#### 1.本地发送

1.创建github账号

2.生成ssh-keygen  -t  rsa -C “邮箱”-----建立本地和网络的连接

3.添加到github

4.检测是否添加成功

	命令：ssh -T git@github.com

5.cd到本地仓库目录如：hello

6.在github中点击+号中的New repository

7.在远程仓库中给文件命名，可以与本地相同也可以不同，并选择是否公开

8.在本地仓库git  remote  add  origin   http：//github.com/Rock/python1902.git-----本地仓库和远程仓库关联起来

9.git push -u origin master--------将本地仓库的推送到远程仓库

10.若存在远程连接可用git remote rm origin删除远程连接

11.在push时注意以下几点：

	1.本地git仓库目录下不能为空
	
	2.本地仓库add后未commit
	
	3.git init错误

12.git stash可以将缓存区的暂停从而不影响commit的步骤

git stash  list显示封存记录

git stash pop 是取出最新的一次暂存数据，pop后，暂存区就不会存在这次数据了

git stash apply 读取暂存区的数据，通过apply后，暂存区的数据依然存在

##### 2.拉取远程仓库的数据

第一种方法：

1.在本地创建空仓库---mkdir + git init

2.连接远程仓库----git remote add origin 远程仓库地址(如：https://github.com/rockluoye/hello.git)

3.拉取主分支的数据----git  pull origin  master

 4.修改后按原步骤提交到远程仓库

第二种方法：

1.git clone  远程仓库地址(如：https://github.com/rockluoye/hello.git)---------------在克隆后会自动在此目录创建远程仓库同名的文件夹此文件夹关联着远程文件夹

2.修改后按原步骤提交

第三种：

git fetch：将某个远程主机的更新，全部取回本地。默认情况下，git fetch取回所有分支的更新。如果只想取回特定分支的更新，可以指定分支名

git  fetch  origin  master：取回origin中的master分支

#### 3.分支与冲突

查看分支状态----git  branch

删除分支----git branch -d dev(分支名称)

当d为D时是强制删除

创建分支----git branch  分支名称

git merge dev：合并分支（Fast Forward）

git merge  --no-ff  -m “log”  dev：合并分支（有记录）

git remote -v----------显示出详细的url地址名和对应的别名

##### 1.创建分支并切换到该分支

git  checkout   -b  dev(新分支名称)

git checkout  分支名称------切换到某分支

##### 2.在分支dev中添加或修改内容

##### 3.切换到主分支，将分支中的修改内容同步过来

git checkout master-----切换到主分支

git merge dev------将分支dev的内容同步过来

##### 4.当分支与主分支有同名文件夹时会发生冲突其内容会合并，需要手动修改，修改后提交

##### 5.使用git log --graph可以查看分支合并图

##### 6.如果合并分支时使用Fast forward，在删除分支的时候会丢掉分支信息

当强制禁用Fast forward模式，git会在merge时生成一个新的commit，这样历史就可以看到分支信息了

本地仓库可连接多个远程用git  remote  add origin2   远程仓库地址(如：https://github.com/rockluoye/hello.git)来增加远程仓库

#### 4.推送分支

git push 