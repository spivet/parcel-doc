# ✂️ 代码分割

Parcel 支持开箱即用的零配置代码分割。这允许你把你的应用程序代码分离到不同的包以便可以按需加载，意味着包的初始化体积更小，加载时间更短。当用户访问你的应用并需要相应模块时，Parcel 会自动加载需要的子模块。

代码分割通过使用动态 `import()` 函数[语法提议](https://github.com/tc39/proposal-dynamic-import)来控制，它和普通的 `import` 或者 `require` 函数使用相似，但是返回的是一个 Promise。这意味着模块时异步加载的。

下面的例子展示了你如何使用动态导入去按需加载一个你程序里的子页面。

```JavaScript
// pages/about.js
export function render() {
  // Render the page
}
```
 
```JavaScript
import('./pages/about').then(function (page) {
  // Render page
  page.render();
});
```

因为 `import()` 返回一个 Promise，所以你也可以使用 async/await 语法。尽管你可能需要配置 Babel 来转换语法，直到它得到浏览器更广泛的支持。

```JavaScript
const page = await import('./pages/about');
// Render page
page.render();
```

动态导入在 Parcel 中同样是懒加载的，因此你仍然可以把你所有的 `import()` 调用放在你文件的最顶端，子包并不会加载它们，直到它们被用到。下面的例子向你展示了怎样动态地懒加载一个应用程序的子页面。

```JavaScript
// Setup a map of page names to dynamic imports.
// These are not loaded until they are used.
const pages = {
  about: import('./pages/about'),
  blog: import('./pages/blog')
};

async function renderPage(name) {
  // Lazily load the requested page.
  const page = await pages[name];
  return page.render();
}
```

**注意：** 如果你喜欢在没有得到支持的浏览器中使用 async/await，记住再你的应用程序里引入 `babel-polyfill` 或者 `babel-runtime` + `babel-plugin-transform-runtime` 库。

```
yarn add babel-polyfill
```

```JavaScript
import "babel-polyfill";
import "./app";
```

阅读 [babel-polyfill](http://babeljs.io/docs/usage/polyfill) 和 [babel-runtime](http://babeljs.io/docs/plugins/transform-runtime) 的文档。