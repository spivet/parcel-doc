# 📦 Packagers

在 Parcel 中，当所有资源被处理，bundle tree 被创建后，一个 `Packager` 会将多个 `资源(Asset)` 合并到一个最终生成的输出包。Packager 是基于输出文件类型注册的，并且已经生成的资源的文件类型会被送到 packager 中去生成最后生成的输出文件。

## Packager 接口

```JavaScript
const {Packager} = require('parcel-bundler');

class MyPackager extends Packager {
  async start() {
    // 可选，写文件头部内容
    await this.dest.write(header);
  }

  async addAsset(asset) {
    // 必须。将资源写入生成文件。
    await this.dest.write(asset.generated.foo);
  }

  async end() {
    // 可选，写文件尾内部内容。
    await this.dest.end(trailer);
  }
}
```

## 注册一个 Packager

你可以用 addPackager 方法在打包工具中注册一个 packager。它接受一个文件类型及 packager 模块的所在路径用于注册。

```JavaScript
const Bundler = require('parcel-bundler');

let bundler = new Bundler('input.js');
bundler.addPackager('foo', require.resolve('./MyPackager'));
```