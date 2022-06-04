# 编写属于你自己的大纲

## 1. 大纲架构介绍

**此节将介绍Doc316所使用的架构，如果只想编写大纲的同学可以跳过此节。**

Doc316由基于python的Read the Docs构建，其支持的文档为Markdown格式。

Doc316工程存储在Github上，每次更改完成后，由本地commit并push到[Github仓库](https://github.com/FZR95/Doc316.git)。后续将建立起基于Github的合作构建。

Doc316使用Read the Docs进行托管，将Github仓库import到该网站，并进行编译即可，由于注册为个人用户，所以网页中可能会有广告。

推荐教程：

+ [Read the Docs 从懵逼到入门](http://t.csdn.cn/t1Tlw)

## 2.Markdown介绍

> markdown不止是HTML的简化版，更重要的是txt的升级版、word的轻量版、笔记的最佳载体。
> 作为一种简单的格式标记语言，不同于txt的无格式，不同于HTML的复杂标记，也不同于word的鼠标调整样式。markdown通过简单的几个字符键入，就可以快捷的定义文档的样式。
> 比如在行首敲一个“#”，就把这行定义为了1级标题，并且有直观完善的着色，这样无需发布为web页面，可直接当word用。
> 掌握markdown，你可以完全抛弃txt和笔记软件的编辑器，并且在大多数场景下替代掉复杂臃肿的word。享受简洁之美、享受效率提升。
>
> ——摘自Hbuilder对md的介绍

更加详细的教程建议参考[菜鸟教程](https://www.runoob.com/markdown/md-tutorial.html)。

建议使用Typora编辑Markdown，他对下面所述插入图片所用的PicGo有专门的支持。Typora自1.0版本后开始收费，建议使用最后一个免费版本[0.11.18](https://www.jianshu.com/p/a80af3a01e1a)。[百度云盘](https://pan.baidu.com/s/19JNVF8wrxRnDnxqDEo3Vug
)，提取码：lt05。

## 3.MkDocs
本网站文档框架为[Material for Mkdocs](https://squidfunk.github.io/mkdocs-material/reference/)，其在原生Markdown的基础上增加了许多扩展。 

## 3.上传Markdown内含的图片

+ 可以将图片上传至网络，并在文件中引用网络图片链接，建议使用PicGo配置SM.MS图床。使用Typora时，在偏好设置-图像中设置插入图片时自动复制到.asset文件夹，设置上传服务为PicGo，回到文档中，在图片上点击右键，上传图片，本地图片会自动替换为图床链接。
+ 可以将图片存在相对目录文件夹，在使用Typora插入图片时，可设置为“复制图片到./{$filename}.assets文件夹”。

## 5. Latex

使用Latex易于编写公式。

[LaTeX公式手册(全网最全) ](https://www.cnblogs.com/1024th/p/11623258.html)

[Typora中利用LaTeX 插入数学公式](https://blog.csdn.net/happyday_d/article/details/83715440)

Latex示例（通过源码查看）：

1. 内联Latex：$a^2+b^2=c^2$

2. Latex块：

$$  
H(s)=\frac{Y(s)}{X(s)}=\dot{A_u}=\frac{\dot{U_o}}{\dot{U_i}} 
$$

跟多Latex示例可以看其他板块。
