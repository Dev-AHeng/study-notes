## 手机Termux使用git

### 1.安装git
 `pkg install git`  
###### 第一次使用时需要安装
### 2.打开要上下传的文件夹
 `cd 路径` ，例如：
 `cd /storage/emulated/0/AppProjects/` 

### 3.初始化git
 `git init` 
###### 初始化完成会在该目录下创建.git文件夹

### 4.添加文件
 `git add .` 
###### 将当前目录下修改的所有代码从工作区添加到暂存区
###### .的意思是添加目录下所有文件

###### 添加单个文件：
 `git add '文件'` 

### 5.查看状态
 `git status` 

### 6.文件注释
 `git commit -m '注释内容'` 

### 7.提交(坑：提交之前要先克隆)
 `git push 你github仓库地址` ，例如：

 `git push https://github.com/xiaoheng666/openfireandsmack.git` 

跟着它会提示 `Username for 'https://github.com':` 要求你输入github账号，跟着又会提示 `Password for 'https://xiaoheng666@github.com':` 要求你输入密码，这里值得注意的是你输入密码是它不会显示，输入完密码直接按回车就会提交了，等待完成即可

-------

## 克隆到本地
 `git init` 

 `git clone https://github.com/xiaoheng666/openfireandsmack.git` 