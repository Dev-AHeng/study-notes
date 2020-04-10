## git的使用 提交

### 1.安装git(第一次使用时)
 `pkg install git`

### 2.打开要上下传的文件夹
 `cd 路径` ，例如：
 `cd /storage/emulated/0/AppProjects/` 

### 3.初始化git
 `git init` 
###### 初始化完成会在该目录下创建.git文件夹

### 4.登录git
```
git config --global user.name 你git用户名
git config --global user.email 你git电子邮箱
```
### 5.指定git创库地址
 `git remote -v origin 远程git地址` ，例如：
 `git remote -v origin git://github.com/xiaoheng666/openfireandsmack.git` 

### 6.添加文件  
###### 1.添加这个文件夹的文件  
 `git add 文件夹名` 
###### 2.添加单个文件  
 `gitv add 文件名` 




-------

## 克隆
 `git init` 

 `git clone https://github.com/xiaoheng666/openfireandsmack.git` 