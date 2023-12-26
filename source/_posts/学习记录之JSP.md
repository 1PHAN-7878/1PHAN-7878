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
