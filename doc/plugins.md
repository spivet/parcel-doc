# 🔌 插件

Parcel 采用与许多其它工具稍微不同的策略，许多常见的格式都被开箱即用地包含进来，而不需要安装或者配置额外的插件。然而，有些情况你可能想用一个非标准的方式去扩展 Parcel，而那些时候，插件是被支持的。安装的插件会基于 package.json 的依赖被自动检测并加载。

当给 Parcel 添加一种新的文件格式，你应该先考虑它会有多通用，还有它的实现会有多标准化。如果它足够通用及标准，该格式很或许应该被添加到 Parcel 的核心，而不是作为一种用户需要安装的插件。如果你有任何其它疑问，[GitHub](https://github.com/parcel-bundler/parcel/issues) 是一个讨论的好地方。

## 插件 API

Parcel 插件很简单。它们只是简单地将几个模块导出成一个函数，它会被 Parcel 在初始化的时候自动调用。函数接收 `Bundler` 对象作为输入，也可以编写一些像注册资源类型和 packager 的配置。

```JavaScript
module.exports = function (bundler) {
  bundler.addAssetType('ext', require.resolve('./MyAsset'));
  bundler.addPackager('foo', require.resolve('./MyPackager'));
};
```
使用 parcel-plugin-` 前缀把这个包发布到 npm，它会如下文描述的那样被自动检测和加载。

## 使用插件

在 Parcel 中使用插件是前所未有地简单。你所做的，只是将它们安装好并保存到 `package.json` 中。插件需要以 `parcel-plugin-` 作为前缀被命名。例如 `parcel-plugin-foo`。任何在 `package.json` 中被列出的带有此前缀的依赖，都会在初始化的时候被自动加载。