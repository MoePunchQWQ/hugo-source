+++
date = '2025-09-25T11:12:20+08:00'
draft = false
title = '记录一下 Blowfish 个性化的一些事宜'
tags = ['Docs']
series = ['建站相关']
+++
在用 Hugo + Blowfish 搭建这个网站的过程中遇到了不少问题，特地写下来记录分享一下。

### 关于中国大陆地区 git submodule 难添加的解决方案
这个问题主要是网络问题导致的，为了在本地正常编辑，我在 Gitee 上同步了 [Blowfish](https://gitee.com/MoePunch/blowfish) 主题的仓库，但是要注意，这个操作仅仅是让你在本地正常使用这个主题，当你完成了主题、个性化之类的事宜时，你应该在网站源码的根目录的 **.gitmodules** 文件中把模块的地址改回 GitHub 的官方地址，这样在你上传到 GitHub repo 时，GitHub actions 可以从官方仓库同步主题，保证时效性，而不是你的同步仓库。  
### 关于更改网站图标
你需要在 网站根目录/layouts/partials/head/ 中添加 custom.html，然后找一个你喜欢的图标，用图标转换器转换为网页可用的格式，我这里用的是 [favicon](https://favicon.io/favicon-converter/)，然后将这些文件（如下图）复制到你网页根目录的 static 文件夹中。你可能需要在 hugo 中执行 `hugo --gc` 启用垃圾回收，清理掉以前的图标文件，然后执行 `hugo server --disableFastRender` 重新渲染你的网页，理论上就可以看见图标的变化了。
<img src="https://i.postimg.cc/sfMh4ZyR/icons.jpg" alt="示例图片" width="600" height="auto">

### 关于自定义的一些提醒
强烈不建议 **直接修改 themes 文件夹中的内容** 。
>为了实现这一点，您永远不应该直接手动更改任何主题核心文件。无论你是使用 Hugo 模块安装，还是作为 git 子模块安装，还是手动将主题安装在 themes/ 目录中，  
你都应该始终保持这些主题文件不变。

这段话来自于 Blowfish 的[官方文档](https://blowfish.page/zh-cn/docs/advanced-customisation/)，正确执行自定义的方法是在网站根目录的对应文件夹中添加你自己的配置，例如我要修改默认的作者头像，正确的做法是把图片文件添加到 <mark>src/assets/img</mark> 中，然后在 <mark>src/config/_default/</mark> 中更改对应的配置文件，而不是直接更改 <mark>themes/blowfish</mark> 中的内容。 
