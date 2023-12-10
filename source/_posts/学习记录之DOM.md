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

