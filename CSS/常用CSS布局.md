# 常用 CSS 布局

## 一、 垂直水平居中

### 1. 定位方式实现

- 1. 设置 父元素 样式
  ```
  position: relative;
  ```
- 2. 设置 子元素元素 样式
  ```
  width: 200px;
  height: 200px;
  position: absolute;
  left: 0;
  top: 0;
  right: 0;
  bottom: 0;
  margin: auto;
  ```

### 2. flex 布局实现

- 1. 设置父元素即可
  ```
  display: flex;
  justify-content: center;
  align-items: center;
  ```

### 3. CSS3 + 定位 实现

- 1. 父元素样式
  ```
  position: relative;
  width: 100%;
  height: 300px;
  background-color: bisque;
  ```
- 2. 子元素
  ```
  position: absolute;
  top: 50%;
  left: 50%;
  background-color: aqua;
  transform: translate(-50%, -50%);
  ```

### 4. 普通 CSS 实现

- 1. 父元素样式
  ```
  display: table-cell;
  width: 800px;
  height: 300px;
  background-color: bisque;
  text-align: center;
  vertical-align: middle;
  ```
- 2. 子元素
  ```
  display: inline-block;
  height: 80px;
  background-color: aqua;
  vertical-align: middle;
  ```

## 二、 两列布局 (一边定宽一边自适应)

### 1. float + margin 方式实现

- 1. HTML
  ```
  <div class="left">定宽</div>
  <div class="right">自适应</div>
  ```
- 2. CSS
  ```
  .left {
    float: left;
    width: 200px;
    height: 300px;
    line-height: 300px;
    text-align: center;
    background: red;
    color: #fff;
  }
  .right {
    margin-left: 210px;
    height: 300px;
    background: yellow;
    text-align: center;
    line-height: 300px;
  }
  ```

### 2. 定位方式实现

- 1. HTML
  ```
  <div class="box">
    <div class="left">定宽</div>
    <div class="right">自适应</div>
  </div>
  ```
- 2. CSS
  ```
  .box {
    position: relative;
  }
  .left {
    position: absolute;
    width: 200px;
    height: 300px;
    line-height: 300px;
    text-align: center;
    background: yellow;
  }
  .right {
    width: 100%;
    height: 300px;
    background: red;
    text-align: center;
    line-height: 300px;
  }
  ```

### 2. flex 布局实现

- 1. HTML
  ```
  <div class="box">
    <div class="left">定宽</div>
    <div class="right">自适应</div>
  </div>
  ```
- 2. CSS
  ```
  .box {
    display: flex;
    flex-direction: row;
    text-align: center;
    line-height: 300px;
  }
  .left {
    width: 200px;
    background: red;
  }
  .right {
    flex: 1;
    width: 200px;
    background: yellow;
  }
  ```
