# 🚀 -getting-started

Parcel 是一个web应该打包工具，不同于开发人员以前所使用的工具。它利用多核处理提供极速性能，并且是零配置。

首先用 Yarn 或者 npm 安装 Parcel:

Yarn:

`yarn global add parcel-bundler`

npm:

`npm install -g parcel-bundler`

使用以下命令在你的项目目录中新建一个 package.json 文件：

`yarn init -y`

或者

`npm init -y`

Parcel 可以使用任何类型的文件作为入口，但是最好是使用HTML或者JavaScript文件。如果你在HTML文件里使用相对路径引入你的主要JavaScript文件，Parcel 同样会处理它，并且将引用替换为输出文件的URL。

接下来，创建一个 index.html 文件和一个 index.js 文件。

```html
<html>
<body>
  <script src="./index.js"></script>
</body>
</html>
```

```JavaScript
console.log("hello world");
```

Parcel 自带一个开发服务器，当你更改文件时会自动重建你的应用，并且支持[热更新](https://github.com/Mcbai/parcel-doc/blob/master/doc/hmr.md)用于快速开发。只需要把他指向你的输入文件：

`parcel index.html`

现在在你的浏览器中打开[http://localhost:1234/](http://localhost:1234/)。你也可以使用 `-p <port number>` 选项更改默认端口。

在你没有自己的服务器或者你的应用完全是客户端渲染的时候使用开发服务器。如果你有自己的服务器，你可以以 `watch` 模式运行 Parcel。这样在文件更改时，依然会自动重建应用，并支持热更新，但不会启动 web 服务器。

`parcel watch index.html`

当你准备为生产构建应用，`build` 模式会关闭监听并且只会构建一次。查看 [Production](https://github.com/Mcbai/parcel-doc/blob/master/doc/production.md) 部分了解更多细节。