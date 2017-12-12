# 🐠-转译

Parcel 支持许多常见的编译，还内置了开箱即用的编译器，尽管许多打包工具都要求你安装和配置插件来编译资源。你可以用 [Babel](https://babeljs.io/) 编译 JavaScript，用 [PostCss](http://postcss.org/) 编译CSS，用 [PostHTML](https://github.com/posthtml/posthtml) 编译HTML。 Parcel 会自动执行这些编译当它在模块中发现相关的配置文件时（比如 `.babelrc`,`.postcssrc`）。

它甚至能再第三方 `node_modules` 中运行：如果配置文件被作为包的一部分一起发布，则编译会自动为该模块开启。打包能够迅速完成，因为只有模块需要被编译才会被处理。这也意味着你不需要手动配置转换来包含和排除某些文件，或者知道为了在你的应用中使用它，第三方代码是如何内置的。

## Babel

[Babel](https://babeljs.io/) 是一个流行的 JavaScript 编译器，有着大量的插件生态系统。在 Parcel 中使用 Babel， 与单独使用或与其他打包工具配合使用 Babel 的方式相同。

在你的应用中安装预设和插件：

`yarn add babel-preset-env`

然后创建一个 `.babelrc` 文件：

```json
{
  "presets": ["env"]
}
```

## PostCSS

[PostCss](http://postcss.org/) 是一个用插件编译 CSS 的工具，比如 [autoprefixer](https://github.com/postcss/autoprefixer), [cssnext](http://cssnext.io/), 和 [CSS Modules](https://github.com/css-modules/css-modules)。你可以通过使用这些名字：`.postcssrc (JSON)`, `.postcssrc.js`, `postcss.config.js` 中的一个创建一份配置文件，以便用 Parcel 配置 PostCSS。

在你的应用中安装插件：

`yarn add postcss-modules autoprefixer`

然后新建一个 `.postcssrc` 文件：

```json
{
  "modules": true,
  "plugins": {
    "autoprefixer": {
      "grid": true
    }
  }
}
```

插件在 `plugins` 对象中作为键值被指定，并且用对象值定义选项。如果没有给插件设定选项，则默认为 `true`。

Autoprefixer ， cssnext 和其他工具的目标浏览器可以在 `.browserslistrc` 文件中指定：

```json
> 1%
last 2 versions
```

CSS Modules 使用顶级 `modules` 键启用稍有不同。这是因为包需要对CSS模块有特殊的支持，因为它们也要导出一个对象，将其包含在JavaScript包中。注意，你需要在你的项目中安装 `postcss-modules`。

## PostHTML

[PostHTML](https://github.com/posthtml/posthtml) 是一个用插件编译 HTML 的工具。你可以通过使用这些名字：`.posthtmlrc (JSON)`, `.posthtmlrc.js`, `posthtml.config.js` 中的一个创建一份配置文件，以便用 Parcel 配置 PostCSS。

在你的应用中安装插件：

`yarn add posthtml-img-autosize`

然后新建一个 `.posthtmlrc` 文件：

```json
{
  "plugins": {
    "posthtml-img-autosize": {
      "root": "./images"
    }
  }
}
```

插件在 `plugins` 对象中作为键值被指定，并且用对象值定义选项。如果没有给插件设定选项，则默认为 `true`。