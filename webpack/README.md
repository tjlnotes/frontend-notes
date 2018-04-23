# webpack

## 关于

从早期的王者Browserify, Grunt，到后来赢得宝座的Gulp，以及独树一帜的fis3, 以及被称为下一代打包神器的Rollup。
自动化构建工具在前端领域技术发展过程中无疑起到了非常重要的作用，本章中将对当前打包工具中的霸者webpack进行探究。（截止写文前，尚未对rollup作研究，暂且抛开不论，后期将补充并单独列出专题进行研究。）

## 概述

作为目前最主流的模块化打包工具，webpack被vue、react、angular等各种主流框架使用来进行构建与打包。
它能将许多松散的模块按照依赖和规则打包成符合生产环境部署的前端资源，还可以将按需加载的模块进行代码分隔，等到实际需要的时候再异步加载。
通过 loader 的转换，任何形式的资源都可以视作模块，比如 CommonJs 模块、 AMD 模块、 ES6 模块、CSS、图片、 JSON、Coffeescript、 LESS 等。
因此，webpack也取代了commonjs、seajs等模块化加载库，成为了目前前端领域功能模块化分离和开发的基础。本章中暂定将对webpack作出如下探究：

1. 了解webpack基本配置，手动创建webpack配置，构建模块化引用。
2. 了解webpack的api使用方法。
3. 了解webpack中常用的插件及其配置方法。
4. 使用webpack构建项目级打包配置，预编译sass、less等样式文件，并模块化加载资源。
5. 搭建webpack开发环境服务器。
6. 使用webpack进行多页应用项目构建配置。
7. 了解webpack异步加载机制。
8. 使用webpack手动构建vue项目脚手架配置。
9. 使用webpack手动构建react项目脚手架配置。
10. 使用webpack手动构建angular项目脚手架配置。
11. 了解打包分析工具的使用，模块构建图的含义。
12. 探究加速webpack打包和优化模块拆分策略以减小包体积。

## 参考文献

- [webpack项目地址](https://github.com/webpack/webpack)
- [webpack中文网](https://www.webpackjs.com/)
