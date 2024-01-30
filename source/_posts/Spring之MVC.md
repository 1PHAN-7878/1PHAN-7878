---
title: Spring之MVC
date: 2024-01-30 12:00:25
tags: java
---

# SpringMVC

基于Spring的javaweb

# 基本使用

## 添加依赖

```xml
<dependencies>
    <!-- Spring MVC -->
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-webmvc</artifactId>
        <version>5.3.10</version> <!-- 使用适用于 Java 17 的 Spring 版本 -->
    </dependency>

    <!-- Spring Context -->
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-context</artifactId>
        <version>5.3.10</version>
    </dependency>

    <!-- Spring Core -->
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-core</artifactId>
        <version>5.3.10</version>
    </dependency>

    <!-- Spring Beans -->
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-beans</artifactId>
        <version>5.3.10</version>
    </dependency>

    <!-- Spring Web -->
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-web</artifactId>
        <version>5.3.10</version>
    </dependency>

    <!-- Spring Expression Language (SpEL) -->
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-expression</artifactId>
        <version>5.3.10</version>
    </dependency>
</dependencies>

```

## 创建SpringMVC控制器

```java
package com.iphan.controller;

import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.ResponseBody;

@Controller
public class UserController {
    @RequestMapping("/test")
    @ResponseBody
    public String save(){
        System.out.println("user is saving");
        return "{'info': 'SringMVC'}";
    }

}
```

## 配置SpringConfig

```java
package com.iphan.config;

import org.springframework.context.annotation.ComponentScan;
import org.springframework.context.annotation.Configuration;

@Configuration
@ComponentScan({"com.iphan.controller"})
public class SpringMvcConfig {

}
```
