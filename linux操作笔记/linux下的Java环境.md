**linux查看jdk安装情况**

```
1. 使用命令"echo $JAVA_HOME"来获取环境变量"$JAVA_HOME"配置的JDK路径。 这个环境变量通常在安装JDK时被设置，它指向JDK的安装目录。
2. 使用命令"rpm -qa | grep java"来查看已安装的JDK包的路径。 这个命令会列出所有包含"java"关键字的已安装软件包，其中包括JDK。 通过查看这些包的路径，可以确定JDK的安装路径。
3. 在配置过jdk的情况下，执行java -verbose指令，在打印出的文本最后两行可以看到jdk的安装路径
```
配置环境变量

```
vim /etc/profile
```

在文件的最下面添加

```
export JAVA_HOME=/source/java/jdk1.8.0_161 #你自己的安装路径
export JRE_HOME=${JAVA_HOME}/jre
export CLASSPATH=.:${JAVA_HOME}/lib:${JRE_HOME}/lib
export PATH=${JAVA_HOME}/bin:$PATH
```
然后wq保存退出

执行下面这个命令才能生效

```
. /etc/profile

java -version
javac
```
