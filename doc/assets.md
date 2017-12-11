# 📦-getting-started

Parcel 是基于资源的。资源可以是任何文件，但是Parcel 对几种特定类型的文件有特别的支持，比如JavaScript、CSS和HTML文件。Parcel 会自动解析这些文件中引用的依赖并打包到输出文件。相似类型的资源会被分组打包输出。如果你导入一个不同类型的资源（比如，从JS中导入了一个CSS文件），它会输出一个子包并在父包里保留它的引用。这将在接下来的部分详细介绍：

## JavaScript

web打包工具最常用的文件类型是JavaScript。Parcel 支持 CommonJs 和 ES6 模块语法来导入文件。它也支持动态 `import()` 函数语法来异步加载模块，这会在 [Code Splitting](https://github.com/Mcbai/parcel-doc/blob/master/doc/code_splitting.md) 部分讨论。

```JavaScript
// Import a module using CommonJS syntax
const dep = require('./path/to/dep');

// Import a module using ES6 import syntax
import dep from './path/to/dep';
```

你也可以从 JavaScript 文件里导入非 JavaScript 资源，比如 CSS 或者甚至是图片文件。当你导入这些文件中的一个，它不会像其它打包工具内联该文件，而是和它的所有依赖一起分别打包到一个包（比如一个CSS文件）。当使用 [CSS Modules](https://github.com/css-modules/css-modules)的时候，导出的类被放置在 JavaScript 包中。其他资源类型导出一个 URL 到 JavaScript 包的输出文件中，所以你可以在你的代码中引用它们。

```JavaScript
// Import a CSS file
import './test.css';

// Import a CSS file with CSS modules
import classNames from './test.css';

// Import the URL to an image file
import imageURL from './test.png';
```

如果你想内联一个文件到JavaScript包里，而不是通过URL引用它，你可以使用Node.js的`fs.readFileSync`API来完成。URL 必须是静态解析，意思是它不能有任何变量（除了 `__dirname` 和 `__filename` ）。

## CSS

CSS资源可以从 JavaScript 或者 HTML 文件中导入，并且可以包含通过 `@import` 语法就想由 `url()` 引用图片，字体等引用的依赖。其它被 `@import` 的CSS文件被内联到同一个 CSS 包里，并且 `url()` 引用被重写为输出文件名。所有文件名都应该是相对于当前的 CSS 文件。

```css
/* Import another CSS file */
@import './other.css';

.test {
  /* Reference an image file */
  background: url('./images/background.png');
}
```

除了原生CSS，其它CSS编译语言比如LESS,SASS,和Stylus 同样也支持，并且工作方式也一样。

## HTML

HTML 资源通常是你提供给 Parcel 的入口文件，但是也可以被 JavaScript 文件引用，比如提供到其它页面的链接。脚本、样式、媒体和其他HTML文件的URL以如上所述的方式被提取并编译。HTML 中的引用被重写以便于它们链接到正确的输出文件。所有的文件名都应该是相对于当前的HTML文件。

```html
<html>
<body>
  <!-- reference an image file -->
  <img src="./images/header.png">

  <a href="./other.html">Link to another page</a>

  <!-- import a JavaScript bundle -->
  <script src="./index.js"></script>
</body>
</html>
```
