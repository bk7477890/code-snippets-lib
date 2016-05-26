# Linux Shell

## SCP

### 文件下载

```bash
scp -P 10022 houpu@10.11.3.193:~/tata ~/

scp -P 10022 houpu@10.11.3.179:~/work/webm_config/online_config.properties ~/

scp -P 10022 houpu@10.19.18.159:/home/mapp/searchservice/target/searchservice.war ~/
```

### 文件上传

```bash
scp -P10022 SearchDemo.tar.gz houpu@10.11.3.193:~/

scp -P 10022 online_config.properties houpu@10.11.3.179:~/work/webm_config/

scp -P10022 searchservice.war houpu@10.11.3.179:/home/houpu/local/apache-tomcat-7.0.67/webapps/

```

## 链接

### 硬连接

ln /home/houpu/work/ssd/pre_config.properties config.properties

ln online_config.properties /tmp/eless/conf/config.properties

### 软链接

ln -s ~/Work/Mogujie_gitlab/searchservice/dev_config.properties /tmp/eless/conf/config.properties


## Java

### Jar

java -jar target/gs-serving-web-content-0.1.0.jar –server.port=8181

如果你不确定是否是被第三方包重置了配置，可以通过在java命令中添加-Dlog4j.debug虚拟机参数来显示log4j加载配置文件的位置。

java -jar costa-app-1.0.0-SNAPSHOT.jar /Users/jiangnan/Work/Mogujie_gitlab/webapp/ 8585

### rpm jdk安装

1. 下载jdk
wget –no-check-certificate –no-cookies –header “Cookie: oraclelicense=accept-securebackup-cookie; gpw_e24=http%3A%2F%2Fwww.oracle.com%2Ftechnetwork%2Fjava%2Fjavase%2Fdownloads%2Fjdk7-downloads-1880260.html” “http://download.oracle.com/otn-pub/java/jdk/7u71-b14/jdk-7u71-linux-x64.rpm”
2. 安装
`yum install jdk-7u71-linux-x64.rpm`
3. 修改环境变量
vim /etc/profile

在profile文件下面追加写入下面信息：

```bash
export JAVA_HOME=/usr/java/jdk1.7.0_71
export CLASSPATH=.:JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar
export PATH=JAVA_HOME/bin
```

## other

### chown -R

chown -R mapp:devops /home/mapp/searchservice/

### 正则

``“_[0-9]+x” 匹配前面的子表达式一次或多次
“_[0-9]*x” 匹配前面的子表达式零次或多次``


## Git

### 提交

```bash
cd existing_folder
git init
git remote add origin git@gitlab.mogujie.org:houpu/ssd.git
git add .
git commit
git push -u origin master
```

Git操作之克隆某一个特定的远程分支
git clone -b <branch name> [remote repository address]

git clone -b cart-78go http://gitlab.mogujie.org/trade/trade-web-cart.git

### 版本回退

git reset –hard HEAD^
git reset –hard 3628164
git reset –hard fb89d59738f46f50f3

### Git 初始化

#### Git global setup

git config --global user.name "houpu"
git config --global user.email "houpu@mogujie.com"

**Create a new repository**

git clone git@gitlab.mogujie.org:houpu/search-service-demo.git
cd search-service-demo
touch README.md
git add README.md
git commit -m "add README"
git push -u origin master

#### Existing folder or Git repository

cd existing_folder
git init
git remote add origin git@gitlab.mogujie.org:houpu/search-service-demo.git
git add .
git commit
git push -u origin master

### git push

git push origin dev2:master

### git clean

删除 untracked files
git clean -f
连 untracked 的目录也一起删掉
git clean -fd
连 gitignore 的untrack 文件/目录也一起删掉 （慎用，一般这个是用来删掉编译出来的 .o之类的文件用的）
git clean -xfd

在用上述 git clean 前，墙裂建议加上 -n 参数来先看看会删掉哪些文件，防止重要文件被误删
git clean -nxfd
git clean -nf
git clean -nfd

### .gitignore 生效

改动过.gitignore文件之后，在repo的根目录下运行：
git rm -r --cached .
git add .
之后可以进行提交：
git commit -m "fixed untracked files"

### git fetch

git checkout -t origin/mock_deploy   (tracker)

git pull

或者
git fetch origin mock_deploy:mock_deploy  (远程分支:本地分支)

在用上述 git clean 前，墙裂建议加上 -n 参数来先看看会删掉哪些文件，防止重要文件被误删
git clean -nxfd
git clean -nf
git clean -nfd

### git 撤消操作

#### 修复已提交文件中的错误

```bash
#撤消最近的一个提交
git revert HEAD
git push

#撤消“上上次”(next-to-last)的提交
git revert HEAD^
```
