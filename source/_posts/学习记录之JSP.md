---
title: 学习记录之JSP
date: 2023-12-26 14:46:51
tags: java
---

# JSP

JSP（JavaServer Pages）是一种用于创建动态Web页面的Java技术。它允许开发人员将Java代码嵌入HTML页面中，以生成动态内容。JSP是在服务器端执行的，它与Servlet一起用于构建Web应用程序。

以下是关于JSP的一些关键点：

1. **动态内容生成：** JSP允许将Java代码嵌入到HTML页面中，使开发人员能够轻松地生成动态内容。这些Java代码被包装在特殊的标签 `<% %>` 中。
2. **易于学习和使用：** 对于熟悉HTML和Java的开发人员而言，学习和使用JSP相对容易。JSP页面的外观类似于常规的HTML页面，但具有嵌入的Java代码。
3. **与Servlet结合使用：** JSP本质上是Servlet的一种简化形式。当JSP页面首次被访问时，容器会将其转换为一个Servlet，并在后续请求中直接执行已编译的Servlet，以提高性能。
4. **标签库（Tag Libraries）：** JSP支持使用标签库来简化页面中的Java代码。标签库提供了一组自定义标签，可用于执行特定的任务，例如访问数据库、控制流程等。
5. **分离业务逻辑和显示逻辑：** JSP有助于将业务逻辑和显示逻辑分开，使得在Web应用程序中更容易维护和管理。
6. **易于集成：** JSP可以轻松地与Java EE（Enterprise Edition）平台的其他技术集成，例如Servlet、EJB（Enterprise JavaBeans）、JavaBeans等。
7. **支持Java标准库：** JSP支持使用Java标准库中的类和方法，这意味着开发人员可以充分利用Java的强大功能。

# 第一个JSP界面

```jsp
<%--
  Created by IntelliJ IDEA.
  User: 7878
  Date: 2023/12/26
  Time: 14:52
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
</head>
<body>

</body>
</html>
```

1. `<%@ page contentType="text/html;charset=UTF-8" language="java" %>`: 这是一个页面指令，用于设置页面的一些属性。
   - `contentType`: 指定响应内容的类型为"text/html"，表示输出的内容是HTML格式的。
   - `charset="UTF-8"`: 指定字符集为UTF-8，确保正确处理包含非英文字符的文本。
   - `language="java"`: 指定在页面中使用的主要编程语言为Java。
2. `<html>`、`<head>`、`<title>`、`<body>`: 这些标签构成了HTML文档的基本结构。

```jsp
<h1>Hello, <%= new Date().toLocaleString()%>!</h1>
```

在首部写入,以导入所需要的包。

```
<%@ page import="java.util.*" %>
```

# 页面元素

JSP 页面通常包含以下主要元素：

1. **HTML 标记：** JSP 页面可以包含标准的 HTML 标记，用于定义页面的结构、样式和布局。

   ```jsp
   <!DOCTYPE html>
   <html>
   <head>
       <title>My JSP Page</title>
   </head>
   <body>
       <h1>Hello, World!</h1>
   </body>
   </html>
   ```

2. **JSP 指令：** JSP 页面中的指令以 `<%@` 开始，用于提供有关页面的全局信息。

   ```jsp
   <%@ page language="java" contentType="text/html; charset=UTF-8" pageEncoding="UTF-8"%>
   ```

3. **JSP 声明：** JSP 声明用于定义在生成的 Servlet 类中的成员变量和方法。

   ```jsp
   <%!
   int counter = 0;
   %>
   ```

4. **JSP 表达式：** JSP 表达式用于在页面中嵌入 Java 表达式的结果。

   ```jsp
   <p>The current counter value is <%= counter %></p>
   ```

5. **JSP 脚本：** JSP 脚本用于插入 Java 代码块，可以包含任意有效的 Java 代码。

   ```jsp
   <% 
   String message = "Hello, JSP!";
   out.println(message);
   %>
   ```

6. **动作元素：** JSP 提供了一些称为动作元素的特殊标签，用于执行特定的操作，如转发请求、包含其他页面等。

   ```jsp
   <jsp:include page="header.jsp" />
   ```

这些元素的组合使得开发者能够在 HTML 页面中嵌入动态内容，利用 Java 代码生成页面的部分或全部内容。

![image-20231226151351362](../images/image-20231226151351362.png)

## 练习

jsp循环打印效果

![image-20231226152405548](../images/image-20231226152405548.png)

```jsp
<%--
  Created by IntelliJ IDEA.
  User: 7878
  Date: 2023/12/26
  Time: 15:15
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" import="java.util.*" %>
<html>
<head>
    <title>Title</title>
</head>
<body>
    <%
        List<String> list = new ArrayList<>();
        list.add("Today");
        list.add("is");
        list.add("a");
        list.add("good");
        list.add("day");
    %>


<table style="align-content: center; width:200px; border-collapse: collapse">


    <% for(String word: list){ %>
        <tr>
            <td> <%=word%> </td>
        </tr>

    <%}%>

</table>

</table>
</body>
</html>
```

# include

在JSP中，`<%@ include %>` 指令用于包含其他文件的内容。通过使用 include 指令，可以将一个文件的内容嵌入到另一个 JSP 文件中。这样可以方便地重用和组织代码。

以下是使用 `<%@ include %>` 指令的基本语法：

```jsp
<%@ include file="relative_path_to_included_file.jsp" %>
```

其中，`file` 属性指定了要包含的文件的相对路径。这个路径是相对于包含文件的 JSP 文件的路径的。



如果需要在包含的文件之间传递参数，可以考虑使用动态包含，即 `<jsp:include>` 标签。

以下是使用 `<jsp:include>` 标签传递参数的示例：

假设有一个包含参数的 JSP 文件 `included.jsp`：

```jsp
<%-- included.jsp --%>
<%@ page language="java" contentType="text/html; charset=UTF-8" pageEncod	ing="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>Included Page</title>
</head>
<body>
    <h2>Value from included page: <%= request.getParameter("param1") %></h2>
</body>
</html>
```

然后，在主 JSP 文件中使用 `<jsp:include>` 标签并传递参数：

```jsp
<%-- main.jsp --%>
<%@ page language="java" contentType="text/html; charset=UTF-8" pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>Main Page</title>
</head>
<body>
    <h1>Main Page</h1>

    <%-- Pass parameter to the included page --%>
    <jsp:include page="included.jsp">
        <jsp:param name="param1" value="Hello from main.jsp" />
    </jsp:include>
</body>
</html>
```

# 页面跳转

在JSP中，可以使用不同的方式来实现页面的跳转。以下是一些常见的方法：

1. **使用 `<jsp:forward>` 标签：**

   ```jsp
   <jsp:forward page="targetPage.jsp" />
   ```

   这个标签用于在当前JSP页面内执行服务器端跳转。`page` 属性指定要跳转的目标页面。

2. **使用 `<% response.sendRedirect("targetPage.jsp"); %>`：** 在脚本元素中使用`response.sendRedirect`方法进行客户端跳转。这会向浏览器发送一个重定向响应，让浏览器重新请求指定的目标页面。

   ```jsp
   <% response.sendRedirect("targetPage.jsp"); %>
   ```

3. **使用相对路径或绝对路径：** 直接使用超链接或表单的 `action` 属性指定目标页面的路径，可以是相对路径或绝对路径。

   ```jsp
   <!-- 使用超链接 -->
   <a href="targetPage.jsp">跳转到目标页面</a>
   
   <!-- 使用表单 -->
   <form action="targetPage.jsp" method="post">
       <!-- 表单内容 -->
       <input type="submit" value="提交" />
   </form>
   ```

# Cookie

在JSP中，你可以使用`Cookie`对象来处理HTTP cookie。Cookie是在客户端（浏览器）和服务器之间传递的小型文本数据，用于在请求之间保持状态信息。以下是在JSP中使用Cookie的基本步骤：

1. **创建Cookie：** 在JSP页面中，你可以使用Java代码创建一个Cookie对象。通常，你会在服务器端脚本中执行这些操作。

   ```jsp
   <% 
       Cookie myCookie = new Cookie("cookieName", "cookieValue");
   	// 设置Cookie的存在时间为一天（60秒 * 60分钟 * 24小时）
      	myCookie.setMaxAge(60 * 60 * 24);
       response.addCookie(myCookie);
   %>
   ```

   上述代码创建了一个名为 "cookieName"，值为 "cookieValue" 的Cookie对象，并通过`response.addCookie`方法将其添加到HTTP响应中。

2. **读取Cookie：** 你可以在后续的请求中读取Cookie，以获取先前存储的信息。

   ```jsp
   <% 
       Cookie[] cookies = request.getCookies();
       if (cookies != null) {
           for (Cookie cookie : cookies) {
               if ("cookieName".equals(cookie.getName())) {
                   String cookieValue = cookie.getValue();
                   // 处理Cookie值
               }
           }
       }
   %>
   ```

   上述代码使用`request.getCookies()`获取请求中的所有Cookie，然后通过遍历找到名为 "cookieName" 的Cookie并获取其值。

> Cookie的路径属性规定了哪些路径下的页面可以访问该Cookie。当服务器创建一个Cookie并发送到客户端时，可以通过设置Cookie的路径来限定哪些路径下的页面可以访问这个Cookie。这有助于控制Cookie的作用范围，增加了一定的安全性和灵活性。
>
> 具体来说，当浏览器向服务器发送请求时，只有在与Cookie的路径匹配的页面才会将相应的Cookie包含在请求中。这有助于确保Cookie仅在需要的上下文中被发送，而不是在整个域中。
>
> 例如，如果设置了以下Cookie：
>
> ```jsp
> <%
>    Cookie myCookie = new Cookie("cookieName", "cookieValue");
>    myCookie.setPath("/myapp");
>    response.addCookie(myCookie);
> %>
> ```
>
> 这个Cookie的路径被设置为"/myapp"，那么它只会被发送到路径为"/myapp"及其子路径下的页面。如果在"/myapp/page1.jsp"中发送请求，浏览器将携带该Cookie。但如果在"/otherapp/page2.jsp"中发送请求，该Cookie将不会被包含在请求中。
>
> 这个路径属性提供了一种方式来限制Cookie的范围，以确保Cookie只在需要的上下文中被传递，从而提高安全性。

## 实践观察

```jsp
<%--
  Created by IntelliJ IDEA.
  User: 7878
  Date: 2023/12/27
  Time: 13:04
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
</head>
<body>
    <%
        Cookie mycookie = new Cookie("id", "1");
        mycookie.setMaxAge(60 * 60 * 24);
        mycookie.setPath("/");
        response.addCookie(mycookie);

        Cookie mycookie2 = new Cookie("password", "666");
        mycookie2.setMaxAge(60 * 60 * 24);
        mycookie2.setPath("/");
        response.addCookie(mycookie2);
    %>
    <a href=""
</body>
</html>
```

```jsp
<%--
  Created by IntelliJ IDEA.
  User: 7878
  Date: 2023/12/27
  Time: 13:07
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
</head>
<body>
<%
    Cookie[] cookies = request.getCookies();
    if (cookies != null) {
        for (Cookie cookie : cookies) {
%>
    <div><%= cookie.getName() %></div>
    <div><%= cookie.getValue() %></div>
<%
        }
    }
%>
</body>
</html>
```

观察方式

![image-20231227131608927](../images/image-20231227131608927.png)

![image-20231227131622311](../images/image-20231227131622311.png)

# session

在JSP中，可以使用`session`对象来管理用户的会话信息。`session`对象在整个用户会话期间保存数据，这意味着用户在不同的页面之间可以共享和保持状态。以下是一些常见的`session`的使用方法：

1. **存储数据到`session`中：**

   ```jsp
   <% 
       // 获取或创建一个session对象
       HttpSession session = request.getSession();
       
       // 存储数据到session中
       session.setAttribute("username", "john_doe");
   %>
   ```

   在上述代码中，`getSession`方法获取或创建与当前请求相关联的`session`对象，然后通过`setAttribute`方法将名为 "username" 的属性设置为 "john_doe"。

2. **从`session`中获取数据：**

   ```jsp
   <% 
       // 获取session对象
       HttpSession session = request.getSession();
       
       // 从session中获取数据
       String username = (String) session.getAttribute("username");
   %>
   ```

   上述代码从`session`中获取名为 "username" 的属性值，并将其存储在字符串变量 `username` 中。请注意，由于`session`中存储的是`Object`类型，因此需要进行类型转换。

3. **销毁`session`：**

   ```jsp
   <% 
       // 获取session对象
       HttpSession session = request.getSession();
       
       // 销毁session
       session.invalidate();
   %>
   ```

   上述代码调用`invalidate`方法销毁当前`session`，这将清除所有与`session`相关的数据。

4. **设置`session`的超时时间：**

   ```jsp
   <% 
       // 获取session对象
       HttpSession session = request.getSession();
       
       // 设置session的超时时间（以秒为单位，例如设置为30分钟）
       session.setMaxInactiveInterval(30 * 60);
   %>
   ```

   上述代码使用`setMaxInactiveInterval`方法设置`session`的超时时间，单位是秒。

## 实践

```jsp
<%--
  Created by IntelliJ IDEA.
  User: 7878
  Date: 2023/12/27
  Time: 13:51
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
</head>
<body>
<%
    HttpSession httpSession = request.getSession();
    httpSession.setAttribute("name", "iphan");
    httpSession.setMaxInactiveInterval(60 * 30);

%>
</body>
</html>
```

```jsp
<%--
  Created by IntelliJ IDEA.
  User: 7878
  Date: 2023/12/27
  Time: 13:52
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
</head>
<body>
<%
    HttpSession httpSession = request.getSession();
%>
<h1 style="color: green; background-color: red"><%= httpSession.getAttribute("name")%></h1>
<%

%>
</body>
</html>
```

![image-20231227135937464](../images/image-20231227135937464.png)

# 作用域

在JSP中，作用域（Scope）指的是变量的可见性和生存期，即变量在程序中的访问范围和存活时间。JSP定义了四个主要的作用域，它们是：

1. **Page（页面作用域）：**

   - 页面作用域是最短的作用域，变量在当前页面有效，不同页面之间的变量不互相影响。
   - 页面作用域的变量在页面的任何地方都可以访问。

   ```jsp
   <%@ page import="java.util.ArrayList" %>
   <% ArrayList<String> list = new ArrayList<>(); %>
   <% pageContext.setAttribute("pageList", list); %>
   ```

2. **Request（请求作用域）：**

   - 请求作用域在一次HTTP请求中有效，当请求被处理后，这个作用域中的变量将被销毁。
   - 不同的请求之间的变量不互相影响。

   ```jsp
   <%@ page import="java.util.HashMap" %>
   <% HashMap<String, Object> data = new HashMap<>(); %>
   <% request.setAttribute("requestData", data); %>
   ```

3. **Session（会话作用域）：**

   - 会话作用域在用户的整个会话期间有效，直到用户关闭浏览器或会话超时。
   - 不同用户之间的变量不互相影响。

   ```jsp
   <%@ page import="java.util.Date" %>
   <% Date loginTime = new Date(); %>
   <% session.setAttribute("loginTime", loginTime); %>
   ```

4. **Application（应用作用域）：**

   - 应用作用域在整个Web应用程序的生命周期中有效，直到服务器关闭或应用被卸载。
   - 在同一个应用程序中的不同页面之间共享变量。

   ```jsp
   <%@ page import="java.util.HashMap" %>
   <% HashMap<String, String> config = new HashMap<>(); %>
   <% application.setAttribute("appConfig", config); %>
   ```

这些作用域允许在不同的层次上存储和检索数据，使得在页面、请求、会话和应用程序级别上共享和保持状态成为可能。选择正确的作用域取决于变量的生命周期和需要在哪个级别上共享数据。

# JSTL

JSTL（JavaServer Pages Standard Tag Library）是一个用于简化JSP页面开发的标准标签库。它是在JSP规范中定义的一组标签和函数，旨在提供更简洁和可维护的JSP页面编写方式。JSTL的标签和函数可用于执行各种常见的任务，如条件判断、循环、格式化文本、访问集合等。

以下是JSTL提供的主要标签库：

1. **Core Tags (`<c:>`):** 提供用于控制流程、变量赋值、迭代和其他基本操作的标签。
   - 例如，`<c:if>`, `<c:forEach>`, `<c:set>`等。
2. **Formatting Tags (`<fmt:>`):** 提供格式化和本地化支持的标签，用于格式化日期、数字和消息。
   - 例如，`<fmt:formatDate>`, `<fmt:formatNumber>`, `<fmt:message>`等。
3. **SQL Tags (`<sql:>`):** 用于执行SQL查询的标签。这部分标签在现代的Java Web应用中并不常用，因为通常将数据库操作放在Java代码中。
   - 例如，`<sql:query>`, `<sql:update>`等。
4. **XML Tags (`<x:>`):** 提供在JSP中处理XML的标签。
   - 例如，`<x:parse>`, `<x:out>`, `<x:forEach>`等。

使用JSTL的优点包括：

- **简化代码：** JSTL标签库提供了一组高级抽象，可以用更简洁的标签替代一些繁琐的Java代码。
- **可读性：** JSTL标签可以使JSP页面更易读和维护，减少了在JSP中嵌入Java代码的需求。
- **模块化：** 可以将JSTL标签视为一种模块，通过在多个JSP页面中重用，提高了代码的可维护性。

为了使用JSTL，你需要在JSP页面的开头引入JSTL标签库的声明，例如：

```jsp
<%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c" %>
<%@ taglib uri="http://java.sun.com/jsp/jstl/fmt" prefix="fmt" %>
```

## 导入依赖

```xml
<dependency>
    <groupId>jakarta.servlet.jsp.jstl</groupId>
    <artifactId>jakarta.servlet.jsp.jstl-api</artifactId>
    <version>2.0.0</version>
    <scope>provided</scope>
</dependency>

<dependency>
    <groupId>org.glassfish.web</groupId>
    <artifactId>jakarta.servlet.jsp.jstl</artifactId>
    <version>2.0.0</version>
</dependency>
```

## 常用标签

JSTL Core标签库提供了一组用于控制流程、变量赋值、迭代和其他基本操作的标签。以下是JSTL Core标签库中一些常用的标签：

1. **`<c:out>`：** 用于在页面上输出数据，可以防范XSS攻击。

   ```jsp
   <c:out value="${variable}" />
   ```

2. **`<c:set>`：** 用于设置变量。

   ```jsp
   <c:set var="name" value="John" />
   <c:set var="name" value="${'aaa'}" />
   ```

3. **`<c:remove>`：** 用于删除指定的变量。

   ```jsp
   <c:remove var="name" />
   ```

4. **`<c:if>`：** 用于条件判断。没有else，条件取反就是else。

   ```jsp
   <c:if test="${condition}">
       <!-- 内容 -->
   </c:if>
   ```

5. **`<c:choose>`, `<c:when>`, `<c:otherwise>`：** 用于多分支条件判断。

   ```jsp
   <c:choose>
       <c:when test="${condition1}">
           <!-- 内容1 -->
       </c:when>
       <c:when test="${condition2}">
           <!-- 内容2 -->
       </c:when>
       <c:otherwise>
           <!-- 默认内容 -->
       </c:otherwise>
   </c:choose>
   ```

6. **`<c:forEach>`：** 用于循环遍历集合。

   ```jsp
   <c:forEach var="item" items="${collection}">
       <!-- 内容 -->
   </c:forEach>
   ```

7. **`<c:import>`：** 用于包含其他页面或资源。

   ```jsp
   <c:import url="path/to/resource.jsp" />
   ```

8. **`<c:url>`：** 用于构建URL。

   ```jsp
   <c:url value="/path/to/page.jsp" var="urlVar" />
   ```

9. **`<c:param>`：** 用于在URL中设置参数。

   ```jsp
   <c:param name="paramName" value="paramValue" />
   ```

10. **`<c:redirect>`：** 用于重定向到另一个URL。

    ```jsp
    <c:redirect url="newPage.jsp" />
    ```

# EL 表达式

EL（Expression Language，表达式语言）是一种用于在JavaEE平台上简化表达式的语言。在JSP页面中，EL 提供了一种简便的方式来访问 JavaBean 中的属性、调用方法、访问集合等。

以下是 EL 的一些基本特性和用法：

1. **变量引用：** 使用 `${}` 语法，可以引用变量的值。例如，`${name}` 可以引用名为 "name" 的变量的值。
2. **属性访问：** EL 允许通过点号 `.` 访问对象的属性。例如，`${user.name}` 可以访问名为 "user" 的对象的 "name" 属性。
3. **集合访问：** EL 支持对集合和数组的访问。例如，`${list[0]}` 可以获取列表的第一个元素。
4. **算术和逻辑运算：** EL 支持常见的算术和逻辑运算。例如，`${x + y}` 表示 x 和 y 的和。
5. **方法调用：** EL 支持调用对象的方法。例如，`${user.getName()}` 表示调用 "user" 对象的 "getName" 方法。
6. **条件运算符：** EL 提供了条件运算符（三元运算符）`?:`，用于简化条件判断。例如，`${score >= 60 ? 'Pass' : 'Fail'}` 表示如果分数大于等于60，则返回 "Pass"，否则返回 "Fail"。

为了保证EL表达式能够正常使用，需要在<%@page 标签里加上**isELIgnored="false"**

```jsp
<%--
  Created by IntelliJ IDEA.
  User: 7878
  Date: 2023/12/27
  Time: 14:21
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java"  %>
<%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c" %>
<%@ taglib uri="http://java.sun.com/jsp/jstl/fmt" prefix="fmt" %>
<html>
<head>
    <title>Title</title>
</head>
<body>
<%
    String name11 = "iphan";
//    我的java代码中也可以设置
    session.setAttribute("myname", name11);
%>
<%--jstl同样可以设置--%>
    <c:set  var="name" value="23" scope="session"/>
<%--采用jstl取出数据--%>
    <c:out value="${name}"/>
<%--采用EL表达式取出数据--%>
    <h1>${name}</h1>
    <h2>${myname}</h2>
<%
    System.out.println(name11);

%>

</body>
</html>

```

