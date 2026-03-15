# CSS CheatSheet | CSS 语法速览与实践清单

```css
/* 注释 */

/* ####################
   ## 选择器
   ####################*/

/* 一般而言，CSS的声明语句非常简单。*/
选择器 {
  属性: 值; /* 更多属性...*/
}

/* 选择器用于指定页面上的元素。

针对页面上的所有元素。*/
* {
  color: red;
}

/*
假定页面上有这样一个元素

<div class='some-class class2' id='someId' attr='value' />
*/

/* 你可以通过类名来指定它 */
.some-class {
}

/* 给出所有类名 */
.some-class.class2 {
}

/* 标签名 */
div {
}

/* id */
#someId {
}

/* 由于元素包含attr属性，因此也可以通过这个来指定 */
[attr] {
  font-size: smaller;
}

/* 以及有特定值的属性 */
[attr="value"] {
  font-size: smaller;
}

/* 通过属性的值的开头指定 */
[attr^="val"] {
  font-size: smaller;
}

/* 通过属性的值的结尾来指定 */
[attr$="ue"] {
  font-size: smaller;
}

/* 通过属性的值的部分来指定 */
[attr~="lu"] {
  font-size: smaller;
}

/* 你可以把这些全部结合起来，注意不同部分间不应该有空格，否则会改变语义 */
div.some-class[attr$="ue"] {
}

/* 你也可以通过父元素来指定。*/

/* 某个元素是另一个元素的直接子元素 */
div.some-parent > .class-name {
}

/* 或者通过该元素的祖先元素 */
div.some-parent .class-name {
}

/* 注意，去掉空格后语义就不同了。
你能说出哪里不同么？*/
div.some-parent.class-name {
}

/* 你可以选择某元素前的相邻元素 */
.i-am-before + .this-element {
}

/* 某元素之前的同级元素（相邻或不相邻）*/
.i-am-any-before ~ .this-element {
}

/* 伪类允许你基于页面的行为指定元素（而不是基于页面结构）*/

/* 例如，当鼠标悬停在某个元素上时 */
:hover {
}

/* 已访问过的链接*/
:visited {
}

/* 未访问过的链接*/
:link {
}

/* 当前焦点的input元素 */
:focus {
}

/* ####################
   ## 属性
   ####################*/

选择器 {
  /* 单位 */
  width: 50%; /* 百分比 */
  font-size: 2em; /* 当前字体大小的两倍 */
  width: 200px; /* 像素 */
  font-size: 20pt; /* 点 */
  width: 5cm; /* 厘米 */
  width: 50mm; /* 毫米 */
  width: 5in; /* 英尺 */

  /* 颜色 */
  background-color: #f6e; /* 短16位 */
  background-color: #f262e2; /* 长16位 */
  background-color: tomato; /* 颜色名称 */
  background-color: rgb(255, 255, 255); /* rgb */
  background-color: rgb(10%, 20%, 50%); /*  rgb 百分比 */
  background-color: rgba(255, 0, 0, 0.3); /*  rgb 加透明度 */

  /* 图片 */
  background-image: url(/path-to-image/image.jpg);

  /* 字体 */
  font-family: Arial;
  font-family: "Courier New"; /* 使用双引号包裹含空格的字体名称 */
  font-family: "Courier New", Trebuchet, Arial; /* 如果第一个
                             字体没找到，浏览器会使用第二个字体，一次类推 */
}
```

# Syntax | 语法

## Selector

```css
:root {
  --red: #ff6f69;
}

#title {
  color: var(--red);
}

.quote {
  color: var(--red);
}
```

# Layout & Position | 布局与定位

## Position | 定位

需要注意的是，如果父元素包含了 transform 属性，那么子元素的 position 为 fixed 属性时会出现异常。

```json
{
  "top": "元素顶部相对于视口顶部的距离",
  "bottom": "元素底部相对于视口底部的距离",
  "left": "元素左边相对于视口左边的距离",
  "right": "元素右边相对于视口左边的距离",
  "height": "元素高度",
  "width": "元素宽度"
}
```

### Center | 居中

## Scroll | 滚动

在 iOS 设备上可以添加 `-webkit-overflow-scrolling` 属性，以使用户感觉懒滚动式地顺滑。

## 省略

多行文本省略

```css
p {
  position: relative;
  line-height: 18px;
  height: 36px;
  overflow: hidden;
}

p::after {
  content: "...";
  font-weight: bold;
  position: absolute;
  bottom: 0;
  right: 0;
  padding: 0 20px 1px 45px;

  /* 为了展示效果更好 */
  background: -webkit-gradient(
    linear,
    left top,
    right top,
    from(rgba(255, 255, 255, 0)),
    to(white),
    color-stop(50%, white)
  );
  background: -moz-linear-gradient(
    to right,
    rgba(255, 255, 255, 0),
    white 50%,
    white
  );
  background: -o-linear-gradient(
    to right,
    rgba(255, 255, 255, 0),
    white 50%,
    white
  );
  background: -ms-linear-gradient(
    to right,
    rgba(255, 255, 255, 0),
    white 50%,
    white
  );
  background: linear-gradient(
    to right,
    rgba(255, 255, 255, 0),
    white 50%,
    white
  );
}
```

# Properties

## content

可以使用 css content 来避免 dom 入侵。我们为查找到采集的元素添加了个性化的样式 data-spmd-container，并为该 dom 添加新属性 data-udata-value 用于记录该元素的点击数据，css 做如下定义

```css
.data-spmd-container:before {
  content: attr(data-udata-value);
  background: #7fbf2d;
  position: absolute;
  font-size: 12px;
  top: 0;
  padding: 0px 3px;
  line-height: 20px;
  color: #333;
  left: 0;
  white-space: nowrap;
}
```

对于 Hover 图标：

```css
.data-spmd-container:hover:before {
  content: url(http://www.mjdemo.com/search.png); //搜索图标
  position: absolute;
  color: #333;
  left: 0;
  white-space: nowrap;
}
```

还可以添加图标点击事件，首先明确一点，对于 css 添加的伪元素，并不真实存在于页面元素里，所以不能直接添加点击事件 \$('.class:before')也不可能查到，不过针对于 udata 的使用情况，采用了迂回方案，即详细的图标大小是固定的，居左上角 20px \* 20px，只要监听该元素的点击范围是不是在图标范围内就可以了，js 事件如下

```js
dom.on("click", e => {
  if (e.offsetX < 20 && e.offsetY < 20) {
    //do something for udata info
    return false;
  }
});
```

# CSS Animation

CSS3 动画相关的几个属性是：transition, transform, animation；分别理解为过渡，变换，动画。transition 指过渡，就是从 a 点都 b 点，是有时间的，是连续的，一般针对常规 CSS 属性；transform 指变换，包含几个固定的属性：旋转、缩放、偏移等等，但是，效果就是很干涩机械的旋转移动，如果配合 transition 属性，变换就会很平滑。

## transition

当你的 left 属性发生变化的时候，执行动画效果（仅仅基于 left 的属性变化，其他的属性不会加入到动画变化里面去）。

```css
.position {
  left: 100px;
  top: 100px;
}

.animate {
  -webkit-transition: left 0.5s ease-out;
  left: 500px;
  top: 500px;
}
```

首先你的元素的 css 为 position。当你将其 cssList 增加 animate 或者替换 position 为 animate 的时候，元素的属性变化，触发 webkit-transition，以指定属性变化前的值为起始值，变化后的属性为结束值，执行动画效果。这是一个简单的两点变化过程，大大简化了 animation 属性的复杂程度。

```css
transition-property : _ //指定过渡的性质，比如 transition-property:backgrond 就是指 backgound 参与这个过渡
transition-duration: _//指定这个过渡的持续时间
transition-delay: _ //延迟过渡时间
transition-timing-function: _//指定过渡类型，有 ease | linear | ease-in | ease-out | ease-in-out | cubic-bezier
```

ease-in 表示先慢后快；ease-out 表示先快后慢；ease-in-out 表示先慢后快再慢，这里的 cubic-bezier 就是贝塞尔曲线，[Easing functions](https://easings.net/en#) 提供了更多的动画函数支持。

## transform

transform 指变换，即拉伸、压缩、旋转、偏移等等。

```css
.trans_skew {
  transform: skew(35deg);
}
.trans_scale {
  transform: scale(1, 0.5);
}
.trans_rotate {
  transform: rotate(45deg);
}
.trans_translate {
  transform: translate(10px, 20px);
}
```

transform 属性要可以加上 transition 的过渡特性:

```css
.trans_effect {
  transition: all 2s ease-in-out;
}
.trans_effect:hover {
  transform: rotate(720deg) scale(2, 2);
}
```

transform 属性是静态属性，一旦写到 style 里面，将会直接显示作用，无任何变化过程。transform 的主要用途是用来做元素的特殊变形，对于做设计的人来说并不是很陌生，简单的来说就是 css 的图形变形工具。关于图形变形的基础条件当中的原点设定，在 css 里面使用的是 transform-origin 来定义的。这个定义的原点应该是该 css 作用的元素的左上角为 0,0 来计算的（有待研究）。其他的属性则根据这个属性来计算进行计算。

- translate3d(x,y,z) 是用来控制元素的位置在页面上的三轴的位置的；

- rotate(deg)是用来控制元素旋转角度的；

- skew[x,y](deg) 这个属性是用来制作倾斜度的，做过设计的人可能会知道，这个是用来在 2d 里面创建 3d 透视图的时候必须的属性；

- scale3d(x,y,z) 用来放大缩小效果，属性是比值；

- matrix3d，css 矩阵。通过这个矩阵属性，涵盖了上面所有的属性值，但是个人觉得可读性极差（全都是数字和单位，背起来有点模糊），目前没有理由推荐使用。

## animation

animation 是典型的帧动画，需要指定动画一个周期持续的时间，以及动画效果的名称。

```css
@keyframes wobble {
  0% {
    left: 100px;
  }
  30% {
    left: 300px;
  }
  100% {
    left: 500px;
  }
}

.animate {
  left: 100px;
  animation: wobble 0.5s ease-out;
  animation-fill-mode: backwards;
}
```

上面这个代码展示了一个 `keyframes 'wobble'`，其中 0％ 代表在变化中不同时间点的属性值，你可以较精确的控制动画变化中任何一个时间点的属性效果。而 animation 则根据这个 keyframes 提供的属性变化方式去计算元素动画当中的属性。与 transition 不同的是，keyframes 提供更多的控制，尤其是时间轴的控制。

动画只播放一次。加入 infinite 关键字，可以让动画无限次播放:

```css
div:hover {
  animation: 1s rainbow infinite;
}

// 完整的 animation 属性
div:hover {
  animation: 1s 1s rainbow linear 3 forwards normal;
}

div:hover {
  animation-name: rainbow;
  animation-duration: 1s;
  animation-timing-function: linear;
  animation-delay: 1s;
  animation-fill-mode: forwards;
  animation-direction: normal;
  animation-iteration-count: 3;
}
```

另外在 animation 属性里面还有一个最重要的就是：animation-fill-mode，这个属性标示是以(from/0%)指定的样式还是以(to/100%)指定的样式为动画完成之后的样式。这个很方便我们控制动画的结尾样式，保证动画的整体连贯。

- none：默认值，回到动画没开始时的状态。

- forwards 表示让动画停留在结束状态

- backwards：让动画回到第一帧的状态。

- both: 根据 animation-direction 轮流应用 forwards 和 backwards 规则。

有时，动画播放过程中，会突然停止。这时，默认行为是跳回到动画的开始状态；如果想让动画保持突然终止时的状态，就要使用 animation-play-state 属性:

```css
div {
  animation: spin 1s linear infinite;
  animation-play-state: paused;
}

div:hover {
  animation-play-state: running;
}
```

# Preprocessors

## SCSS

## Less

```less
@sectionHeight: calc(~"100vh - 130px");
```

# CSS Modularization | CSS 模块化

## CSS Modules

```js
import styles from "./style.css";
// import { className } from "./style.css";

element.innerHTML = '<div class="' + styles.className + '">';
```

CSS Modules 中也支持设置全局样式：

```less
:global {
  .global-class-name {
    color: green;
  }
}
```

```css
.className {
  color: green;
  background: red;
}

// 合并其他样式类
.otherClassName {
  composes: className;
  color: yellow;
}

// 合并来自其他文件的样式
.otherClassName {
  composes: className from "./style.css";
}
```
