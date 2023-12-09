---
title: 学习记录之JavaScript
date: 2023-12-09 22:19:49
tags: 前端
---

学习记录：~

# 语言基础

## 1.1 输出

```javascript
<script>
  document.write("Hello Javascript");
</script>
```



## 1.2 位置

javascript代码必须放在script标签中

script标签可以放在html的任何地方，一般建议放在head标签里

```javascript
<html>
  <script src="https://how2j.cn/study/hello.js"></script>
</html>
```

## 1.3 注释

类似c/c++，

```javascript
<script>
    //单行注释
    /*
    	多行注释
    */
  document.write("Hello Javascript");
</script>
```

## 1.4 变量

使用或不适用var声明

```javascript
<script>
  var x = 10;
  document.write("变量x的值:"+x);
</script>
```

## 1.5 基本数据类型

undefined,Boolean,Number,String,null

var是动态类型

类型判断`typeof x`

## 1.6 类型转换

Number，Boolean，String都有toString方法，转化为字符串。

转化为数字parseInt，parseFloat

转化为布尔，Boolean();

## 1.7 函数

```javascript
function print(){
    document.write("这是函数的输出");
}
print();
```

```javascript
function printmessage(message){
	document.write(message + "<br>");
}
printmessage(1);
printmessage(2);
```

## 1.8 练习1

![image-20231209161803653](E:/hexo/1PHAN-7878.github.io/source/images/image-20231209161803653.png)

```html
	<input id="num1" type="text">
     + 
    <input id="num2" type="text">
     =  
    <input id="result" type="text">

    <button id="button" onclick="f1()">计算</button>
    <script>
        function f1(){
            var value1 = parseInt(document.getElementById("num1").value);
            var value2 = parseInt(document.getElementById("num2").value);
            var result = value1 + value2;
            document.getElementById("result").value = result;

        }
    </script>
```

## 1.9 事件

鼠标点击事件

```html
<script>
    function show(){
       alert("Hello");
}
</script>
 
<button onclick="show()">点击一下</button>
```

## 1.10 运算符

仅有== 与 === 不相同

==仅仅判断值是否相同

===还要判断类型

# 对象

## 2.1 数字对象

```html
	<script>
        var x = new Number(111);
        document.write(x + "<br>");     //111
        document.write(typeof x);       //Object
        var y = 10;
        document.write(typeof y);       //number
    </script>	
```

最大最小值 `Number.MIN_VALUE Number.MAX_VALUE`

判断是不是数字对象`isNaN()`

返回x位小数`.toFixed(3)`

返回科学计数法`.toExponential()`

## 练习

![image-20231209200016752](E:/hexo/1PHAN-7878.github.io/source/images/image-20231209200016752.png)

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <input type="number" id="x"></input>
     * 
    <input type="number" id="y"></input>
     = 
    <input type="text" name="" id="ans"></input>
    <button onclick="f1()">计算</button>
    <script>
        function f1(){
            var x = document.getElementById("x").value;
            var y = document.getElementById("y").value;
            document.getElementById("ans").value = Number(x * y).toExponential().toString();

        }
    </script>
</body>
</html>
```

## 2.2 字符串对象

```html
	<script>
        var str = new String("333");
        document.write(str + 
        "<br>");

    </script>
```

长度.length

获取指定位置的字符``.charAt()``

拼接``.concat()``

第一次出现的位置``.indexOf()``

是否相同``.localeCompare()``

截取一段子字符串``.substring(a, b);``左闭右开

通过分隔符分离``.split(" ", 2); `第二个参数可选表示保留几个

替换``.replace(search, replacement);``

## 练习

![image-20231209204127173](E:/hexo/1PHAN-7878.github.io/source/images/image-20231209204127173.png)

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <h1>字符串替换工具</h1>
    <div>
        <p>源字符串：</p>
        <input type="text" id="init">
    </div>
    <div>
        <p>查询：</p>
        <input type="text" id="search">
    </div>
    <div>
        <p>替换为：</p>
        <input type="text" id="replacement">

    </div>
    <div>
        <p>替换结果</p>
        <input type="text" id="result">
    </div>
    <button id="button" onclick="f1()">替换</button>
    <script>
        function f1(){
            var str = new String(document.getElementById("init").value);
            var search = new String(document.getElementById("search").value);
            var replacement = new String(document.getElementById("replacement").value);
            while(str.indexOf(search) != -1){
                //JavaScript 的 replace 方法不会修改原始字符串，而是返回一个新的字符串。
                //str.replace(search, replacement);
                str = str.replace(search, replacement);
            }
            document.getElementById("result").value = str;
        }
    </script>
</body>
</html>
```

## 2.3 数组

```JavaScript
创建数组：
// 使用数组字面量创建数组
var fruits = ["Apple", "Banana", "Orange"];

// 使用构造函数创建数组
var numbers = new Array(1, 2, 3, 4, 5);
```

类似数组访问`numbers[0]`

数组长度`.length`

末尾操作`.push(), .pop()`

开头操作`.shift(), .unshift()`

删除`.splice(a,b)`	从a,删除b个元素

返回子数组`slice(a, b)` 返回子数组[a, b)

排序`.sort()` 

采用自定义的排序，需要使用自定义函数

```javascript
var a = new Array(1, 2, 8, 4, 5, 7);
//a[0];
document.write(a[2]);
function cmp(v1, v2){
	return v2 - v1;
}
a.sort(cmp);
```

翻转 `.reverse()`



## 练习

![image-20231209205901219](E:/hexo/1PHAN-7878.github.io/source/images/image-20231209205901219.png)

```html
	<script>
        var a = new Array(1,3,4,5,7,4,5,6,7,7);
        a.sort();
        var b =  new Array();
        for(var i = 0; i < a.length; i++){
            if(i == 0){
                b.push(a[i]);
            }else{
                if(a[i] != a[i-1]) b.push(a[i]);
            }
        }
        document.write(b);
    </script>
```

![image-20231209210523827](E:/hexo/1PHAN-7878.github.io/source/images/image-20231209210523827.png)

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <!-- <script>
        var a = new Array(1,3,4,5,7,4,5,6,7,7);
        a.sort();
        var b =  new Array();
        for(var i = 0; i < a.length; i++){
            if(i == 0){
                b.push(a[i]);
            }else{
                if(a[i] != a[i-1]) b.push(a[i]);
            }
        }
        document.write(b);
    </script> -->
    <p>输入一段英文字符串</p>
    <input type="text" id="init">
    <p>正向排列</p>
    <input type="text" id="zheng">
    <p>反向排列</p>
    <input type="text" id="fanxiang">
    <button id="zimu" onclick="f1()">按字母</button>
    <button id="zifu" onclick="f2()">按字符</button>
    <script>
        //手搓
        function f1(){
            var str = document.getElementById("init").value;
            var strArr = new Array();
            for(var i = 0; i <str.length; i++){
                strArr.push(str[i]);
            }
            strArr.sort();
            var strZheng = new String();
            for(var i = 0; i < strArr.length; i++){
                strZheng += strArr[i];
            }
            document.getElementById("zheng").value = strZheng;
            strArr.reverse();
            var strFanxiang = new String();
            strArr.forEach(function (char) {
                strFanxiang += char;
            })
            document.getElementById("fanxiang").value = strFanxiang;

        }


        //改进
        function f2(){
            var str = new String(document.getElementById("init").value);
            var strArr = str.split(' ');
            strArr.sort();
            var strZheng = strArr.join(' ');
            document.getElementById("zheng").value = strZheng;
            strArr.reverse();
            var strFanxiang = strArr.join(' ');
            document.getElementById("fanxiang").value = strFanxiang;
        }
    </script>
</body>
</html>
```

## 2.4 时间

### 创建一个 Date 对象

```JavaScript
// 创建一个表示当前日期和时间的 Date 对象
var currentDate = new Date();

// 创建一个表示特定日期和时间的 Date 对象（年、月、日、时、分、秒）
var specificDate = new Date(2023, 0, 1, 12, 0, 0); // 月份从0开始，0 表示一月
```

### 获取日期和时间的各个部分

```javascript
var year = currentDate.getFullYear(); // 年份
var month = currentDate.getMonth(); // 月份（0 到 11）
var day = currentDate.getDate(); // 日期
var hours = currentDate.getHours(); // 小时
var minutes = currentDate.getMinutes(); // 分钟
var seconds = currentDate.getSeconds(); // 秒钟
var milliseconds = currentDate.getMilliseconds(); // 毫秒
```

### 设置日期和时间的各个部分

```JavaScript
currentDate.setFullYear(2023);
currentDate.setMonth(5); // 月份从0开始，5 表示六月
currentDate.setDate(15);
currentDate.setHours(18);
currentDate.setMinutes(30);
currentDate.setSeconds(45);
currentDate.setMilliseconds(500);
```

### 格式化日期和时间字符串

```JavaScript
var formattedDate = currentDate.toDateString(); // 格式化为日期字符串
var formattedTime = currentDate.toTimeString(); // 格式化为时间字符串
var formattedDateTime = currentDate.toLocaleString(); // 格式化为日期和时间字符串
```

### 获取时间戳

```JavaScript
var timestamp = currentDate.getTime(); // 获取表示当前时间的时间戳（毫秒数）
```

## 练习

![image-20231209220145733](E:/hexo/1PHAN-7878.github.io/source/images/image-20231209220145733.png)

本来要照着做，结果发现这个日期判断跟算法题似的。

就做了个框架，但是这个里面也有可以学习到的知识。

```html
<div>
        <span>选择出生年份：</span>
        <select name="year" id="year">
            <script type="text/javascript">
                var a, s = "";
                for(a = 1960; a < 2023; a++){
                    if(a == 2000){
                        s = s + "<option selected="+ "selected" + ">" + a + "</option><br>"
                    }else{
                        s = s + "<option>" + a + "</option><br>";
                    }
                }
                document.write(s);
            </script>
        </select>
        <br>
        <span>选择出生月份：</span>
        <select name="month" id="month">
            <script>
                for(var i = 1; i <= 12; i++){
                    document.write(`<option>${i}</option>`);
                }
            </script>
        </select>
        <br>
        <span>请选择出生日：</span>
        <select name="day" id="day">
            <script>
                for(var i = 1; i <= 31; i++){
                    document.write(`<option${i === 15 ? " selected" : ""}>${i}</option>`);
                }
            </script>
        </select>
    </div>
```

