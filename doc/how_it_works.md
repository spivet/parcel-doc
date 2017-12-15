# 🛠 How It Works

Parcel 将 **资源(assets)** 树转换成 **bundles** 树。许多其它的打包工具基本上是基于 JavaScript 资源，还有附加在其上的其它格式的资源。例如，在 JS 文件中内联成字符串。 Parcel 是对文件类型无感知的，它能按你所期待的方式那样与任意类型的资源工作，且毋须配置。Parcel 的打包流程共有三个步骤。

### 1. 构建资源树（Asset Tree）

Parcel 接收单个入口资源作为输入，它可以是任意类型：一个JS文件、HTML、CSS、图片文件等。Parcel 中定义了多种不同的[资源类型](https://parceljs.org/asset_types.html)，它知道怎样处理特定的文件类型。资源被解析，依赖被提取，然后它们被转换成最终编译的形态。这个过程就创建了一个资源树。

### 2. 构建Bundle Tree

一旦资源树构建完毕，资源就会被放置在 bundle tree 中。入口资源创建一个 bundle，被动态 import() 的会创建 child bundles，这就实现了代码分割。

当不同类型的文件资源被引入，Sibling bundles 就会被创建。例如你从 JavaScript 中引入了一个 CSS 文件，那它会被放置在一个与 JavaScript 文件相对应的 sibling bundle 中。

如果一个资源被不止一个 bundle 引用，它会被提升到 bundle tree 中最近的公共祖先中，这样该资源就不会被多次打包。

### 3. 打包

在 bundle tree 被构建之后，每个 bundle 都会通过一个特定的文件 [打包器（packagers）](https://parceljs.org/packagers.html) 写到一个文件中。packagers 知道如何从每个资源中将代码合并起来，生成到最终被浏览器加载的文件中。