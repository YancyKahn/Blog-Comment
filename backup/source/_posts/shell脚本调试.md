---
title: shell脚本调试
toc: true
date: 2018-08-24 09:42:08
tags: [debugging, shell]
categories: debugging
---

# Shell 脚本调试方法
我们在使用 **Unix-like** 系统时, shell编程是必不可少的, 在编写shell脚本的时候也不可避免会产生bug, 所以我们就需要学习shell脚本的调试方法.
1. 直接调试
> 何为直接调试, 相信大家在编写c/c++程序调试时候都经常会在程序中加一个 ***printf*** 用来输出中间值达到调试的效果. 当然, 在shell脚本调试的时候这种方式也是同样适用的, 我们在程序中添加 ***echo*** 达到输出中间值的效果, 这里就不做过多的赘述.
如下面这个脚本

    ```
    #!/bin/sh
    mkdir file_dir
    cd file_dir
    for ((i=0;i<10;i++))
    do
        file_name=file_$i.txt
        touch $file_name
        echo $file_name
    done
    ```
    >echo 输出文件名
    <img src='/assert/debug/shell/1.jpg' width=1200>
 <br>
2. 使用 Shell 脚本调试命令调试
