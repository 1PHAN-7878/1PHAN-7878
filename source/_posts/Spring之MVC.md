---
title: Spring之MVC
date: 2024-01-30 12:00:25
tags: java
---

# SpringMVC

基于Spring的javaweb

# 基本使用

## 添加依赖，不要加这么多

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

```xml
	<dependency>
      <groupId>javax.servlet</groupId>
      <artifactId>javax.servlet-api</artifactId>
      <version>4.0.1</version>
      <scope>provided</scope>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-webmvc</artifactId>
      <version>5.2.10.RELEASE</version> <!-- 使用适用于 Java 11 的 Spring 版本 -->
    </dependency>
```



## 创建SpringMVC控制器

```java
package com.iphan.controller;

import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.ResponseBody;
//控制器
@Controller
public class UserController {
    //匹配路径
    @RequestMapping("/test")
    //表示返回值写入响应体
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

## 配置SpringMvcConfig

```java
package com.iphan.config;


import org.springframework.stereotype.Component;
import org.springframework.web.context.WebApplicationContext;
import org.springframework.web.context.support.AnnotationConfigWebApplicationContext;
import org.springframework.web.servlet.support.AbstractAnnotationConfigDispatcherServletInitializer;
import org.springframework.web.servlet.support.AbstractDispatcherServletInitializer;

//通过注解类完成注册
public class ServletContainersInitConfig extends AbstractAnnotationConfigDispatcherServletInitializer {

    @Override
    protected Class<?>[] getRootConfigClasses() {
        return new Class[0];
    }
	
    @Override
    protected Class<?>[] getServletConfigClasses() {
        return new Class[]{SpringMvcConfig.class};
    }

    @Override
    protected String[] getServletMappings() {
        return new String[]{"/"};
    }
}

//
//public class ServletContainersInitConfig extends AbstractDispatcherServletInitializer {
//    @Override
//    protected WebApplicationContext createServletApplicationContext() {
//        AnnotationConfigWebApplicationContext ctx = new AnnotationConfigWebApplicationContext();
//
////        AnnotationConfigWebApplicationContext ctx;
//        ctx.register(SpringMvcConfig.class);
//        return ctx;
//    }
//
//    @Override
//    protected String[] getServletMappings() {
//        return new String[]{"/"};
//    }
//
//    @Override
//    protected WebApplicationContext createRootApplicationContext() {
//        return null;
//    }
//}
```

## 实现效果

访问相应路径，SpringMvc处理请求并返回。

![image-20240131141757725](../images/image-20240131141757725.png)

# Bean控制

![image-20240131141812443](../images/image-20240131141812443.png)

![image-20240131142107077](../images/image-20240131142107077.png)

在SpringConfig中完成对于业务层数据层的Bean控制

```java
package com.iphan.config;

import org.springframework.context.annotation.ComponentScan;
import org.springframework.context.annotation.Configuration;

@Configuration
@ComponentScan({"com.iphan.service","com.iphan.dao"})
public class SpringConfig {
}
```

在SpringMvcConfig中完成表现层控制

```java
package com.iphan.config;

import org.springframework.context.annotation.ComponentScan;
import org.springframework.context.annotation.Configuration;
import org.springframework.web.servlet.config.annotation.EnableWebMvc;

@Configuration
@ComponentScan("com.iphan.controller")
public class SpringMvcConfig {

}
```

进行注册

```java
package com.iphan.config;


import org.springframework.stereotype.Component;
import org.springframework.web.context.WebApplicationContext;
import org.springframework.web.context.support.AnnotationConfigWebApplicationContext;
import org.springframework.web.servlet.support.AbstractAnnotationConfigDispatcherServletInitializer;
import org.springframework.web.servlet.support.AbstractDispatcherServletInitializer;


public class ServletContainersInitConfig extends AbstractAnnotationConfigDispatcherServletInitializer {

    @Override
    protected Class<?>[] getRootConfigClasses() {
        return new Class[]{SpringConfig.class};
    }

    @Override
    protected Class<?>[] getServletConfigClasses() {
        return new Class[]{SpringMvcConfig.class};
    }

    @Override
    protected String[] getServletMappings() {
        return new String[]{"/"};
    }
}

//
//public class ServletContainersInitConfig extends AbstractDispatcherServletInitializer {
//    @Override
//    protected WebApplicationContext createServletApplicationContext() {
//        AnnotationConfigWebApplicationContext ctx = new AnnotationConfigWebApplicationContext();
//
////        AnnotationConfigWebApplicationContext ctx;
//        ctx.register(SpringMvcConfig.class);
//        return ctx;
//    }
//
//    @Override
//    protected String[] getServletMappings() {
//        return new String[]{"/"};
//    }
//
//    @Override
//    protected WebApplicationContext createRootApplicationContext() {
//        return null;
//    }
//}
```

# 请求映射路径

如果目前有很多的controller，每一个都有重复的功能，访问路径相同，例如save，delete。可以再类前注解加上相应类名区分，访问时也要加上类的路径以及方法的路径。

```java
package com.iphan.controller;

import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.ResponseBody;

@Controller
//加上类的访问路径
@RequestMapping("/user")
public class UserController {
    @RequestMapping("/save")
    @ResponseBody
    public String save(String name){
        System.out.println("this is save");
        System.out.println(name);
        return "{'model':'spring'}";
    }
}
```

# 接受参数

`@RequestParam`

`@RequestBody`

`@PathVariable`

![image-20240131202454898](../images/image-20240131202454898.png)

直接写方法中的参数即可。可以通过post或者get请求获得。

- GET 请求：`/user/save?name=John`
- POST 请求（使用表单数据或 JSON 数据）。

中文编码问题，在连接配置中，增加过滤器。

```java
public class ServletContainersInitConfig extends AbstractAnnotationConfigDispatcherServletInitializer {

    @Override
    protected Class<?>[] getRootConfigClasses() {
        return new Class[]{SpringConfig.class};
    }

    @Override
    protected Class<?>[] getServletConfigClasses() {
        return new Class[]{SpringMvcConfig.class};
    }

    @Override
    protected String[] getServletMappings() {
        return new String[]{"/"};
    }

    @Override
    protected Filter[] getServletFilters() {
        CharacterEncodingFilter filter = new CharacterEncodingFilter();
        filter.setEncoding("UTF-8");
        return new Filter[]{filter};
    }
}
```

1.普通参数，请求名与形参相同，直接接受。

2.普通参数，请求名与形参不相同，使用参数绑定。

```java
@ResponseBody
@RequestMapping(value = "/testdiffname")
public String testdiffname(@RequestParam("name") String diff){
    System.out.println(diff);
    return "it 's ok";
}
```

3.pojo类，请求参数与形参相同。

```java
@ResponseBody
@RequestMapping(value = "/testpojo")
public String testpojo(Man man){
    System.out.println(man);
    return "ok";
}
```

```java
package com.iphan.pojo;

public class Man {
    public String name;
    public int id;

    public String getName() {
        return name;
    }

    @Override
    public String toString() {
        return "Man{" +
                "name='" + name + '\'' +
                ", id=" + id +
                '}';
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getId() {
        return id;
    }

    public void setId(int id) {
        this.id = id;
    }

    public Man(String name, int id) {
        this.name = name;
        this.id = id;
    }
}
```

4.数组，直接形参与变量名对应即可。

5.List，接受时前加`@RequestParam`

6.JSON类型

+ 添加依赖

  ```xml
  <dependency>
    <groupId>com.fasterxml.jackson.core</groupId>
    <artifactId>jackson-databind</artifactId>
    <version>2.13.0</version>
  </dependency>
  ```

+ ==开始`@EnableWebMvc`==
+ 设置JSON数据
+ ![image-20240131162216162](../images/image-20240131162216162.png)

+ JSON接受的pojo类中要有无参构造

  ```java
  public Man(){};
  ```

+ ```java
  @ResponseBody
  @RequestMapping(value = "/testjson")
  public String testjson(@RequestBody Man man){
      return "this JSON ok";
  }
  ```

7.日期

![image-20240131170118252](../images/image-20240131170118252.png)

# REST风格

表现形式状态转换。

+ 隐藏资源的访问，无法通过URL知道资源是什么，安全性。
+ 书写简化。

通过不同的method进行确定。

==模块名一般使用/****s==复数形式加以描述

![image-20240131195531382](../images/image-20240131195531382.png)

```java
package com.iphan.controller;

import com.iphan.pojo.Book;
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.*;

import java.util.ArrayList;
import java.util.List;
//表示了@Controller以及@ResponseBody
@RestController
@RequestMapping("/books")
public class BookController {

    //表示是post请求，用于添加
    @PostMapping()
    public String addBook(@RequestBody Book book){
        System.out.println("book is added!");
        System.out.println(book);
        return "book add is ok";
    }

    //GET表示查询请求
    @GetMapping()
    public List<Book> showAll(){
        Book book1 = new Book("book1", 1);
        Book book2 = new Book("Book2:)", 2);
        List<Book> list = new ArrayList<>();
        list.add(book1);
        list.add(book2);
        System.out.println("books are found");
        return list;
    }

    //Delete表示删除请求
    @DeleteMapping("/{id}")
    public String deleteBook(@PathVariable int id){
        System.out.println("delete " + id +"is ok");
        return "delete" + id;
    }

    //Put表示修改请求
    @PutMapping()
    public String setBook(@RequestBody Book book){
        System.out.println("set book " + book);
        return "book set have done";
    }
}
```

# 资源访问筛选

一些静态资源不希望经过DispatcherServlet，而是直接由容器处理，可以通过配置 `ResourceHandler` 来实现。这样，当请求匹配到静态资源路径时，容器将直接提供这些资源，而不需要通过 DispatcherServlet。

```java
package com.iphan.config;

import org.springframework.stereotype.Component;
import org.springframework.web.servlet.config.annotation.ResourceHandlerRegistry;
import org.springframework.web.servlet.config.annotation.WebMvcConfigurationSupport;
//作为配置类
@Component
public class SpringMvcSupport extends WebMvcConfigurationSupport {
    @Override
    protected void addResourceHandlers(ResourceHandlerRegistry registry) {
        registry.addResourceHandler("/hello/**").addResourceLocations("/hello/");
    }
}
```

SpringMvcConfig中进行扫描。

```java
package com.iphan.config;

import org.springframework.context.annotation.ComponentScan;
import org.springframework.context.annotation.Configuration;
import org.springframework.web.servlet.config.annotation.EnableWebMvc;

@Configuration
@ComponentScan({"com.iphan.controller", "com.iphan.config"})
@EnableWebMvc
public class SpringMvcConfig {

}
```

![image-20240131204002584](../images/image-20240131204002584.png)
