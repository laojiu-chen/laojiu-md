## ssr服务器端渲染

### 介绍
什么是服务器端渲染：Vue.js 是构建客户端应用程序的框架。默认情况下，可以在浏览器中输出 Vue 组件，进行生成 DOM 和操作 DOM。然而，也可以将同一个组件渲染为服务器端的 HTML 字符串，将它们直接发送到浏览器，最后将这些静态标记"激活"为客户端上完全可交互的应用程序。


为什么使用服务器端渲染 (SSR)？
与传统 SPA (单页应用程序 (Single-Page Application)) 相比，服务器端渲染 (SSR) 的优势主要在于：
1. 更好的SEO,由于搜索引擎爬虫抓取工具可以直接查看完全渲染的页面.
2. 更快的内容到达时间 (time-to-content)，特别是对于缓慢的网络情况或运行缓慢的设备。无需等待所有的 JavaScript 都完成下载并执行，才显示服务器渲染的标记，所以你的用户将会更快速地看到完整渲染的页面。通常可以产生更好的用户体验，并且对于那些「内容到达时间(time-to-content) 与转化率直接相关」的应用程序而言，服务器端渲染 (SSR) 至关重要。
3. 开发条件所限。浏览器特定的代码，只能在某些生命周期钩子函数 (lifecycle hook) 中使用；一些外部扩展库 (external library) 可能需要特殊处理，才能在服务器渲染应用程序中运行。
4. 涉及构建设置和部署的更多要求。与可以部署在任何静态文件服务器上的完全静态单页面应用程序 (SPA) 不同，服务器渲染应用程序，需要处于 Node.js server 运行环境。
5. 更多的服务器端负载。在 Node.js 中渲染完整的应用程序，显然会比仅仅提供静态文件的 server 更加大量占用 CPU 资源 (CPU-intensive - CPU 密集)，因此如果你预料在高流量环境 (high traffic) 下使用，请准备相应的服务器负载，并明智地采用缓存策略。

### 基本用法
**安装**
>npm install vue vue-server-renderer --save

注意:
+ 推荐使用 Node.js 版本 6+。
+ vue-server-renderer 和 vue 必须匹配版本。
+ vue-server-renderer 依赖一些 Node.js 原生模块，因此只能在 Node.js 中使用。我们可能会提供一个更简单的构建，可以在将来在其他「JavaScript 运行时(runtime)」运行。

**渲染一个vue实例**
```js
// 第 1 步：创建一个 Vue 实例
const Vue = require('vue')
const app = new Vue({
  template: `<div>Hello World</div>`
})

// 第 2 步：创建一个 renderer
const renderer = require('vue-server-renderer').createRenderer()

// 第 3 步：将 Vue 实例渲染为 HTML
renderer.renderToString(app, (err, html) => {
  if (err) throw err
  console.log(html)
  // => <div data-server-rendered="true">Hello World</div>
})

// 在 2.5.0+，如果没有传入回调函数，则会返回 Promise：
renderer.renderToString(app).then(html => {
  console.log(html)
}).catch(err => {
  console.error(err)
})
```
**与服务器集成**

```js
const Vue = require('vue')
const server = require('express')()
const renderer = require('vue-server-renderer').createRenderer()

server.get('*', (req, res) => {
  const app = new Vue({
    data: {
      url: req.url
    },
    template: `<div>访问的 URL 是： {{ url }}</div>`
  })

  renderer.renderToString(app, (err, html) => {
    if (err) {
      res.status(500).end('Internal Server Error')
      return
    }
    res.end(`
      <!DOCTYPE html>
      <html lang="en">
        <head><title>Hello</title></head>
        <body>${html}</body>
      </html>
    `)
  })
})

server.listen(8080)
```

**使用一个页面模板**

当你在渲染 Vue 应用程序时，renderer 只从应用程序生成 HTML 标记 (markup)。在这个示例中，我们必须用一个额外的 HTML 页面包裹容器，来包裹生成的 HTML 标记。

为了简化这些，你可以直接在创建 renderer 时提供一个页面模板。多数时候，我们会将页面模板放在特有的文件中，例如 index.template.html：

```html
<!DOCTYPE html>
<html lang="en">
  <head><title>Hello</title></head>
  <body>
    <!--vue-ssr-outlet-->
  </body>
</html>
```
注意 <!--vue-ssr-outlet--> 注释 -- 这里将是应用程序 HTML 标记注入的地方。
然后，我们可以读取和传输文件到 Vue renderer 中：
```js
const renderer = require('vue-server-renderer').createRenderer({
  template: require('fs').readFileSync('./index.template.html', 'utf-8')
})

renderer.renderToString(app, (err, html) => {
  console.log(html) // html 将是注入应用程序内容的完整页面
})
```

**模板插值**
模板还支持简单插值。给定如下模板：
```html
<html>
  <head>
    <!-- 使用双花括号(double-mustache)进行 HTML 转义插值(HTML-escaped interpolation) -->
    <title>{{ title }}</title>

    <!-- 使用三花括号(triple-mustache)进行 HTML 不转义插值(non-HTML-escaped interpolation) -->
    {{{ meta }}}
  </head>
  <body>
    <!--vue-ssr-outlet-->
  </body>
</html>
```

我们可以通过传入一个"渲染上下文对象"，作为 renderToString 函数的第二个参数，来提供插值数据：
```js
const context = {
  title: 'hello',
  meta: `
    <meta ...>
    <meta ...>
  `
}

renderer.renderToString(app, context, (err, html) => {
  // 页面 title 将会是 "Hello"
  // meta 标签也会注入
})
```
模板支持一些高级特性，例如：

+ 在使用 *.vue 组件时，自动注入「关键的 CSS(critical CSS)」；
+ 在使用 clientManifest 时，自动注入「资源链接(asset links)和资源预加载提示(resource hints)」；
+ 在嵌入 Vuex 状态进行客户端融合(client-side hydration)时，自动注入以及 XSS 防御。

**完整实例代码**
```js
const Vue = require('vue');
const server = require('express')();

const template = require('fs').readFileSync('./index.template.html', 'utf-8');

const renderer = require('vue-server-renderer').createRenderer({
  template,
});

const context = {
    title: 'vue ssr',
    metas: `
        <meta name="keyword" content="vue,ssr">
        <meta name="description" content="vue srr demo">
    `,
};

server.get('*', (req, res) => {
  const app = new Vue({
    data: {
      url: req.url
    },
    template: `<div>访问的 URL 是： {{ url }}</div>`,
  });

  renderer
  .renderToString(app, context, (err, html) => {
    console.log(html);
    if (err) {
      res.status(500).end('Internal Server Error')
      return;
    }
    res.end(html);
  });
})

server.listen(8080);
```

