# Maven 安装


## 下载 Maven

最新版下载地址 http://maven.apache.org/download.cgi

历史版 https://archive.apache.org/dist/maven/maven-3/

apache-maven-3.3.9-bin.tar.gz

## 配置环境变量

检查JAVA_HOME环境变量

```
echo %JAVA_HOME%
```

配置环境变量

M2_HOME maven解压目录

path    追加 `;%M2_HOME%\bin`


检查是否配置成功
```
mvn -v
```
...








