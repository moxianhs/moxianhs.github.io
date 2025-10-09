+++
date = '2025-10-09T10:59:15+08:00'
draft = false
title = '离线环境下使用 everthing 版本 ISO 安装 openEuler 系统并换源'
+++


# 安装

如正常安装 openEuler 一样安装。

# 换源

先找到设备号

```bash
lsblk # 在结果里找到 TYPE 为 rom 的设备，看看大小对不对
```

假设是 `/dev/sr0` （大概率是这个）

挂载：

```bash
mkdir -p /mnt/everything

mount /dev/sr0 /mnt/everything
```


测试一下：

```bash
yum clean all
yum makecache
yum install vim
```

不出意外应该就能装了
