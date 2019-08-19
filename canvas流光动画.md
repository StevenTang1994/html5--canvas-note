# 流光动画说明

学习 `canvas` 也差不多小一个月了，现在差不多是检查学习成果的时候了，来做一个类似腾讯云首页的效果。下面介入正题

## 开始

### 流光动画思路

首先从布局开始，一张背景图片上面浮这一个 canvas。然后在 canvas 上面对应好坐标展现出流光效果。

### 流光动画实现

#### css 实现

- 初始化页面
- 设置好背景图片，设置大小
- 设置 canvas 使居中
``` css
*{
    padding: 0;
    margin: 0px;
}
.box{
    width: 100%;
    height: 500px;
    background-image: url("./canvas文档图片/腾讯云图片.png");
    background-position: top center;
    background-repeat: no-repeat;
    display: inline-block;
    position: absolute;
    top: 0px;
    left: 0px;
    background-size: 1920px 500px;
}
.canvas{
    width: 100%;
    height: 500px;
    position: absolute;
    top: 0;
    left: 0;
    overflow: hidden;
    text-align: center;
}
#myCanvas{
    margin-left: auto;
    margin-right: auto;
}
```
#### dom 结构

- box 为背景图片
- canvas 为控制 canvas居中设置
```html
<div class="box"></div>
<div class="canvas">
    <canvas id="myCanvas" width="1920" height="500"></canvas>
</div>
```

#### JavaScript 结构

要做出流光动画的效果必须要用到`MutationObserver`(做响应式)、`requestAnimationFrame` (回调函数更新动画)。

MutationObserver：接口提供了监视对DOM树所做更改的能力。它被设计为旧的Mutation Events功能的替代品，该功能是DOM3 Events规范的一部分。[^1]

requestAnimationFrame： window.requestAnimationFrame() 告诉浏览器——你希望执行一个动画，并且要求浏览器在下次重绘之前调用指定的回调函数更新动画。该方法需要传入一个回调函数作为参数，该回调函数会在浏览器下一次重绘之前执行。[^2]

MutationObserver
```JavaScript
// 首先获取box的宽度

```

## 参考文献
[^1]: [MutationObserver - Web API 接口参考 | MDN](https://developer.mozilla.org/zh-CN/docs/Web/API/MutationObserver)

[^2]: [window.requestAnimationFrame - Web API 接口参考 | MDN](https://developer.mozilla.org/zh-CN/docs/Web/API/Window/requestAnimationFrame)
