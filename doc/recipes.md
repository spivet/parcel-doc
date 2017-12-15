# 🍰 食谱

## React

首先需要为 React 安装依赖：

[Blog Post](http://blog.jakoblind.no/react-parcel/)

```
npm install --save react
npm install --save react-dom
npm install --save-dev parcel-bundler
npm install --save-dev babel-preset-env
npm install --save-dev babel-preset-react
```

或者用 Yarn
```
yarn add react
yarn add react-dom
yarn add --dev parcel-bundler
yarn add --dev babel-preset-env
yarn add --dev babel-preset-react
```

然后确保拥有下面的 Babel 配置文件。

```json
// .babelrc
{
  "presets": ["env", "react"]
}
```

在 `package.json` 中添加开始脚本：

```json
// package.json
"scripts": {
  "start": "parcel index.html"
}
```

## Preact

首先需要为 Preact 安装依赖：

```
npm install --save preact
npm install --save preact-compat
npm install --save-dev parcel-bundler
npm install --save-dev babel-preset-env
npm install --save-dev babel-preset-preact
```

或者用 Yarn
```
yarn add preact
yarn add preact-compat
yarn add --dev parcel-bundler
yarn add --dev babel-preset-env
yarn add --dev babel-preset-preact
```

然后确保拥有下面的 Babel 配置文件。

```json
// .babelrc
{
  "presets": ["env", "react"]
}
```

在 `package.json` 中添加开始脚本：

```json
// package.json
"scripts": {
  "start": "parcel index.html"
}
```