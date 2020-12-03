# 1px 问题

## CSS 媒体查询

```
.div {
  border-width: 1px;
}
/* 两倍像素下 */
@media screen and (-webkit-min-device-pixel-ratio: 2) {
  .div {
    border-width: 0.5px;
  }
}
/* 三倍像素下 */
@media screen and (-webkit-min-device-pixel-ratio: 3) {
  .div {
    border-width: 0.333333px;
  }
}

```

缺点：

- 代码量多
- 低版本 IE 不兼容

## transform

```
.div {
  width: 200%;
  transform: scale(0.5);
  transform-origin: top left;
}
```

缺点：

- 对于已经使用的伪类(如：clearfix)，可能需要多层嵌套

## box-shadow 模拟边框

```
.div {
  box-shadow: inset 0px -1px 1px -1px #c8c7cc;
}
```

缺点：

- 会有颜色渐变
