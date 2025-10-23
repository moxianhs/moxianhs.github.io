+++
date = '2025-03-11T16:46:20+08:00'
draft = true
title = 'Bpftrace and Pid'
+++

- 在 `BEGIN{}` 中获取的 pid 和 curtask->pid 没有区别，都是bpftrace的pid。
- 在 探针 中获取 pid 和 curtask-> pid 不同，pid 与 curtask->tgid 相同。

  - `[uprobe] pid == curtask->tgid`
  - `[uprobe] curtask-real_parent->pid == bpftrace_pid === bpftrace_tgid;`
