# webpack基本配置

## 概述

从本文开始，我们开始探究webpack的使用。作为源远流长的传统，这里通过一个“Hello World”来介绍webpack的基本配置，通过手动配置webpack文件进行代码编译并藉此了解webpack的基础关键api和如何使用webpack实现模块化加载。

## 安装webpack

当下被大众广泛接受的前端工具都是基于nodejs环境，webpack也不例外，所以，在安装webpack工具前请先确保nodejs环境已成功安装。可参考[快速搭建 Node.js / io.js 开发环境以及加速 npm](https://fengmk2.com/blog/2014/03/node-env-and-faster-npm.html)，此处不作赘述。

nodejs环境安装完成后，使用npm包管理器安装webpack。
```shell
npm install -g webpack
```
注意：此处加上`-g`参数进行模块的全局安装，安装后的模块bin目录文件将被注册到系统全局命令并允许直接调用。若此处没有带上该参数则直接使用webpack的命令时将报无法找到的错误，需要配置npm的script命令脚本进行调用。

## 使用weebpack编译js文件

创建html文件和引用js：
```html
<!-- inde.html -->

<!DOCTYPE html>
<html>
<head>
  <title>base--demo for webpack</title>
</head>
<body>
  <script src="./index.js" charset="utf-8"></script>
</body>
</html>

```
```js
/** index.js **/
var print = function () {
  alert('Hello World!');
}

print();

```
这是一个最简单的实现提示“Hello World”弹窗的页面，接下来使用webpack将它进行编译运行。

### 默认配置

> 以下示例代码，详见`../demo/base/default`

从 webpack v4.0.0 开始，可以不用引入配置文件，使用默认配置直接执行webpack命令。而在默认配置中，webpack会在当前目录下寻找`src`文件夹，将其中的`index.js`文件编译到`dist`文件夹中，编译后的默认文件名为`main.js`。所以我们需要将`index.js`文件放入新建的`src`文件夹，并将html中对js的引用修改为：
```html
<script src="./dist/main.js" charset="utf-8"></script>
```
命令行下执行webpack命令：
```shell
$ webpack

Hash: 234423c68c3e7ca0c714
Version: webpack 4.1.0
Time: 319ms
Built at: 2018-4-23 17:37:54
  Asset       Size  Chunks             Chunk Names
main.js  566 bytes       0  [emitted]  main
Entrypoint main = main.js
   [0] ./src/index.js 63 bytes {0} [built]

WARNING in configuration
The 'mode' option has not been set. Set 'mode' option to 'development' or 'production' to enable defaults for this environment.
```
编译完成，可以看到目录下多出了一个`dist`文件夹，其中存放了`main.js`.在浏览器中打开`index.html`，得到正确结果。

此处你可能会发现，编译结束后报出一个警告。此警告是因为没有设置编译模式，暂时可不予关注。当然，对于部分强迫症患者，可以在编译时使用`--mode development`参数消除此警告。`development`代表开发环境，可换成`production`为生产环境，两者存在一些配置差异，最直观的就是可以看到生产环境配置产出的js进行了压缩，具体细节后文中会讲到，此处不作过多描述。可参考：[官网文档--模式](https://www.webpackjs.com/concepts/#%E6%A8%A1%E5%BC%8F)

### 使用自定义配置编译

我们可以根据命令行参数来修改编译的文件及路径名称，如：
```shell
webpack ./index.js --mode production --o dist1/index.js
```
执行完毕便会将当前目录下的`index.js`文件编译到`dist1`目录下的`index.js`。但是当我们的配置参数越来越多，比如输入文件、输出文件、输出路径、输出模式以及后边涉及到的别名、插件、加载器等众多参数，命令行配置的形式显然变得非常不合理。这个时候，我们就需要通过配置文件来维护和修改这些参数了。

> 以下示例代码，详见`../demo/base/custom`

在项目根目录下创建
