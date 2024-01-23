---
title: Spring之IOC
date: 2024-01-20 15:32:00
tags: java
---

# IOC

"IOC" 是 "Inversion of Control"（控制反转）的缩写。这是一种编程原则，它改变了传统的程序设计流程，主要体现在对象的控制权从应用程序代码中转移到外部容器（通常是框架或容器）。

在传统的程序设计中，应用程序代码负责创建和管理对象。但在控制反转中，这一控制权被颠倒过来，对象的创建和管理被外部容器负责。这意味着，应用程序不再直接创建对象，而是通过容器提供的机制来获取所需的对象。

具体来说，在 Java 中，常常使用 Spring 框架实现控制反转。在 Spring 中，对象的创建和依赖关系的管理交给了 Spring 容器。通过配置文件或注解，开发者描述了对象之间的关系，而不需要手动创建这些对象。Spring 容器负责根据配置文件或注解，实例化对象、管理它们的生命周期，并在需要的地方注入依赖。

这种方式有助于降低组件之间的耦合度，提高代码的可维护性和灵活性。控制反转是面向对象编程的一种思想，旨在提高代码的模块化程度和可测试性。

# Spring配置

采用Java17版本

```xml
<dependencies>
        <!-- Spring Core -->
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-context</artifactId>
            <version>5.3.10</version> <!-- 使用适当的版本号 -->
        </dependency>

        <!-- 其他 Spring 模块，根据需要添加 -->
    </dependencies>
```

至此可以使用Spring中的Bean实现IOC

## 例子

```java
//简单Book类
package pojo;

public class Book {

    private String name;
    private int id;
    private int count;

    public Book(){
        name = "default";
        id = 0;
        count = 0;
    }

    public void test(){
        System.out.println("this is a test method");
    }
}

```

```xml
<!--  命名为applicationContext  -->
<!--  放在src.main.resources下 -->

<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
    <!--  通过id访问对象，class为类限定名 -->
    <bean id="book" class="pojo.Book"/>

</beans>
```



# 依赖注入

## 构造函数注入

在 XML 文件中定义需要注入依赖的 Bean，并使用 `<constructor-arg>` 元素来指定构造函数参数：

```xml
<!-- 定义需要注入依赖的目标 Bean -->
<bean id="employee" class="com.example.Employee">
    <!-- 使用构造函数注入参数 -->
    <!-- value是基本类型 -->
    <constructor-arg name="name" value="John Doe" />
    <!-- ref是引用类型 -->
    <constructor-arg name="department" ref="department" />
</bean>

<bean id="department" class="com.example.Department">
    <property name="name" value="Engineering" />
</bean>
```

在上述示例中，`Employee` 类有一个接受两个参数的构造函数，通过 `<constructor-arg>` 元素分别注入 `name` 和 `department`。

## Setter注入

在 XML 文件中定义需要注入依赖的 Bean，并使用 `<property>` 元素来指定属性值：

```xml
<!-- 定义需要注入依赖的目标 Bean -->
<bean id="employee" class="com.example.Employee">
    <!-- 使用setter方法注入属性 -->
    <property name="name" value="John Doe" />
    <property name="department" ref="department" />
</bean>

<bean id="department" class="com.example.Department">
    <property name="name" value="Engineering" />
</bean>
```

在上述示例中，`Employee` 类有两个属性 `name` 和 `department`，通过 `<property>` 元素分别注入值。

## 泛型

1. **List 注入**：

   ```xml
   <bean id="listHolder" class="com.example.ListHolder">
       <property name="stringList">
           <list>
               <value>Item 1</value>
               <value>Item 2</value>
               <value>Item 3</value>
           </list>
       </property>
   </bean>
   ```

   在这个例子中，`ListHolder` 类有一个名为 `stringList` 的 List 属性。

2. **Map 注入**：

   ```xml
   <bean id="mapHolder" class="com.example.MapHolder">
       <property name="dataMap">
           <map>
               <entry key="Key 1" value="Value 1" />
               <entry key="Key 2" value="Value 2" />
               <entry key="Key 3" value="Value 3" />
           </map>
       </property>
   </bean>
   ```

## 例子

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
    
    <bean id="book" class="pojo.Book">
        <!--Setter注入-->
        <property name="count" value="1"/>
        <property name="id" value="1"/>
        <property name="name" value="default"/>
        <!--引用类型-->
        <property name="agent" ref="agent"/>
    </bean>

    <bean id="agent" class="pojo.Agent">
        <!--构造注入-->
        <constructor-arg name="id" value="1"/>
        <constructor-arg name="name" value="人"/>

    </bean>
</beans>
```

# 自动注入

在 Spring 中，可以使用 XML 配置文件进行自动装配，主要有三种方式：`autowire="byName"`、`autowire="byType"` 和 `autowire="constructor"`。

以下是每种自动装配方式的示例：

1. **按名称自动装配 (`autowire="byName"`)：**

   ```xml
   <bean id="person" class="com.example.Person" autowire="byName">
       <!-- 需要自动装配的属性 -->
   </bean>
   ```

   在这个例子中，Spring 会根据属性的名称，在容器中查找匹配的 Bean，并将其自动装配到对应的属性上。

2. **按类型自动装配 (`autowire="byType"`)：**==最常用==

   ```xml
   <bean id="person" class="com.example.Person" autowire="byType">
       <!-- 需要自动装配的属性 -->
   </bean>
   ```

   Spring 会根据属性的类型，在容器中查找匹配的 Bean，并将其自动装配到对应的属性上。

3. **构造函数自动装配 (`autowire="constructor"`)：**

   ```xml
   <bean id="person" class="com.example.Person" autowire="constructor">
       <!-- 需要自动装配的属性 -->
   </bean>
   ```

   Spring 会根据构造函数的参数类型，在容器中查找匹配的 Bean，并将其自动装配到对应的构造函数参数上。

# 使用

```java
import org.springframework.context.ApplicationContext;
import org.springframework.context.support.ClassPathXmlApplicationContext;
import pojo.Agent;
import pojo.Book;

public class Application {
    public static void main(String[] args) {
        //加载配置文件初始化容器
        ApplicationContext ctx = new ClassPathXmlApplicationContext("applicationContext.xml");
        Book book = (Book) ctx.getBean("book");
        Agent agent = book.getAgent();
        System.out.println(agent.getName());
    }
}
```

# 注解开发

## 配置maven依赖

```xml
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-context</artifactId>
    <version>5.3.10</version> <!-- 使用适当的版本号 -->
</dependency>
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-core</artifactId>
    <version>5.3.10</version>
</dependency>
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-beans</artifactId>
    <version>5.3.10</version>
</dependency>
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-aop</artifactId>
    <version>5.3.10</version>
</dependency>
<dependency>
            <groupId>javax.annotation</groupId>
            <artifactId>javax.annotation-api</artifactId>
            <version>1.2</version>
        </dependency>
```

## 定义bean

使用`@Component`定义bean

```java
package pojo;

import org.springframework.stereotype.Component;

@Component("newBook")
public class NewBook {

}
```

### 三个层次

Spring提供了几个与 `@Component` 注解相关的衍生注解，用于更精确地定义组件的角色。这些衍生注解分别是：`@Repository`、`@Service`、和 `@Controller`。这些注解的作用是更好地表达组件的用途，以及在使用Spring自动组件扫描时对不同层次的组件进行更细粒度的区分。

1. **`@Repository`：**

   - `@Repository` 注解用于标识数据访问层（DAO）的组件。它表明被注解的类负责数据库访问、数据存储等持久化层的工作。通常与 Spring 的异常转换机制一起使用，将数据访问层的异常转换为 Spring 的 DataAccessException。

   ```java
   @Repository
   public class MyRepository {
       // 数据访问相关的方法
   }
   ```

2. **`@Service`：**

   - `@Service` 注解用于标识业务逻辑层的组件。它表明被注解的类包含业务逻辑，负责处理业务规则、流程等。通常在服务层使用。

   ```java
   @Service
   public class MyService {
       // 业务逻辑相关的方法
   }
   ```

3. **`@Controller`：**

   - `@Controller` 注解用于标识控制层的组件，通常用于处理Web请求。它表明被注解的类是一个控制器，处理用户的HTTP请求，并返回相应的视图。

   ```java
   @Controller
   public class MyController {
       // 处理HTTP请求的方法
   }
   ```

## 配置类

Spring3.0采用注解开发，用配置类代替xml配置，加快开发速度。

```java
package config;

import org.springframework.context.annotation.ComponentScan;
import org.springframework.context.annotation.Configuration;
//声明当前为配置类
@Configuration
//设置扫描路径，多个路径书写为字符串格式
@ComponentScan({"config", "pojo", "service"})
public class AppConfig {
}
```

```java
import config.AppConfig;
import org.springframework.context.ApplicationContext;
import org.springframework.context.annotation.AnnotationConfigApplicationContext;
import pojo.NewBook;

public class Application2 {

    public static void main(String[] args) {
        //加载配置类，初始化Spring容器
        ApplicationContext ctx = new AnnotationConfigApplicationContext(AppConfig.class);
        //获取对象
        NewBook newBook = (NewBook) ctx.getBean("newBook");
        newBook.func();
    }


}
```

## @Scope作用域

1. **Singleton（默认）：**

   - `@Scope("singleton")` 或 `@Scope(value = ConfigurableBeanFactory.SCOPE_SINGLETON)`。
   - 表示在 Spring 容器中，只存在一个共享的 Bean 实例。这是默认的作用域。

   ```java
   @Component
   @Scope("singleton")
   public class MySingletonBean {
       // ...
   }
   ```

2. **Prototype：**

   - `@Scope("prototype")` 或 `@Scope(value = ConfigurableBeanFactory.SCOPE_PROTOTYPE)`。
   - 表示每次通过容器的 `getBean` 方法获取 Bean 时，都会创建一个新的实例。

   ```java
   @Component
   @Scope("prototype")
   public class MyPrototypeBean {
       // ...
   }
   ```

3. **Request：**

   - `@Scope("request")`。
   - 表示在一次 HTTP 请求内，共享同一个 Bean 实例。仅在 Spring Web 应用中有效，需要启用 `RequestScope`。

   ```java
   @Component
   @Scope("request")
   public class MyRequestScopedBean {
       // ...
   }
   ```

4. **Session：**

   - `@Scope("session")`。
   - 表示在一个用户会话中，共享同一个 Bean 实例。同样需要在 Spring Web 应用中使用，并启用 `SessionScope`。

   ```java
   @Component
   @Scope("session")
   public class MySessionScopedBean {
       // ...
   }
   ```

5. **GlobalSession：**

   - `@Scope("globalSession")`。
   - 表示在全局 HTTP Session 中，共享同一个 Bean 实例。同样需要在 Spring Web 应用中使用，并启用 `GlobalSessionScope`。

   ```java
   @Component
   @Scope("globalSession")
   public class MyGlobalSessionScopedBean {
       // ...
   }
   ```

选择适当的作用域取决于你的应用程序的需求。默认的 Singleton 适用于大多数情况，但在某些情况下，如需要 Bean 每次调用时都是新实例，可以使用 Prototype。对于 Web 应用程序，Request、Session 和 GlobalSession 作用域通常与 Web 框架一起使用。

## 生命周期

在 Spring 中，可以使用 `@PostConstruct` 和 `@PreDestroy` 注解来控制初始化和销毁方法，而不必依赖于 XML 配置。这些注解分别用于标识初始化和销毁方法，并在 Bean 的生命周期中自动调用。

1. **使用 `@PostConstruct` 注解进行初始化：**

   - `@PostConstruct` 注解用于标识在 Bean 初始化时需要执行的方法。该方法会在依赖注入之后、任何自定义初始化方法之前被调用。

   ```java
   import javax.annotation.PostConstruct;
   import org.springframework.stereotype.Component;
   
   @Component
   public class MyBean {
   
       @PostConstruct
       public void init() {
           // 这里可以放置初始化逻辑
           System.out.println("Bean 初始化方法被调用");
       }
   
       // 其他业务方法
   }
   ```

2. **使用 `@PreDestroy` 注解进行销毁：**

   - `@PreDestroy` 注解用于标识在 Bean 销毁时需要执行的方法。该方法会在容器关闭之前被调用。

   ```java
   import javax.annotation.PreDestroy;
   import org.springframework.stereotype.Component;
   
   @Component
   public class MyBean {
   
       // 其他业务方法
   
       @PreDestroy
       public void destroy() {
           // 这里可以放置销毁逻辑
           System.out.println("Bean 销毁方法被调用");
       }
   }
   ```

需要注意的是，为了使用 `@PostConstruct` 和 `@PreDestroy` 注解，确保以下几点：

- 在类上添加 `@Component` 或其他 Spring 注解，以使这个类被 Spring 容器扫描并作为 Bean 进行管理。
- 确保 Spring 容器开启了对注解的扫描。可以通过在配置类上添加 `@ComponentScan` 注解或在 XML 配置中启用 `<context:component-scan>`。

## 依赖注入

- 通过在成员变量上使用 `@Autowired`，Spring 容器会尝试将匹配的 bean 注入到成员变量中。

```java
@Service
public class MyService {

    @Autowired
    private MyRepository myRepository;

    // 其他业务方法
}
```

> `@Qualifier` 是 Spring 框架中用于解决自动装配（`@Autowired`）时，多个候选 bean 产生歧义性的注解。当存在多个符合类型的 bean 可以注入时，`@Qualifier` 允许指定具体要注入的 bean 的名称或标识符。
>
> 通常情况下，`@Autowired` 注解会根据类型自动装配一个 bean，但当有多个相同类型的 bean 存在时，Spring 就会产生歧义性。`@Qualifier` 注解就是为了解决这个问题。
>
> 以下是使用 `@Qualifier` 的例子：
>
> ```java
> @Service
> public class MyService {
> 
>     private final MyRepository myRepository;
> 
>     @Autowired
>     @Qualifier("myRepositoryImpl") // 使用 @Qualifier 指定要注入的 bean 的名称
>     public MyService(MyRepository myRepository) {
>         this.myRepository = myRepository;
>     }
> 
>     // 其他业务方法
> }
> ```
>
> 在上述例子中，`@Qualifier("myRepositoryImpl")` 表示要注入名为 "myRepositoryImpl" 的 bean。这样，即使有多个 `MyRepository` 类型的 bean，Spring 会根据 `@Qualifier` 提供的信息选择合适的 bean 进行注入。
>
> 如果 bean 的标识符（通常是 bean 的名称）与 `@Qualifier` 中指定的名称一致，也可以省略 `@Qualifier` 注解，因为 Spring 默认会根据标识符来进行匹配。
>
> ```java
> @Service
> public class MyService {
> 
>     private final MyRepository myRepository;
> 
>     @Autowired
>     public MyService(@Qualifier("myRepositoryImpl") MyRepository myRepository) {
>         this.myRepository = myRepository;
>     }
> 
>     // 其他业务方法
> }
> ```
> 
```
//基本类型依赖
@Value("100")
private int num;
```

## 例子

```java
package pojo;

//import jakarta.annotation.PostConstruct;
//import jakarta.annotation.PreDestroy;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.beans.factory.annotation.Value;
import org.springframework.stereotype.Component;

import javax.annotation.PostConstruct;
import javax.annotation.PreDestroy;

@Component("newBook")
public class NewBook {
    @Value("100")
    private int num;
    //依赖注入
    @Autowired
    private NewBookContro newBookContro;

//    @Autowired
//    public NewBook(@Value("100") int num, NewBookContro newBookContro){
//        this.num = num;
//        this.newBookContro = newBookContro;
//    }
    public void func(){
        System.out.println("this is New do!");
        System.out.println("num is" + num);
        System.out.println("id is" + newBookContro.getId());
    }
    @PostConstruct
    public void init() {
        // 这里可以放置初始化逻辑
        System.out.println("Bean 初始化方法被调用");
        num = 0;

    }
    @PreDestroy
    public void destroy(){
        System.out.println("Bean 被销毁了");
    }
}
```

```java
package pojo;

import org.springframework.beans.factory.annotation.Value;
import org.springframework.stereotype.Component;

@Component("newBookContro")
public class NewBookContro {
    public int getId() {
        return id;
    }

    public void setId(int id) {
        this.id = id;
    }

    @Value("100")
    private int id;
}
```

```java
import config.AppConfig;
import org.springframework.context.ApplicationContext;
import org.springframework.context.annotation.AnnotationConfigApplicationContext;
import pojo.NewBook;

public class Application2 {

    public static void main(String[] args) {
        //加载配置类，初始化Spring容器
        ApplicationContext ctx = new AnnotationConfigApplicationContext(AppConfig.class);
        NewBook newBook = (NewBook) ctx.getBean("newBook");
        newBook.func();

    }


}
```

```
Bean 初始化方法被调用
this is New do!
num is0
id is100
```

