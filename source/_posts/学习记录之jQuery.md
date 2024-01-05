# JQuery

jQuery 是一个快速、小巧且功能丰富的 JavaScript 库。它简化了在网页中进行常见任务的复杂性，提供了跨浏览器的解决方案，使得开发者能够更容易地处理 DOM 操作、事件处理、动画效果、Ajax 请求等。

以下是一些 jQuery 的主要特点和用途：

1. **跨浏览器兼容性：** jQuery 解决了在不同浏览器之间处理 DOM 操作和事件的差异，为开发者提供了一致的接口。
2. **简化 DOM 操作：** 使用 jQuery，你可以使用简洁而强大的选择器语法来轻松选择、操作和遍历 DOM 元素。
3. **事件处理：** jQuery 提供了简单的事件处理机制，使得添加、移除和触发事件变得容易，同时解决了跨浏览器的事件兼容性问题。
4. **Ajax 请求：** jQuery 简化了进行 Ajax 请求的过程，通过 `$.ajax()` 方法，你可以轻松地进行数据交换而无需刷新整个页面。
5. **动画和效果：** 提供了丰富的动画和效果功能，例如淡入淡出、滑动、展开折叠等，使页面更生动有趣。
6. **链式操作：** jQuery 允许你在一行代码中执行多个操作，通过链式调用方法，可以使代码更简洁。
7. **插件生态系统：** 有大量的 jQuery 插件可用，可以轻松扩展 jQuery 的功能，满足不同项目的需求。
8. **轻量级：** 尽管功能强大，但 jQuery 本身的文件相对较小，加载速度较快。

由于这些优点，jQuery 在过去的Web开发中非常流行，但随着现代浏览器对原生 JavaScript 和其他库的支持增强，一些新的框架和库也逐渐崭露头角。然而，仍然有很多项目和网站在使用 jQuery，并且它仍然是一个有用的工具，特别是在需要兼容旧版本浏览器的情况下。

# 基础语法

```javascript
$(function(){
    /* code */ 
});
```



 是 jQuery 中用于在文档准备就绪时执行代码的一种缩写形式。这是一种常见的用法，用于确保你的代码在文档加载完成后再执行，以避免在DOM元素尚未完全加载时进行操作。

**选择器（Selectors）：**

- 通过元素名称选择：`$("p")` 选择所有 `<p>` 元素。
- 通过类名选择：`$(".myClass")` 选择所有具有类名 "myClass" 的元素。
- 通过ID选择：`$("#myId")` 选择具有ID "myId" 的元素。
- 多重选择器：`$("p, .myClass, #myId")` 可以选择多个元素。

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script src="https://cdn.bootcdn.net/ajax/libs/jquery/3.7.1/jquery.min.js"></script>
</head>
<body>
    <div id="container" style="display: inline;">
        <span>这是文字</span>
    </div>
    <button id="show">show</button>
    <button id="hide">hide</button>
    <script>
        //通过jQuery来控制其中的信息显示与否
        $(function(){
            $("#show").click(function(){
                $("#container").show();
                alert("this is show!");
            });
            $("#hide").click(function(){
                $("#container").hide();
            });
        });
    </script>
</body>
</html>
```

## .val()

在 jQuery 中，`.val()` 方法主要用于获取或设置表单元素的值。它可以应用于一系列不同类型的表单元素，包括：

1. **文本框（Text Input）：**

   ```javascript
   var textValue = $("input[type='text']").val();
   ```

2. **密码框（Password Input）：**

   ```javascript
   var passwordValue = $("input[type='password']").val();
   ```

3. **文本区域（Textarea）：**

   ```javascript
   var textareaValue = $("textarea").val();
   ```

4. **单选按钮（Radio Button）：**

   ```javascript
   var radioValue = $("input[type='radio']:checked").val();
   ```

5. **复选框（Checkbox）：**

   ```javascript
   var checkboxValue = $("input[type='checkbox']").val(); // 只获取第一个复选框的值
   ```

   如果有多个复选框，应该使用 `.each()` 遍历它们：

   ```javascript
   var checkboxValues = [];
   $("input[type='checkbox']:checked").each(function() {
       checkboxValues.push($(this).val());
   });
   ```

6. **下拉框（Select）：**

   ```javascript
   var selectValue = $("select").val(); // 只获取选中项的值
   ```

   如果需要获取所有选项的值，应该使用 `.each()` 遍历它们：

   ```javascript
   var selectValues = [];
   $("select option:selected").each(function() {
       selectValues.push($(this).val());
   });
   ```

## .html() .text()

1. **`.html()` 方法：**

   - **获取内容：** 用于获取元素的 HTML 内容，包括 HTML 标签。

   ```javascript
   var htmlContent = $("div").html();
   ```

   - **设置内容：** 用于设置元素的 HTML 内容。

   ```javascript
   $("div").html("<p>New HTML content</p>");
   ```

2. **`.text()` 方法：**

   - **获取内容：** 用于获取元素的纯文本内容，不包含 HTML 标签。

   ```javascript
   var textContent = $("div").text();
   ```

   - **设置内容：** 用于设置元素的纯文本内容。

   ```javascript
   $("div").text("New text content");
   ```

关键区别：

- **HTML vs. 文本：** `.html()` 获取和设置的是包含 HTML 标签的内容，而 `.text()` 获取和设置的是去除 HTML 标签后的纯文本内容。
- **潜在的安全性问题：** 当你使用用户提供的数据时，要注意潜在的安全性问题。使用用户提供的内容作为 `.html()` 的参数可能导致 XSS（跨站点脚本攻击）问题，因为它会将提供的 HTML 代码解释为实际的 HTML。相比之下，`.text()` 不会解释 HTML，因此更安全。

```html
	<div id="container" style="display: inline;">
        这是div中的文字
        <span>这是span中的文字</span>
    </div>
    <script>
    $(function(){
                $("#disp").text(
                    $("#container").text()
                );
            });
    </script>
    	
```

![image-20231227192524022](../images/image-20231227192524022.png)

```html
	<div id="container" style="display: inline;">
        这是div中的文字
        <span>这是span中的文字</span>
    </div>
    <script>
    $(function(){
                $("#disp").text(
                    $("#container").html()
                );
            });
    </script>
```

![image-20231227192630357](../images/image-20231227192630357.png)

# css调整

jQuery 提供了多种方法来操作元素的 CSS 样式，以下是一些常见的 jQuery CSS 操作：

1. **获取或设置单个样式属性：**

   - 获取样式属性：

     ```JavaScript
     var fontSize = $("div").css("font-size");
     ```

   - 设置样式属性：

     ```JavaScript
     $("div").css("color", "red");
     ```

2. **获取或设置多个样式属性：**

   - 获取多个样式属性：

     ```JavaScript
     var styles = $("div").css(["font-size", "color"]);
     ```

   - 设置多个样式属性：

     ```JavaScript
     $("div").css({
         "font-size": "16px",
         "color": "blue"
     });
     ```

3. **操作类（Class）：**

   - 添加类：

     ```JavaScript
     $("div").addClass("highlight");
     ```

   - 移除类：

     ```JavaScript
     $("div").removeClass("highlight");
     ```

   - 切换类（存在则移除，不存在则添加）：

     ```JavaScript
     $("div").toggleClass("highlight");
     ```

4. **检查类是否存在：**

   ```JavaScript
   if ($("div").hasClass("highlight")) {
       // 类存在的处理逻辑
   }
   ```

5. **操作元素的可见性：**

   - 显示元素：

     ```JavaScript
     $("div").show();
     ```

   - 隐藏元素：

     ```JavaScript
     $("div").hide();
     ```

   - 切换元素的可见性：

     ```JavaScript
     $("div").toggle();
     ```

6. **设置宽度和高度：**

   ```JavaScript
   $("div").width(200);
   $("div").height(150);
   ```

7. **动画效果：**

   - 淡入：

     ```JavaScript
     $("div").fadeIn();
     ```

   - 淡出：

     ```JavaScript
     $("div").fadeOut();
     ```

   - 滑动显示：

     ```JavaScript
     $("div").slideDown();
     ```

   - 滑动隐藏：

     ```JavaScript
     $("div").slideUp();
     ```

这些是一些基本的 jQuery CSS 操作方法。使用这些方法，你可以方便地操控元素的样式、类、可见性和动画效果。

# 选择器

jQuery 中的选择器是一种强大的工具，用于选择 HTML 文档中的元素。以下是一些常用的 jQuery 选择器：

1. **元素选择器：**
   - `element`：选择所有指定类型的元素，例如 `p` 选择所有段落元素。
2. **ID 选择器：**
   - `#id`：选择指定 id 属性的元素，例如 `#header` 选择 id 为 "header" 的元素。
3. **类选择器：**
   - `.class`：选择指定 class 属性的元素，例如 `.highlight` 选择所有具有 "highlight" 类的元素。
4. **属性选择器：**
   - `[attribute]`：选择具有指定属性的元素，例如 `[type]` 选择所有具有 "type" 属性的元素。
   - `[attribute=value]`：选择具有指定属性和值的元素，例如 `[name="username"]` 选择所有 name 属性值为 "username" 的元素。
5. **通配符选择器：**
   - `*`：选择所有元素。
6. **子元素选择器：**
   - `parent > child`：选择指定父元素下的子元素，例如 `ul > li` 选择 ul 下的所有 li 元素。
7. **后代元素选择器：**
   - `ancestor descendant`：选择指定祖先元素下的后代元素，例如 `div p` 选择所有 div 下的 p 元素。
8. **同级元素选择器：**
   - `prev + next`：选择紧接在指定元素后面的同级元素，例如 `h2 + p` 选择紧接在 h2 后面的 p 元素。
9. **相邻元素选择器：**
   - `prev ~ siblings`：选择与指定元素在同一级别的所有同级元素，例如 `h2 ~ p` 选择与 h2 具有相同父元素的所有 p 元素。
10. **过滤选择器：**
    - `:first`：选择匹配的第一个元素。
    - `:last`：选择匹配的最后一个元素。
    - `:even`：选择匹配的偶数索引元素。
    - `:odd`：选择匹配的奇数索引元素。
    - `:eq(index)`：选择匹配给定索引值的元素。

## 练习

实现斑马线效果

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script src="https://cdn.bootcdn.net/ajax/libs/jquery/3.7.1/jquery.min.js"></script>
    <style>
        table{
            border-collapse: collapse;
            table-layout: fixed;
            width: 800px;
        }
        td{
            text-align: center;
            margin: 1px solid black;
            padding: 8px;
        }
        tr{
            margin-bottom: 1px;
            border: 1px solid black;
            
        }
        .odd{
            background-color: aqua;
        }
    </style>
</head>
<body>
    <table>
        <tr>
            <td>
                表头1
            </td>
            <td>
                表头2
            </td>
            <td>
                表头3
            </td>
        </tr>
        <tr>
            <td>
                1
            </td>
            <td>
                2
            </td>
            <td>
                3
            </td>
        </tr>
        <tr>
            <td>
                1
            </td>
            <td>
                2
            </td>
            <td>
                3
            </td>
        </tr>
        <tr>
            <td>
                1
            </td>
            <td>
                2
            </td>
            <td>
                3
            </td>
        </tr>
        <tr>
            <td>
                1
            </td>
            <td>
                2
            </td>
            <td>
                3
            </td>
        </tr>
        <tr>
            <td>
                1
            </td>
            <td>
                2
            </td>
            <td>
                3
            </td>
        </tr>
        <tr>
            <td>
                1
            </td>
            <td>
                2
            </td>
            <td>
                3
            </td>
        </tr>
    </table>
    <button id="button">修改</button>
    <script>
        $(function(){
            $("#button").click(
                function(){
                    $("table tr:odd").toggleClass("odd");
                }
            );
        });
        
    </script>
</body>
</html>
```

## 属性操作

jQuery 提供了一系列方法，用于操作元素的属性。以下是一些常用的 jQuery 属性操作方法：

1. **获取或设置元素的属性：**

   - `attr(name)`: 获取指定属性的值。

   - `attr(name, value)`: 设置指定属性的值。

   - 例子：

     ```JavaScript
     var value = $("img").attr("src"); // 获取 img 元素的 src 属性值
     $("img").attr("alt", "New Alt Text"); // 设置 img 元素的 alt 属性值
     ```

2. **删除元素的属性：**

   - `removeAttr(name)`: 删除指定的属性。

   - 例子：

     ```JavaScript
     $("img").removeAttr("alt"); // 删除 img 元素的 alt 属性
     ```

## prop

1. **`prop` 方法：**

   - `prop` 方法用于获取或设置元素的属性值，特别是那些在 HTML 中被定义为属性（而非属性和属性值的形式）的属性，例如 `checked`、`disabled` 等。

   - `prop` 方法更适用于处理布尔属性，它返回属性的当前状态，而不仅仅是属性的初始值。

   - 例子：

     ```JavaScript
     var isChecked = $("input").prop("checked"); // 获取第一个 <input> 元素的 checked 属性值
     $("input").prop("disabled", true); // 设置所有 <input> 元素的 disabled 属性为 true
     ```

2. **`attr` 方法：**

   - `attr` 方法用于获取或设置元素的属性值，包括那些在 HTML 中被定义为属性和属性值的形式的属性，例如 `src`、`alt`、`class` 等。

   - `attr` 方法更适用于处理非布尔属性，它返回属性的字符串值。

   - 例子：

     ```JavaScript
     var srcValue = $("img").attr("src"); // 获取第一个 <img> 元素的 src 属性值
     $("img").attr("alt", "New Alt Text"); // 设置所有 <img> 元素的 alt 属性值
     ```

**总结：**

- 使用 `prop` 主要用于处理布尔属性，例如复选框的 `checked`、输入框的 `disabled`。
- 使用 `attr` 主要用于处理其他属性，例如图片的 `src`、链接的 `href`、元素的 `class`。

# 动画

jQuery 提供了一系列用于创建动画和效果的方法。以下是一些常用的 jQuery 效果：

1. **显示和隐藏效果：**

   - `show(speed)`: 以指定速度显示元素。
   - `hide(speed)`: 以指定速度隐藏元素。
   - `toggle(speed)`: 切换元素的显示和隐藏状态。

   ```
   javascriptCopy code$("div").show(1000); // 以1秒的速度显示 div 元素
   $("div").hide("slow"); // 以慢速度隐藏 div 元素
   $("div").toggle(500); // 以0.5秒的速度切换 div 元素的显示和隐藏状态
   ```

2. **淡入和淡出效果：**

   - `fadeIn(speed)`: 以指定速度淡入元素。
   - `fadeOut(speed)`: 以指定速度淡出元素。
   - `fadeToggle(speed)`: 切换元素的淡入和淡出状态。

   ```JavaScript
   $("div").fadeIn("fast"); // 以快速速度淡入 div 元素
   $("div").fadeOut(1500); // 以1.5秒的速度淡出 div 元素
   $("div").fadeToggle("slow"); // 以慢速度切换 div 元素的淡入和淡出状态
   ```

3. **滑动效果：**

   - `slideDown(speed)`: 以指定速度滑下显示元素。
   - `slideUp(speed)`: 以指定速度滑上隐藏元素。
   - `slideToggle(speed)`: 切换元素的滑动显示和隐藏状态。

   ```JavaScript
   $("div").slideDown(1000); // 以1秒的速度滑下显示 div 元素
   $("div").slideUp("slow"); // 以慢速度滑上隐藏 div 元素
   $("div").slideToggle(500); // 以0.5秒的速度切换 div 元素的滑动显示和隐藏状态
   ```

4. **自定义动画效果：**

   - `animate(properties, speed, easing, complete)`: 通过指定的 CSS 属性进行自定义动画。

   ```JavaScript
   $("div").animate({ left: '250px', opacity: '0.5' }, "slow");
   ```

## 练习

使得表格变长变短

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script src="https://cdn.bootcdn.net/ajax/libs/jquery/3.7.1/jquery.min.js"></script>
    <style>
        table{
            border-collapse: collapse;
            table-layout: fixed;
            width: 800px;
        }
        td{
            text-align: center;
            margin: 1px solid black;
            padding: 8px;
            
        }
        tr{
            height: 50px;
            margin-bottom: 1px;
            border: 1px solid black;
            
        }
        .odd{
            background-color: aqua;
        }
    </style>
</head>
<body>
    <table>
        <tr>
            <td>
                表头1
            </td>
            <td>
                表头2
            </td>
            <td>
                表头3
            </td>
        </tr>
        <tr>
            <td>
                1
            </td>
            <td>
                2
            </td>
            <td>
                3
            </td>
        </tr>
        <tr>
            <td>
                1
            </td>
            <td>
                2
            </td>
            <td>
                3
            </td>
        </tr>
        <tr>
            <td>
                1
            </td>
            <td>
                2
            </td>
            <td>
                3
            </td>
        </tr>
        <tr>
            <td>
                1
            </td>
            <td>
                2
            </td>
            <td>
                3
            </td>
        </tr>
        <tr>
            <td>
                1
            </td>
            <td>
                2
            </td>
            <td>
                3
            </td>
        </tr>
        <tr>
            <td>
                1
            </td>
            <td>
                2
            </td>
            <td>
                3
            </td>
        </tr>
    </table>
    <button id="button">修改</button>
    <button id="long">缓慢变长</button>
    <button id="short">缓慢变短</button>
    <script>
        $(function(){
            $("#button").click(
                function(){
                    $("table tr:odd").toggleClass("odd");
                }
            );
        });
        $(
            function(){
                $("#long").click(
                    function(){
                        $("tr:even").animate({height : "100px"}, 1000);
                    }
                );
                $("#short").click(
                    function(){
                        $("tr:even").animate({height : "50px"}, 1000);
                    }
                );
            }
        );
    </script>
</body>
</html>
```

# 事件

在 jQuery 中，事件是与用户交互或浏览器操作相关的行为，例如点击、鼠标悬停、键盘输入等。jQuery 提供了一系列方法来处理和绑定这些事件。以下是一些常用的 jQuery 事件：

1. **鼠标事件：**

   - `click()`: 当元素被点击时触发。
   - `dblclick()`: 当元素被双击时触发。
   - `mousedown()`: 当鼠标按下时触发。
   - `mouseup()`: 当鼠标释放时触发。
   - `mousemove()`: 当鼠标在元素上移动时触发。
   - `mouseover()`: 当鼠标移入元素时触发。
   - `mouseout()`: 当鼠标移出元素时触发。

   ```JavaScript
   $("button").click(function() {
       alert("Button Clicked!");
   });
   
   $("div").mouseover(function() {
       $(this).css("background-color", "yellow");
   });
   ```

2. **键盘事件：**

   - `keydown()`: 当键盘按下任意键时触发。
   - `keypress()`: 当键盘按下字符键时触发。
   - `keyup()`: 当键盘释放任意键时触发。

   ```JavaScript
   $(document).keydown(function(event) {
       console.log("Key pressed: " + event.key);
   });
   ```

3. **表单事件：**

   - `submit()`: 当表单提交时触发。
   - `change()`: 当表单元素的值发生改变时触发。
   - `focus()`: 当元素获得焦点时触发。
   - `blur()`: 当元素失去焦点时触发。

   ```JavaScript
   $("form").submit(function(event) {
       event.preventDefault(); // 阻止表单提交
       alert("Form Submitted!");
   });
   
   $("input").change(function() {
       console.log("Input value changed: " + $(this).val());
   });
   ```

4. **窗口事件：**

   - `resize()`: 当浏览器窗口大小发生改变时触发。
   - `scroll()`: 当页面滚动时触发。

   ```JavaScript
   $(window).resize(function() {
       console.log("Window resized!");
   });
   
   $(window).scroll(function() {
       console.log("Page scrolled!");
   });
   ```