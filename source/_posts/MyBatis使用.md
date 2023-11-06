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

# 配置mapper代理

在 MyBatis 中，你可以使用 Mapper 代理开发方式来访问数据库而不需要编写实现类，代理会根据你的映射文件执行相应的 SQL。以下是设置 Mapper 代理开发的步骤：

1. **创建映射文件**：首先，你需要创建一个 XML 映射文件，它描述了 SQL 查询、插入、更新或删除操作。这个映射文件通常包含在 MyBatis 配置文件中。

   例如，这是一个简单的映射文件示例：==名称空间是包的名称中接口==

   ```xml
   <?xml version="1.0" encoding="UTF-8" ?>
   <!DOCTYPE mapper
     PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
     "https://mybatis.org/dtd/mybatis-3-mapper.dtd">
   <mapper namespace="com.example.mapper.MyMapper">
     <select id="selectUser" resultType="com.example.User">
       SELECT * FROM users WHERE id = #{id}
     </select>
   </mapper>
   ```

2. **创建 Java 接口**：接下来，你需要创建一个 Java 接口，该接口定义了与映射文件相对应的方法。这些方法的名称和参数应该与映射文件中的 SQL 查询操作相匹配。==方法对应的是xml中的id==

   ```java
   package com.example.mapper;
   
   import com.example.User;
   
   public interface MyMapper {
       User selectUser(int id);
   }
   ```

3. **配置 MyBatis**：在 MyBatis 配置文件（通常是 `mybatis-config.xml`）中，确保已包含了映射文件的引用，如下所示：==通常使用包名==

   ```xml
   <mappers>
     <mapper resource="com/example/mapper/MyMapper.xml" />
   </mappers>
   ```

4. **使用 Mapper 代理**：在你的应用程序中，你可以通过创建 `SqlSession` 并获取 Mapper 接口的代理对象来使用 Mapper 代理。然后，你可以使用该代理对象来执行映射文件中定义的方法。

   ```java
   SqlSession sqlSession = sessionFactory.openSession();
   MyMapper myMapper = sqlSession.getMapper(MyMapper.class);
   User user = myMapper.selectUser(123);
   ```

5. **关闭 SqlSession**：在完成操作后，不要忘记关闭 `SqlSession` 以释放资源。

   ```java
   sqlSession.close();
   ```

这样，你就可以使用 Mapper 代理开发方式与数据库交互，而无需显式实现每个 SQL 操作。Mapper 代理会根据你的接口定义和映射文件执行相应的 SQL 操作。

目录结构如下

![image-20231106093649924](../images/image-20231106093649924.png)

# 结果映射

在 XML 中使用 `<resultMap>` 元素是为了定制查询结果映射到对象的方式。 `<resultMap>` 元素通常用于 MyBatis（一个流行的 Java 持久层框架）的配置文件中，用于定义如何将查询结果映射到 Java 对象。以下是如何使用 `<resultMap>` 元素的示例：

```xml
<resultMap id="userResultMap" type="com.example.User">
  <!-- 指定结果集中的列到 Java 对象的属性的映射 -->
  <result property="id" column="user_id"/>
  <result property="username" column="username"/>
  <result property="email" column="user_email"/>
</resultMap>
```

上面的示例中，`<resultMap>` 元素定义了一个名为 `userResultMap` 的映射，将查询结果映射到 `com.example.User` 类型的对象。它使用 `<result>` 元素指定了查询结果中的列与 Java 对象的属性之间的映射关系。

接下来，你可以在 SQL 查询语句中引用这个 `<resultMap>`，如下所示：

```xml
<select id="getUserById" resultMap="userResultMap">
  SELECT user_id, username, user_email
  FROM users
  WHERE user_id = #{id}
</select>
```

在上面的 `<select>` 元素中，通过 `resultMap` 属性指定了要使用的 `<resultMap>`，这将告诉 MyBatis 如何将查询结果映射到 `com.example.User` 对象。

使用 `<resultMap>` 元素的主要目的是为了灵活地映射查询结果，允许你将查询结果中的列映射到不同的 Java 对象属性，以及支持高级的映射配置，如复杂的嵌套对象映射等。这对于定制数据映射非常有用。

# 引用参数

在 MyBatis 的 XML 配置文件中，你可以定义带有参数的 SQL 语句，并在需要时引用这些参数。以下是一个示例，演示了如何在 MyBatis XML 中使用带有参数的 SQL 语句：

首先，在 MyBatis XML 配置文件中定义带有参数的 SQL 语句，你可以使用 `${paramName}` 来引用参数：

```xml
<mapper namespace="com.example.MyMapper">
  <!-- 定义带有参数的 SQL 语句 -->
  <select id="getUserById" resultType="com.example.User">
    SELECT * FROM users WHERE id = ${id}
  </select>
</mapper>
```

在上面的示例中，`getUserById` 查询使用 `${id}` 来引用一个参数，它会匹配方法参数的名称。

接下来，你可以在 Java 代码中调用这个 SQL 语句，将参数传递给它：

```java
import com.example.User;
import org.apache.ibatis.annotations.Param;

public interface MyMapper {
    User getUserById(@Param("id") int id);
}
```

在上面的 Java 代码中，`@Param("id")` 注解指定了参数的名称，这个名称应该与 SQL 语句中的 `${id}` 匹配。

然后，你可以在应用中调用这个方法，并传递参数：

```java
public class MyApp {
    public static void main(String[] args) {
        SqlSessionFactory sqlSessionFactory = MyBatisUtil.getSqlSessionFactory();
        SqlSession session = sqlSessionFactory.openSession();

        MyMapper myMapper = session.getMapper(MyMapper.class);
        User user = myMapper.getUserById(1);

        System.out.println(user);
        
        session.close();
    }
}
```

在上面的示例中，`getUserById` 方法接收一个参数，该参数与 SQL 语句中的 `${id}` 匹配，MyBatis 将执行 SQL 查询并将结果映射到 `User` 对象中。

这是一个简单的示例，演示了如何在 MyBatis XML 配置文件中定义带有参数的 SQL 语句，并在 Java 代码中使用它。你可以根据你的需要定义更复杂的 SQL 语句，引用多个参数，并执行各种查询和操作。
