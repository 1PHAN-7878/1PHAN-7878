---
title: Spring之AOP
date: 2024-01-24 12:45:44
tags: java
---

# AOP

AOP（Aspect-Oriented Programming，面向切面编程）是一种编程范式，它通过将横切关注点（cross-cutting concerns）从主要业务逻辑中分离出来，使得我们能够更清晰、更模块化地组织和维护代码。

在传统的面向对象编程中，我们主要关注业务逻辑的实现，例如类的行为、方法的执行流程等。然而，很多应用都包含一些横切关注点，例如日志记录、事务管理、安全控制、性能优化等，这些关注点不属于核心业务逻辑，但却分布在整个代码基底。AOP 的目标就是将这些横切关注点模块化，使得我们能够更好地维护和管理它们。

AOP 主要通过两个概念来实现：切面（Aspect）和连接点（Join Point）。

1. **切面（Aspect）：** 切面是一个模块化单元，它封装了横切关注点的代码。切面定义了在何处（连接点）以及如何应用横切关注点。在 AOP 中，切面可以包括通知（Advice）、切点（Pointcut）和引介（Introduction）等。
2. **连接点（Join Point）：** 连接点是在应用中程序执行的点，例如方法的执行、异常的处理等。切面通过定义切点来选择连接点，然后在这些连接点上应用通知，从而插入横切关注点的逻辑。

AOP 的一些关键概念：

- **通知（Advice）：** 通知是切面的具体行为，它定义了在连接点上执行的代码。常见的通知类型包括前置通知（在连接点之前执行代码）、后置通知（在连接点之后执行代码）、环绕通知（在连接点前后执行代码，可以控制连接点的执行）、异常通知（在连接点抛出异常时执行代码）等。
- **切点（Pointcut）：** 切点定义了一组连接点的集合，通知被应用到这些连接点上。切点通过表达式或者是通过指定方法名来定义。
- **引介（Introduction）：** 引介允许我们在不修改类结构的情况下，向类添加新的方法或属性。

AOP 的主要优势在于它提高了代码的模块化程度，将横切关注点从核心业务逻辑中解耦，使得代码更易于理解和维护。在 Java 中，Spring 框架提供了强大的支持，通过 Spring AOP 可以轻松实现面向切面的编程。

## 配置maven

```xml
<dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-context</artifactId>
            <version>5.3.10</version> <!-- 使用适当的版本号 -->
        </dependency>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-aop</artifactId>
            <version>5.3.10</version> <!-- 使用适当的版本号 -->
        </dependency>
        <dependency>
            <groupId>org.aspectj</groupId>
            <artifactId>aspectjweaver</artifactId>
            <version>1.9.7</version> <!-- 使用适当的版本号 -->
        </dependency>
```

## 基本使用方法

一个bean中有不同的方法↓

```java
package dao;

import org.springframework.stereotype.Repository;
//使其成为bean
@Repository
public class BookDao {
    //func1在内部实现了输出当前时间的功能
    public void func1(){
        System.out.println(System.currentTimeMillis());
        System.out.println("this is func1");
    }
    //func2要通过AOP的方式实现
    public void func2(){
        System.out.println("this is func2");
    }
}

```

创建通知类，实现相应效果。

```java
package aop;

import org.aspectj.lang.annotation.Aspect;
import org.aspectj.lang.annotation.Before;
import org.aspectj.lang.annotation.Pointcut;
import org.springframework.stereotype.Component;
//定义为可识别的bean
@Component
//定义为AOP类型
@Aspect

public class MyAdvice {

    @Pointcut("execution(void dao.BookDao.func2())")
    //切入点
    private void pt(){}

    //提供绑定
    @Before("pt()")
    //这是一个通知类
    public void method(){
        System.out.println(System.currentTimeMillis());
    }
}

```

对Spring进行配置，创建配置类。

```java
package config;

import org.springframework.context.annotation.ComponentScan;
import org.springframework.context.annotation.Configuration;
import org.springframework.context.annotation.EnableAspectJAutoProxy;

//配置文件
@Configuration
@ComponentScan({"aop","config", "dao"})
@EnableAspectJAutoProxy
public class SpringConfig {
}
```

调用实现

```java
import config.SpringConfig;
import dao.BookDao;
import org.springframework.context.ApplicationContext;
import org.springframework.context.annotation.AnnotationConfigApplicationContext;

public class Application {
    public static void main(String[] args) {
        ApplicationContext ctx = new AnnotationConfigApplicationContext(SpringConfig.class);
        BookDao bookDao = (BookDao) ctx.getBean("bookDao");
        bookDao.func1();
        bookDao.func2();

    }

}

```

# 工作流程

1. **目标对象方法调用：** 首先，程序执行到某个连接点，通常是目标对象（Target Object）的方法调用。这是 AOP 中切面要织入的具体业务逻辑的执行起点。
2. **切面的匹配：** 在连接点上，AOP 框架会检查所有定义的切面，看哪些切面的切点匹配当前的连接点。切点定义了切面要应用的位置。
3. **通知的执行：** 一旦切面的切点匹配了连接点，相应的通知就会被执行。通知是切面中具体的业务逻辑，包括前置通知、后置通知、环绕通知等。不同类型的通知会在不同的时机执行。
4. **目标对象方法的继续执行（对于环绕通知）：** 如果切面是环绕通知，它在执行自己的逻辑后需要决定是否调用连接点（目标对象方法）。在环绕通知中，连接点的执行由切面来控制。

# 切入点表达式

切入点表达式的一般结构包括以下几个部分：

1. **execution：** 这是关键字，指定匹配方法执行的切入点。在 Spring AOP 中，通常以 `execution` 关键字开始。
2. **返回类型：** 用一个通配符 `*` 表示匹配任意返回类型的方法。如果你想具体指定返回类型，可以使用类的全限定名。
3. **包路径：** 表示要匹配的包路径，可以使用通配符 `*` 匹配任意包名，也可以指定具体的包路径。
4. **类名：** 使用 `*` 匹配任意类名，如果要匹配特定的类，可以指定类的名称。
5. **方法名：** 使用 `*` 匹配任意方法名，如果要匹配特定的方法，可以指定方法的名称。
6. **参数列表：** 使用 `(..)` 表示匹配任意参数列表。如果要匹配特定类型和顺序的参数，可以在括号内指定。

切入点表达式的一般结构如下：

```
execution([返回类型] [包路径].[类名].[方法名]([参数列表]))
```

其中，方括号中的部分可以根据需要省略，使用通配符或具体指定。以下是一些例子：

- `execution(* com.example.service.*.*(..))`: 匹配 `com.example.service` 包下所有类的所有方法。
- `execution(public * com.example.service.UserService.*(..))`: 匹配 `com.example.service.UserService` 类中所有公共方法。
- `execution(* com.example.service.*.find*(Long))`: 匹配 `com.example.service` 包下所有类中以 "find" 开头且接受一个 Long 类型参数的方法。

# 通知类型

在 AOP 中，通知是切面中具体行为的定义，它指定了在连接点（方法执行、异常抛出等）上执行的代码。通知类型主要包括以下几种：

1. **前置通知（Before Advice）：** 在连接点方法执行之前执行的通知。可以用于执行一些准备工作或者验证操作。

   ```java
   @Before("execution(* com.example.service.*.*(..))")
   public void beforeAdvice() {
       // 在连接点方法执行之前执行的逻辑
   }
   ```

2. **后置通知（After Returning Advice）：** 在连接点方法成功执行之后执行的通知。可以用于执行一些清理或记录日志等操作。

   ```java
   @AfterReturning(pointcut = "execution(* com.example.service.*.*(..))", returning = "result")
   public void afterReturningAdvice(Object result) {
       // 在连接点方法成功执行之后执行的逻辑，可以访问连接点方法的返回值
   }
   ```

3. ==**环绕通知（Around Advice）：** ===在连接点方法前后执行的通知，可以完全控制连接点方法的执行。需要手动调用连接点方法。

   ```java
   @Around("execution(* com.example.service.*.*(..))")
   //最常用，记得抛出异常，创建返回值
   public Object aroundAdvice(ProceedingJoinPoint joinPoint) throws Throwable {
       // 在连接点方法执行之前执行的逻辑
       Object result = joinPoint.proceed(); // 手动调用连接点方法
       // 在连接点方法执行之后执行的逻辑
       return result;
   }
   ```

4. **异常通知（After Throwing Advice）：** 在连接点方法抛出异常时执行的通知。可以用于处理异常情况。

   ```java
   @AfterThrowing(pointcut = "execution(* com.example.service.*.*(..))", throwing = "exception")
   public void afterThrowingAdvice(Exception exception) {
       // 在连接点方法抛出异常时执行的逻辑，可以访问连接点方法抛出的异常
   }
   ```

5. **最终通知（After Advice）：** 无论连接点方法是否抛出异常，都会执行的通知。常用于执行一些收尾工作，比如资源释放。

   ```java
   @After("execution(* com.example.service.*.*(..))")
   public void afterAdvice() {
       // 无论连接点方法是否抛出异常，都会执行的逻辑
   }
   ```
