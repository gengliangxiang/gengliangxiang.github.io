## 文本溢出显示省略号

- 单行溢出

```
overflow:hidden;
text-overflow:ellipsis;
white-space:nowrap
```

- 多行溢出(只有-webkit 内核才有作用)

```
overflow: hidden;
text-overflow: ellipsis;
display: -webkit-box;
-webkit-line-clamp: 2;
-webkit-box-orient: vertical;
```

## css 设置鼠标事件不响应

> 子元素会继承,子元素设置`pointer-events: none;`可以去除

```
pointer-events: none;
```

## css 禁止用户选择文本

```
-webkit-touch-callout: none;
-webkit-user-select: none;
-khtml-user-select: none;
-moz-user-select: none;
-ms-user-select: none;
user-select: none;
```

## css 设置文本下划线

```
text-decoration: none // 去除a标签的下划线
text-decoration: underline  // 文本添加下划线
text-decoration: overline   // 文本顶部加线
text-decoration: line-through   // 文本中间加线
```

## 控制文字自动换行

```
word-wrap: break-word;
word-break：break-all;
```

## 取消 input 的边框

```
border: none;
outline: none;
```

## 设置 input 的 placeholder 的字体样式

```
input::-webkit-input-placeholder {    /* Chrome/Opera/Safari */
    color: red;
}
input::-moz-placeholder { /* Firefox 19+ */
    color: red;
}
input:-ms-input-placeholder { /* IE 10+ */
    color: red;
}
input:-moz-placeholder { /* Firefox 18- */
    color: red;
}
```

## css 滤镜

```
// 高斯模糊效果
.blur {
    -webkit-filter: blur(4px);
    filter: blur(4px);
}
// 使图片变亮
.brightness {
    -webkit-filter: brightness(0.30);
    filter: brightness(0.30);
}
// 调整图像的对比度
.contrast {
    -webkit-filter: contrast(180%);
    filter: contrast(180%);
}
// 图像转换为灰度图像
.grayscale {
    -webkit-filter: grayscale(100%);
    filter: grayscale(100%);
}
// 给图像应用色相旋转
.huerotate {
    -webkit-filter: hue-rotate(180deg);
    filter: hue-rotate(180deg);
}
// 反转输入图像
.invert {
    -webkit-filter: invert(100%);
    filter: invert(100%);
}
// 转化图像的透明程度
.opacity {
    -webkit-filter: opacity(50%);
    filter: opacity(50%);
}
// 转换图像饱和度
.saturate {
    -webkit-filter: saturate(7);
    filter: saturate(7);
}
// 将图像转换为深褐色
.sepia {
    -webkit-filter: sepia(100%);
    filter: sepia(100%);
}
// 给图像设置一个阴影效果
.shadow {
    -webkit-filter: drop-shadow(8px 8px 10px green);
    filter: drop-shadow(8px 8px 10px green);
}
```

##
