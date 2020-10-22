# CSS 选择器笔记

## 一、 基本选择器

```
#box       id
.box       类名
div        标签选择器
*          通配符
div p      后代(所有后代)
div>p      子代(直接子元素)
div,p      并集
div.box    交集
div+p      div后面的第一个p标签(div同级)
div~p      div后面所有的p标签(div同级)
```

## 二、 CSS3 选择器

### 1. 属性选择器

```
div[title]      选中页面中带有title属性的div
div[title="aa"] 选中页面中带有title属性的div,并且title属性取值为aa

^ 开始  $ 结束 * 包含
div[title^="aa"] 选中页面中带有title属性的div,并且title属性取值以aa开始
div[title$="aa"] 选中页面中带有title属性的div,并且title属性取值以aa结尾
div[title*="aa"] 选中页面中带有title属性的div,并且title属性取值包含aa
```

### 2. 结构 伪类选择器

```
li:first-child:选中li的父盒子下面的第一个子盒子
li:last-child:选中li的父盒子下面的最后一个子盒子
li:nth-child(n):选中li的父盒子下面的第n个子盒子
li:nth-last-child(n): 从后向前选中第n个子元素

n 是从0开始正整数 0,1,2,3,4,5....  n小于1是无效的
偶数： 2n  even   奇数：2n+1 2n-1  odd
3n 所有 3 的倍数  -n+5  选中前 5 个
nth-child( -n+5)       选中前 5 个
nth-last-child(n+5)    选中最后 5 个
```

> 注意点 ： 选择是分类型，排序是不分类型的

```
<div id='e1'>
    <span id='e2'>1111</span>
    <p id='e3'>2222</p>
    <p id='e4'>3333</p>
</div>


span:nth-child(1)
p:nth-child(2)
p:nth-child(3)
```

### 3. empty 伪类

```
div:empty{border: 1px solid #000;}
仅仅当div内为空时样式才有效
```

### 4. not 排除伪类

```
div:not(.box){border: 1px solid #000;}
div中除了带有类名 .box 都具有该样式
```

### 5. target 伪类

`target伪类 表示 元素 被激活的状态 必须配合锚点使用`

```
h2:target{  /* 表示h2标签 被激活后 的状态 */
  color:red;
}
<ul class="nav">
    <li><a href="#title1">标题1</a></li>
    <li><a href="#title2">标题2</a></li>
    <li><a href="#title3">标题3</a></li>
</ul>
<!-- 点击列表可以激活状态 h2文字变红色 -->
<div class="content">
    <h2 id="title1">标题2</h2>
    <p>段落1段落1段落1段落1</p>
    <p>段落1段落1段落1段落1</p>
    <h2 id="title2">标题2</h2>
    <p>段落2段落2段落2段落2</p>
    <p>段落2段落2段落2段落2</p>
    <h2 id="title3">标题3</h2>
    <p>段落3段落3段落3段落3</p>
    <p>段落3段落3段落3段落3</p>
</div>
```

### 6. 伪元素

```
本质上使用css 模拟的 标签 效果
::before ,::after 是在标签的内部的前后分别模拟出来标签的效果
他们默认是行内元素
必须有content属性，如果内容为空 可以 content:"";

作用： 有利于seo优化 简化网页结构
```

### 7. 伪元素选择器

```
<div>
    111111111111111<br>
    111111111111111<br>
    111111111111111<br>
</div>
```

在 div 中有多行文字

```
/* 选中第一行*/
div::first-line{
  color:red;
}
/* 选中第一个字*/
div::first-letter{
  color:green;
  font-size: 30px;
  float: left; /*浮动*/
}
/* 设置选中区域的样式，通常设置背景颜色和文字颜色*/
div::selection{
  color:red;
  background:rgba(0,0,0,0.3);
  font-size: 100px;
  line-height: 200px;
}
```
