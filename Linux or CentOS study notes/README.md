## Linux基础命令笔记

### 0.输入命令行操作

```
帮助
man xx命令 或 info xx命令

清空本行
Ctrl+u

回到文开头
Ctrl加a
回到文末
Ctrl加e

回到行末删除一个字符
Ctrl+_

删除光标本段后一段
Alt加d
删除光标本段前一段
Ctrl加w

删除光标后的全部
Ctrl加k

删除光标前一个
Ctrl加h
删除光标后一个
Ctrl加d

光标后直到本段结束全部小写字母变大写
Alt加u

换行重写
Ctrl加c

清除输入
Ctrl加l
Ctrl加d
clear

退出终端
exit

```

### 1.重启
```
1.普通重启
reboot

2.立即重启
shutdown -r now
```

-------

### 2.vim

#### 打开文件
```
打开单个文件  
vim 文件名
// 没有还文件则会创建，想不保存:q!即可

打开多个文件 
vim file1 file2 file3
// 显示多个文件 :vsplit
// 切换窗口 ctrl+w+方向键
```

#### 内容操作

```
在光标所在字符后插入
a
在光标所在行尾插入
A
在光标所在字符前插入
i
在光标所在行行首插入
I
在光标下插入新行
o
在光标上插入新行
O

:w 将编辑过的文本保存
:w! 若文本属性为只读时，强制保存
:q 退出vim
:q! 不管编辑或未编辑都不保存退出
:wq 保存，退出
:e! 将文档还原成最原始状态
ZZ 若文档没有改动，则不储存离开，若文档改动过，则储存后离开，等同于:wq
:w [filename] 编辑后的文档另存为filename
:r [filename] 在当前光标所在行的下面读入filename文档的内容
:set nu 在每行的行首显示行号
:set nonu 取消行号
n1,n2 w [filename] 将n1到n2的内容另存为filename这个文档
:! command 暂时离开vim运行某个linux命令
```

-------

### 3.远程拷贝

```
将原地址下的README.md拷贝到服务器的root目录下来
scp ./README.md root@120.78.209.130:/root/

从服务器将整个文件夹内容拷贝到本地
scp -r root@120.78.209.130:/root/openfire
```

-------

### 4.

```
.bnnnn
```

-------

### 5.查看文件

```
将文件内容全部列出
cat log.txt
带行号列出全部内容(空行忽略行号，只计算有内容的行)
cat -b log.txt
带行号列出全部内容
cat -n log.txt

列出部分文件内容
more [选项] log.txt
// 显示文件中从第3行起的内容 more +3 log.txt
// 设定每屏显示5行 more -5 log.txt
// 按空格查看10%
// 按回车查看一行
// 向下查看一屏 f
// 向上查看一屏 b
// 退出查看 q
// 搜索内容 / 内容

打开文件搜索关键词
grep [选项] 关键词 文件名
// 例如 grep 你好 test.cpp
// 显示行号 grep -n as 你好 test.cpp
// 反转关键词 -v
// 反转关键词并显示行数 -vn
// 关键词忽略大小写 -i
// 关键词忽略大小写并显示行号 -in
// 搜索关键词中有空格要用引号 grep "你好 世界" test.cpp
// 关键词位于行首 grep ^关键词 文件名
// 关键词位于行末 grep 关键词$ 文件名
```

-------

### 6.重定向

```
将输出信息ls -lh 的输出信息重定向保存到inputinfo.txt中
命令 > 文件名
// 例如 ls -lh > inputinfo.txt

文件内容末尾追加重定向
命令 >> 文件名

将输入的内容输入(并不会执行该命令，只是单纯将输入的内容输出一下)
echo 命令
```

-------

### 7.管道|

```
通过管道|将ls的内容给more显示
ls -lha | more 
通过管道将ls内容搜索
ls -lha | grep 关键词
```

-------

### 8.查看配置信息

```
查看全部信息
ifconfig 
通过管道并过滤查看ipv4(inet)
ifconfig | grep inet

查看ping连接
ping ip地址或域名
// 检测本地的 ping localhost
// 按Ctrl+c停止ping
// ping值越小越快
```

-------

### 9.ssh连接

```
ssh -p 端口号 账户@公网ip/域名
// 例如 ssh -p 22 root@127.0.0.1
// 简写可去掉-p 22

ssh特点
// 加密传输，安全
// 压缩传输，快
// 需要开启22端口
```

-------

### 10.ssh免密码登陆(注：在客户端生成)

```
回到home
cd ~
打开 .ssh
cd .ssh
生产Key
ssh-keygen
// 按回车输入密码，会生产id_rsa.pub文件

复制客户端生产的公有密匙到服务端的~/.ssh/authorized_keys
ssh-copy-id -i ~/.ssh/id_rsa.pub 服务器用户名@公网ip
然后以后连接该服务端不用输入密码了
ssh account@ip
```

-------

### 11.ssh连接设置别名

```
在客户端.ssh目录下创建config
touch config
写配置
vim config

配置内容:
Host 别名
  HostName 120.78.209.130
  Port 22
  User root
  IdentityFile ~/.ssh/id_rsa.pub
  IdentitiesOnly yes

连接
ssh 别名
```

-------

### 12.文件操作

```
注：可配合以下使用
// 不显示大小单位 -l 
// 显示大小单位 -h 
// 显示隐藏文件 -a 
// 可以混合使用 -lha 

列出文件 
ls [选项] 或 ll [选项] 
// 详细显示 -l
// 简单显示文件名，配合使用可可显示k单位 -h
// 显示隐藏文件 -a
// 配合使用 -lha 

文件树形式列出
tree 路径
// termux需要安装，按提示即可

打开文件夹
cd 
// 打开根目录 cd /
// 打开上级目录 cd ..
// 打开上两级目录 cd ../..

显示当前目录
pwd 

创建文件
touch 文件名

删除文件
rm [选项] 文件名
// 删除的时候会提示是否确认删除，一次删除多个文件则每一个文件都会提醒 -i 
// 一次删除多个文件（大于三个），提示消息只提示一次 -I
// 递归删除，用于删除目录 -r 
// 用于删除空目录，如果目录不为空，则无法删除 -d 
// 强制删除并不询问(慎用慎用慎用) -f 
// 强制删除并不提示删除home目录所有文件 rm -rf home/*

创建文件夹
mkdir [选项] 文件夹名
// 创建多层次 mkdir -p a/b/c/d
// 同层次创建多个文件 

删除文件夹
rmdir [选项] 文件夹名

复制文件
cp [选项] 源文件或目录 目标文件或目录
// 将home/log.txt复制到当前目录 cp /home/log.txt .
// 将当前目录的log.txt复制到/home/并改名test.txt 
cp log.txt /home/test.txt
// 显示复制结果 -v 
// 连带文件属性复制(即原文件的日期权限等) -p 
// 复制文件夹 -r 
// 复制并覆盖(覆盖前会询问) -i 
// 强制复制文件或文件夹，无论目标文件或文件夹是否存在 -f 
cp -f a.txt b.txt

移动文件
mv [选项] 源文件或目录 目标文件或目录
// 若需覆盖文件，则覆盖前先行备份 -b 
// force 强制的意思，如果目标文件已经存在，不会询问而直接覆盖 -f 
// 若目标文件存在则会询问 -i 
// 若目标文件已经存在，且内容比较新，才会移动 -u 
```

#### 打开文件夹

```
绝对路径打开目录
cd /storage/emulated/0

匹配打开QQfile_recv
cd *recv

匹配打开/storage/emulated/0
cd /*age/*ted/0

打开上一次cd路径
cd !$

打开根目录
cd /

打开主目录
cd ~ 或 cd $HOME 或 cd 

打开上一级目录
cd ..

打开上两级目录
cd ../..

打开此目录之前所在的目录
cd -
```

#### 找文件

```
find 路径 [选项] "搜索内容(可用通配符*)"
// 按文件名找 -name
// 例如找apk后缀的文件
// 一定要加路径  当前路径`pwd`
find /home/ -name '*apk'

正侧查找 在当前目录及子目录中，查找大写字母开头的txt文件
find . -name '[A-Z]*.txt' -print 

查找2天内被更改过的文件 
find . -mtime -2 -type f -print 

查找2天前被更改过的文件 
find . -mtime +2 -type f -print 

查找一天内被访问的文件 
find . -atime -1 -type f -print 

查找一天前被访问的文件 
find . -atime +1 -type f -print 

查找一天内状态被改变的文件 
find . -ctime -1 -type f -print 

查找一天前状态被改变的文件 
find . -ctime +1 -type f -print 

查找10分钟以前状态被改变的文件 
find . -cmin +10 -type f -print 
```

#### 文件权限

```
文件权限说明
属主：该文件创建者或被指定的文件所属者
属组：文件的所属组（在该组内的非属主用户对该文件拥有该属组权限）
其他：其他用户，既不属于属主又不在属组的用户
// d rwx r-- r-- 分别为：是文件夹 属主(user) 属组(group) 其他(other)
// 文件夹 d
// 只能读 r-- 
// 只能写 -w-
// 只能执行 --x
// 可读可执行 r-x
// 可读可写可执行 rwx
// 以此类推

修改文件权限
chmod 权限 文件
// 例如 chmod 777 log.txt 
// 这个里的777分别代表user，group，other的权限，777可读可写可执行
```

-------

### 13.系统操作

```
注：可配合以下使用
// 不显示大小单位 -l 
// 显示大小单位 -h 
// 显示隐藏文件 -a 
// 可以混合使用 -lha 

查看日期
date

查看日历
cal [选项] 
// 整一年的日历

查看当前连接到服务器的所有用户列表
who

查看当前连接到服务器的用户(自己)
whoami

查看磁盘
df [选项] 
// 单位为kb -k
// 单位为mb -m

查看系统文件
du [选项] 

查看公网ip
curl members.3322.org/dyndns/getip 

查看服务器名称
hostname

查看网络信息
ifconfig

Linux查看版本当前操作系统发行版信息
cat /etc/redhat-release

CPU信息
cat /proc/cpuinfo

查看内核/操作系统/CPU信息
uname -a

查看环境变量资源
env

查看用户登陆日志
netstat -antp

查看网络统计信息进程
netstat -s

查看所有已经建立的连接
netstat -antp

查看所有安装的软件包
rpm -qa

查看用户
id 用户名

查看CPU型号
cat /proc/cpuinfo | grep name | cut -f2 -d: | uniq -c

Linux内核版本和gcc版本
cat /proc/version

显示内存空间的统计信息，对分析虚拟内存行为很有用
cat /proc/zoneinfo
```

#### 进程(PID)

```
查询进程详细状况
ps [选项] 
// -a
// -u
// -x

动态显示运行的进程并排序
top

终止进程
kill [选项] 进程代号(PID)
// 强制杀死 -9
```

-------

### 14.自定义命令

```
vim打开.bashrc
vim ~/.bashrc
// 没有该文件自己创建

添加自定义命令
alias 自定义命令 = '命令'
// 例如 
alias sshlink='ssh root@120.78.209.130' (坑：这里等于号左右不能有空格)

if [ -f /etc/bashrc ]; then
. /etc/bashrc
fi

自定义命令生效
source ~/.bashrc

重启后失效 难受🌚
```

-------

### 15.端口(坑：腾讯云阿里云服务器需要到控制台安全组里设置端口，命令没用)

```
查看已经放行的端口
firewall-cmd --list-ports 
// 坑：腾讯云安全组里的查不到

列出所有端口
netstat -ntlp 
// 可以看安全组里的

查看某一端口是否开放如8080端口
firewall-cmd --query-port=8080/tcp
// 开放返回 yes否则为 no

永久开放8080端口
firewall-cmd --zone=public --add-port=8080/tcp --permanent
开放成功返回 success

移除开放的8080端口
firewall-cmd --permanent --zone=public --remove-port=8080/tcp

重启防火墙
 firewall-cmd --reload
// 添加或删除端口要重启防火墙

```

#### 一些常用端口/使用宝塔

```
20/tcp FTP文件传输协议(默认数据口)
21/tcp FTP文件传输协议(控制)
22/tcp SSH远程登录协议
80/tcp http,用于网页浏览
888/tcp phpmyadmin
8888/tcp 宝塔后台登录
8080/tcp WWW代理开放此端口
39000-40000/tcp
```


