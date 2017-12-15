# 📝 资源类型

正如 [资源](https://github.com/Mcbai/parcel-doc/blob/master/doc/assets.md) 里描述的，Parcel 将输入的文件看作 `资源（Asset）`。资源类型被看作继承自基础 `资源` 类的子类，并实现了必须的接口，去解析、分析依赖、转换及生成代码。

因为 Parcel 在多处理器内核中并行处理资源，因此资源类型所能够实施的转换行为，会被限制为那些可以在单一时间内操作单一文件的转换行为。而那些需要操作多个文件的转换行为，则需要一个自定义的 [Packager](https://github.com/Mcbai/parcel-doc/blob/master/doc/packagers.md)。

## 资源接口

```JavaScript
const {Asset} = require('parcel-bundler');

class MyAsset extends Asset {
  type = 'foo'; // set the main output type.

  parse(code) {
    // parse code to an AST
    return ast;
  }

  pretransform() {
    // optional. transform prior to collecting dependencies.
  }

  collectDependencies() {
    // analyze dependencies
    this.addDependency('my-dep');
  }

  transform() {
    // optional. transform after collecting dependencies.
  }

  generate() {
    // code generate. you can return multiple renditions if needed.
    // results are passed to the appropriate packagers to generate final bundles.
    return {
      foo: 'my stuff here', // main output
      js: 'some javascript' // alternative rendition to be placed in JS bundle if needed
    };
  }
}
```

## 注册一个资源类型

你可以通过 `addAssetType` 方法使用打包器注册一个你自己的资源类型。它接受一个文件扩展名，以及资源类型模块的路径。它是一个路径，而非实际的对象，所以它可以被传递到 worker 进程中。

```JavaScript
const Bundler = require('parcel-bundler');

let bundler = new Bundler('input.js');
bundler.addAssetType('.ext', require.resolve('./MyAsset'));
```