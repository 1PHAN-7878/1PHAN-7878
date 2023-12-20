---
title: 学习记录之DOM
date: 2023-12-10 10:36:04
tags: 前端
---

# 节点

在 DOM（文档对象模型）中，节点（Node）是文档结构的基本构建块。DOM 是一种树状结构，它表示网页的层次结构，其中每个元素、属性、文本等都被表示为一个节点。节点之间的关系形成了整个文档的结构。

DOM 中的节点主要分为三类：元素节点、文本节点和属性节点。以下是它们的简要解释：

1. **元素节点（Element Node）：** 表示 HTML 元素，如 `<div>`、`<p>`、`<a>` 等。元素节点可以包含其他节点，形成嵌套关系。一个 HTML 文档就是由元素节点组成的树状结构。
2. **文本节点（Text Node）：** 表示 HTML 元素中的文本内容。文本节点是元素节点的子节点，它们不包含其他节点。例如，`<p>这是一个文本节点</p>` 中的 "这是一个文本节点" 就是一个文本节点。==`childNodes[0]` 返回一个元素的第一个子节点。这个子节点可以是元素节点、文本节点、注释节点等等。==
3. **属性节点（Attribute Node）：** 表示 HTML 元素的属性。每个元素可以有零个或多个属性，每个属性都是属性节点。例如，`<a href="https://www.example.com">` 中的 `href` 就是一个属性节点。==`attributes` 返回的是一个包含元素节点的所有属性的 `NamedNodeMap` 对象==

节点在 DOM 中的位置关系形成了父子关系、兄弟关系等。DOM 提供了许多用于访问、操作和修改节点的方法和属性，例如 `getElementById`、`appendChild`、`removeChild` 等。

示例：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>DOM Node Example</title>
</head>
<body>
    <div id="parent">
        <p>This is a text node.</p>
        <a href="https://www.example.com">Link</a>
    </div>

    <script>
        // 获取父节点
        var parent = document.getElementById("parent");

        // 获取子节点列表
        var childNodes = parent.childNodes;
        console.log(childNodes);

        // 获取第一个子节点（文本节点）
        var firstChild = parent.firstChild;
        console.log(firstChild);
        
		// 获取属性节点
        var attributesList = parent.attributes;
        console.log('Attributes List:', attributesList);
        
        // 获取第一个元素子节点
        var firstElementChild = parent.firstElementChild;
        console.log(firstElementChild);
    </script>
</body>
</html>
```

在这个例子中，`<div>` 元素是一个父节点，它包含了一个文本节点（`<p>` 元素内的文本）和一个元素节点（`<a>` 元素）。节点之间的关系在 JavaScript 中可以通过 DOM API 进行访问和操作。

想象一本大大的故事书，这本书里有很多有趣的故事。在这本书中，每个小故事都是一个节点。这些节点可以是主要的故事（就像一张大图片），也可以是小细节（就像书中的文字或一些插图）。

1. **元素节点（Element Node）：** 想象一张大图片，这就是一个元素节点。比如，有一张大大的彩虹图片，这就是一个元素节点。而且，这张图片下面还可以有小图片或者文字，它们都是这个元素节点的一部分。
2. **文本节点（Text Node）：** 想象你看到的一些文字，比如书中的文字描述。这些文字就是文本节点。例如，书中可能有一句话说：“一天，小猫在阳光下玩耍。”，这句话就是一个文本节点。
3. **属性节点（Attribute Node）：** 想象你看到的一些标签上的特殊说明，就像书中的小注释。这些小注释是属性节点。比如，有一个链接，链接上写着 `href="https://www.example.com"`，这里的 `href` 就是一个属性节点。

节点之间就像书中的章节、段落、文字一样，它们组合在一起构成了整个故事。而在 JavaScript 中，我们可以使用一些代码来找到这些节点，就像你可以用手指指向书中的一些部分一样。这样，我们就可以对这些节点进行操作，就像你可以选择读哪一页的故事一样。

# 获取节点

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>DOM Node Examples</title>
</head>
<body>
    <div id="myDiv" class="container">
        <p class="paragraph">This is a paragraph.</p>
        <ul>
            <li>Item 1</li>
            <li>Item 2</li>
            <li>Item 3</li>
        </ul>
    </div>

    <script>
        // 通过ID获取单个节点
        var divElement = document.getElementById('myDiv');
        console.log(divElement);

        // 通过类名获取节点列表
        var paragraphElements = document.getElementsByClassName('paragraph');
        console.log(paragraphElements);

        // 通过标签名获取节点列表
        var listItems = document.getElementsByTagName('li');
        console.log(listItems);

        // 通过选择器获取单个节点
        var firstParagraph = document.querySelector('p');
        console.log(firstParagraph);

        // 通过选择器获取节点列表
        var allParagraphs = document.querySelectorAll('p');
        console.log(allParagraphs);
    </script>
</body>
</html>

```

# 节点属性

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>DOM Node Properties</title>
</head>
<body>
    <div id="myElement" class="example-class">
        <p id="myChild">This is a paragraph.</p>
    </div>
    <p id="myText">Hello, World!</p>

    <script>
        // 节点类型属性
        var elementType = document.getElementById('myElement').nodeType;
        console.log('Node Type:', elementType);

        // 节点内容属性
        var textContent = document.getElementById('myText').nodeValue;
        console.log('Node Value (Text):', textContent);

        var elementText = document.getElementById('myElement').textContent;
        console.log('Text Content:', elementText);

        var elementHTML = document.getElementById('myElement').innerHTML;
        console.log('Inner HTML:', elementHTML);

        // 节点关系属性
        var parentElement = document.getElementById('myChild').parentNode;
        console.log('Parent Node:', parentElement);

        var childNodes = document.getElementById('myElement').childNodes;
        console.log('Child Nodes:', childNodes);

        var firstChild = document.getElementById('myElement').firstChild;
        var lastChild = document.getElementById('myElement').lastChild;
        console.log('First Child:', firstChild);
        console.log('Last Child:', lastChild);

        // 节点属性
        var elementId = document.getElementById('myElement').id;
        var elementClassName = document.getElementById('myElement').className;
        console.log('Element ID:', elementId);
        console.log('Element Class Name:', elementClassName);

        var attributesList = document.getElementById('myElement').attributes;
        console.log('Attributes:', attributesList);
    </script>
</body>
</html>

```

![image-20231210105858848](../images/image-20231210105858848.png)

```javascript
function changeDiv1(){
  document.getElementById("d1").childNodes[0].nodeValue= "通过childNode[0].value改变内容";
}
function changeDiv2(){
  document.getElementById("d1").innerHTML= "通过innerHTML改变内容";
}
```

## 练习1

![image-20231210111908530](../images/image-20231210111908530.png)

```html
	<input type="text" id="id" value="324">
    <button id="button" onclick="f1()">提交</button>
    <script>
        function f1(){
            var node = document.getElementById("id");
            console.log(node.value);
            var str = new String(node.value);
            if(str[0] == 'A' || str[0] == 'Z' || str[str.length - 1] == 'A' || str[str.length - 1] == 'Z'){
                alert("账号已经存在了！");
            }else{
                alert("注册成功");
            }
        }
    </script>
```

## 练习二

![image-20231212103816156](../images/image-20231212103816156.png)

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <button id="pic1" onclick="f1()">这个是图片1</button>
    <button id="pic2" onclick="f2()">这个是图片2</button>
    <img src="./pic1.png" alt="图片一" width="300px" height="300px" id="pic">
    <script>
        function f1(){
            img1 = document.getElementById("pic");
            img1.src = "./pic1.png";
        }
        function f2(){
            img2 = document.getElementById("pic");
            img2.src = "./pic2.png";
        }
    </script>
</body>
</html>
```

# 样式

1. **直接修改样式属性：**

   ```JavaScript
   // 获取元素
   var myElement = document.getElementById("myElement");
   
   // 直接修改样式属性
   myElement.style.color = "red";
   myElement.style.fontSize = "16px";
   ```

2. **使用`setProperty`方法：**

   ```JavaScript
   // 获取元素
   var myElement = document.getElementById("myElement");
   
   // 使用 setProperty 方法设置样式属性
   myElement.style.setProperty("color", "blue");
   ```

3. **通过`cssText`属性设置多个样式：**

   ```JavaScript
   // 获取元素
   var myElement = document.getElementById("myElement");
   
   // 使用 cssText 属性设置多个样式
   myElement.style.cssText = "color: green; font-size: 18px;";
   ```

4. **动态添加和移除CSS类：**

   ```JavaScript
   // 获取元素
   var myElement = document.getElementById("myElement");
   
   // 添加CSS类
   myElement.classList.add("newClass");
   
   // 移除CSS类
   myElement.classList.remove("oldClass");
   ```

## 练习三

![image-20231212110251773](../images/image-20231212110251773.png)

![image-20231212110241198](../images/image-20231212110241198.png)

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <table id="table">
        <tr style="background-color: blue;" class="tr1">
            
            <td>id</td>
            <td>姓名</td>
            <td>血量</td>
            <td>伤害</td>
        </tr>
        <tr class="tr2">
            <td>1</td>
            <td>gareen</td>
            <td>300</td>
            <td>5</td>
        </tr>
        <tr class="tr1">
            <td>2</td>
            <td>teemo</td>
            <td>200</td>
            <td>10</td>
        </tr>
        <tr class="tr2">
            <td>3</td>
            <td>teemo</td>
            <td>100</td>
            <td>15</td>
        </tr>
    </table>
    <script>
        var table = document.getElementById("table");
        console.log(document.childNodes);
        
        var tr1 = document.getElementsByClassName("tr1");
        tr1 = Array.from(tr1);
        tr1.forEach(function(element) {
            element.style.cssText = "background-color: blue;";
        });
        
        var tr2 = document.getElementsByClassName("tr2");
        tr2 = Array.from(tr2);
        tr2.forEach(function(element) {
            element.style.cssText = "background-color: green;";
        });
    </script>
</body>
</html>
```

![image-20231212110919351](../images/image-20231212110919351.png)

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <table id="table" style="border-collapse: collapse;
    align-content: center;">
        <tr style="background-color: blue;" class="tr1">
            
            <td>id</td>
            <td>姓名</td>
            <td>血量</td>
            <td>伤害</td>
        </tr>
        <tr class="tr2">
            <td>1</td>
            <td>gareen</td>
            <td>300</td>
            <td>5</td>
        </tr>
        <tr class="tr1">
            <td>2</td>
            <td>teemo</td>
            <td>200</td>
            <td>10</td>
        </tr>
        <tr class="tr2">
            <td>3</td>
            <td>teemo</td>
            <td>100</td>
            <td>15</td>
        </tr>
    </table>
    <script>
        var tag = document.getElementsByTagName("tr");
        for(var i = 0; i < tag.length; i+=2){
            tag[i].style.backgroundColor = "gray";
        }
    </script>
</body>
</html>
```

# 事件

DOM（文档对象模型）中有许多事件，它们是与 HTML 元素相关联的行为或状态的表示。以下是一些常用的 DOM 事件：

1. **点击事件（click）：** 当用户点击某个元素时触发。
2. **鼠标移入事件（mouseover）：** 当鼠标指针移动到某个元素上方时触发。
3. **鼠标移出事件（mouseout）：** 当鼠标指针从某个元素移开时触发。
4. **双击事件（dblclick）：** 当用户双击某个元素时触发。
5. **键盘按下事件（keydown）：** 当用户按下键盘上的任意键时触发。
6. **键盘释放事件（keyup）：** 当用户释放键盘上的按键时触发。
7. **表单提交事件（submit）：** 当用户提交表单时触发。
8. **输入框失去焦点事件（blur）：** 当元素失去焦点时触发。
9. **输入框获得焦点事件（focus）：** 当元素获得焦点时触发。
10. **输入框内容改变**：记得表单中元素，使用value属性获取。
11. **窗口加载事件（load）：** 当页面加载完成时触发。
12. **窗口改变大小事件（resize）：** 当窗口大小改变时触发。
13. **滚动事件（scroll）：** 当用户滚动页面时触发。
14. **鼠标按下事件（mousedown）：** 当鼠标按钮被按下时触发。
15. **鼠标释放事件（mouseup）：** 当鼠标按钮被释放时触发。
16. **鼠标移动事件（mousemove）：** 当鼠标指针在元素上移动时触发。

## 练习

![image-20231212111852358](../images/image-20231212111852358.png)

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<style>
    
div{
    display: none;
}
 a{
    display: none;
    /* display: block; */
    font-size: 14px;
    font-family: 宋体;
    color: gray;
    text-decoration: none;   
    padding: 10px 0px 10px 0px;
}
</style>
<body>
    <span id="sp1" onmouseover="dips('menu1')" onmouseleave="disappare('menu1')">武器</span>
    <span id="sp2" onmouseover="dips('menu2')" onmouseleave="disappare('menu2')">护甲</span>
    <span id="sp3" onmouseover="dips('menu3')" onmouseleave="disappare('menu3')">英雄</span>
    <div id="menu1">
        <a href="">大剑</a>
        <a href="">斧子</a>
        <a href="">牛魔</a>
    </div>
    <div id="menu2">
        <a href="">胸甲</a>
        <a href="">护腕</a>
        <a href="">头盔</a>
    </div>
    <div id="menu3">
        <a href="">盖伦</a>
        <a href="">提莫</a>
        <a href="">果汁</a>
    </div>
    <script>
        function dips(name = "menu1"){
            var menu = document.getElementById(name);
            menu.style.display = "block";
    
            console.log(menu.childElementCount);
            Array.from(menu.children).forEach(function(element){
                element.style.display = "block";
            });
        }
        function disappare(name = 'menu1'){
            var menu = document.getElementById(name);
            menu.style.display = "none";
    
            console.log(menu.childElementCount);
            Array.from(menu.children).forEach(function(element){
                element.style.display = "none";
            });
        }
        
    </script>
</body>
</html>
```

![image-20231214162822952](../images/image-20231214162822952.png)

```html
<!DOCTYPE html>
<html lang="zh-CN">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        .ok {
            color: green;
            display: none;
            font-size: 20px;
        }

        .nook {
            color: red;
            display: none;
            font-size: 20px;
        }

        #username {
            display: inline-block;
        }
    </style>
</head>

<body>
    <div>

        <input type="text" name="username" id="username" width="200px" oninput="f1()" onblur="f2()">
    </div>
    
        <span class="ok">用户名可以使用</span>
        <span class="nook">用户名不可以使用</span>
    
    <script>

        function f1() {
            var username = document.getElementById("username");
            var s = username.value;
            var ok = document.getElementsByClassName("ok");
            var nook = document.getElementsByClassName("nook");
            console.log(s);
            if (s != null && s[0] != 'a') {
                Array.from(nook).forEach(function (element) {
                    element.style.display = 'none';
                });
                Array.from(ok).forEach(function (element) {
                    element.style.display = 'inline';
                });
                
            } else {
                Array.from(ok).forEach(function (element) {
                    element.style.display = 'none';
                });
                Array.from(nook).forEach(function (element) {
                    element.style.display = 'inline';
                });
                
            }
        }
        function f2() {
            var username = document.getElementById("username");
            var s = username.value;
            var ok = document.getElementsByClassName("ok");
            var nook = document.getElementsByClassName("nook");
            if (s == null || s[0] != 'a') {
                Array.from(ok).forEach(function (element) {
                    element.style.display = 'none';
                });
                Array.from(nook).forEach(function (element) {
                    element.style.display = 'none';
                });
            } else {
                Array.from(ok).forEach(function (element) {
                    element.style.display = 'none';
                });
                Array.from(nook).forEach(function (element) {
                    element.style.display = 'inline';
                });
            }
        }

    </script>
</body>

</html>
```



# 创建节点

`createELement`

在JavaScript中，可以使用以下步骤创建DOM对象并使用：

1. **创建元素节点：** 使用 `document.createElement` 方法创建一个新的元素节点。

   ```JavaScript
   var newElement = document.createElement('div');
   ```

2. **设置元素属性：** 使用 `element.setAttribute` 方法设置元素的属性。

   ```JavaScript
   newElement.setAttribute('id', 'myElement');
   newElement.setAttribute('class', 'myClass');
   ```

3. **设置元素内容：** 使用 `element.innerHTML` 或 `element.textContent` 设置元素的内容。

   ```JavaScript
   newElement.innerHTML = 'This is a new element!';
   ```

4. **将元素添加到文档中：** 使用 `document.appendChild` 或其他 DOM 操作方法将新元素添加到文档中。

   ```JavaScript
   document.body.appendChild(newElement);
   ```

## 练习

![image-20231218093518803](../images/image-20231218093518803.png)

```html
<!DOCTYPE html>
<html lang="zh-CN">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        .mytable {
            border-collapse: collapse;
        }

        td {
            width: 200px;
        }
    </style>
</head>

<body>
    <div id="div">
    </div>
    <script>
        var div = document.getElementById("div");
        var newTable = document.createElement("table");
        newTable.setAttribute("id", "mytable");
        newTable.setAttribute("class", "mytable");
        div.appendChild(newTable);

        var newtr = document.createElement("tr");
        newtr.setAttribute("class", "tr");
        newtr.style.cssText = "border-bottom-style: solid;border-bottom-width: 1px;border-bottom-color: lightgray;height: 35px;";

        var newtd1 = document.createElement("td");
        newtd1.textContent = "id";
        newtd1.style.textAlign = "center";
        newtr.appendChild(newtd1);
        var newtd2 = document.createElement("td");
        newtd2.textContent = "名称";
        newtd2.style.textAlign = "center";
        newtr.appendChild(newtd2);
        var newtd3 = document.createElement("td");
        newtd3.textContent = "血量";
        newtd3.style.textAlign = "center";
        newtr.appendChild(newtd3);
        var newtd4 = document.createElement("td");
        newtd4.textContent = "伤害";
        newtd4.style.textAlign = "center";
        newtr.appendChild(newtd4);
        newTable.appendChild(newtr);

        newTable.appendChild(document.createElement('br'));
        var newtr = document.createElement("tr");
        newtr.setAttribute("class", "tr");
        newtr.style.cssText = "border-bottom-style: solid;border-bottom-width: 1px;border-bottom-color: lightgray;height: 35px;";

        var newtd1 = document.createElement("td");
        newtd1.textContent = "1";
        newtd1.style.textAlign = "center";
        newtr.appendChild(newtd1);
        var newtd2 = document.createElement("td");
        newtd2.textContent = "gareen";
        newtd2.style.textAlign = "center";
        newtr.appendChild(newtd2);
        var newtd3 = document.createElement("td");
        newtd3.textContent = "340";
        newtd3.style.textAlign = "center";
        newtr.appendChild(newtd3);
        var newtd4 = document.createElement("td");
        newtd4.textContent = "58";
        newtd4.style.textAlign = "center";
        newtr.appendChild(newtd4);
        newTable.appendChild(newtr);

    </script>

</body>

</html>
```

```html
<!DOCTYPE html>
<html lang="zh-CN">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        .mytable {
            border-collapse: collapse;
        }

        td {
            width: 200px;
            text-align: center;
            border-bottom: 1px solid lightgray;
            height: 35px;
        }
    </style>
</head>

<body>
    <div id="div">
    </div>
    <script>
        var div = document.getElementById("div");
        var newTable = document.createElement("table");
        newTable.setAttribute("id", "mytable");
        newTable.setAttribute("class", "mytable");
        div.appendChild(newTable);

        var headers = ["id", "名称", "血量", "伤害"];
        var data = [
            ["1", "gareen", "340", "58"]
        ];

        var headerRow = newTable.insertRow();
        headers.forEach(function(header) {
            var th = document.createElement("th");
            th.textContent = header;
            headerRow.appendChild(th);
        });

        data.forEach(function(rowData) {
            var row = newTable.insertRow();
            rowData.forEach(function(cellData) {
                var cell = row.insertCell();
                cell.textContent = cellData;
            });
        });

    </script>

</body>

</html>

```

# 删除节点

1. `parentNode.removeChild(childNode)`: 这个方法让您能够通过其父节点删除一个子节点。

```javascript
var childNode = document.getElementById("myElement");
childNode.parentNode.removeChild(childNode);
```

1. `remove()`: 这是一种更简洁的方法，直接从DOM中删除元素。

```javascript
var element = document.getElementById("myElement");
element.remove();
```

## 练习

![image-20231218095734262](../images/image-20231218095734262.png)

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <button onclick="f1()">点击加载js</button>
    <script>
        function f1(){
            var newScript = document.createElement("script");
            newScript.setAttribute("src", "1.js");
            document.body.append(newScript);
        }

    </script>
</body>
</html>
```

```javascript
var button = document.getElementById("button");
button.onclick = function(){
    f1();
};
```

# 练习

![image-20231219113230774](../images/image-20231219113230774.png)

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <div>
        <span>账号：</span>
        <input type="text" name="account" id="account">
    </div>
    <div>
        <span>密码：</span>
        <input type="password" name="password" id="password">

    </div>
    <button onclick="f1()">提交</button>
    <script>
        function f1(){
            var account = document.getElementById("account").value;
            var password = document.getElementById("password").value;
            if(account == "" || password == ""){
                alert("有空的，不彳");
            }else{
                alert("可以了");
                location.reload();
            }
        }

    </script>
</body>
</html>
```

