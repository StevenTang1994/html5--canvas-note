---
toc:
  depth_from: 1
  depth_to: 6
  ordered: true
---

[toc]
# canvas 基础用法

写在最前面

自己很久以前想学习`canvas`的，但是本人一直没有时间，刚好现在公司的项目要用到`canvas`，还是一个比较复杂的需求。下面介入正题

## 描述

Canvas API（画布）是在`HTML5`中新增的标签用于在网页实时生成图像，并且可以操作图像内容，基本上它是一个可以用`JavaScript`操作的位图（bitmap）。

Canvas 对象表示一个 HTML 画布元素 - `canvas`。它没有自己的行为，但是定义了一个 API 支持脚本化客户端绘图操作。

`canvas` 标记在 Safari 1.3 中引入，在制作此参考页时，它在 Firefox 1.5 和 Opera 9 中也得到了支持。在 IE 中，`canvas` 标记及其 API 可以使用位于excanvas点sourceforge点net的 ExplorerCanvas 开源项目来模拟。[^1]

### 浏览器的兼容性

| 浏览器 | 最低版本 |
| -- | --|
|Internet Explorer| 9 |
|Firefox| 大部分现代版本|
|Opera| 大部分现代版本|
|Chrome| 大部分现代版本|
|Safari| 大部分现代版本|

> 注释：Internet Explorer 8 以及更早的版本不支持 `canvas` 元素。

## 基本用法

```html {.line-numbers}
<div class="box">
    <canvas id="mycanvas" width="1077px" height="500"></canvas>
</div>
    <!-- canvas标签的大小通常在标签里面直接用属性设置
    与正常的标签一样，可以写style样式。
    如果你不想在用画布的时候出一些莫名其妙的错误
    建议不要用类名或者id还有style里面设置画布的大小 -->
<script>
    var c = document.getElementById("mycanvas");
    // 获取画布
    var ctx = c.getContext('2d');
    // getContext() 方法可返回一个对象，该对象提供了用于在画布上绘图的方法和属性。 2d作为现写阶段唯一的参数（2019-07-26）
    ctx.fillStyle="#0000ff";
    // 设置画布的颜色
    ctx.fillRect(20,20,150,100);
    // fillRect() 方法绘制“已填色”的矩形。默认的填充颜色是黑色。
</script>
```

基本上 `cnavas` 上可以实现矩形（可以设置圆角==>圆），文本、图像绘制、像素操作、点线连接、线条样式等基本操作。（待修改）[^2]

较为的交互方式（动画之类。。。）需要额外用其他的方法去实现。

### 画布的坐标

相信大家在小学初中在数学课上都学习过十字坐标系，画布的坐标和我们学习过的十字坐标系的坐标**不一样**

> 浏览器的坐标和画布坐标系一样

如图：
<div align=center><img src="/canvas文档图片/十字坐标系与画布坐标系的区别.png" alt="十字坐标系与画布坐标系的区别"/></div>


### 线条

#### 语法定义
- moveTo(x, y)用来定义起始坐标。
- lineTo(x, y)用来定义结束坐标。

#### 例
```JavaScript {.line-numbers}
    var c = document.getElementById("mycanvas");
    var ctx = c.getContext('2d');
    ctx.moveTo(50, 60);
    ctx.lineTo(200, 100);
    ctx.stroke();
```
如图：
<div align=center><img src="/canvas文档图片/线.png" alt="线"/></div>

画多条线时，需要用到 `beginPath` 开始一条路径，或重置当前的路径。

```JavaScript {.line-numbers}
    var c = document.getElementById("mycanvas");
    var ctx = c.getContext('2d');
    ctx.moveTo(50, 60);
    ctx.lineTo(200, 100);
    ctx.stroke();

    ctx.beginPath();
    ctx.moveTo(100, 100);
    ctx.lineTo(300, 300);
    ctx.stroke();
```
如图：
<div align=center><img src="/canvas文档图片/beginPath线.png" alt="beginPath线"/></div>

可以用`lineWidth`（改变线条的宽度）和`strokeStyle`（改变线条的颜色）

```JavaScript {.line-numbers}
var c = document.getElementById("mycanvas");
var ctx = c.getContext('2d');
ctx.lineWidth = "5";  //设置线条的宽度
ctx.strokeStyle = "green";  //设置线条的颜色
ctx.moveTo(50, 60);
ctx.lineTo(200, 100);
ctx.stroke();
```
如图：
<div align=center><img src="/canvas文档图片/颜色和宽度.png" alt="颜色和宽度"/></div>

>注意： 这里如果多条线段，第一条设置了属性，第二条会继承第一条的属性，可以覆盖

```JavaScript {.line-numbers}
var c = document.getElementById("mycanvas");
var ctx = c.getContext('2d');
ctx.lineWidth = "5"; //第一条设置宽度
ctx.strokeStyle = "green";
ctx.moveTo(50, 60);
ctx.lineTo(200, 100);
ctx.stroke();

// 第二条不设置
ctx.beginPath();
ctx.strokeStyle = "red";
ctx.moveTo(100, 100);
ctx.lineTo(300, 300);
ctx.stroke();
```

如图：
<div align=center><img src="/canvas文档图片/线段继承属性.png" alt="线段继承属性"/></div>

> 继承了第一条线的宽度


可以创建从当前点到开始点的路径 `closePath() ` 


```javaScript {.line-numbers}
var c=document.getElementById("myCanvas");
var ctx=c.getContext("2d");
ctx.beginPath();
ctx.moveTo(200,200);
ctx.lineTo(200,300);
ctx.lineTo(300,300);
ctx.closePath();
ctx.stroke();
```

如图：
<div align=center><img src="/canvas文档图片/closePath线.png" alt="closePath线"/></div>

可以用 `fill()` 和 `fillStyle()` 设置颜色

```javaScript {.line-numbers}
var c=document.getElementById("myCanvas");
var ctx=c.getContext("2d");
ctx.beginPath();
ctx.moveTo(200,200);
ctx.lineTo(200,300);
ctx.lineTo(300,300);
ctx.closePath();
ctx.stroke();
ctx.fillStyle="green";
ctx.fill();
```
## 参考文献

[^1]: [canvas HTML5新增标签 百度百科](https://baike.baidu.com/item/canvas/16416421#viewPageContent)

[^2]: [W3C HTML 5 Canvas 参考手册](http://www.w3school.com.cn/tags/html_ref_canvas.asp)