+++
date = '2024-11-26T14:58:18+08:00'
title = 'Hugo Configuration'
+++

# Hugo 安装

在安装`Hugo`之前，请首先自行安装`go`和`git`到你的系统上。

## Windows

### Chocolatey

`choco install hugo-extended`

### Scoop

`scoop install hugo-extended`

### Winget

`winget install hugo-extended`

## macOS

`brew install hugo`

## Linux

### ArchLinux

`sudo pacman -S hugo`

### Ubuntu/Debian

`sudo apt install hugo`

### Fedora

`sudo dnf install hugo`

### Others

有`prebuilt`可供下载，此事于[Hugo 官网](https://gohugo.io/installation/linux/)亦有记载。

## 验证安装成功

`hugo version`
输出依据版本平台等有所不同，示例如下：

```shell
hugo v0.136.5+extended darwin/arm64 BuildDate=2024-10-24T12:26:27Z VendorInfo=brew
```

# Blowfish 安装

## CLI

`npx blowfish-tools`

or

`npm i -g blowfish-tools`

而后：

`blowfish-tools`

## Non-CLI

```shell
cd mywebsite
git init
git submodule add -b main https://github.com/nunocoracao/blowfish.git themes/blowfish
```

在项目根目录，删除由 Hugo 自动生成的 `hugo.toml`，从 `themes/blowfish/config/_default` 里复制 `hugo.toml` 到根目录。

# 开始使用 Hugo

开一个新博客：

`hugo new site <site-name>`

写一篇新文章：

`hugo new posts/<article-name>.md`

启动：

`hugo server`

启动（带草稿）：

`hugo server -D`

更多请见：[Basic usage](https://gohugo.io/getting-started/usage/)