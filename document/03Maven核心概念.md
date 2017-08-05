# Maven 核心概念

约定优于配置

Maven使用约定而不是配置，意味着开发者不需要自己创建构建过程

* POM
* 约定的目录结构
* 坐标
* 依赖管理
* 仓库管理
* 生命周期
* 插件和目标
* 继承
* 聚合

## POM

Project Object Model：项目对象模型。将 Java 工程的相关信息封装为对象作为便于操作和管理的模型。

Maven 工程的核心配置。可以说学习 Maven 就是学习 pom.xml 文件中的配置。

## 约定的目录结构

约定的目录结构对于 Maven 实现自动化构建而言是必不可少的一环，就拿自动编译来说，Maven 必须
能找到 Java 源文件，下一步才能编译，而编译之后也必须有一个准确的位置保持编译得到的字节码文件。

我们在开发中如果需要让第三方工具或框架知道我们自己创建的资源在哪，那么基本上就是两种方式：
* 通过配置的形式明确告诉它
* 基于第三方工具或框架的约定

Maven 对工程目录结构的要求就属于后面的一种。

![](resources/03_01.png)

## 坐标

使用如下三个向量在 Maven 的仓库中唯一的确定一个 Maven 工程。
* groupid：所属组
* artifactId：模块ID
* version：模块版本

```
<groupId>com.labi.interfaceSys</groupId>
<artifactId>interfaceSys</artifactId>
<version>1.3.0</version>
```

## 依赖管理

Maven 中最关键的部分，我们使用 Maven 最主要的就是使用它的依赖管理功能

### 依赖的目的是什么

当 A jar 包用到了 B jar 包中的某些类时，A 就对 B 产生了依赖，使用 dependency 标签指定被依赖 jar 包的坐标就可以了

```
<dependency>
  <groupId>com.labi.interfaceSys</groupId>
  <artifactId>interfaceSys</artifactId>
  <version>1.3.0</version>
</dependency>
```

### scope 依赖的范围

* compile 默认
* test 测试依赖
* provided 开发依赖
* runtime 运行时
* system 需要显式提供包含依赖的jar，Maven不会在Repository中查找它

```
<dependency>
  <groupId>com.labi.interfaceSys</groupId>
  <artifactId>interfaceSys</artifactId>
  <version>1.3.0</version>
  <scope>compile</scope>
</dependency>
```

有效性总结

|       | compile | test | provided |
|-------|---------|------|----------|
|主程序  |    是   |   否  |    是    |
|测试程序|    是   |   是  |    是    |
|参与部署|    是   |   否  |    否    |


### 依赖的传递性

A 依赖 B，B 依赖 C，A 能否使用 C 呢？那要看 B 依赖 C 的范围是不是 compile，
如果是则可用，否则不可用。

### 依赖的排除

如果我们在当前工程中引入了一个依赖是 A，而 A 又依赖了 B，那么 Maven 会自动将 A 依赖的 B 引入当
前工程，但是个别情况下 B 有可能是一个不稳定版，或对当前工程有不良影响。这时我们可以在引入 A 的时
候将 B 排除。

```
<dependency>
  <groupId>com.9fbank.mcl</groupId>
  <artifactId>busserver</artifactId>
  <version>1.0.8</version>
  <exclusions>
    <exclusion>
      <groupId>*</groupId>
      <artifactId>*</artifactId>
    </exclusion>
  </exclusions>
</dependency>
```

### 统一管理所依赖 jar 包的版本

对同一个框架的一组 jar 包最好使用相同的版本。为了方便升级框架，可以将 jar 包的版本信息统一提
取出来

* 统一版本号
```
<properties>
  <interfaceSys.version>1.3.0</interfaceSys.version>
</properties>

<dependency>
  <groupId>com.labi.interfaceSys</groupId>
  <artifactId>interfaceSys</artifactId>
  <version>${interfaceSys.version}</version>
  <scope>compile</scope>
</dependency>
```

* 指定项目编码
```
<properties>
  <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
</properties>
```



