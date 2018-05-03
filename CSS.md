# CSS

CSS 用于控制网页的样式和布局。

CSS3 是最新的 CSS 标准。

## CSS 3模块

CSS3 被划分为模块。

其中最重要的 CSS3 模块包括：

- 选择器
- 框模型
- 背景和边框
- 文本效果
- 2D/3D 转换
- 动画
- 多列布局
- 用户界面

## 文本

| 属性                                                         | 描述                     |
| ------------------------------------------------------------ | ------------------------ |
| color     | 设置文本颜色             |
| direction | 设置文本方向。           |
| letter-spacing | 设置字符间距             |
| line-height | 设置行高                 |
| text-align | 对齐元素中的文本         |
| text-decoration | 向文本添加修饰           |
| text-indent | 缩进元素中文本的首行     |
| text-shadow | 设置文本阴影             |
| text-transform | 控制元素中的字母         |
| unicode-bidi | 设置或返回文本是否被重写 |
| vertical-align | 设置元素的垂直对齐       |
| white-space | 设置元素中空白的处理方式 |
| word-spacing | 设置字间距               |

## 盒模型

![CSS box-model](http://www.runoob.com/images/box-model.gif)

当用绝对的值设置盒子的大小时（比如，固定像素的 width 和 height），内容可能会超出设置的大小，此时内容就会溢流盒子。要控制这时候发生的事情，我们可以使用 `overflow` 属性。 该属性有几个可能的取值，不过最常用的是：

- `auto`：如果内容太多，那么溢流的内容会被隐藏，滚动条显示出来，从而可以让用户滚动看到所有内容。
- `hidden`：如果内容太多，那么溢流的内容被隐藏了。
- `visible`：如果内容太多，溢流的内容显示在盒子之外（这通常是默认的行为）。

### 设置宽和高的约束

其它一些属性可以用更灵活的方式控制内容盒的大小  —  是通过设置大小约束，而不是设置一个绝对大小。这是通过属性 [`min-width`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/min-width)、[`max-width`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/max-width)、[`min-height`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/min-height) 和 [`max-height`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/max-height) 实现的。

一个明显的用处是，如果想通过设置将一个布局的外层容器的宽度设置为百分比，从而让布局的宽度变得灵活，不过又不想让它变得太宽或者太窄，因为这样布局就开始看起来很糟糕。一个选择是用响应式网页设计技术，但是更简单的方法也许只是给布局一个最大和最小宽度约束即可：

```
width: 70%;
max-width: 1280px;
min-width: 480px;
```

您可以将这段代码与以下代码结合，可以将应用这段代码的容器在它的父容器内居中：

```
margin: 0 auto;
```

0会使顶部和底部边距为0，而auto（在这种情况下）共享父容器左右边距之间的可用空间使它居中。 最终的呈现的效果是：当父容器在最小和最大宽度限制内时，它将填满整个视口宽度；当父容器超过1280px宽度时，布局将保持在1280px宽，并开始在可用空间内居中。 当宽度低于480px时，视口将小于容器，您必须滚动才能看得到完全的内容。

## Filters（过滤器）

## Blend modes（混合模式）

这里有两个在 CSS中用到的属性:

- [`background-blend-mode`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/background-blend-mode), 用来将单个元素的多重背景图片和背景颜色设置混合在一起。
- [`mix-blend-mode`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/mix-blend-mode), 用来将一个元素与它覆盖的那些元素各自所设置的背景（background）和内容(content)混合在一起。

## Float（浮动）

float 属性有四个可能的值：

- `left` — 将元素浮动到左侧。
- `right` — 将元素浮动到右侧。
- `none` — 默认值, 不浮动。
- inherit — 继承父元素的浮动属性。

## Position（定位）

有四种主要的定位类型需要我们了解：

- **静态定位(Static positioning)**是每个元素默认的属性——它表示“将元素放在文档布局流的默认位置——没有什么特殊的地方”。
- **相对定位(Relative positioning)**允许我们相对元素在正常的文档流中的位置移动它——包括将两个元素叠放在页面上。这对于微调和精准设计(design pinpointing)非常有用。
- **绝对定位(Absolute positioning)**将元素完全从页面的正常布局流中移出，类似将它单独放在一个图层中. 我们可以将元素相对于页面的 `<html>` 元素边缘固定，或者相对于离元素最近的被定位的祖先元素(ancestor element)。绝对定位在创建复杂布局效果时非常有用，例如通过标签显示和隐藏的内容面板或者通过按钮控制滑动到屏幕中的信息面板.
- **固定定位(Fixed positioning)**与绝对定位非常类似，除了它是将一个元素相对浏览器视口固定，而不是相对另外一个元素。 在创建类似页面滚动总是处于页面上方的导航菜单时非常有用。

## Display显示

**块级元素(block)特性：**

- 总是独占一行，表现为另起一行开始，而且其后的元素也必须另起一行显示;
- 宽度(width)、高度(height)、内边距(padding)和外边距(margin)都可控制;

**内联元素(inline)特性：**

- 和相邻的内联元素在同一行;
- 宽度(width)、高度(height)、内边距的top/bottom(padding-top/padding-bottom)和外边距的top/bottom(margin-top/margin-bottom)都不可改变，就是里面文字或图片的大小;

主要用的CSS样式有以下三个：

- display:block  -- 显示为块级元素
- display:inline  -- 显示为内联元素
- display:inline-block -- 显示为内联块元素，表现为同行显示并可修改宽高内外边距等属性

## 定位

通过使用 [position 属性](http://www.w3school.com.cn/cssref/pr_class_position.asp)，我们可以选择 4 种不同类型的定位，这会影响元素框生成的方式。

position 属性值的含义：

- static

  元素框正常生成。块级元素生成一个矩形框，作为文档流的一部分，行内元素则会创建一个或多个行框，置于其父元素中。

- relative

  元素框偏移某个距离。元素仍保持其未定位前的形状，它原本所占的空间仍保留。

- absolute

  元素框从文档流完全删除，并相对于其包含块定位。包含块可能是文档中的另一个元素或者是初始包含块。元素原先在正常文档流中所占的空间会关闭，就好像元素原来不存在一样。元素定位后生成一个块级框，而不论原来它在正常流中生成何种类型的框。

- fixed

  元素框的表现类似于将 position 设置为 absolute，不过其包含块是视窗本身。

| 属性                                                         | 描述                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [position](http://www.w3school.com.cn/cssref/pr_class_position.asp) | 把元素放置到一个静态的、相对的、绝对的、或固定的位置中。     |
| [top](http://www.w3school.com.cn/cssref/pr_pos_top.asp)      | 定义了一个定位元素的上外边距边界与其包含块上边界之间的偏移。 |
| [right](http://www.w3school.com.cn/cssref/pr_pos_right.asp)  | 定义了定位元素右外边距边界与其包含块右边界之间的偏移。       |
| [bottom](http://www.w3school.com.cn/cssref/pr_pos_bottom.asp) | 定义了定位元素下外边距边界与其包含块下边界之间的偏移。       |
| [left](http://www.w3school.com.cn/cssref/pr_pos_left.asp)    | 定义了定位元素左外边距边界与其包含块左边界之间的偏移。       |
| [overflow](http://www.w3school.com.cn/cssref/pr_pos_overflow.asp) | 设置当元素的内容溢出其区域时发生的事情。                     |
| [clip](http://www.w3school.com.cn/cssref/pr_pos_clip.asp)    | 设置元素的形状。元素被剪入这个形状之中，然后显示出来。       |
| [vertical-align](http://www.w3school.com.cn/cssref/pr_pos_vertical-align.asp) | 设置元素的垂直对齐方式。                                     |
| [z-index](http://www.w3school.com.cn/cssref/pr_pos_z-index.asp) | 设置元素的堆叠顺序。                                         |

## 对齐

要水平居中对齐一个元素, 可以使用 margin: auto;。

设置到元素的宽度将防止它溢出到容器的边缘。

元素通过指定宽度，并将两边的空外边距平均分配：

如果没有设置 width 属性(或者设置 100%)，居中对齐将不起作用。

## 前缀

### **CSS3中-MS-,-MOZ-,-WEBKIT-,-O-浏览器私有前缀详解**

(1)-moz-：代表FireFox浏览器私有属性

(2)-ms-：代表IE浏览器私有属性

(3)-webkit-：代表safari、chrome浏览器私有属性

(4)-o-：代表opera浏览器私有属性

## Reference

1. [CSS教程](http://www.w3school.com.cn/css3/index.asp)