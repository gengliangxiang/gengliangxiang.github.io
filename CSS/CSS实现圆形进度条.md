# CSS实现圆形进度条
## 示例图
![图片描述][1]
## 结构
首先一个父级div设置相对定位，内部含有四个半圆div和一个用于遮罩的小圆div
## 实现步骤
- 先写出基本html结构
```
<div class="box">
  <div class="bg1"></div>
  <div class="bg2"></div>
  <div class="pr1"></div>
  <div class="pr2"></div>
  <div class="content"></div>
</div>
```
-  父级div和content添加样式
```
.box{
  position: relative;
}
.content {
  top: 10px;
  left: 10px;
  width: 100px;
  height: 100px;
  border-radius: 50%;
  position: absolute;
  background:red;
  z-index: 5;
}
```
当前效果：
![图片描述][2]
- 添加第一个背景半圆
```
.bg1{
  position: absolute;
  width: 60px;
  height: 120px;
  border-radius: 120px 0 0 120px;
  z-index: 3;
  background: sandybrown;
}
```
![图片描述][3]

- 添加第二个背景半圆
```
.bg2{
  left: 60px;
  position: absolute;
  width: 60px;
  height: 120px;
  border-radius: 0px 120px 120px 0;
  z-index: 1;
  background: sandybrown;
}
```
![图片描述][4]

- 添加第一个进度半圆，这个时候，去页面调整rotate的角度可以看到进度旋转
```
.pr1 {
  position: absolute;
  left: 60px;
  width: 60px;
  height: 120px;
  border-radius: 0px 120px 120px 0px;
  z-index: 2;
  background: forestgreen;
  transform: rotate(-180deg);
  transform-origin: 0px 60px;
}
```
![图片描述][5]

- 添加第二个半圆，第一个半圆只能旋转到50%，所以需要第二个半圆来走完剩下的一半
```
.pr2 {
  position: absolute;
  left: 60px;
  border-radius: 0px 120px 120px 0px;
  z-index: 4;
  background: forestgreen;
  transform: rotate(-180deg);
  transform-origin: 0px 60px;
}
```
- 添加动画函数，在分别把动画函数添加到.pr1和.pr2中，在实际需求中可以用js控制连个进度半圆的旋转角度


```
.pr1 {
...
animation: pr1A 5s infinite linear forwards;
}
.pr2 {
...
animation: pr2A 5s infinite linear forwards;
}
@keyframes pr1A {
  0% {
    transform: rotate(-180deg);
  }
  50% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(0deg);
  }
}
@keyframes pr2A {
  0% {
    transform: rotate(-180deg);
  }
  100%{
    width: 60px;
    height: 120px;
    transform: rotate(180deg);
  }
}
```
以上完成


  [1]: /img/bVbxYOu
  [2]: /img/bVbxYQc
  [3]: /img/bVbxYQl
  [4]: /img/bVbxYQq
  [5]: /img/bVbxYSd