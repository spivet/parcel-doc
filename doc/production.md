# ✨ 生产

当需要为生产环境打包应用程序时，你可以使用 Parcel 的生产模式。

```
parcel build entry.js
```

这会使监听模式和热更新失效，所以它只会构建一次。它还支持压缩所有输出包以减小文件体积。Parcel 使用的压缩器分别是处理JavaScript的 [uglify-es](https://github.com/mishoo/UglifyJS2/tree/harmony)，处理 CSS 的 [cssnano ](http://cssnano.co/) 和 处理 HTML 的[htmlnano](https://github.com/posthtml/htmlnano).

启动生产模式还会设置环境变量 `NODE_ENV=production`。像 React 这种拥有仅开发环境的大型库，只有调试功能通过设置环境变量被禁用，从而让生产更小更快。

### 选项

#### 设置输出目录

默认：“dist”

```
parcel build entry.js --out-dir build/output
or
parcel build entry.js -d build/output
```

```
root
- build
- - output
- - - entry.js
```

#### 设置公共存储路劲

默认：--out-dir option

```
parcel build entry.js --public-url ./
```

输出：

```HTML
<link rel="stylesheet" type="text/css" href="1a2b3c4d.css">
or
<script src="e5f6g7h8.js"></script>
```

#### 禁止压缩

默认：minification enabled

```
parcel build entry.js --no-minify
```

#### 禁止文件系统缓存

默认：cache enabled

```
parcel build entry.js --no-cache
```