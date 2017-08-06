# Maven 常用命令

* mvn archetype:generate 创建项目
* mvn compile 编译
* mvn clean 清理所有编译
* mvn site 生成站点
* mvn package 打包
* mvn install 安装到本地仓库
* mvn deploy 发布到私服
* mvn jar:jar 生成jar包


## mvn archetype:generate

mvn archetype:generate   固定格式
* -DgroupId              所属组ID
* -DartifactId           项目ID
* -DarchetypeArtifactId  利用 archetypeArtifactId 模型（骨架）
* -DinteractiveMode      是否使用交换模式
* -DarchetypeCatalog     local（使用本地）

指定 ArchetypeId
* maven-archetype-quickstart，创建一个Java Project；
* maven-archetype-webapp，创建一个Web Project


快速创建

```
$ mvn archetype:generate -DgroupId=com.labi.common -DartifactId=labi -DarchetypeArtifactId=maven-archetype-webapp -DinteractiveMode=false
```

创建速度慢
在下载 https://repo.maven.apache.org/maven2/archetype-catalog.xml 文件

-DarchetypeCatalog=local 使用本地
