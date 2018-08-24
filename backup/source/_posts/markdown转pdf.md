---
title: markdown转pdf
toc: true
date: 2018-08-24 09:59:50
tags: [markdown, pdf]
categories: markdown
---

# Markdown 转化为 PDF 文档
------
虽说markdown文件好用, 但是毕竟比较小众, 这里介绍如何把markdown转化为pdf文档

主要思想是:
<center>
<font size = 4 color = blue>
***markdown***  -->>   ***html***      --->>    ***pdf***
<font>
</center>

------

1. <h5> markdown -> html </h5>
> 相信大家都用过atom这个编辑器吧, atom是github官方提供的编辑器, 界面友好, 功能强大, 插件丰富. [下载链接](https://atom.io/)
**使用markdown-preview插件(自带)**
打开.md文件, crtl+shift+m 打开markdown-preview, 在打开页面右键, 选择保存为 HTML (save as HTML)
<img src='/assert/markdown/toPdf/1.jpg' width=1200>
</img>
-------
2. <h5> HTML -> pdf </h5>
> 使用谷歌浏览器打开刚才生成的HTML文件, 右键选择打印(print), 就可以生成pdf了
------
