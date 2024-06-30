---
title: '哪些工具能平替vercel的v0代码自动生成'
date: '2024/6/7'
lastmod: '2024/6/7'
tags: [技术]
draft: false
summary: 'AI写代码'
images: []
layout: PostLayout
---

# 背景介绍

随着 chatgpt 和 AI 的持续发展，相信作为紧跟潮流的程序员，或多或少已经用过了不少 AI 产品，诸如 ChatGPT、Bing、MJ 等等聊天，绘画工具

# v0 自动生成页面介绍

> 比较出名的自然是 vercel 推出的代码自动生成平台 **[v0](https://v0.dev/)**，可以从 v0 开始不断根据输入对话交互迭代生成你的页面，且可以通过命令行和 nextjs 深度集成，也能直接拷贝代码粘贴到 react 生态中

举例我们输入描述（生成一个产品页）![v0产品生产描述](https://cdn.jsdelivr.net/gh/SilverComet7/image-bed@main/blog/v0产品生产描述.png)

# 助力开发

> 通过使用 AI 技术来生成网站及部分简单页面，**可以大大减少网站提升开发效率**

以下是一些可能的应用场景

1. 快速验证方案，对还原度要求不高的项目
2. 生成代码后手动进行二次开发

# 随之而来的问题

虽然生成的代码质量稳定，但是 vercel 作为 next.js 的开发厂商，只支持 react 生态的代码，那么我们想要快速生成 vue 以及 angular 或其它框架的代码，那么有没有什么类似的工具呢？

1.  首先想到的是直接生成 vue 代码网站，类似 [vue0](https://www.vue0.dev/)
2.  或者考虑**曲线救国** react 与 vue 互转，先通过 vercel v0 生成 react 代码，再通过 react 转 vue
    参照这个思路这个转换网址或许有帮助 [转换](https://runjs.work/code-converter/vue-to-react)

## 结合

虽然一些取巧的办法能够解决上述问题，那么有没有什么网站能支持多样版本的代码生成呢？这样可以省去一些转换步骤，毕竟有时候只是想快速生成一个页面，之后还是得手动调整

目前已经有实现该想法的开源项目啦,参考 screen-to-code 二开的 [ancodeai](https://www.ancodeai.com/) 支持生成多样的代码 ![alt text](https://cdn.jsdelivr.net/gh/SilverComet7/image-bed@main/blog/多样组合选择.png)

## 设想中的特性

1. 支持不同厂商不同模型的自由选择
2. 支持不同框架 + 不同 UI 的自由选择

想法很美好，但是想让 AI 达成和需求完美结合使用离不开工程师不断的调教

# 参考资料

- https://juejin.cn/post/7316796251149090851
- https://github.com/sparrow-js/an-codeAI
