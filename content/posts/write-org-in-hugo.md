+++
title = "如何在 Hugo 里写 Org"
author = ["Mox W"]
date = 2025-10-11T00:00:00+08:00
draft = false
+++

## 配置 {#配置}

我是使用 Doom Emacs 的配置，所以在添加 ox-hugo 支持方面比较简单。

```elisp
(doom!
 ;; 其他配置
 :lang
 (org +pretty
      +hugo)
 )
```

## 生成 Markdown {#生成-markdown}

直接使用 `org` 写就的文章，需要转换成 Markdown 才能被 Hugo 识别。
