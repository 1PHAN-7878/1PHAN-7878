---
title: 学习记录之Ajax
date: 2024-01-12 18:14:09
tags: 前端
---

# Ajax

AJAX（Asynchronous JavaScript and XML）是一种用于在网页上进行异步数据交换的技术。它通过在后台与服务器进行小规模的数据交换，使网页能够在不重新加载整个页面的情况下更新部分内容。AJAX 的核心是使用 JavaScript 在客户端发起异步请求，与服务器进行通信，并在不刷新整个页面的情况下更新部分内容。

主要特点和组成部分包括：

1. **异步性：** AJAX 允许在不阻塞用户界面的情况下发起请求。这使得用户可以继续与页面交互，而不必等待请求的完成。
2. **数据交换格式：** 初始时，XML（eXtensible Markup Language）被广泛用作 AJAX 数据的交换格式。然而，随着 JSON（JavaScript Object Notation）的普及，现代的 AJAX 应用通常更倾向于使用 JSON 作为数据格式，因为它更轻量且易于处理。
3. **DOM 操作：** 通过获取服务器返回的数据，JavaScript 可以使用 DOM（Document Object Model）操作来更新页面的特定部分，而无需重新加载整个页面。
4. **XMLHttpRequest 对象：** AJAX 请求通常使用 XMLHttpRequest 对象来实现。这个对象允许 JavaScript 代码向服务器发送请求，然后处理服务器返回的数据。

AJAX 的出现使得 web 应用程序能够更加动态地更新内容，提高了用户体验。典型的应用包括在表单提交时进行验证、实时搜索建议、动态加载数据等。虽然最初的名字是 "Asynchronous JavaScript and XML"，但现在 AJAX 已经成为一种更为通用的技术，不仅限于使用 XML，而是可以使用多种数据格式。

# XMLHttpRequest

`XMLHttpRequest` 是一个在 JavaScript 中用于发起 HTTP 请求的 API。它是 AJAX 技术的核心组成部分，允许在不重新加载整个页面的情况下，通过异步方式与服务器进行通信。`XMLHttpRequest` 对象允许网页中的 JavaScript 代码向服务器发送请求，获取数据，然后在不刷新整个页面的情况下更新页面的内容。

主要的方法和属性包括：

1. **`open(method, url, async)`：** 用于指定请求的类型、URL 和是否异步处理请求。`method` 表示 HTTP 请求方法（例如 "GET" 或 "POST"），`url` 表示请求的目标 URL，`async` 表示是否异步处理请求。
2. **`send(data)`：** 发送 HTTP 请求。可以通过参数 `data` 向服务器发送数据，例如在 POST 请求中发送表单数据。
3. **`setRequestHeader(header, value)`：** 设置 HTTP 请求的头部。可以在发送请求之前使用该方法设置请求头，例如设置 Content-Type。
4. **`onreadystatechange`：** 一个事件处理程序，在 `XMLHttpRequest` 对象的 `readyState` 属性改变时被触发。`readyState` 表示请求的状态，而 `onreadystatechange` 允许开发者在请求不同阶段执行相应的操作。
5. **`responseText` 和 `responseXML`：** 分别包含服务器响应的文本和 XML 数据。根据服务器响应的内容类型，你可以选择使用其中的一个。

以下是一个简单的使用 `XMLHttpRequest` 的例子：

```JavaScript
var xhr = new XMLHttpRequest();
xhr.open("GET", "https://example.com/data", true);	
xhr.onreadystatechange = function() {
  if (xhr.readyState == 4 && xhr.status == 200) {
    console.log(xhr.responseText);
  }
};
xhr.send();
```

这个例子创建了一个 `XMLHttpRequest` 对象，使用 `open` 方法指定了请求的类型、URL 和异步处理方式，设置了 `onreadystatechange` 事件处理程序来处理请求的不同阶段，最后使用 `send` 方法发送了请求。当请求完成后，如果响应的状态码为 200，那么响应的文本内容将被输出到控制台。

# 响应

## 服务器响应属性

| 属性         | 描述                        |
| :----------- | :-------------------------- |
| responseText | 获取字符串形式的响应数据    |
| responseXML  | 获取 XML 数据形式的响应数据 |

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
</head>
<body>
<div id="d">这是一段文字</div>
<button onclick="f1()">按钮</button>
<script>
  function f1(){
    var xhr = new XMLHttpRequest();
    xhr.onreadystatechange = function(){
      if(xhr.readyState == 4 && xhr.status == 200){
        console.log(200);
        document.getElementById("d").innerText = this.responseText;
      }
    }

    xhr.open("GET", "a.txt", true);
    xhr.send();

  }
</script>
</body>
</html>


```

# 好处

使用异步判断用户名的好处在于提高用户体验和页面响应速度。当用户在输入框中输入用户名时，异步地发送请求来检查用户名的有效性，而无需等待整个页面重新加载或等待同步的后端响应。这带来了一些优势：

1. **实时反馈：** 用户可以实时地看到他们输入的用户名是否有效，而无需等待整个表单的提交。这提供了更快的反馈，增加了用户体验。
2. **减轻服务器负担：** 异步验证使得只有在必要时才向服务器发出请求，而不是每次用户键入字符都发送一次请求。这减轻了服务器的负担，特别是在具有大量用户的系统中。
3. **避免页面刷新：** 异步验证避免了每次验证都重新加载整个页面的需求。这使得用户可以保持当前页面状态，而无需中断他们的工作。
4. **减少网络流量：** 只发送用户名而不是整个表单的数据可以减少传输的数据量，减少了网络流量。

在没有 AJAX 技术的早期，人们通常采用传统的同步方式来处理用户名判断问题。以下是一些可能的方法：

1. **表单提交后端验证：** 用户填写完整个表单并点击提交按钮后，整个表单数据将被提交到后端。后端服务器验证用户名的唯一性，然后返回验证结果。这种方式要求用户提交整个表单，可能会导致用户等待时间较长，尤其是在网络速度较慢的情况下。
2. **页面刷新：** 用户填写完用户名后，可能需要点击一个特殊的按钮或者离开输入框（失去焦点），页面会刷新并显示用户名的验证结果。这种方式会导致用户体验较差，因为页面的刷新可能会中断用户当前的操作。

# 一个例子

后端检查用户名是否合法

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script src="https://cdn.bootcdn.net/ajax/libs/jquery/3.7.1/jquery.min.js"></script>
    <style>
        #userok{
            display: none;
        }
    </style>
</head>
<body>
<input type="text" name="username" id="username">
<span id="userok">初始</span>
<script>
    $(function(){
        $("#username").keyup(
            function(){
                //这里要写上主机名，端口，上下文，花费好长时间找。
                var rootPath = window.location.origin + window.location.pathname;
                var urlToCheckName = rootPath + "checkname.jsp";
                console.log("URL to CheckName:", urlToCheckName);

                $.post({
                    url: urlToCheckName,
                    method: "post",
                    data: {"username": $(this).val()},
                    success: function(resp){
                        if("ok" === resp){
                            $("#userok").css("display", "inline");
                            $("#userok").css("color", "green");
                            $("#userok").text(resp);
                        }
                        else{
                            $("userok").css("display", "inline");
                            $("#userok").css("color", "red");
                            $("#userok").text("no");
                        }

                    },
                    //也就是说这里是返回响应不是200才使用的， 而不是不符合标准使用的。
                    error: function() {
                        $("#userok").css("display", "inline");
                        $("#userok").css("color", "red");
                        $("#userok").text = "no";
                    }
                });
            }
        );
    })
</script>
</body>
</html>
```

```java
package com.example.demo11;

import jakarta.servlet.ServletException;
import jakarta.servlet.http.HttpServlet;
import jakarta.servlet.http.HttpServletRequest;
import jakarta.servlet.http.HttpServletResponse;

import java.io.IOException;

public class CheckNameServlet extends HttpServlet
{
    @Override
    protected void service(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        resp.setContentType("text/plain");
        resp.setCharacterEncoding("UTF-8");
        if("aaa".equals(req.getParameter("username"))){
            resp.getWriter().print("ok");

        }else{
            resp.getWriter().print("no");
        }
    }

//    @Override
//    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
//        resp.setContentType("text/plain");
//        resp.setCharacterEncoding("UTF-8");
//        if(req.getParameter("username").equals("aaa")){
//            resp.getWriter().print("不彳亍！");
//
//        }else{
//            resp.getWriter().print("这个彳亍！");
//    }
//}

}
```

```xml
<servlet>
    <servlet-name>CheckNameServlet</servlet-name>
    <servlet-class>com.example.demo11.CheckNameServlet</servlet-class>
</servlet>

<servlet-mapping>
    <servlet-name>CheckNameServlet</servlet-name>
    <url-pattern>/checkname.jsp</url-pattern>
</servlet-mapping>
```

```jsp
<%--
  Created by IntelliJ IDEA.
  User: 7878
  Date: 2024/1/12
  Time: 19:27
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
</head>
<body>
    <h1>哈哈哈</h1>
<script>
    alert("出现了");
</script>
</body>
</html>
```
