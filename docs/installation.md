---
sidebar_position: 2
---

# 安装和开发

Suika 项目本身没有发布 NPM 包。

如果你需要基于 Suika 进行二次开发，你需要克隆项目，通过直接改项目的源码的方式来开发。

> 项目目前 API 还不稳定，功能需补全，待稳定时会向外发布版本，提供 SDK。

## 环境准备

1. 安装 Git
2. 安装 Node.js。建议使用最新的 LTS 版本，另外 MacOS 用户推荐使用 nvm 安装，可以方便切换 Node.js 版本。

Node.js 自带了 NPM 包管理器，但 Suika 项目使用的是另一种包管理器 PNPM，这是为了支持 monorepo 方式的开发。

所以我们还要在全局安装 PNPM 包管理器：

```sh
npm install -g pnpm
```

## 启动项目

使用 git clone 项目：

```sh
git clone git@github.com:F-star/suika.git
```

安装依赖包：

```sh
pnpm install
```

启动项目：

```sh
pnpm dev
```

浏览器打开 `http://localhost:6167`，可以看到 Suika 项目的开发页面。

这是热更新的开发模式，当你修改代码保存时，网页会自动热更新或刷新。

## 生产构建

前面的 `pnpm dev` 是开发环境，如果要部署到生产环境，我们需要构建生产环境产物：

```sh
pnpm build
```

构建产物为 `packages/suika/build` 目录。