# GitHub

## 工作流

你的本地仓库由 git 维护的三棵"树"组成。第一个是你的 工作目录，它持有实际文件；第二个是 暂存区（Index），它像个缓存区域，临时保存你的改动；最后是 HEAD，它指向你最后一次提交的结果。

•-add将工作目录添加到暂存区

•-commit将改动提交

•-push将最后一次提交改动推送到远端仓库

![image-20220324144958400](https://gitee.com/FZR95/pic316/raw/master/image-20220324144958400.png)

## 远端

•-clone将远端服务器仓库克隆到本地

•-fetch获取远端改动历史（记录）

•-pull将远端改动拉取到本地

![image-20220324145030677](https://gitee.com/FZR95/pic316/raw/master/image-20220324145030677.png)

## 分支

分支是用来将特性开发绝缘开来的。在你创建仓库的时候，master （现在叫main）是"默认的"分支。在其他分支上进行开发，完成后再将它们合并到主分支上。

•-checkout切换分支

•-merge将分支合并

![image-20220324145048235](https://gitee.com/FZR95/pic316/raw/master/image-20220324145048235.png)