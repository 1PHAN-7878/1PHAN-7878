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
