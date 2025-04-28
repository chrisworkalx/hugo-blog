+++
date = '2025-04-28T18:54:52+08:00'
draft = false
title = 'Java Pom.xml'
comments = true
author = "chrisworkalx"
tags = ["Js"]
categories =  ["初级"]
description = "关于pom.xml常见标签字段"
slug = "pom-xml"
+++

## pom.xml 常用标签大全

### 标签 作用 示例

```xml
<project> 必须的根标签，所有内容都包裹在里面。 <project xmlns=...>...</project>
<modelVersion> 定义 POM 模型的版本（固定写法）。通常是 4.0.0。 <modelVersion>4.0.0</modelVersion>
<groupId> 项目组织 ID，通常是公司或组织的域名倒写。 <groupId>com.example</groupId>
<artifactId> 项目的名字，通常是模块或应用名称。 <artifactId>admin-backend</artifactId>
<version> 项目的版本号。 <version>1.0.0</version>
<packaging> 打包方式，默认是 jar，也可以是 war（Web 项目）。 <packaging>jar</packaging>
<name> 项目的名称（可选，主要用于描述）。 <name>Admin Backend System</name>
<description> 项目的简短描述（可选）。 <description>A Spring Boot Admin system</description>
```

### 依赖管理相关标签

### 标签 作用 示例

```xml
<dependencies> 依赖列表，包含所有 <dependency>。 <dependencies>...</dependencies>
<dependency> 单个依赖项。 <dependency>...</dependency>
<groupId> 依赖库的组织 ID。 <groupId>org.springframework.boot</groupId>
<artifactId> 依赖库的名称。 <artifactId>spring-boot-starter-web</artifactId>
<version> 依赖库的版本号。 <version>3.1.2</version>
<scope> 依赖范围（如 compile、test、provided）。 <scope>test</scope>
```

### 常见 scope：

```xml
compile（默认）：编译、运行、打包都需要。

test：仅在测试阶段需要。

provided：编译需要，运行环境已提供，比如 Servlet API。
```

### 构建配置相关标签

### 标签 作用 示例

```xml
<build> 构建配置（比如插件、输出目录）。 <build>...</build>
<plugins> 插件列表，包含多个 <plugin>。 <plugins>...</plugins>
<plugin> 单个插件。比如 Maven 编译器插件、打包插件等。 <plugin>...</plugin>
```

### 例子：指定 Java 版本

```xml
<build>
  <plugins>
    <plugin>
      <groupId>org.apache.maven.plugins</groupId>
      <artifactId>maven-compiler-plugin</artifactId>
      <version>3.10.1</version>
      <configuration>
        <source>17</source>
        <target>17</target>
      </configuration>
    </plugin>
  </plugins>
</build>

```

### 其他常见的标签

| 标签             | 作用                                                     | 示例                                                               |
| ---------------- | -------------------------------------------------------- | ------------------------------------------------------------------ |
| \<properties\>   | 定义一些可以重复使用的属性，比如 Java 版本号、编码格式。 | \<properties\>\<java.version\>17\<\/java.version\>\<\/properties\> |
| \<repositories\> | 指定 Maven 仓库地址（如果用私服）。                      | \<repositories\>...\<\/repositories\>                              |
| \<profiles\>     | 多环境配置，比如开发版、生产版不同配置。                 | \<profiles\>...\<\/profiles\>                                      |

### 常见配置举例

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0
         http://maven.apache.org/xsd/maven-4.0.0.xsd">

  <modelVersion>4.0.0</modelVersion>

  <!-- 项目信息 -->
  <groupId>com.example</groupId>
  <artifactId>springboot-demo</artifactId>
  <version>1.0.0</version>
  <packaging>jar</packaging>

  <name>springboot-demo</name>
  <description>Spring Boot 后端项目模板</description>

  <!-- 父工程，管理 Spring Boot 依赖版本 -->
  <parent>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-parent</artifactId>
    <version>3.2.2</version> <!-- 根据你的 Spring Boot 版本选择 -->
    <relativePath/>
  </parent>

  <!-- 统一配置 -->
  <properties>
    <java.version>17</java.version> <!-- Java 17 -->
    <maven.compiler.source>${java.version}</maven.compiler.source>
    <maven.compiler.target>${java.version}</maven.compiler.target>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
  </properties>

  <!-- 项目依赖 -->
  <dependencies>
    <!-- Spring Boot 核心 -->
    <dependency>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter-web</artifactId>
    </dependency>

    <!-- Spring Boot Security -->
    <dependency>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter-security</artifactId>
    </dependency>

    <!-- Spring Data JPA -->
    <dependency>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter-data-jpa</artifactId>
    </dependency>

    <!-- MySQL 驱动 -->
    <dependency>
      <groupId>com.mysql</groupId>
      <artifactId>mysql-connector-j</artifactId>
      <scope>runtime</scope>
    </dependency>

    <!-- JWT -->
    <dependency>
      <groupId>io.jsonwebtoken</groupId>
      <artifactId>jjwt</artifactId>
      <version>0.9.1</version>
    </dependency>

    <!-- Lombok -->
    <dependency>
      <groupId>org.projectlombok</groupId>
      <artifactId>lombok</artifactId>
      <optional>true</optional>
    </dependency>

    <!-- 测试 -->
    <dependency>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter-test</artifactId>
      <scope>test</scope>
    </dependency>
  </dependencies>

  <!-- 构建配置 -->
  <build>
    <plugins>
      <!-- 编译 Java 版本 -->
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-compiler-plugin</artifactId>
        <version>3.10.1</version>
        <configuration>
          <source>${java.version}</source>
          <target>${java.version}</target>
        </configuration>
      </plugin>

      <!-- Spring Boot Maven 插件：用于打包 jar -->
      <plugin>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-maven-plugin</artifactId>
      </plugin>
    </plugins>
  </build>

</project>

```
