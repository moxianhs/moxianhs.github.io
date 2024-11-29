+++
date = '2024-11-29T16:01:37+08:00'
title = 'Linux虚拟机中命令行简单硬盘扩容'
+++


# 流程

## 扩容虚拟硬盘

首先在虚拟机管理中，给虚拟磁盘扩容。此处省略。

## 查看容量


启动虚拟机之后，可以查看容量：

```shell
lsblk
NAME               MAJ:MIN RM  SIZE RO TYPE MOUNTPOINTS
sda                  8:0    0  100G  0 disk
├─sda1               8:1    0    1M  0 part
├─sda2               8:2    0    1G  0 part /boot
└─sda3               8:3    0   39G  0 part
  ├─openeuler-root 253:0    0   35G  0 lvm  /
  └─openeuler-swap 253:1    0    4G  0 lvm  [SWAP]
sr0                 11:0    1 21.6G  0 rom
```

可以看到`sda`已经有了100G的大小，但是还没有应用到`sda3`上。

## 查看分区表

运行如下命令，查看分区表。

- 如果分区表类型为 GPT，直接操作即可。
- 如果是 MBR，扩展主分区可能有限制（建议转 GPT）。

```shell
sudo parted /dev/sda print

型号：ATA VMware Virtual I (scsi)
磁盘 /dev/sda：107GB
扇区大小 (逻辑/物理)：512B/512B
分区表：gpt
磁盘标志：pmbr_boot

编号  起始点  结束点  大小    文件系统  名称  标志
 1    1049kB  2097kB  1049kB                  bios_grub
 2    2097kB  1076MB  1074MB  ext4
 3    1076MB  42.9GB  41.9GB                  lvm

```

我这里是GPT，故直接下一步。

## 扩容物理卷

```shell
sudo parted /dev/sda
GNU Parted 3.6
使用 /dev/sda
欢迎使用 GNU Parted！输入 'help' 来查看命令列表。
(parted) unit MiB
(parted) print free
型号：ATA VMware Virtual I (scsi)
磁盘 /dev/sda：102400MiB
扇区大小 (逻辑/物理)：512B/512B
分区表：gpt
磁盘标志：pmbr_boot

编号  起始点    结束点     大小      文件系统  名称  标志
      0.02MiB   1.00MiB    0.98MiB   可用空间
 1    1.00MiB   2.00MiB    1.00MiB                   bios_grub
 2    2.00MiB   1026MiB    1024MiB   ext4
 3    1026MiB   40959MiB   39933MiB                  lvm
      40959MiB  102400MiB  61441MiB  可用空间

(parted) resizepart 3 100%
(parted) quit
```

命令说明：
- `unit MiB` 更改大小显示单位
- `print free` 显示包含剩余可用空间的信息
- `resizepart 3 100%` 重置编号`3`即`sda3`的大小到能够得到100%，即把所有空余空间都分配给`sda3`。

更新内核分区信息，让系统识别新的分区大小：

`sudo partprobe /dev/sda`

```shell
lsblk
NAME               MAJ:MIN RM  SIZE RO TYPE MOUNTPOINTS
sda                  8:0    0  100G  0 disk
├─sda1               8:1    0    1M  0 part
├─sda2               8:2    0    1G  0 part /boot
└─sda3               8:3    0   99G  0 part
  ├─openeuler-root 253:0    0   35G  0 lvm  /
  └─openeuler-swap 253:1    0    4G  0 lvm  [SWAP]
sr0                 11:0    1 21.6G  0 rom
```

可以看到这里，`sda3`的大小已经正确扩展了，但逻辑卷还是之前的大小。

## 扩容逻辑卷

```shell
sudo lvextend -l +100%FREE /dev/mapper/openeuler-root

Device read short 16896 bytes remaining
  Size of logical volume openeuler/root changed from 35.04 GiB (8971 extents) to 95.04 GiB (24331 extents).
  Logical volume openeuler/root successfully resized.
```
这里的 `+100%FREE` 表示使用所有可用空间。

而且需要注意，要保证命令中逻辑卷的名字需要和`lsblk`的结果中看到的一致。

```shell
lsblk
NAME               MAJ:MIN RM  SIZE RO TYPE MOUNTPOINTS
sda                  8:0    0  100G  0 disk
├─sda1               8:1    0    1M  0 part
├─sda2               8:2    0    1G  0 part /boot
└─sda3               8:3    0   99G  0 part
  ├─openeuler-root 253:0    0   95G  0 lvm  /
  └─openeuler-swap 253:1    0    4G  0 lvm  [SWAP]
sr0                 11:0    1 21.6G  0 rom
```

能看到，`openeuler-root`已经是扩容完成了。
