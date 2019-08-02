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

### 矩形

首先在canvas上关于矩形类的方法，一共四种。

| 方法  | 描述 |
| -- | --|
|   [rect()](#rect)  | 创建矩形 |
|   [fillRect()](#fillRect)  |   绘制“被填充”的矩形  |
|   [strokeRect()](#strokeRect)    |   绘制矩形（无填充）  |
|   [clearRect()](#clearRect) |   在给定的矩形内清除指定的像素    |


<div id= "rect"> </div>

#### 创建矩形--rect()

定义：rect() 方法创建矩形。

##### rect的javascript的语法

```JavaScript

context.rect(x,y,width,height);

//(画布的X坐标,画布的Y坐标,画布的宽,画布的高)

```

```javascript {.line-numbers}
var c=document.getElementById("myCanvas"); // 获取画布

var ctx=c.getContext("2d"); 
// getContext() 方法可返回一个对象，该对象提供了用于在画布上绘图的方法和属性
// 个人理解：可以把getContext()这个方法理解为画布的画笔。

ctx.rect(20,20,150,100); // 设置坐标

ctx.stroke(); // 绘制已经定义的点
```
<div id = "rectDemo"></div>
可以通过 `strokeStyle` 设置或返回用于笔触的颜色、渐变或模式和 `lineWidth` 设置或返回当前的线条宽度。

设置一个**红色线框矩形**，线条的宽度为 **6** 像素。

```JavaScript {.line-numbers}
var c = document. getElementById("myCanvas");
var ctx=c.getContext("2d"); 

ctx.strokeStyle = 'red'; // 设置矩形的红色
ctx.lineWidth = '6';    // 设置矩形线条的宽度为 6
ctx.rect(200,150,300,200);
ctx.stroke();
```
显示效果

<div align=center><img src="/canvas文档图片/red-6.png" alt="red-6"/></div>


如果想在一张画布里面画多个矩形或者其他的图形需要用到 `beginPath` 起始一条路径，或重置当前路径

##### 设置多个矩形

```JavaScript {.line-numbers}
// 红色线框矩形 线条的宽度为6像素。
var c = document. getElementById("myCanvas");
var ctx=c.getContext("2d"); 

ctx.strokeStyle = 'red'; // 设置矩形的颜色
ctx.lineWidth = '6';    // 设置矩形线条的宽度
ctx.rect(200,150,300,200);
ctx.stroke();

ctx.beginPath(); // 重置路径
ctx.strokeStyle = 'green'; // 设置矩形的颜色
ctx.lineWidth = '4';    // 设置矩形线条的宽度
ctx.rect(250,100,200,180);
ctx.stroke();
```
>如果第二矩形没有设置颜色的与线宽的话，它会继承上一个矩形的属性

显示效果
<div align=center><img src="/canvas文档图片/redAndgreen.png" alt="redAndgreen"></div>

<div id="fillRect"></div>

#### “被填充”的矩形--fillRect()

定义：fillRect() 方法绘制“已填色”的矩形。默认的填充颜色是黑色。

##### fillRect的javascript的语法

```javaScript {.line-numbers}

context.fillRect(x,y,width,height);
```

```javaScript {.line-numbers}
var c = document.getElementById("mycanvas");
var ctx = c.getContext('2d');
ctx.fillRect(20,20,150,100);
```

显示效果

<div align=center><img src="/canvas文档图片/fillRect000.png" alt="fillRect000"></div>

可以通过 `fillStyle` 设置矩形的颜色

```javaScript {.line-numbers}
var c = document.getElementById("mycanvas");
var ctx = c.getContext('2d');
ctx.fillStyle = "green";
ctx.fillRect(20,20,150,100);
```
显示效果

<div align=center><img src="/canvas文档图片/fillRectGreen.png" alt="fillRectGreen"></div>

通过 `createLinearGradient` 设置渐变颜色 (简要说明,后面细谈)

> createLinearGradient() 方法创建线性的渐变对象。
>渐变可用于填充矩形、圆形、线条、文本等等。

```javaScript {.line-numbers}
var c = document.getElementById("mycanvas");
var ctx = c.getContext('2d');
// 设置渐变
var my_gradient = ctx.createLinearGradient(20,20,170,120);
my_gradient.addColorStop(0,"red");
my_gradient.addColorStop(1,"white");

ctx.fillStyle=my_gradient;
ctx.fillRect(20,20,150,100);
```
显示效果

<div align=center><img src="/canvas文档图片/red000.png" alt="red000"></div>

<div id="strokeRect"></div>

#### 绘制矩形"无填充"--strokeRect

定义: strokeRect() 方法绘制矩形（不填色）。笔触的默认颜色是黑色。

> 改方法与[rect()](#rect)基本相同

##### strokeRect的javaScript的语法

```javaScript {.line-numbers}
context.strokeRect(x,y,width,height);
```

```javaScript {.line-numbers}
var c=document.getElementById("myCanvas");
var ctx=c.getContext("2d");
ctx.strokeRect(20,20,150,100);
```

显示效果

<div align=center><img src="/canvas文档图片/strokeRect.png" alt="strokeRect"></div>

同样和 [rect](#rectDemo) 一样可以通过 `strokeStyle` 设置或返回用于笔触的颜色、渐变或模式和 `lineWidth` 设置或返回当前的线条宽度。

<div id="clearRect"></div>

#### 清空矩形--clearRect
定义: clearRect() 方法清空给定矩形内的指定像素。

##### clearRect的JavaScript语法

```JavaScript {.line-numbers}
context.clearRect(x,y,width,height);
```

```JavaScript {.line-numbers}
var c=document.getElementById("myCanvas");
var ctx=c.getContext("2d");
ctx.fillStyle="green";
ctx.fillRect(0,0,300,150);
ctx.clearRect(20,20,100,50);
```

显示效果

<div align=center><img src="/canvas文档图片/clearRect.png" alt="clearRect"></div>

## 矩形动画

思路: 使用延时函数---setTimeout，来控制矩形的位置和颜色等。

演示: 动画矩形
```javascript {.line-numbers}
var c = document.getElementById('myCanvas');
var ctx = c.getContext('2d');
i = 30;
function demo() {
    if (i>1000){
        clearInterval(box);
    }else{
        i++;
        ctx.clearRect(0,0,1077,500); // 全局清空像素
        ctx.beginPath();
        ctx.strokeStyle ="green";
        ctx.rect(i,0,300,150);
        ctx.stroke();
    }
}
var box = setInterval (demo,10);
```

## 参考文献

[^1]: [canvas HTML5新增标签 百度百科](https://baike.baidu.com/item/canvas/16416421#viewPageContent)

[^2]: [W3C HTML 5 Canvas 参考手册](http://www.w3school.com.cn/tags/html_ref_canvas.asp)