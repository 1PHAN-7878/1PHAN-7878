---
title: 学习记录之Servlet
date: 2023-12-20 19:36:59
tags: java
---

# Servlet

# 2 第一个尝试

在webapp的包里创建一个html，设置好post请求以便于触发servlet。

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
    <form action="myweb" method="post">
        <div>
            <span>姓名:</span>
            <input name="name">

        </div>
        <div>
            <span>密码:</span>
            <input name="password">
        </div>
        <button type="submit">提交</button>
    </form>

</body>
</html>
```

在src/main/java/com/example/demo1这个目录下创建myweb.java实现doPost请求

```java
package com.example.demo1;

import com.sun.nio.sctp.AbstractNotificationHandler;
import jakarta.servlet.ServletException;
import jakarta.servlet.http.HttpServlet;
import jakarta.servlet.http.HttpServletRequest;
import jakarta.servlet.http.HttpServletResponse;

import java.io.IOException;

public class myweb extends HttpServlet {
    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //super.doPost(req, resp);
        String name = req.getParameter("name");
        String password = req.getParameter("password");
        System.out.println(name);
        System.out.println(password);
    }
}

```

在webapp下的WEB-INF中的web.xml配置好关联信息

```xml
		<servlet>
            <servlet-name>myweb</servlet-name>
            <servlet-class>com.example.demo1.myweb</servlet-class>
        </servlet>

        <servlet-mapping>
            <servlet-name>myweb</servlet-name>
            <url-pattern>/myweb</url-pattern>
        </servlet-mapping>

        <welcome-file-list>
            <welcome-file>myweb.html</welcome-file>
        </welcome-file-list>
```

==servlet-class在这里是全限定名==

启动tomcat之后可以观察到运行效果。

![image-20231220200342786](../images/image-20231220200342786.png)

证明我的post请求已经获取到了，开始进一步的学习。
