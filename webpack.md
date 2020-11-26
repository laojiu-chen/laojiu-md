# webpack
## 概念 
本质上，webpack 是一个现代 JavaScript 应用程序的静态模块打包器(module bundler)。当 webpack 处理应用程序时，它会递归地构建一个依赖关系图(dependency graph)，其中包含应用程序需要的每个模块，然后将所有这些模块打包成一个或多个 bundle。

### 入口(entry) 
入口起点(entry point)指示 webpack 应该使用哪个模块，来作为构建其内部依赖图的开始。进入入口起点后，webpack 会找出有哪些模块和库是入口起点（直接和间接）依赖的。

在配置文件webpack.config.js中配置
```
module.exports = {
  entry: './path/to/my/entry/file.js'
};
```

### 出口(output)
output 属性告诉 webpack 在哪里输出它所创建的 bundles，以及如何命名这些文件，默认值为 ./dist。基本上，整个应用程序结构，都会被编译到你指定的输出路径的文件夹中。

在配置文件webpack.config.js中配置
```
const path = require('path');

module.exports = {
  entry: './path/to/my/entry/file.js',
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'my-first-webpack.bundle.js'
  }
};
```

### loader
loader 让 webpack 能够去处理那些非 JavaScript 文件（webpack 自身只理解 JavaScript）。loader 可以将所有类型的文件转换为 webpack 能够处理的有效模块，然后你就可以利用 webpack 的打包能力，对它们进行处理。

**注意，loader 能够 import 导入任何类型的模块（例如 .css 文件），这是 webpack 特有的功能，其他打包程序或任务执行器的可能并不支持。我们认为这种语言扩展是有很必要的，因为这可以使开发人员创建出更准确的依赖关系图。**

在更高层面，在 webpack 的配置中 loader 有两个目标：

1. test 属性，用于标识出应该被对应的 loader 进行转换的某个或某些文件。
2. use 属性，表示进行转换时，应该使用哪个 loader。

在配置文件webpack.config.js中配置
```
const path = require('path');

const config = {
  output: {
    filename: 'my-first-webpack.bundle.js'
  },
  module: {
    rules: [
      { test: /\.txt$/, use: 'raw-loader' }
    ]
  }
};

module.exports = config;
```
以上配置中，对一个单独的 module 对象定义了 rules 属性，里面包含两个必须属性：test 和 use。这告诉 webpack 编译器(compiler) 如下信息：
*“嘿，webpack 编译器，当你碰到「在 require()/import 语句中被解析为 '.txt' 的路径」时，在你对它打包之前，先使用 raw-loader 转换一下。”*

### 插件(plugins)
插件可以用于执行范围更广的任务。插件的范围包括，从打包优化和压缩，一直到重新定义环境中的变量。插件接口功能极其强大，可以用来处理各种各样的任务。

想要使用一个插件，你只需要 require() 它，然后把它添加到 plugins 数组中。多数插件可以通过选项(option)自定义。你也可以在一个配置文件中因为不同目的而多次使用同一个插件，这时需要通过使用 new 操作符来创建它的一个实例。

在配置文件webpack.config.js中配置
```
const HtmlWebpackPlugin = require('html-webpack-plugin'); // 通过 npm 安装
const webpack = require('webpack'); // 用于访问内置插件

const config = {
  module: {
    rules: [
      { test: /\.txt$/, use: 'raw-loader' }
    ]
  },
  plugins: [
    new HtmlWebpackPlugin({template: './src/index.html'})
  ]
};

module.exports = config;
```

### 模式
通过选择 development 或 production 之中的一个，来设置 mode 参数，你可以启用相应模式下的 webpack 内置的优化
>module.exports = {
  mode: 'production'
}

这是两个webpack打包模式，development（开发）是在程序员开发时使用，打包的适合进行后续的开发工作，而production（生产）是在为产品上线作准备的，它为打包的代码做了各种优化，如去点注释空格等。

## 入口起点(entry points)


### 单个入口（简写）语法

**用法：entry: string|Array<string>**

webpack.config.js
```
const config = {
  entry: {
    main: './path/to/my/entry/file.js'
  }
};

//下面是简写
const config = {
  entry: './path/to/my/entry/file.js'
};

module.exports = config;
```

### 对象语法

**用法：entry: {[entryChunkName: string]: string|Array<string>}**

webpack.config.js
```
const config = {
  entry: {
    app: './src/app.js',
    vendors: './src/vendors.js'
  }
};
```
### 常见场景
分离 应用程序(app) 和 第三方库(vendor) 入口
webpack.config.js
```
const config = {
  entry: {
    app: './src/app.js',
    vendors: './src/vendors.js'
  }
}
```
这是什么？从表面上看，这告诉我们 webpack 从 app.js 和 vendors.js 开始创建依赖图(dependency graph)。这些依赖图是彼此完全分离、互相独立的（每个 bundle 中都有一个 webpack 引导(bootstrap)）。这种方式比较常见于，只有一个入口起点（不包括 vendor）的单页应用程序(single page application)中。

为什么？此设置允许你使用 CommonsChunkPlugin 从「应用程序 bundle」中提取 vendor 引用(vendor reference) 到 vendor bundle，并把引用 vendor 的部分替换为 __webpack_require__() 调用。如果应用程序 bundle 中没有 vendor 代码，那么你可以在 webpack 中实现被称为长效缓存的通用模式。

### 多页面应用程序
webpack.config.js
```
const config = {
  entry: {
    pageOne: './src/pageOne/index.js',
    pageTwo: './src/pageTwo/index.js',
    pageThree: './src/pageThree/index.js'
  }
};
```

为什么？在多页应用中，（译注：每当页面跳转时）服务器将为你获取一个新的 HTML 文档。页面重新加载新文档，并且资源被重新下载。然而，这给了我们特殊的机会去做很多事：
+ 使用 CommonsChunkPlugin 为每个页面间的应用程序共享代码创建 bundle。由于入口起点增多，多页应用能够复用入口起点之间的大量代码/模块，从而可以极大地从这些技术中受益。

*根据经验：每个 HTML 文档只使用一个入口起点。*

## 输出(output)
配置 output 选项可以控制 webpack 如何向硬盘写入编译文件。注意，即使可以存在多个入口起点，但只指定一个输出配置。
### 用法(Usage)
在 webpack 中配置 output 属性的最低要求是，将它的值设置为一个对象，包括以下两点：
+ filename 用于输出文件的文件名。
+ 目标输出目录 path 的绝对路径。
webpack.config.js
```
const config = {
  output: {
    filename: 'bundle.js',
    path: '/home/proj/public/assets'
  }
};

module.exports = config;
```
此配置将一个单独的 bundle.js 文件输出到 /home/proj/public/assets 目录中。

### 多个入口起点
如果配置创建了多个单独的 "chunk"（例如，使用多个入口起点或使用像 CommonsChunkPlugin 这样的插件），则应该使用占位符(substitutions)来确保每个文件具有唯一的名称。
```
{
  entry: {
    app: './src/app.js',
    search: './src/search.js'
  },
  output: {
    filename: '[name].js',
    path: __dirname + '/dist'
  }
}

// 写入到硬盘：./dist/app.js, ./dist/search.js
```

### 高级进阶
以下是使用 CDN 和资源 hash 的复杂示例：
config.js
```
output: {
  path: "/home/proj/cdn/assets/[hash]",
  publicPath: "http://cdn.example.com/assets/[hash]/"
}
```
在编译时不知道最终输出文件的 publicPath 的情况下，publicPath 可以留空，并且在入口起点文件运行时动态设置。如果你在编译时不知道 publicPath，你可以先忽略它，并且在入口起点设置 __webpack_public_path__。
```
__webpack_public_path__ = myRuntimePublicPath

// 剩余的应用程序入口
```

## 模式(mode)
提供 mode 配置选项，告知 webpack 使用相应模式的内置优化。

### 用法
只在配置中提供 mode 选项：
```
module.exports = {
  mode: 'production'
};
```
|选项|描述|
|---|---|
|development|开发模式|
|production|生产模式|

## loader
loader 用于对模块的源代码进行转换。loader 可以使你在 import 或"加载"模块时预处理文件。因此，loader 类似于其他构建工具中“任务(task)”，并提供了处理前端构建步骤的强大方法。loader 可以将文件从不同的语言（如 TypeScript）转换为 JavaScript，或将内联图像转换为 data URL。loader 甚至允许你直接在 JavaScript 模块中 import CSS文件！

### 示例
例如，你可以使用 loader 告诉 webpack 加载 CSS 文件，或者将 TypeScript 转为 JavaScript。为此，首先安装相对应的 loader：
>npm install --save-dev css-loader
npm install --save-dev ts-loader

然后指示 webpack 对每个 .css 使用 css-loader，以及对所有 .ts 文件使用 ts-loader：

webpack.config.js
```
module.exports = {
  module: {
    rules: [
      { test: /\.css$/, use: 'css-loader' },
      { test: /\.ts$/, use: 'ts-loader' }
    ]
  }
};
```

### 使用 loader
在你的应用程序中，有三种使用 loader 的方式：

+ 配置（推荐）：在 webpack.config.js 文件中指定 loader。
+ 内联：在每个 import 语句中显式指定 loader。
+ CLI：在 shell 命令中指定它们。

**配置[Configuration]**
module.rules 允许你在 webpack 配置中指定多个 loader。 这是展示 loader 的一种简明方式，并且有助于使代码变得简洁。同时让你对各个 loader 有个全局概览：
```
  module: {
    rules: [
      {
        test: /\.css$/,
        use: [
          { loader: 'style-loader' },
          {
            loader: 'css-loader',
            options: {
              modules: true
            }
          }
        ]
      }
    ]
  }
  ```

  **内联**
  可以在 import 语句或任何等效于 "import" 的方式中指定 loader。使用 ! 将资源中的 loader 分开。分开的每个部分都相对于当前目录解析。
  >import Styles from 'style-loader!css-loader?modules!./styles.css';

  *这种方式比较麻烦不推荐使用*

  **CLI**
  你也可以通过 CLI 使用 loader：
  ```
  webpack --module-bind jade-loader --module-bind 'css=style-loader!css-loader'
  ```
  这会对 .jade 文件使用 jade-loader，对 .css 文件使用 style-loader 和 css-loader。

### loader 特性

+ loader 支持链式传递。能够对资源使用流水线(pipeline)。一组链式的 loader 将按照相反的顺序执行。loader 链中的第一个 loader 返回值给下一个 loader。在最后一个 loader， 返回 webpack 所预期的 JavaScript。
+ loader 可以是同步的，也可以是异步的。
+ loader 运行在 Node.js 中，并且能够执行任何可能的操作。
+ loader 接收查询参数。用于对 loader 传递配置。
+ loader 也能够使用 options 对象进行配置。
+ 除了使用 package.json 常见的 main 属性，还可以将普通的 npm 模块导出为 loader，做法是在 package.json 里定义一个 loader 字段。
+ 插件(plugin)可以为 loader 带来更多特性。
+ loader 能够产生额外的任意文件。
**loader 通过（loader）预处理函数，为 JavaScript 生态系统提供了更多能力。 用户现在可以更加灵活地引入细粒度逻辑，例如压缩、打包、语言翻译和其他更多。**

### 解析 loader
loader 遵循标准的模块解析。多数情况下，loader 将从模块路径（通常将模块路径认为是 npm install, node_modules）解析。

**loader 模块需要导出为一个函数**，并且使用 Node.js 兼容的 JavaScript 编写。通常使用 npm 进行管理，但是也可以将自定义 loader 作为应用程序中的文件。按照约定，loader 通常被命名为 xxx-loader（例如 json-loader）。有关详细信息，请查看 如何编写 loader？。

## 插件(plugins)
插件是 webpack 的支柱功能。webpack 自身也是构建于，你在 webpack 配置中用到的相同的插件系统之上！

插件目的在于解决 loader 无法实现的其他事。

### 剖析
webpack 插件是一个具有 apply 属性的 JavaScript 对象。apply 属性会被 webpack compiler 调用，并且 compiler 对象可在整个编译生命周期访问。

ConsoleLogOnBuildWebpackPlugin.js
```
const pluginName = 'ConsoleLogOnBuildWebpackPlugin';

class ConsoleLogOnBuildWebpackPlugin {
    apply(compiler) {
        compiler.hooks.run.tap(pluginName, compilation => {
            console.log("webpack 构建过程开始！");
        });
    }
}
```
compiler hook 的 tap 方法的第一个参数，应该是驼峰式命名的插件名称。建议为此使用一个常量，以便它可以在所有 hook 中复用。
### 用法
由于插件可以携带参数/选项，你必须在 webpack 配置中，向 plugins 属性传入 new 实例。

根据你的 webpack 用法，这里有多种方式使用插件。

### 配置
webpack.config.js
```
const HtmlWebpackPlugin = require('html-webpack-plugin'); //通过 npm 安装
const webpack = require('webpack'); //访问内置的插件
const path = require('path');

const config = {
  entry: './path/to/my/entry/file.js',
  output: {
    filename: 'my-first-webpack.bundle.js',
    path: path.resolve(__dirname, 'dist')
  },
  module: {
    rules: [
      {
        test: /\.(js|jsx)$/,
        use: 'babel-loader'
      }
    ]
  },
  plugins: [
    new webpack.optimize.UglifyJsPlugin(),
    new HtmlWebpackPlugin({template: './src/index.html'})
  ]
};

module.exports = config;
```
## 配置(configuration)
你可能已经注意到，很少有 webpack 配置看起来很完全相同。这是因为 webpack 的配置文件，是导出一个对象的 JavaScript 文件。此对象，由 webpack 根据对象定义的属性进行解析。

因为 webpack 配置是标准的 Node.js CommonJS 模块，你可以做到以下事情：

+ 通过 require(...) 导入其他文件
+ 通过 require(...) 使用 npm 的工具函数
+ 使用 JavaScript 控制流表达式，例如 ?: 操作符
+ 对常用值使用常量或变量
+ 编写并执行函数来生成部分配置

## 模块(modules)
在模块化编程中，开发者将程序分解成离散功能块(discrete chunks of functionality)，并称之为模块。

每个模块具有比完整程序更小的接触面，使得校验、调试、测试轻而易举。 精心编写的模块提供了可靠的抽象和封装界限，使得应用程序中每个模块都具有条理清楚的设计和明确的目的。

Node.js 从最一开始就支持模块化编程。然而，在 web，模块化的支持正缓慢到来。在 web 存在多种支持 JavaScript 模块化的工具，这些工具各有优势和限制。webpack 基于从这些系统获得的经验教训，并将模块的概念应用于项目中的任何文件。

### 什么是 webpack 模块
对比 Node.js 模块，webpack 模块能够以各种方式表达它们的依赖关系，几个例子如下：
+ ES2015 import 语句
+ CommonJS require() 语句
+ AMD define 和 require 语句
+ css/sass/less 文件中的 @import 语句。
+ 样式(url(...))或 HTML 文件(<img src=...>)中的图片链接(image url)

### 支持的模块类型
webpack 通过 loader 可以支持各种语言和预处理器编写模块。loader 描述了 webpack 如何处理 非 JavaScript(non-JavaScript) _模块_，并且在 bundle 中引入这些依赖。 webpack 社区已经为各种流行语言和语言处理器构建了 loader，包括：
+ CoffeeScript
+ TypeScript
+ ESNext (Babel)
+ Sass
+ Less
+ Stylus

## 模块解析(module resolution)
resolver 是一个库(library)，用于帮助找到模块的绝对路径。一个模块可以作为另一个模块的依赖模块，然后被后者引用，如下：
```
import foo from 'path/to/module'
// 或者
require('path/to/module')
```
所依赖的模块可以是来自应用程序代码或第三方的库(library)。resolver 帮助 webpack 找到 bundle 中需要引入的模块代码，这些代码在包含在每个 require/import 语句中。 当打包模块时，webpack 使用 enhanced-resolve 来解析文件路径

### webpack 中的解析规则
使用 enhanced-resolve，webpack 能够解析三种文件路径：
**绝对路径**
相对于根路径的完整路径
```
import "/home/me/file";

import "C:\\Users\\me\\file";
```

**相对路径**
就是相对于该路径的文件路径
```
import "../src/file1";
import "./file2";
```
**模块路径**
```
import "module";
import "module/lib/file";
```

模块将在 resolve.modules 中指定的所有目录内搜索。 你可以替换初始模块路径，此替换路径通过使用 resolve.alias 配置选项来创建一个别名。

一旦根据上述规则解析路径后，解析器(resolver)将检查路径是否指向文件或目录。如果路径指向一个文件：

+ 如果路径具有文件扩展名，则被直接将文件打包。
+ 否则，将使用 [resolve.extensions] 选项作为文件扩展名来解析，此选项告诉解析器在解析中能够接受哪些扩展名（例如 .js, .jsx）。

如果路径指向一个文件夹，则采取以下步骤找到具有正确扩展名的正确文件：
+ 如果文件夹中包含 package.json 文件，则按照顺序查找 resolve.mainFields 配置选项中指定的字段。并且 package.json 中的第一个这样的字段确定文件路径。
+ 如果 package.json 文件不存在或者 package.json 文件中的 main 字段没有返回一个有效路径，则按照顺序查找 resolve.mainFiles 配置选项中指定的文件名，看是否能在 import/require 目录下匹配到一个存在的文件名。
+ 文件扩展名通过 resolve.extensions 选项采用类似的方法进行解析。

### 解析 Loader(Resolving Loaders)
Loader 解析遵循与文件解析器指定的规则相同的规则。但是 resolveLoader 配置选项可以用来为 Loader 提供独立的解析规则。

### 缓存
每个文件系统访问都被缓存，以便更快触发对同一文件的多个并行或串行请求。在观察模式下，只有修改过的文件会从缓存中摘出。如果关闭观察模式，在每次编译前清理缓存。

## 依赖图(dependency graph)
任何时候，一个文件依赖于另一个文件，webpack 就把此视为文件之间有 依赖关系 。这使得 webpack 可以接收非代码资源(non-code asset)（例如图像或 web 字体），并且可以把它们作为 _依赖_ 提供给你的应用程序。

webpack 从命令行或配置文件中定义的一个模块列表开始，处理你的应用程序。 从这些 入口起点 开始，webpack 递归地构建一个 依赖图 ，这个依赖图包含着应用程序所需的每个模块，然后将所有这些模块打包为少量的 bundle - 通常只有一个 - 可由浏览器加载。

## manifest
在使用 webpack 构建的典型应用程序或站点中，有三种主要的代码类型：

+ 你或你的团队编写的源码。
+ 你的源码会依赖的任何第三方的 library 或 "vendor" 代码。
+ webpack 的 runtime 和 manifest，管理所有模块的交互。
本文将重点介绍这三个部分中的最后部分，runtime 和 manifest。

**Runtime**
如上所述，我们这里只简略地介绍一下。runtime，以及伴随的 manifest 数据，主要是指：在浏览器运行时，webpack 用来连接模块化的应用程序的所有代码。runtime 包含：在模块交互时，连接模块所需的加载和解析逻辑。包括浏览器中的已加载模块的连接，以及懒加载模块的执行逻辑。

**Manifest**
当编译器(compiler)开始执行、解析和映射应用程序时，它会保留所有模块的详细要点。这个数据集合称为 "Manifest"，当完成打包并发送到浏览器时，会在运行时通过 Manifest 来解析和加载模块。无论你选择哪种模块语法，那些 import 或 require 语句现在都已经转换为 __webpack_require__ 方法，此方法指向模块标识符(module identifier)。通过使用 manifest 中的数据，runtime 将能够查询模块标识符，检索出背后对应的模块。

## 构建目标(targets)
因为服务器和浏览器代码都可以用 JavaScript 编写，所以 webpack 提供了多种构建目标(target)，你可以在你的 webpack 配置中设置。
### 用法
要设置 target 属性，只需要在你的 webpack 配置中设置 target 的值。
>module.exports = {
  target: 'node'
};

在上面例子中，使用 node webpack 会编译为用于「类 Node.js」环境（使用 Node.js 的 require ，而不是使用任意内置模块（如 fs 或 path）来加载 chunk）。