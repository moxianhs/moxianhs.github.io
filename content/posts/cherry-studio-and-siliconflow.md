+++
date = '2025-10-08T17:17:08+08:00'
title = '给完全陌生者的 Cherry Studio 和 SiliconFlow 入门指南'

categories = ['技术教程']
tags = ['AI', 'Cherry Studio', 'SiliconFlow', '教程', '工具']
+++


## 概览

通过使用 Cherry Studio ，你可以调用各种各样的大语言模型（Large Language Model）来完成你需要 AI 回答你的任何问题。

这些大模型都是各个厂商通过应用程序接口（Application Programming Interface, API）的形式提供。

你可以选择使用 OpenAI 提供的 ChatGPT 或者 Anthropic 提供的 Claude 等等，但服务受限，喜欢封号，价格昂贵是不得不考虑的问题。

你也可以选择使用开源模型服务平台，这里会用云平台提供大量的已经部署好的开源模型，可以直接调用，且价格低廉。

你经历过使用官方的 DeepSeek ，不断重复服务忙服务暂时不可用的事情吗？你有经历过使用腾讯元宝或者其他第三方部署的 DeepSeek ，发现参数量不透明性能不好不能及时更新版本吗？

使用硅基流动（SiliconFlow）这种平台就能解决这些问题。

## 硅基流动

首先在硅基流动的 [官网](https://siliconflow.cn) 里，像其他网站一样注册一个账号。

> 通过我的邀请链接注册，你和我都会获得 14 元的赠送余额，所以，拜托了：[注册链接](https://cloud.siliconflow.cn/i/40nvTwOA)

登录后，就会进入到模型广场的界面：

![playground](/img/siliconflow/playground.png)

在这里就可以知道当前有哪些模型可以供你调用。

需要注意的是，硅基流动的费用体系，分为「赠送余额」和「充值余额」：

![balance](/img/siliconflow/balance.png)

部分模型例如 Pro 开头的模型，都是只能使用充值余额的，但不带 Pro 前缀的模型，基本上都是可以使用赠送余额的。

- 「💰」图标表示的就是支持使用充值余额。
- 「🎁」图表表示的就是支持使用赠送余额。

赠送余额是注册时赠送的，完成校园认证也会给一些。

点击一个模型，就会弹出其详情页面，会展示其类型、参数量、价格等一系列信息。点击模型名后面的复制图标，可快捷复制模型名，以供调用时使用：

![detail](/img/siliconflow/detail.png)

点击在线体验，可以直接跳转到试用界面，直接尝试对应的模型，此处的使用方式就和其他服务（ChatGPT, DeepSeek） 没什么太大的区别了：

![tryit](/img/siliconflow/tryit.png)

挑选好心仪的模型（不知道怎么选，就选最新的）后，就可以进入到下一节了。

## Cherry Studio

Cherry Studio 直译就是樱桃工作室，可以在本地调用各种服务商提供的大模型服务，且所有数据都存在本地，故软件本身不会引入任何隐私风险。

打开 Cherry Studio 的 [官网](https://www.cherry-ai.com/) ，点击下载客户端即可：

![homepage](/img/cherry/homepage.png)

对于一般 Windows 系统，下载 Windows 标准版即可。

下载安装完成之后，打开 Cherry Studio ，就能得到类似以下界面：

![homepage](/img/cherry/studio.png)

点击左下角的齿轮设置图标，进入设置界面，需要配置硅基流动的 API 密钥才能愉快使用之前在硅基流动那边选好的模型。

![settings](/img/cherry/settings.png)

回到硅基流动这边，点击侧边栏的钥匙按钮，进入密钥管理的界面：

![key](/img/siliconflow/key.png)

![keylist](/img/siliconflow/keylist.png)

点击「新建 API 密钥」，输入密钥描述即可点击「新建密钥」：

![new](/img/siliconflow/new.png)

复制新的密钥：

![copy](/img/siliconflow/copy.png)

回到 Cherry Studio 这里，在设置里输出硅基流动的 API Key：

![setkey](/img/cherry/setkey.png)

点击右侧的检测按钮，在弹出页面里，随意选择一个内置的模型，点击确定，弹出「连接成功」或者密钥右侧的检测按钮变成绿色的对钩，就可以了。

还记得之间可以复制模型名吗？现在到时候了。

复制好需要的模型名，在 Cherry Studio 的硅基流动设置页面里，滚动到最下面，有个添加模型，把你复制的模型名贴进去就好啦。

![addmodel](/img/cherry/addmodel.png)

添加好，就可以回到最开始 Cherry Studio 的页面，开始一轮对话啦。

在对话页面，点击话题，就可以看到过往的聊天记录和新增话题的按钮。

其中，顶部的模型名点击之后可以切换模型，如果没有你想要的则去设置里添加：

![changemodel](/img/cherry/changemodel.png)

现在，一个可以使用的 Cherry Studio 就展现在你面前，在输入框里提一个问题，然后按下回车吧。

## 课后习题

Cherry Studio 还有很多很多按钮我没有介绍是什么，但此时已经有一个可以使用的提问系统了，所以你应该怎么做，就不用我多说了吧？

> 不知道？去问 AI 啊。
