---
title: 新一代Vue组件库 Quasar CLI 的基本使用
tags:
  - Quasar
  - Vue
  - JavaScript
  - Node.js
categories:
  - 前端
abbrlink: d1a3df2c
date: 2021-06-23 20:15:03
---

# 前言
> Quasar, 不只是组件库。 

在使用 Vue 框架开发的过程中，我们不可避免的会使用到各种各样的UI组件库。国内比较有名的组件库有 [ElementUI](https://element.eleme.io/)（饿了么前端出品）, [Antd Vue](https://www.antdv.com/)（Ant Design的Vue实现）等等。然而对于喜欢类似 [Material Design](https://material-io.cn/) 风格的开发者们来说，这些组件库都有一些不尽人意。

尽管已出现 [Vue Material](https://vuematerial.io/) 这种 Material Design 风格的组件库，但其功能存在很大的缺失。寻寻觅觅之下，我找到了这一款组件库 —— [Quasar](http://www.quasarchs.com/)。


在提供大量美观组件的同时，Quasar 提供了一套完整的多平台构建解决方案。从SPA（单页面富应用）到桌面平台（Eletron），甚至适用于Android和iOS的移动APP（Cordova/Capacitor），只需一份代码，Quasar 就能完成全平台的构建。

完整的中文文档，全面的平台支持，大量的美观组件，活跃的开发社区（据说开发者全职维护这个项目），等什么？用它。

![Quasar 中文网首页](https://cdn.jsdelivr.net/gh/b1acksoil/blog-cdn/img/article/quasar-homepage.jpg)

---

# 安装
Quasar 有三种安装方法。
- **UMD/Standalone** - 通过CDN的方式引用，使用传统web开发模式开发
- **Vue CLI 3 插件** - 通过Vue原生CLI3插件的方式引用
- **Quasar CLI** -  Quasar团队开发的脚手架，提供了大量开箱即用的功能，可以理解为一个Vue CLI的Quasar定制版。本文着重介绍这种方式。

## 环境需求
**Node.js**: >=10  
**NPM**: >=5 或 **yarn**  
{% note warning %}
**不要使用任何高于14的Node版本。**Webpack 4不支持任何高于此版本的Node，如果不进行重大更改，Quasar无法移动到Webpack 5。但是，Quasar将在将来的版本中支持webpack5。
{% endnote %}
{% note warning %}
**不要使用非偶数的Node版本，例如13，15等等。**这些版本没有用Quasar进行测试，并且由于它们的实验性质，经常会引起问题。强烈建议始终使用Node的LTS版本。
{% endnote %}

## 安装
全局安装`@quasar/cli`
```bash
# NPM方式
$ sudo npm install -g @quasar/cli
# yarn方式
$ sudo yarn global add @quasar/cli
```

# 基本使用
## 创建项目
首先创建一个 Quasar 项目
```bash
# 'quasarapp' 可换成任何其他名字
$ quasar create quasarapp
```
创建过程中会从GitHub下载初始化模板。由于GitHub在国内访问较慢，可能会报如下错误：
```error
Quasar CLI · Failed to download repo quasarframework/quasar-starter-kit#master: read ECONNRESET
```
可以使用Gitee上的镜像仓库：
```bash
$ git clone https://gitee.com/b1acksoil/quasar-starter-kit.git
$ mkdir quasarapp && cd quasarapp
$ quasar create --kit ../quasar-starter-kit

? Generate project in current directory? Yes
```

创建过程中会提示输入配置，对于学习使用来说一路回车就好：
```bash
# 项目名称
? Project name (internal usage for dev) quasarapp

# 生产环境名称（与构建桌面及移动程序有关）
? Project product name (must start with letter if building mobile apps) Quasar A
pp

# 项目描述
? Project description A Quasar Framework app

# 作者信息
? Author Username <Email>

# CSS预处理器，根据个人喜好选择即可
? Pick your CSS preprocessor: 
❯ Sass with SCSS syntax  # SASS
  Sass with indented syntax   # SCSS
  None (the others will still be available)   # 不选择

# 项目功能选择，会自动安装对应依赖
# 空格选中，回车确认
? Check the features needed for your project: (Press <space> to select, <a> to t
oggle all, <i> to invert selection)
❯◉ ESLint (recommended)
 ◯ TypeScript
 ◯ Vuex
 ◯ Axios
 ◯ Vue-i18n

# 选择ESLint预设，若上一步未选择ESLint则不会出现
? Pick an ESLint preset: (Use arrow keys)
❯ Prettier (https://github.com/prettier/prettier) 
  Standard (https://github.com/standard/standard) 
  Airbnb (https://github.com/airbnb/javascript) 

# 询问是否现在开始安装依赖
? Continue to install project dependencies after the project has been created? (
recommended) (Use arrow keys)
❯ Yes, use Yarn (recommended)   # 使用yarn
  Yes, use NPM   # 使用NPM
  No, I will handle that myself   # 稍后自行安装
```
最后提示 `[*] Quasar Project initialization finished!` 即为安装成功。

{% note info %}
若刚刚创建项目时没有选择立即安装依赖，请记得执行`npm install`或`yarn`来安装
{% endnote %}

## 项目结构
```bash
$ tree                             
.
├── babel.config.js           # Babel相关配置
├── jsconfig.json             # JS相关配置
├── package.json              # Node包信息
├── public/                   # 静态资源，其中的文件会直接复制到生产环境目录
│   ├── favicon.ico
│   └── icons/
│       ├── favicon-128x128.png
│       ├── favicon-16x16.png
│       ├── favicon-32x32.png
│       └── favicon-96x96.png
├── quasar.conf.js            # Quasar配置文件
├── README.md                 # 自述文件
└── src/                      # 源码
    ├── App.vue               # Vue根组件
    ├── assets/               # 动态资源
    │   └── quasar-logo-vertical.svg
    ├── boot/                 # 启动文件
    ├── components            # Vue组件目录
    │   └── EssentialLink.vue
    ├── css/                  # css文件目录
    │   └── app.css
    ├── index.template.html   # 主网页模板
    ├── layouts/              # 布局
    │   └── MainLayout.vue
    ├── pages/                # 页面
    │   ├── Error404.vue
    │   └── Index.vue
    └── router/               # Vue Router
        ├── index.js
        └── routes.js
```

## 基本命令
创建好项目之后，我们在项目根目录下运行如下命令：
```bash
$ quasar dev
```
编译成功后，打开`http://localhost:8080/`，即可看到Quasar的欢迎界面。
![欢迎界面](https://cdn.jsdelivr.net/gh/b1acksoil/blog-cdn/img/article/quasar-dev.jpg)

使用`quasar dev`启动的服务器具有热重载功能，可以在修改代码后即时预览。

一段时间开发后，我们要将项目打包部署，就可以用到`quasar build`命令：
```bash
$ quasar build
```
待进度条走完，输出提示将打包好的文件放在了`./dist/spa/`目录下，来看看打包出了哪些东西：
```bash
$ tree dist/spa 
dist/spa
├── css
│   ├── app.31d6cfe0.css
│   └── vendor.7fbd9725.css
├── favicon.ico
├── fonts
│   ├── flUhRq6tzZclQEJ-Vdg-IuiaDsNa.ed0c933c.woff
│   ├── flUhRq6tzZclQEJ-Vdg-IuiaDsNcIhQ8tQ.044abb9e.woff2
│   ├── KFOkCnqEu92Fr1MmgVxIIzQ.9391e6e2.woff
│   ├── KFOlCnqEu92Fr1MmEU9fBBc-.ddd11dab.woff
│   ├── KFOlCnqEu92Fr1MmSU5fBBc-.877b9231.woff
│   ├── KFOlCnqEu92Fr1MmWUlfBBc-.0344cc3c.woff
│   ├── KFOlCnqEu92Fr1MmYUtfBBc-.b555d228.woff
│   └── KFOmCnqEu92Fr1Mu4mxM.9b78ea3b.woff
├── icons
│   ├── favicon-128x128.png
│   ├── favicon-16x16.png
│   ├── favicon-32x32.png
│   └── favicon-96x96.png
├── index.html
└── js
    ├── 193.e23a89e4.js
    ├── 430.e839a4ff.js
    ├── 717.cc2a06e8.js
    ├── app.e8070269.js
    └── vendor.69ef76f6.js
```
符合标准的Webpack打包结构，可以愉快地部署了。

# 参考
- [Quasar 中文文档](http://www.quasarchs.com/introduction-to-quasar)