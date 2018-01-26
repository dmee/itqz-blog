---
title: Flex弹性盒子模型布局
tags: 
    - CSS
    - Flex
category: CSS
date: 2018-01-26 17:04:43
---

# 容器的属性
## 1、display
 - flex
 - inline-flex
 
> 注意： 设为 Flex 布局以后，子元素的float、clear和vertical-align属性将失效。


## 2、flex-direction
### 属性决定主轴的方向（即项目的排列方向）：

 - row（默认值）：主轴为水平方向，起点在左端。
 - row-reverse：主轴为水平方向，起点在右端。
 - column：主轴为垂直方向，起点在上沿。
 - column-reverse：主轴为垂直方向，起点在下沿。

## 3、flex-wrap
 - nowrap：不换行
 - wrap：换行，新行在下方
 - wrap-reverse：换行，新行在上方

## 4、flex-flow
> 是 *flex-direction*属性和*flex-wrap*属性的简写形式，默认值为*row nowrap*

## 5、justify-content
> 定义了项目在主轴上的对齐方式

 - flex-start（默认值）：左对齐
 - flex-end：右对齐
 - center： 居中
 - space-between：两端对齐，项目之间的间隔都相等。
 - space-around：每个项目两侧的间隔相等。所以，项目之间的间隔比项目与边框的间隔大一倍。

![](/static/images/css/flex/justify-content.png)
## 6、align-items
>定义项目在交叉轴上如何对齐

 - flex-start：交叉轴的起点对齐。
 - flex-end：交叉轴的终点对齐。
 - center：交叉轴的中点对齐。
 - baseline: 项目的第一行文字的基线对齐。
 - stretch（默认值）：如果项目未设置高度或设为auto，将占满整个容器的高度

![](/static/images/css/flex/align-items.png)

## 7、align-content
 > 定义了多根轴线的对齐方式。如果项目只有一根轴线，该属性不起作用
 
 - flex-start：与交叉轴的起点对齐。
 - flex-end：与交叉轴的终点对齐。
 - center：与交叉轴的中点对齐。
 - space-between：与交叉轴两端对齐，轴线之间的间隔平均分布。
 - space-around：每根轴线两侧的间隔都相等。所以，轴线之间的间隔比轴线与边框的间隔大一倍。
 - stretch（默认值）：轴线占满整个交叉轴。

![](/static/images/css/flex/align-content.png)
# 项目的属性
## 1、order
> 定义项目的排列顺序。数值越小，排列越靠前，默认为0
## 2、flex-grow
> 定义项目的放大比例，默认为0，即如果存在剩余空间，也不放大

## 3、flex-shrink
> 定义了项目的缩小比例，默认为1，即如果空间不足，该项目将缩小。
## 4、flex-basis
> 定义了在分配多余空间之前，项目占据的主轴空间（main size）。浏览器根据这个属性，计算主轴是否有多余空间。它的默认值为auto，即项目的本来大小。

```css
.item {
  flex-basis: <length> | auto; /* default auto */
}
```
## 5、flex
> 是flex-grow, flex-shrink 和 flex-basis的简写，默认值为0 1 auto。后两个属性可选

```css
.item {
  flex: none | [ <'flex-grow'> <'flex-shrink'>? || <'flex-basis'> ]
}
```

## 6、align-self
> 允许单个项目有与其他项目不一样的对齐方式，可覆盖align-items属性。默认值为auto，表示继承父元素的align-items属性，如果没有父元素，则等同于stretch。
```css
.item {
  align-self: auto | flex-start | flex-end | center | baseline | stretch;
}
```
![](/static/images/css/flex/align-self.png)
 