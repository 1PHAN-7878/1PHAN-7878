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
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>8.0.27</version>
        </dependency>
        <dependency>
            <groupId>org.mybatis</groupId>
            <artifactId>mybatis</artifactId>
            <version>3.5.7</version> <!-- 使用适当的版本号 -->
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

# 下述基本使用

1.首先来准备一个数据库。

2.接下来创建一个普通的 Maven 工程，不用创建 Web 工程，JavaSE 工程即可。项目创建完成后，添加 MyBatis 依赖。

```xml

```

3.接下来，准备一个 Mapper 文件，Mapper 是用来在 MyBatis 中定义 SQL 的 XML 配置文件。

4.在 Mapper 中，定义一个简单的查询方法，根据 id 查询一个Book。

5.定义Book实现类。

6.创建 MyBatis 配置文件。

![image-20240128212333046](../images/image-20240128212333046.png)

# 快速使用

## maven依赖

```xml
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <version>8.0.27</version>
</dependency>
<dependency>
    <groupId>org.mybatis</groupId>
    <artifactId>mybatis</artifactId>
    <version>3.5.7</version> <!-- 使用适当的版本号 -->
</dependency>
```

## mybatis配置

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "https://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
    <environments default="development">
        <environment id="development">
<!--配置信息-->
            <transactionManager type="JDBC"/>
            <dataSource type="POOLED">
                <property name="driver" value="com.mysql.cj.jdbc.Driver"/>
                <property name="url" value="jdbc:mysql://localhost:3306/db_book"/>
                <property name="username" value="root"/>
                <property name="password" value="666"/>
            </dataSource>
        </environment>
    </environments>
<!-- 这里是所有的mapper写全限定名-->
    <mappers>
        <mapper resource="mappers/myMapper.xml"/>
    </mappers>
</configuration>
```

## 编写相应实现类

```java
package models;

public class Bookm {
    public int bookId;
    public String bookName;
    public String bookAuthor;
    public double bookPrice;
    public int bookStock;
    public String bookDesc;

    public int getBookId() {
        return bookId;
    }

    public void setBookId(int bookId) {
        this.bookId = bookId;
    }

    public String getBookName() {
        return bookName;
    }

    public void setBookName(String bookName) {
        this.bookName = bookName;
    }

    public String getBookAuthor() {
        return bookAuthor;
    }

    public void setBookAuthor(String bookAuthor) {
        this.bookAuthor = bookAuthor;
    }

    public double getBookPrice() {
        return bookPrice;
    }

    public void setBookPrice(double bookPrice) {
        this.bookPrice = bookPrice;
    }

    public int getBookStock() {
        return bookStock;
    }

    public void setBookStock(int bookStock) {
        this.bookStock = bookStock;
    }

    public String getBookDesc() {
        return bookDesc;
    }

    public void setBookDesc(String bookDesc) {
        this.bookDesc = bookDesc;
    }

    public Bookm(int bookId, String bookName, String bookAuthor, double bookPrice, int bookStock, String bookDesc) {
        this.bookId = bookId;
        this.bookName = bookName;
        this.bookAuthor = bookAuthor;
        this.bookPrice = bookPrice;
        this.bookStock = bookStock;
        this.bookDesc = bookDesc;
    }

    @Override
    public String toString() {
        return "Bookm{" +
                "bookId=" + bookId +
                ", bookName='" + bookName + '\'' +
                ", bookAuthor='" + bookAuthor + '\'' +
                ", bookPrice=" + bookPrice +
                ", bookStock=" + bookStock +
                ", bookDesc='" + bookDesc + '\'' +
                '}' + '\n';
    }


}
```

设置mapper接口供调用

```java
package mapper;

import models.Bookm;

import java.util.List;

public interface MyMapper {
    List<Bookm> selectAllBook();
    Bookm selectBook(int id);
    void insertBook(Bookm bookm);

}
```

## 设置mapper.xml实现对应

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "https://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="mapper.MyMapper">
    <resultMap id="bookResultMap" type="models.Bookm">
        <id property="bookId" column="book_id"/>
        <result property="bookName" column="book_name"/>
        <result property="bookAuthor" column="book_author"/>
        <result property="bookPrice" column="book_price"/>
        <result property="bookStock" column="book_stock"/>
        <result property="bookDesc" column="book_desc"/>
    </resultMap>
    
    <select id="selectAllBook" resultType="models.Bookm">
<!--        select * from books where book_id = #{id}-->
        select * from books
    </select>
    
    <select id="selectBook" resultType="models.Bookm">
        select * from books where book_id = #{id}
    </select>
    
    <insert id="insertBook" parameterType="models.Bookm">
        insert into books (book_name, book_author, book_price, book_stock, book_desc)
        values(#{bookName}, #{bookAuthor},#{bookPrice},#{bookStock},#{bookDesc})
    </insert>
    
</mapper>
```

调用类

```java
import config.SpringConfig;
import dao.BookDao;
import mapper.MyMapper;
import models.Bookm;
import org.apache.ibatis.io.Resources;
import org.apache.ibatis.session.SqlSession;
import org.apache.ibatis.session.SqlSessionFactory;
import org.apache.ibatis.session.SqlSessionFactoryBuilder;
import org.springframework.context.ApplicationContext;
import org.springframework.context.annotation.AnnotationConfigApplicationContext;
import util.MybatisUtil;

import java.io.IOException;
import java.io.InputStream;
import java.util.List;

public class Application {
    public static void main(String[] args) throws IOException {
//        ApplicationContext ctx = new AnnotationConfigApplicationContext(SpringConfig.class);
//        BookDao bookDao = (BookDao) ctx.getBean("bookDao");
//        bookDao.func1();
//        bookDao.func2();
//        bookDao.func3();



        //指定了 MyBatis 的配置文件的路径
        String resource = "mybatis-config.xml";
        //这一行通过 MyBatis 提供的 Resources 工具类，根据配置文件的路径获取对应的输入流
        InputStream inputStream = Resources.getResourceAsStream(resource);
        //这一行使用 SqlSessionFactoryBuilder 构建器创建了 SqlSessionFactory 对象。
        //SqlSessionFactory 是 MyBatis 中的核心接口，它负责创建 SqlSession 对象，而 SqlSession 是执行 SQL 语句的关键对象。
        SqlSessionFactory sqlSessionFactory = new SqlSessionFactoryBuilder().build(inputStream);
        //通过 SqlSessionFactory 打开了一个 SqlSession 对象。
        //SqlSession 提供了执行 SQL 语句的方法，可以进行数据库操作，包括查询、插入、更新、删除等。
        SqlSession sqlSession = sqlSessionFactory.openSession();
        MyMapper mapper = sqlSession.getMapper(MyMapper.class);
        List<Bookm> bookms = mapper.selectAllBook();
        if(bookms == null){
            System.out.println("is null") ;
        }
        else{
            System.out.println(bookms);
        }

        Bookm bookm = mapper.selectBook(1);
        if(bookm == null){
            System.out.println("is null");
        }else{
            System.out.println(bookm);
        }
//        bookm = new Bookm(3, "新的书", "iphan", 25.0, 10, "是个测试");
//        mapper.insertBook(bookm);
//        sqlSession.commit();
    }


}
```

# CURD

## 增

```xml
<insert id="insertBook" parameterType="models.Bookm">
    insert into books (book_name, book_author, book_price, book_stock, book_desc)
    values(#{bookName}, #{bookAuthor},#{bookPrice},#{bookStock},#{bookDesc})
</insert>
```

```java
void insertBook(Bookm bookm);
```

## 删

```xml
<delete id="deleteBookById" parameterType="int">
    delete from books where book_id = #{id}
</delete>
```

```java
void deleteBookById(int id);
```

## 改

```xml
<update id="updateBook" parameterType="models.Bookm">
    update books set book_price = #{bookPrice} where book_id = #{bookId}
</update>
```

```java
void updateBook(Bookm bookm);
```

## 查

```xml
<select id="selectAllBook" resultType="models.Bookm">
<!--        select * from books where book_id = #{id}-->
        select * from books
    </select>
    <select id="selectBook" resultType="models.Bookm">
        select * from books where book_id = #{id}
    </select>
```

```java
List<Bookm> selectAllBook();
Bookm selectBook(int id);
```

# 配置

## 1 properties

properties 可以连接一个外部配置，比如一些配置文件在 resources 目录下添加一个 db.properties 文件作为数据库的配置文件，文件内容如下：

```properties
db.username=root
db.password=66
db.driver=com.mysql.cj.jdbc.Driver
db.url=jdbc:mysql://localhost:3306/db_book
```

然后，利用 mybatis-config.xml 配置文件中的 properties 属性，引入这个配置文件，然后在 DataSource 中使用这个配置文件，最终配置如下：

```xml
<configuration>
    <properties resource="db.properties"></properties>
    <environments default="development">
        <environment id="development">
            <transactionManager type="JDBC"/>
            <dataSource type="POOLED">
                <property name="driver" value="${db.driver}"/>
                <property name="url" value="${db.url}"/>
                <property name="username" value="${db.username}"/>
                <property name="password" value="${db.password}"/>
            </dataSource>
        </environment>
    </environments>
    <mappers>
        <package name="org.javaboy.mybatis.mapper"/>
    </mappers>
</configuration>
```

## 2 parameterType

表示输入的参数类型。

在 MyBatis 中，`#{}` 和 `${}` 是两种不同的占位符语法，它们在 SQL 语句中的使用有一些区别：

1. **`#{}` 占位符：**

   - 使用 `#{}` 时，MyBatis 会使用预编译的方式处理参数，它会将参数值以及相应的 JDBC 类型信息传递给 JDBC 驱动，以防止 SQL 注入攻击。
   - `#{}` 可以在 SQL 语句中插入参数值，MyBatis 会自动为参数添加适当的引号和转义特殊字符。

   示例：

   ```xml
   <!-- 使用 #{userId} 占位符 -->
   SELECT * FROM users WHERE user_id = #{userId}
   ```

2. **`${}` 占位符：**

   - 使用 `${}` 时，MyBatis 会直接将参数值插入 SQL 语句，不进行预编译处理。这可能导致潜在的 SQL 注入风险，因此要特别注意不要直接从用户输入中使用 `${}`。
   - `${}` 主要用于动态拼接 SQL 片段，例如表名、列名等，而不是用于传递参数值。

   示例：

   ```xml
   <!-- 使用 ${tableName} 占位符 -->
   SELECT * FROM ${tableName}
   ```

**使用建议：**

- 一般来说，推荐使用 `#{}` 占位符，特别是在涉及用户输入的情况下，以避免 SQL 注入风险。
- 在需要动态拼接表名、列名等情况下，可以使用 `${}`，但要确保输入是可信任的，以防止潜在的安全问题。

综合来说，`#{}` 更适合用于传递参数值，而 `${}` 更适合用于动态拼接 SQL 片段。

## 3 resultType

resultType 是返回类型，在实际开发中，如果返回的数据类型比较复杂，一般我们使用 resultMap，但是，对于一些简单的返回，使用 resultType 就够用了。

## 4 resultMap

是一种映射方式，比如java并没有User类型，但是我可以映射一个。

`resultMap` 是 MyBatis 中用于映射查询结果到实体类的一种配置方式。通过 `resultMap` 可以定义如何将数据库查询的列映射到 Java 对象的属性上。通常，`resultMap` 的配置会在 XML 文件中，用于更灵活地处理复杂的映射关系。

以下是一个简单的 `resultMap` 的示例：

```xml
<!-- 在 XML 文件中定义 resultMap -->
<resultMap id="userResultMap" type="User">
    <!-- id描述主键 -->
    <id property="id" column="user_id"/>
    <result property="name" column="user_name"/>
    <result property="age" column="user_age"/>
    <!-- 其他属性映射... -->
</resultMap>
```

在这个例子中，`userResultMap` 定义了如何将查询结果映射到 `User` 类型的对象。具体的映射规则包括：

- `<id>`：定义主键的映射关系，其中 `property` 是 Java 对象的属性名，`column` 是数据库列名。
- `<result>`：定义普通属性的映射关系，同样包括 `property` 和 `column`。

接下来，可以在 SQL 查询语句中引用这个 `resultMap`：

```xml
<!-- 在查询语句中引用 resultMap -->
<select id="getUserById" resultMap="userResultMap">
    SELECT * FROM users WHERE user_id = #{userId}
</select>
```

在上述查询语句中，通过 `resultMap="userResultMap"` 将查询结果映射到 `User` 对象上。MyBatis 将根据 `resultMap` 中的配置，将查询结果的列值赋给相应的 Java 对象属性。

`resultMap` 的使用可以提供更灵活和可读性更好的映射配置，尤其是当数据库表和 Java 对象之间存在一些不同的命名规范时。此外，`resultMap` 还支持一些高级的映射配置，例如继承、关联查询等。

# 注解开发

1. **`@Select`：** 用于配置查询操作的 SQL 语句。

   ```java
   @Select("SELECT * FROM users WHERE id = #{userId}")
   User getUserById(@Param("userId") Long userId);
   ```

2. **`@Insert`：** 用于配置插入操作的 SQL 语句。

   ```java
   @Insert("INSERT INTO users (name, age) VALUES (#{name}, #{age})")
   @Options(useGeneratedKeys = true, keyProperty = "id")
   int insertUser(User user);
   ```

3. **`@Update`：** 用于配置更新操作的 SQL 语句。

   ```java
   @Update("UPDATE users SET name = #{name} WHERE id = #{id}")
   int updateUser(User user);
   ```

4. **`@Delete`：** 用于配置删除操作的 SQL 语句。

   ```java
   @Delete("DELETE FROM users WHERE id = #{userId}")
   int deleteUserById(@Param("userId") Long userId);
   ```

5. **`@ResultMap`：** 用于映射查询结果到实体类的注解，通常与 XML 中的 `<resultMap>` 配合使用。

   ```java
   @Select("SELECT * FROM users")
   @ResultMap("userResultMap")
   List<User> getAllUsers();
   ```

6. **`@Result`：** 用于配置查询结果到实体类属性的映射关系，通常与 `@ResultMap` 配合使用。

   ```java
   @ResultMap("userResultMap")
   @Results({
       @Result(property = "id", column = "user_id"),
       @Result(property = "name", column = "user_name"),
       // ...
   })
   User getUserById(@Param("userId") Long userId);
   ```

7. **`@Param`：** 用于传递参数的注解，主要用于在 SQL 语句中引用参数。

   ```java
   @Select("SELECT * FROM users WHERE id = #{userId} AND name = #{userName}")
   User getUserByIdAndName(@Param("userId") Long userId, @Param("userName") String userName);
   ```

8. **`@Options`：** 用于配置一些特定的选项，比如生成主键值。

   ```java
   @Insert("INSERT INTO users (name, age) VALUES (#{name}, #{age})")
   @Options(useGeneratedKeys = true, keyProperty = "id")
   int insertUser(User user);
   ```

这些注解用于在接口方法上配置 SQL 语句，通过 MyBatis 提供的动态 SQL 和注解，可以更灵活地进行数据库操作。同时，也可以与 XML 文件结合使用，以更好地组织和维护 SQL 语句。
