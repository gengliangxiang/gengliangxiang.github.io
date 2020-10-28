# ajax、axios 和 fetch

## ajax

```
$.ajax({
    type: 'POST',
    url: url,
    data: data,
    dataType: dataType,
    success: function () {},
    error: function () {}
});
```

- `ajax` 是对原生`XHR(XMLHttpRequest)`的封装，除此以外还增添了对 JSONP 的支持。多个请求之间如果有先后关系的话，就会出现回调地狱。
- 基于原生的`XHR`开发，`XHR`本身的架构不清晰。
- `JQuery`整个项目太大，单纯使用`ajax`却要引入整个`JQuery`非常的不合理（采取个性化打包的方案又不能享受 CDN 服务）

## axios

```
axios({
    method: 'post',
    url: '/user/12345',
    data: {
        firstName: 'Fred',
        lastName: 'Flintstone'
    }
})
.then(function (response) {
    console.log(response);
})
.catch(function (error) {
    console.log(error);
});
```

- 从浏览器中创建 `XMLHttpRequest`
- 支持 `Promise API`
- 客户端支持防止`CSRF`(跨站点请求伪造)
- 提供了一些并发请求的接口（重要，方便了很多的操作）
- 从 `node.js `创建 `http` 请求
- 拦截请求和响应
- 转换请求和响应数据
- 取消请求
- 自动转换`JSON`数据

## fetch

```
fetch('http://example.com/movies.json')
  .then(function(response) {
    return response.json();
  })
  .then(function(myJson) {
    console.log(myJson);
  });
```

- `fetch` 是一个底层的 `API`,只对网络请求报错，对 400，500 都当做成功的请求，需要封装去处理
- `fetch` 默认不会带 cookie，需要添加配置项`fetch(url, {credentials: 'include'})`
- `fetch` 不支持 `abort`,不支持超时控制，使用 `setTimeout` 及 `Promise.reject` 的实现的超时控制并不能阻止请求过程继续在后台运行，造成了流量的浪费
- `fetch` 没有办法原生监测请求的进度，而 `XHR` 可以
- `fetch` 中可以设置 `mode` 为`"no-cors"`（不跨域）
