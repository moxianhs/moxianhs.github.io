+++
date = '2024-12-23T15:18:43+08:00'

title = '简单的Gcov+Lcov使用'
+++


# Gcov + Lcov

> Gcov is a source code coverage analysis and statement-by-statement profiling tool. Gcov generates exact counts of the number of times each statement in a program is executed and annotates source code to add instrumentation. Gcov comes as a standard utility with the GNU Compiler Collection (GCC) suite.

`Gcov`是一个用来做代码覆盖率的测试工具，可以记录每一行代码的执行次数。

`Lcov`是一个可以将`Gcov`的数据转化为可以直观查看的HTML网页的工具。

## 安装

`gcov`应该已经随`gcc`安装，不需要单独安装。

`lcov` 使用各自系统的命令安装。

还有可能需要安装一下，`genhtml`。

## 修改Makefile

在需要包含进覆盖率测试的每一个单独的`Makefile`里，都加上以下这行：

```shell
CFLAGS += -g -fprofile-arcs -ftest-coverage
```

在编译入口的那个`Makefile`里，添加类似以下的内容：

```shell
gcov: $(LIB)
        gcc benchmark.c  -g -o libzstd-gcov -I./lib -I./examples -O2 -fprofile-arcs -ftest-coverage ./lib/libzstd.a
        gcc benchmark.c  -g -o libzstd-gcov.s -I./lib -I./examples -O2 -fprofile-arcs -ftest-coverage -S ./lib/libzstd.a
```
假设`benchmark.c`是此次测试的入口文件，`libzstd`是本次测试的库，主要是需要处理好依赖，虽然麻烦，但只要把报错里缺的都填上去就好了。

## 指令序列

```shell
make clean
make -j$(nproc)
make gcov
gcov libzstd-gcov
./libzstd-gcov xxx
lcov -c -d . -o libzstd-gcov.info
genhtml -o gcov-$i libzstd-gcov.info
tar -cvf gcov.tar gcov/ #这一步可选，只是打了个包
```

经过以上步骤，如果没有意外的话，就会生成一个`gcov`文件夹，在里面找到`index.html`打开，即可以看到美观的覆盖率结果，也可以点到每一个文件里去，看到每一行代码的执行次数。
