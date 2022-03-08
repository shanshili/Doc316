# 编写属于你自己的大纲

## 1. 大纲架构介绍

**此节将介绍Doc316所使用的架构，如果只想编写大纲的同学可以跳过此节。**

Doc316由基于python的Sphinx构建，其原生支持的文档为 reStructuredText 即.rst格式文件。但Markdown在日常生活中使用更加普遍，因此为了使Sphinx支持Markdown，添加了recommonmark插件。本篇介绍使用Markdown编写。但插件对于Markdown的支持还是有限，比如格式要求严格，无法支持Latex等，如果不是上传之前写好的Markdown，或者纯文本文件，否则不推荐使用Markdown编写大纲。

Doc316工程存储在Github上，每次更改完成后，由本地commit并push到[Github仓库](https://github.com/FZR95/Doc316.git)。后续将建立起基于Github的合作构建。

Doc316使用Read the Docs进行托管，将Github仓库import到该网站，并进行编译即可，由于注册为个人用户，所以网页中可能会有广告。

推荐教程：

+ [Read the Docs 从懵逼到入门](http://t.csdn.cn/t1Tlw)

## 2. 使用reStructuredText 编写

建议使用reStructuredText编写大纲，具体实例请看《使用reStructuredText 编写大纲》。

> Sphinx 是一种文档工具，它可以令人轻松的撰写出清晰且优美的文档, 由 Georg Brandl 在BSD 许可证下开发. 新版的Python文档就是由Sphinx生成的， 并且它已成为Python项目首选的文档工具,同时它对 C/C++ 项目也有很好的支持; 并计划对其它开发语言添加特殊支持。 除了写程序项目的文档之外，还可以用Sphinx写博客，其实用它来写博士论文都不在话下。 本文当然也是使用 Sphinx生成的，它采用reStructuredText! （博客首页为: [https://www.scibyte.cn/blog/zh/blog.html](https://link.zhihu.com/?target=https%3A//www.scibyte.cn/blog/zh/blog.html)) 所以，Sphinx和rst有着不可分割的关系。 可以这么理解：Sphinx是一个Python写的程序，可以使用Python写配置及插件，将rst标记的文档生成各种优美的格式。 其特性如下：
>
> 1. **「丰富的输出格式:」** 支持 HTML (包括 Windows 帮助文档), LaTeX (可以打印PDF版本), manual pages（man 文档）, 纯文本
> 2. **「完备的交叉引用:」** 语义化的标签,并可以自动化链接函数,类,引文,术语及相似的片段信息
> 3. **「明晰的分层结构:」** 可以轻松的定义文档树,并自动化链接同级/父级/下级文章
> 4. **「美观的自动索引:」** 可自动生成美观的模块索引
> 5. **「精确的语法高亮:」** 基于 Pygments 自动生成语法高亮
> 6. **「开放的扩展:」** 支持代码块的自动测试,并包含Python模块的自述文档(API docs)等
> 7. Sphinx 使用 reStructuredText 作为标记语言, 可以享有Docutils为reStructuredText提供的分析，转换等多种工具.
>
> ——引用自知乎：[Sphinx和rst在科研笔记和学术博客中的高效用法](https://zhuanlan.zhihu.com/p/143141024)

## 3.使用Markdown编写

***尽管本大纲架构已经添加了对于Markdown文件的支持，但并不支持其中的Latex（实际上Markdown本身并不要求支持Latex，但很多地方贴心地提供了支持）！因此如果不是纯文本大纲，不推荐使用Markdown。本教程是纯文本结构，也是为了推荐大家在日常其他地方使用Markdown，因此使用了Markdown提供参考。***

Doc316内的大纲使用Markdown进行编写。你可以在网页右上角点击“ Edit on GitHub”查看构成本页的.md文件。

> markdown不止是HTML的简化版，更重要的是txt的升级版、word的轻量版、笔记的最佳载体。
> 作为一种简单的格式标记语言，不同于txt的无格式，不同于HTML的复杂标记，也不同于word的鼠标调整样式。markdown通过简单的几个字符键入，就可以快捷的定义文档的样式。
> 比如在行首敲一个“#”，就把这行定义为了1级标题，并且有直观完善的着色，这样无需发布为web页面，可直接当word用。
> 掌握markdown，你可以完全抛弃txt和笔记软件的编辑器，并且在大多数场景下替代掉复杂臃肿的word。享受简洁之美、享受效率提升。
>
> ——摘自Hbuilder对md的介绍

更加详细的教程建议参考[菜鸟教程](https://www.runoob.com/markdown/md-tutorial.html)。

建议使用Typora编辑Markdown，他对下面所述插入图片所用的PicGo有专门的支持。Typora自1.0版本后开始收费，建议使用最后一个免费版本[0.11.18](https://www.jianshu.com/p/a80af3a01e1a)。[百度云盘](https://pan.baidu.com/s/19JNVF8wrxRnDnxqDEo3Vug
)，提取码：lt05。

## 3.上传Markdown内含的图片

鉴于Sphinx的静态图片只能放到根目录下的_static文件夹，这对多用户，多项目并不方便，因此需要大家将图片上传至网络，并在文件中引用网络图片链接。

建议使用PicGo配置Gitee图床，[参考链接](https://www.jianshu.com/p/26b4529dfd13)。注意Gitee要建立开源仓库，否则别人看不到图片。

使用Typora时，在偏好设置-图像中设置插入图片时自动复制到.asset文件夹，设置上传服务为PicGo，回到文档中，在图片上点击右键，上传图片，本地图片会自动替换为图床链接。

## 4. Latex

放心，你是逃不了Latex的。。。更多Latex实例请看《使用reStructuredText 编写大纲》。

[LaTeX公式手册(全网最全) ](https://www.cnblogs.com/1024th/p/11623258.html)

[Typora中利用LaTeX 插入数学公式](https://blog.csdn.net/happyday_d/article/details/83715440)

