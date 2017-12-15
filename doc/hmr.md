# 🔥 模块热更新

热更新通过在运行时浏览器自动更新模块而不用刷新整个页面来提升开发体验。这意味着当你改变了一些细小的东西时，应用程序的状态会被保留。Parcel 的 HMR 实现支持对 JavaScript 和 CSS 两种资源开箱即用。在生产模式下，HMR 自动停止。

在你保存文件时，Parcel 会重新构建改变的部分并且把新代码更新到所有正在运行的客户端。然后新代码会替换掉旧的版本，并且与所有父级一起被重新计算。你可以用 `module.hot` API 接入这个处理，它能在一个模块即将被处理或者有新的代码版本时通知你。像 [react-hot-loader](https://github.com/gaearon/react-hot-loader)这样的项目可以帮助处理，并且通过 Parcel 开箱即用。

这有两种方法可以了解：`module.hot.accept` 和 `module.hot.dispose`。通过调用带有一个回调函数的 `module.hot.accept`，回调函数在模块摸着任何依赖升级时执行。`module.hot.dispose` 接收一个回调函数，回调函数当模块即将被替换时调用。

```JavaScript
if (module.hot) {
  module.hot.dispose(function () {
    // module is about to be replaced
  });

  module.hot.accept(function () {
    // module or one of its dependencies was just updated
  });
}
```