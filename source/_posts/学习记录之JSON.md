---
title: 学习记录之JSON
date: 2023-12-18 10:16:56
tags: 前端
---

# 什么是JSON

JSON（JavaScript Object Notation）是一种轻量级的数据交换格式，它基于JavaScript的对象字面量语法。JSON格式易于阅读和编写，并且也易于机器解析和生成。它常用于客户端和服务器之间的数据传输。

JSON的基本数据结构包括对象（键值对集合）、数组（值的有序列表）、字符串、数字、布尔值和空值。它与JavaScript对象字面量的语法非常相似，但是它是一种独立于编程语言的数据格式，因此可以被多种语言解析和生成。

JSON常用于Web开发中，例如在将数据从服务器传输到客户端或在不同系统之间交换数据时。 JSON格式的数据易于处理和解析，因此在各种应用程序中广泛使用。

```xml
//1.Maven中导入alibaba的fastjson
<dependency>
            <groupId>com.alibaba</groupId>
            <artifactId>fastjson</artifactId>
            <version>1.2.62</version>
</dependency>
//2.在类中导入
import com.alibaba.fastjson.JSON;
//3.将list转化为json格式
String json = JSON.toJSONString(result);
```

# 使用

1. 使用 `JSON.parse()` 方法将 JSON 字符串转换为 JavaScript 对象：

```JavaScript
var jsonString = '{"name":"John", "age":30, "city":"New York"}';
var obj = JSON.parse(jsonString);
console.log(obj.name); // 输出 "John"
```

2. 使用 `JSON.stringify()` 方法将 JavaScript 对象转换为 JSON 字符串：

```JavaScript
var obj = { name: "John", age: 30, city: "New York" };
var jsonString = JSON.stringify(obj);
console.log(jsonString); // 输出 '{"name":"John","age":30,"city":"New York"}'
```

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <script>
        var json = {"name":"彳亍", "id":"1"};
        console.log(json.name);
        console.log(json.id);
        console.log(json);
        
    </script>
</body>
</html>
```

![image-20231218102607816](../images/image-20231218102607816.png)
