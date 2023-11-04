---
title: MyBatis使用
date: 2023-11-04 19:48:15
tags: java
---

# 官方网站

https://mybatis.org/mybatis-3/zh/index.html

# 什么是Mybatis

一种用于 Java 编程语言的开源持久性框架。它提供了一种将对象与数据库表进行映射的方法，允许开发人员使用面向对象的编程方式来访问和操作数据库。

MyBatis 的主要功能和特点包括：

1. **对象-关系映射（ORM）**：MyBatis 允许开发人员将 Java 对象和数据库表进行映射，从而避免了手动编写大量的 SQL 查询语句。这使得开发人员可以更专注于业务逻辑，而不是 SQL 语句的编写。
2. **XML 或注解配置**：MyBatis 支持通过 XML 文件或注解来配置数据映射和 SQL 查询。这种配置的方式使得开发人员可以更容易地维护和修改 SQL 查询。
3. **动态 SQL**：MyBatis 支持动态 SQL 查询，这意味着你可以根据不同的条件生成不同的 SQL 查询语句，而不必编写大量重复的 SQL 语句。
4. **缓存支持**：MyBatis 具有内置的缓存支持，可以提高应用程序的性能，减少数据库查询的次数。
5. **自动映射**：MyBatis 可以自动将查询结果映射到 Java 对象，无需手动编写映射代码。
6. **批处理**：MyBatis 支持批处理操作，可以有效地处理多个数据库操作。
7. **插件支持**：MyBatis 允许开发人员编写自定义插件来扩展框架的功能。

MyBatis 在 Java 开发中广泛使用，特别是在与关系型数据库的交互方面。它为开发人员提供了一种直观且灵活的方法，以简化数据库访问和操作。

# 配置

在maven中配置,修改版本号

```xml
<dependency>
  <groupId>org.mybatis</groupId>
  <artifactId>mybatis</artifactId>
  <version>x.x.x</version>
</dependency>
```

sources中的配置，修改驱动等信息，同时修改所使用的mapper对象

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
  PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
  "https://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
  <environments default="development">
    <environment id="development">
      <transactionManager type="JDBC"/>
      <dataSource type="POOLED">
        <property name="driver" value="${driver}"/>
        <property name="url" value="${url}"/>
        <property name="username" value="${username}"/>
        <property name="password" value="${password}"/>
      </dataSource>
    </environment>
  </environments>
  <mappers>
    <mapper resource="org/mybatis/example/BlogMapper.xml"/>
  </mappers>
</configuration>
```

配置用户的mappers，包含sql语句等

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
  PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
  "https://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="org.mybatis.example.BlogMapper">
  <select id="selectBlog" resultType="Blog">
    select * from Blog where id = #{id}
  </select>
</mapper>
```

# 使用

MyBatis 包含一个名叫 Resources 的工具类，它包含一些实用方法，使得从类路径或其它位置加载资源文件更加容易。

```java
String resource = "org/mybatis/example/mybatis-config.xml";
InputStream inputStream = Resources.getResourceAsStream(resource);
SqlSessionFactory sqlSessionFactory = new SqlSessionFactoryBuilder().build(inputStream);
```

既然有了 SqlSessionFactory，顾名思义，我们可以从中获得 SqlSession 的实例。SqlSession 提供了在数据库执行 SQL 命令所需的所有方法。你可以通过 SqlSession 实例来直接执行已映射的 SQL 语句。例如：

```java
try (SqlSession session = sqlSessionFactory.openSession()) {
  Blog blog = (Blog) session.selectOne("org.mybatis.example.BlogMapper.selectBlog", 101);
}
```

目录结构为resources和java同级，在main下一级

![image-20231104211112060](../images/image-20231104211112060.png)

使用修改后的代码如下

```java
package com.example.batis;

import java.io.IOException;
import java.io.InputStream;
import java.util.List;

import org.apache.ibatis.io.Resources;
import org.apache.ibatis.session.SqlSession;
import org.apache.ibatis.session.SqlSessionFactory;
import org.apache.ibatis.session.SqlSessionFactoryBuilder;

public class Test {
	
 
	private int book_id;
	private String book_name;
	private String book_author;
	private double book_price;
	private int book_stock;
	private String book_desc;
	
	
	public Test(int book_id, String book_name, String book_author, double book_price, int book_stock,
			String book_desc) {
		super();
		this.book_id = book_id;
		this.book_name = book_name;
		this.book_author = book_author;
		this.book_price = book_price;
		this.book_stock = book_stock;
		this.book_desc = book_desc;
	}
	

	@Override
	public String toString() {
		return "Test [book_id=" + book_id + ", book_name=" + book_name + ", book_author=" + book_author
				+ ", book_price=" + book_price + ", book_stock=" + book_stock + ", book_desc=" + book_desc + "]";
	}


	public static void main(String[] args) throws IOException {
		// TODO 自动生成的方法存根
		String resource = "mybatis-config.xml";
		InputStream inputStream = Resources.getResourceAsStream(resource);
		SqlSessionFactory sqlSessionFactory = new SqlSessionFactoryBuilder().build(inputStream);
		SqlSession sqlSession = sqlSessionFactory.openSession();
		List<Test> list =  sqlSession.selectList("test.All");
		
		System.out.println(list);
	}

}

```

