+++
date = '2024-11-26T14:59:37+08:00'
title = 'Github Pages Configuration'
categories = ['技术教程']
tags = ['GitHub', '部署', '静态博客', '教程']
+++

## 流程概览

1. 在本地唰唰写。
2. push 到你的 `GitHub` 仓库。
3. GitHub Actions 自动执行 deploy 动作。
4. 部署成功访问 `<username>.github.io` 查看。

## 创建仓库

## 仓库名

在`GitHub`上创建一个名为`<username>.github.io`的仓库，比如我这个仓库就叫作：`moxianhs.github.io`，后面访问网页也是这个地址。

你当然可以选择一个其他的名字，后面的流程也都能跑通，但唯一的问题就是：如果使用其他名字命名仓库，例如`mox-blog`，后面部署完成之后，访问地址就变成了`moxianhs.github.io/mox-blog`，如果不进行额外的配置，所有的 css、js、亦或是资源文件，都将找不到正确路径。

## 主分支

注意主分支最好是`main`，主要的文件都放在这里，如果你选择用其他类似于`master`作为主分支，当然可以，注意在后面的 deploy 文件里改好对应字段。

## 配置仓库

## Action 权限

进入你的仓库，在`Settings -> Actions -> General -> Workflow permissions`处，选择 `Read and write permissions`，否则，自动化动作无法将生成页面 push 进对应分支。

## 部署

## 本地配置

### deploy.yaml

在本地创建`.github/workflows/deploy.yaml`文件。

内容大致如下：

```yaml
name: Deploy Hugo site to GitHub Pages

on:
  push:
    branches:
      - main

jobs:
  deploy:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout repository
        uses: actions/checkout@v3
        with:
          submodules: true

      - name: Setup Hugo
        uses: peaceiris/actions-hugo@v2
        with:
          hugo-version: "latest"

      - name: Build site
        run: hugo build

      - name: Deploy to GitHub Pages
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./public
```

注意`on.push.branches`的值，这里必须设置成你的主分支的名字。

### 禁用 jekyll

`GitHub Pages` 可能会默认以 `Jekyll` 的方式解析文件，即使项目是 `Hugo` 构建的。这样就会出现构建失败的问题。故需要在项目根目录生成一个`static/.nojekyll`的空文件以禁用 `jekyll` 解析。

### 本地仓库设置

1. 设置远端仓库为之前配置好的空的`GitHub`仓库。
2. 远端上游分支设置为主分支，如`main`。
3. 在本地事先测试好博客能正常运行。
4. `git add` 所有除了 `public`的文件。
5. `git push` 到远端上游即可。

## 远端配置

### Pages

`Settings -> Pages` 里在 `Branch` 处，记得检查是否已经选择好`gh-pages`作为发布分支。

以能看到
>Your GitHub Pages site is currently being built from the gh-pages branch.`
这句话为准。

## 事后

如果能在`Settings -> Pages`里看到类似:

> Your site is live at <https://moxianhs.github.io/>

那就证明部署成功了，可以直接点击路径访问，旁边也有一个`Visit site`的按键，一键直达。

如果失败，可以在仓库的`Actions`页面，看到部署的全过程，可以查看每一个步骤的日志，检查具体的失败信息，对症下药。
