---
title: 'vue&react 共同使用'
date: '2024/7/5'
lastmod: '2024/7/5'
tags: [技术]
draft: false
summary: '框架'
images: ['https://s2.51cto.com/oss/202309/14/66b455a846b1cfa290228375a914e97ac27556.jpg)']
layout: PostLayout
---

# 竟然可以在一个项目中混用 Vue 和 React？

React 和 Vue 是前端开发中的两大热门框架，各自都有着强大的功能和丰富的生态系统。然而，你有没有想过，在一个项目中同时使用 React 和 Vue？是的，你没有听错，可以在同一个项目中混用这两个框架！本文就来分享 3 个用于混合使用 React 和 Vue 的工具！

## Veaury

Veaury 是一个基于 React 和 Vue3 的工具库，主要用于 React 和 Vue 在一个项目中公共使用的场景，主要运用在项目迁移、技术栈融合的开发模式、跨技术栈使用第三方组件的场景。

Veaury 的特点如下：

- 同时支持 Vue3 和 React，方便在一个项目中公共使用。
- 支持同一个应用中出现的 vue 组件和 react 组件的 context 共享。
- 支持跨框架的 hooks 调用，可以在 react 组件中使用 vue 的 hooks，也可以在 vue 组件中使用 react 的 hooks。
- 可以解决 React 和 Vue 在公共使用时的代码重复、冗余的问题。
- 在一个应用中可以随意使用 React 或者 Vue 的第三方组件, 比如 antd, element-ui, vuetify。
- 提供了详细的官方文档，包括英文版和中文版。

![](https://s2.51cto.com/oss/202309/14/66b455a846b1cfa290228375a914e97ac27556.jpg)

Veaury 的文档写的非常详细，这里就不再详细介绍其使用方式了。需要注意的是，Veaury 并不支持 Vue 2，如果需要使用 Vue 2，可以使用下面要介绍的工具库。

**Github：**https://github.com/devilwjp/veaury。

## Vuera

Vuera 是一个用于在 Vue 应用中使用 React 组件的库，同时也支持在 React 应用中使用 Vue 组件。它提供了一种方便的方式，使开发人员能够在不同的框架之间无缝地使用对方的组件。

要在 Vue 应用中使用 React 组件，可以按照以下步骤使用 Vuera。

### 安装插件

安装 Vuera：使用 npm 或 yarn 在您的 Vue 项目中安装 Vuera 库。

安装依赖。

由于需要在 Vue 中使用 React 组件，所以首先需要在项目中安装 React，安装指令如下：

### 项目配置

在 babel.config.js 文件中添加以下配置即可：

接下来在项目中以插件的形式来引入并使用 vuera 库，可以在  main.js  中加入如下代码：

### 基本使用

完成上述配置之后，就可以在 Vue 项目中引入并使用 React 组件了。

React 组件代码如下：

Vue 组件代码如下：

在 Vue 项目中引入了这个 React 组件，效果如下：

![](https://s7.51cto.com/oss/202309/14/06bfa9a0531c1e751b1523a8a344223a14bea1.jpg)

可以看到，这里实现了 Vue 到 React 组件的传值，并显示在了页面上。根据右上角的 Chrome 插件显示，这个项目中既使用了 Vue 又使用了 React。

点击页面中的按钮，可以看到，数据从 React 子组件传递到了 Vue 中：

![](https://s9.51cto.com/oss/202309/14/687cace958c6440a0e79647432b12b26f59645.jpg)

这样就简单实现了 React 和 Vue 组件之间的数据通信。

### 其他使用方式

如果不想通过 Babel plugin 的方式引入的话，可以使用以下这两种方法。

#### （1）使用 wrapper 组件

#### （2）使用高阶组件的 API

在 React 项目中使用 Vue 组件也是同理，可以参考官方文档。

### 注意

Vuera 是一个比较成熟的 JavaScrip 库，但是目前已经不再维护（最近一次更新是三年前）。并且，该库不支持 Vue 3，如果想要支持 Vue 3，可以使用 Vueury。

**Github：** https://github.com/akxcv/vuera。

## #vuereact-combined

vuereact-combined 是一个用于 Vue 和 React 快捷集成的工具包，并且适合复杂的集成场景。通过这个工具，可以在任何的 Vue 和 React 项目中使用另一个类型框架的组件，并且解决了复杂的集成问题。

vuera 开辟了 Vue 和 React 融合的想法，但是 vuera 只能解决非常基础的组件融合，并且存在插槽(children)和数据变更后的渲染性能问题，因此无法用于复杂的场景以及生产环境。

vuereact-combined 将融合做到了极致，支持了大部分的 Vue 和 React 组件的功能，并且在渲染更新上使用了和 vuera 不同的思路，完美解决了渲染性能问题

![](https://s9.51cto.com/oss/202309/14/a7ce12c08cc4e193078162e6ee6abf85b7278f.jpg)

注意，该项目只支持使用 Vue 2，如果想要使用 Vue 3，可以使用上面的介绍的 Veaury。

使用 vuereact-combined 的步骤如下。

### #安装插件

在项目中安装 vuereact-combined：

### 项目配置

在 Vue 和 React 的入口文件中引入  vuereact-combined：

配置 Babel 以支持 JSX 语法和 Vue.js 的特性。安装 babel-plugin-transform-vue-jsx 和 babel-preset-react，并在.babelrc 文件中添加相应的配置：

在 webpack 配置文件中添加相应的 loader 和 plugin：

配置完毕后，就可以在 Vue 和 React 之间进行快捷的集成了。

### 基本使用

假设有一个 React 组件，它是一个简单的函数组件：

可以在 Vue 项目中引入并使用这个组件。下面是一个使用 vuereact-combined 的 Vue 文件示例：

这里，首先引入了 MyReactComponent，然后在 Vue 组件中使用它。通过将 React 组件注册为 Vue 组件，我们可以在 Vue 模板中使用它，就像使用普通的 Vue 组件一样。

这里只展示了最基本的使用方法，其他使用场景可以参考官方文档。

### 注意事项

- 在 Vue 项目中使用第三方的 React 组件：第三方的 react 组件已经是通过 babel 进行过处理，不包含 React 的 jsx。此情况下，可以直接在项目中使用 applyReactInVue 对第三方的 React 组件进行处理。
- 在 React 项目中使用第三方的 Vue 组件：第三方的 Vue 组件已经是通过 vue-loader 和 babel 进行过处理，不包含.vue 文件以及 Vue 的 jsx。此情况下，可以直接在项目中使用 applyVueInReact 对第三方的 Vue 组件进行处理。

在 React 项目中引入 Vue 组件的支持程度：

![](https://s9.51cto.com/oss/202309/14/635241840930f5b6388340d4d492036d58580a.jpg)

在 Vue 项目中引入 React 组件：

![](https://s3.51cto.com/oss/202309/14/485b2df00ed4b6206f307655b4af07b8567ebf.jpg)

**Github：** https://github.com/devilwjp/vuereact-combined。
