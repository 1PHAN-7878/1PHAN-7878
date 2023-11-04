---
title: maven
date: 2023-11-04 13:49:53
tags: java
---

# 简介

Apache Maven（通常简称为 Maven）是一个开源的项目管理和构建工具，用于构建、管理和部署Java应用程序。它提供了一种结构化的方式来管理项目的构建过程、依赖管理、文档生成和发布过程。Maven 的主要目标是提供一种一致的构建方法，减少开发人员的配置工作，以及提供自动化构建的能力。

Maven 提供了以下主要功能和特点：

1. **项目结构和约定**：Maven 鼓励开发者遵循一组约定，以简化项目的组织和结构。这些约定包括源代码目录、资源目录、测试目录等。
2. **依赖管理**：Maven 支持管理项目的依赖关系。你可以定义项目依赖，Maven 会自动下载和管理这些依赖的库文件。这减轻了手动管理JAR文件的负担。
3. **生命周期和构建阶段**：Maven 定义了一组生命周期和构建阶段，包括编译、测试、打包、部署等。开发者可以配置和执行这些构建阶段，以满足项目的需求。
4. **插件体系**：Maven 使用插件来扩展其功能。它有丰富的插件生态系统，允许开发者使用现有的插件或编写自定义插件以满足特定需求。
5. **POM 文件**：Maven 使用项目对象模型（Project Object Model，POM）文件来描述项目的配置信息、依赖关系和构建过程。POM 文件以 XML 格式编写。
6. **自动化构建**：Maven 提供了一种自动化构建过程，可以生成项目的可执行文件、文档、测试报告等。
7. **集成测试和部署**：Maven 支持集成测试和部署到不同环境的过程，有助于构建和交付可靠的应用程序。

Maven 的强大功能和生态系统使其成为 Java 开发社区中最受欢迎的项目管理和构建工具之一。它有助于简化项目的构建和管理，并提高开发效率。

# eclipse中使用maven

新建maven项目

![image-20231104135249214](../images/image-20231104135249214.png)

1. **maven-archetype-quickstart**：
   - 这是一个基本的 Maven 项目模板，用于创建简单的 Java 项目。
   - 包括了一个示例的 Java 类和一个简单的 `pom.xml` 配置文件。
   - 适用于快速创建基本的 Java 项目。
2. **maven-archetype-webapp**：
   - 用于创建基本的 Web 应用程序项目，包括了一个简单的 Java Servlet 和 Web 目录结构。
   - 适用于开发简单的 Web 应用程序。
3. **maven-archetype-j2ee-simple**：
   - 创建了一个简单的 Java EE 项目，包括了一个 EJB 模块和一个 WAR 模块。
   - 适用于创建较复杂的 Java EE 项目。
4. **maven-archetype-quickstart-jdk8**：
   - 类似于 "maven-archetype-quickstart"，但是使用 Java 8 作为目标 JDK 版本。
   - 适用于在 Java 8 环境下开发的项目。
5. **maven-archetype-archetype**：
   - 用于创建自定义 Maven "archetype" 的模板。
   - 适用于开发自定义项目模板的高级用户。

![image-20231104135514615](../images/image-20231104135514615.png)

1. **Group ID (groupId)**：Group ID 是你的项目的组织或包的唯一标识符。通常，它使用逆域名（reverse domain name）的方式来定义，例如 `com.example`。这个标识符用于区分不同的项目和组织。你可以根据你的组织或项目的实际情况来定义 Group ID。
2. **Artifact ID (artifactId)**：Artifact ID 是你的项目的名称标识符。它代表项目本身的名称。例如，如果你的项目是一个名为 "myapp" 的应用程序，那么 Artifact ID 可以设置为 `myapp`。
3. **Package (package)**：Package 是你的 Java 类的默认包名。通常，它是根据 Group ID 和 Artifact ID 自动生成的，形式为 `groupId.artifactId`。例如，如果 Group ID 是 `com.example`，Artifact ID 是 `myapp`，那么默认的包名将是 `com.example.myapp`。

下面是一个示例：

- Group ID: `com.example`
- Artifact ID: `myapp`
- Package: `com.example.myapp`

# 添加后产生错误

![image-20231104140409713](../images/image-20231104140409713.png)

这个错误是由于 Maven 无法从默认的中央仓库（https://repo.maven.apache.org/maven2）下载所需的依赖项，特别是与 Maven 插件和工具有关的依赖项。通常，这种问题可能是网络连接问题或中央仓库服务器问题导致的。

解决方法：

1. 打开 Eclipse。

2. 转到 "Window" 菜单，选择 "Preferences"。

3. 在 Preferences 窗口中，展开 "Maven" 部分，然后选择 "User Settings"。

4. 在 "User Settings" 下，你会看到 "User Settings" 文件的路径。通常情况下，这是 `$USER_HOME/.m2/settings.xml`，其中 `$USER_HOME` 表示你的用户主目录。

5. 打开这个文件以编辑 Maven 的设置。

6. 在 `settings.xml` 文件中，你可以添加镜像源配置，如以下示例所示：

   ```xml
   <mirrors>
     <mirror>
       <id>aliyun-maven</id>
       <mirrorOf>central</mirrorOf>
       <url>https://maven.aliyun.com/repository/central</url>
     </mirror>
   </mirrors>
   ```

   你可以根据你的需求添加镜像源，确保镜像源的 URL 和 `<mirrorOf>` 标签中的值正确。

7. 保存 `settings.xml` 文件。

然后，尝试重新构建你的项目，Maven 应该会使用你配置的镜像源来下载依赖项。如果 `settings.xml` 文件不存在，你可以创建一个并添加所需的配置。确保 Eclipse 中的 Maven 插件能够正确找到这个文件。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<metadata>
  <groupId>org.jetbrains.externalAnnotations.junit</groupId>
  <artifactId>junit</artifactId>
  <versioning>
    <latest>4.12-an1</latest>
    <release>4.12-an1</release>
    <versions>
      <version>4.12-an1</version>
    </versions>
    <lastUpdated>20210416102806</lastUpdated>
  </versioning>
  
  <mirrors>
  <mirror>
    <id>aliyun-maven</id>
    <mirrorOf>central</mirrorOf>
    <url>https://maven.aliyun.com/repository/central</url>
  </mirror>
  </mirrors>

</metadata>

```

![image-20231104141116493](../images/image-20231104141116493.png)

最后update本地文件

![image-20231104141357297](../images/image-20231104141357297.png)

测试输出helloworld

![image-20231104141823736](../images/image-20231104141823736.png)

# 添加依赖

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>

  <groupId>com.example</groupId>
  <artifactId>myapp</artifactId>
  <version>0.0.1-SNAPSHOT</version>
  <packaging>jar</packaging>
	
  <name>myapp</name>
  <url>http://maven.apache.org</url>

  <properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
  </properties>

  <dependencies>
    <dependency>
      <groupId>junit</groupId>
      <artifactId>junit</artifactId>
      <version>3.8.1</version>
      <scope>test</scope>
    </dependency>
	
	<!-- MySQL Connector/J 8.0.27 的依赖 -->
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>8.0.27</version>
        </dependency>

  </dependencies>
</project>

```

![image-20231104142540115](../images/image-20231104142540115.png)

update可以看到增加了jar包

进行测试成功

![image-20231104144200991](../images/image-20231104144200991.png)
