---
title: jquery中的fadeIn/fadeOut与fadeTo区别
date: 2024-03-06 17:29:30
tags: 前端
---

# 问题发现

打算创建表格，控制删除与增加时添加渐变的效果，本能的使用了fadein，fadeout，但发现会更改display的css属性，由于我使用了bootstrap框架，更改这个属性会让表格变得无法看到。所以继而更换了fadeto，又发现fadeto是通过更改css的opacity属性实现的效果。如此一来，不会对本身的框架产生影响。

# 理论

1. **fadeIn()**: 这个方法用于将元素淡入显示。当元素最初处于隐藏状态时（比如通过CSS设置`display: none`），调用`fadeIn()`方法将使其逐渐变得可见。它不需要传递透明度参数，因为它会自动将元素的透明度从0逐渐增加到1。
2. **fadeOut()**: 这个方法与`fadeIn()`相反，用于将元素淡出隐藏。调用`fadeOut()`方法将使元素逐渐变得不可见，并最终完全隐藏。同样，它不需要传递透明度参数，因为它会自动将元素的透明度从1逐渐减少到0。
3. **fadeTo()**: 与前两者不同，`fadeTo()`方法允许您直接指定元素的目标透明度。您需要传递两个参数：目标透明度值（0到1之间的数字）和动画持续时间（以毫秒为单位）。调用`fadeTo()`将使元素的透明度从当前值渐变到指定的目标透明度值。

# 实践

```JavaScript
$("#searchresult tbody").append(newTr);
//对应关系是不同的
//opacity是fadeTo
//display是display
newTr.css("opacity", "0");
//newTr.fadeIn(1000);
newTr.fadeTo(1000, 1);
```

```JavaScript
$("#clear").click(function (){
  //fadeinout更改属性，用fadeTo只改变透明度
  // $("#searchresult tbody").empty().fadeOut(1000, function (){
  //   $(this).css("display", "block");
  // });
  $("#searchresult tbody").fadeTo(1000, 0, function (){
    $(this).empty();
    //默认的opacity设置为0了，后续添加新的表格不显示了
    $(this).css("opacity", "1");
  })
});
```
