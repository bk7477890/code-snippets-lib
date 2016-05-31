# Software
## PhpStorm
### Mac 下配置  phpStorm
[参考文档](http://www.ifun.cc/blog/2014/02/09/macxia-pei-zhi-shen-qi-phpstromkai-fa-huan-jing/)

## Idea
### 整合tomcat
参考文档 [地址](https://segmentfault.com/q/1010000002419203)

before launch： 添加 Maven goal： package -Dmaven.test.skip=true （添加一个 maven 的命令）

### jar包重新引入
Press CTRL+SHIFT+A to find actions, and input "reimport", you will find the "Reimport All Maven Projects". On a Mac, use CMD+SHIFT+A instead.

### JRebel for IntelliJ

https://plugins.jetbrains.com/plugin/4441?pr=&showAllUpdates=true

[Artifacts配置](http://blog.csdn.net/z69183787/article/details/41416189)

[JRebel配置](http://wiki.jikexueyuan.com/project/intellij-idea-tutorial/jrebel-setup.html)

## iTerm2
Terminal alarm 可以关掉的。#iTerm2 是 Profioes - Terminal - Notifications，勾选 silence bell RT

## Redis
### redis 安装
/Users/jiangnan/Library/LaunchAgents/homebrew.mxcl.redis.plist -> /usr/local/opt/redis/homebrew.mxcl.redis.plist

launchctl load ~/Library/LaunchAgents/homebrew.mxcl.redis.plist

redis 启动 /usr/local/opt/redis/bin/redis-cli

## Vim
NERDTreeQuitOnOpen 打开文件后是否关闭NerdTree窗口

安装 [spf13-vim](https://github.com/spf13/spf13-vim) 编辑 ~/.vimrc ,将 let NERDTreeQuitOnOpen=1 改为 let NERDTreeQuitOnOpen=0， 打开文件后是否关闭NerdTree窗口

## Maven
### [Maven resources 及 Filtering机制](http://xj84.iteye.com/blog/1135594)
costa-templete.xml

```xml
    <build>
        <sourceDirectory>src/main/java</sourceDirectory>
        <resources>
            <resource>
                <directory>src/main/java</directory>
                <excludes>
                    <exclude>**/*.java</exclude>
                </excludes>
            </resource>
        </resources>
    </build>
```

costa-web.xml

```xml
     <build>
        <finalName>${project.webwar.name}</finalName>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-war-plugin</artifactId>
                <version>2.1-alpha-1</version>
                <configuration>
                    <webResources>
                        <resource>
                            <!-- 元配置文件的目录，相对于pom.xml文件的路径 -->
                            <directory>src/main/webapp/WEB-INF</directory>
                            <filtering>true</filtering>
                            <!-- 目标路径 -->
                            <targetPath>WEB-INF</targetPath>
                        </resource>
                    </webResources>
                </configuration>
            </plugin>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <configuration>
                    <source>1.7</source>
                    <target>1.7</target>
                </configuration>
            </plugin>
        </plugins>
    </build>
```

### skip compiler some java file

```xml
    <profiles>
       <profile>
           <id>canary</id>
           <build>
               <plugins>
                   <plugin>
                       <groupId>org.apache.maven.plugins</groupId>
                       <artifactId>maven-compiler-plugin</artifactId>
                       <configuration>
                            <optimize>true</optimize>
                            <excludes>
                                <exclude>com/mogujie/searchservice/biz/service/external/*.java</exclude>
                            </excludes>
                        </configuration>
                    </plugin>
                </plugins>
            </build>
        </profile>
    </profiles>
```

### maven profile

```xml
<build>
   <plugins>
     <plugin>
       <groupId>org.apache.maven.plugins</groupId>
       <artifactId>maven-antrun-plugin</artifactId>
       <version>1.7</version>
     </plugin>
   </plugins>
</build>
<profiles>
    <profile>
       <id>dev</id>
       <activation>
           <activeByDefault>true</activeByDefault>
       </activation>
       <build>
           <plugins>
             <plugin>
              <artifactId>maven-antrun-plugin</artifactId>
              <executions>
                <execution>
                  <phase>compile</phase>
                  <goals><goal>run</goal></goals>
                  <configuration>
                     <tasks>
                     <delete file="${project.build.outputDirectory}/config/application_product.properties"/>
                                        <move file="${project.build.outputDirectory}/config/application_dev.properties"
                                              tofile="${project.build.outputDirectory}/config/application.properties"/>
                                    </tasks>
                                </configuration>
                            </execution>
                        </executions>
                    </plugin>
                </plugins>
            </build>
        </profile>
    </profiles>
```

mvn spring-boot:run -Pproduct -Dmaven.test.skip=true

查看项目依赖项 mvn help:effective-pom

### Maven 可运行 jar包

```xml
<project>
<build>
<plugins>
<plugin>
    <artifactId>maven-assembly-plugin</artifactId>
    <configuration>
        <appendAssemblyId>false</appendAssemblyId>
        <descriptorRefs>
            <descriptorRef>jar-with-dependencies</descriptorRef>
        </descriptorRefs>
        <archive>
            <manifest>
                <mainClass>cn.vsp.TestMain</mainClass>
            </manifest>
        </archive>
    </configuration>
    <executions>
        <execution>
            <id>make-assembly</id>
            <phase>package</phase>
            <goals>
                <goal>assembly</goal>
            </goals>
        </execution>
    </executions>
</plugin>
</plugins>
</build>
</project>
```

编译生成jar包 mvn assembly:assembly

`java -jar *.jar`

### maven SNAPSHOT
快照是一个特殊版本，指出目前开发复印件。不同于常规版本，Maven的检查新的快照版本中，每生成一个远程存储库。

现在，数据服务团队将公布更新后的代码每次的快照存储库说，数据服务:1.0-SNAPSHOT替换一个旧的SNAPSHOT jar。

maven [SNAPHOT](http://juvenshun.iteye.com/blog/376422) maven [快照](http://www.yiibai.com/maven/maven_snapshots.html)

mvn clean install -U

从1.0-SNAPSHOT到1.0到1.1-SNAPSHOT

### [Maven 多 module](http://blog.csdn.net/whuslei/article/details/7989102)
1. 创建项目 -DarchetypeCatalog=internal 将从本地获取archetype-catalog.xml
2. mvn archetype:generate -DgroupId=com.mogujie.searchservice -DartifactId=searchservice -DarchetypeArtifactId=maven-archetype-quickstart -DarchetypeCatalog=internal
3. 删除src , 修改pom.xml文件的packaging属性为pom。
4. 在ssd目录下添加新的module
5. mvn archetype:generate -DgroupId=com.mogujie.searchservice -DartifactId=searchservice-web -DarchetypeArtifactId=maven-archetype-quickstart -DarchetypeCatalog=internal
6. mvn archetype:generate -DgroupId=com.mogujie.ssd -DartifactId=ssd-biz -DarchetypeArtifactId=maven-archetype-quickstart -DarchetypeCatalog=internal
7. 在ssd的pom中添加module信息(貌似会自动添加)
8. 修改子module的文件夹名，将父pom中的配置信息一并修改。

[参考文档](http://blog.csdn.net/hubin0011/article/details/20404053)

### Maven Spring-boot:run
run.jvmArguments

持久代溢出处理 mvn spring-boot:run -Drun.jvmArguments="-Xmx1024m -XX:MaxPermSize=128M"

## Tomcat
### web root 问题
Web app root system property already set to different value: 'webapp.root' = [/usr/local/apache-tomcat-7.0.67/webapps/houpuss/] instead of [/usr/local/apache-tomcat-7.0.67/webapps/changwenss/] - Choose unique values for the 'webAppRootKey' context-param in your web.xml files!

web root 重复 web.xml中添加

```xml
   <context-param>
        <param-name>webAppRootKey</param-name>
        <param-value>webapp.root1</param-value>
    </context-param>
```

### PermGen space
[lib共享](http://my.oschina.net/fuyung/blog/206112?fromerr=dGoVce37)

### Tomcat远程调试
1. 代码部署到tomcat容器中
2. 在IDEA中点击右上角那个"Edit Configurations"按钮，然后在弹出的界面中点击左上角的加号，选择tomcat server->remote

browser配置到 应用目录 （配置Before launch）
1. 根据idea配置页面中

address=61277 说明 port为61277

将JPDA_ADDRESS=61277拷贝到tomcat bin/catalina.sh 第一行， 将startup.sh中最后一行 exec "$PRGDIR"/"$EXECUTABLE" start "$@" 注释掉 添加 exec "$PRGDIR"/"$EXECUTABLE" jpda start "$@"

cd .default/webapps/ROOT/WEB-INF/lib/

./appctl pubstart

### 部署脚本

```bash
#!/bin/bash
EXCONFIG_DIR=/tmp/eless/conf
EXCONFIG_FILENAME=config.properties
USED_CONFIG_LOCATION=/home/houpu/work/searchservice_config/pre_config.properties
USED_WEBXML=/home/houpu/work/searchservice_config/web.xml
TOMCAT_LOCATION=/usr/local/apache-tomcat-7.0.67
PROJECT_NAME=searchservice

EXCONFIG_LOCATION=$EXCONFIG_DIR/$EXCONFIG_FILENAME
BASEDIR=`pwd`
TEMP_PROJECT_NAME=${BASEDIR:6}
FINAL_PROJECT_NAME=${TEMP_PROJECT_NAME%%/*}ss

PROJECT_LOCATION=$BASEDIR/$PROJECT_NAME
WAR_LOCATION=$PROJECT_LOCATION/web/target/$PROJECT_NAME.war
FINAL_WAR_LOCATION=$PROJECT_LOCATION/web/target/$FINAL_PROJECT_NAME.war

if [ ! -f $USED_CONFIG_LOCATION ]; then
    echo "can not find config file in $USED_CONFIG_LOCATION";
    exit 1;
fi

if [ ! -f $USED_WEBXML]; then
    echo "can not find web.xml in $USED_WEBXML";
    exit 1;
fi

cp -f $USED_WEBXML $PROJECT_LOCATION/web/src/main/webapp/WEB-INF/


## create config file
if [ ! -d $EXCONFIG_DIR ]; then
    mkdir -p $EXCONFIG_DIR
fi

if [ -f $EXCONFIG_LOCATION ]; then
    rm -r $EXCONFIG_LOCATION
fi

ln -n $USED_CONFIG_LOCATION  $EXCONFIG_DIR/$EXCONFIG_FILENAME

cd $PROJECT_LOCATION

mvn clean compile package -DskipTests

if [ ! -f $WAR_LOCATION ]; then
    echo "can not find war in $WAR_LOCATION";
    exit 1;
fi

sh $TOMCAT_LOCATION/bin/shutdown.sh

# force kill service
PID=`ps aux |grep "tomcat" |grep -v "grep" |awk 'BEGIN{FS=" ";} {print $2;}'`
if [ ! -z $PID  ]; then
    echo "try force kill tomcat..."
    kill $PID && sleep 5
    PID=`ps aux |grep "tomcat" |grep -v "grep" |awk 'BEGIN{FS=" ";} {print $2;}'`
    if [ ! -z $PID  ]; then
        kill -9 $PID
    fi
fi
rm -rf $TOMCAT_LOCATION/webapps/$FINAL_PROJECT_NAME

rm  $TOMCAT_LOCATION/webapps/$FINAL_PROJECT_NAME.war

mv $WAR_LOCATION $FINAL_WAR_LOCATION

mv $FINAL_WAR_LOCATION $TOMCAT_LOCATION/webapps/

sh $TOMCAT_LOCATION/bin/startup.sh
```

## 压力测试工具
[文档](https://github.com/wg/wrk)

OS X   INSTALL： make WITH_OPENSSL=/usr/local/opt/openssl

```bash
# This runs a benchmark for 30 seconds, using 12 threads, and keeping400 HTTP connections open.

wrk -t12 -c400 -d30s http://127.0.0.1:8080/index.html
```

[参考文档](http://docs.spring.io/spring-boot/docs/1.4.0.BUILD-SNAPSHOT/maven-plugin/examples/run-debug.html)
