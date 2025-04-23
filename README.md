# 安装 hugo

```shell
1. brew install hugo
2. docker可以安装


windows
3. 访问 Hugo 的 GitHub：https://github.com/gohugoio/hugo/releases

如下载hugo_extended_0.146.7_windows-amd64.zip

下载带有 extended 的 Windows 版本 zip 包；

解压到任意目录；

把解压目录加入到系统环境变量（Path）中。注意文件夹包含到hugo.exe的目录；
```

# 文件目录

- archetypes：存放用 hugo 命令新建的 Markdown 文件应用的 front matter 模版
- content：存放内容页面，比如「博客」、「读书笔记」等
- layouts：存放定义网站的样式，写在 layouts 文件下的样式会覆盖安装的主题中的 layouts 文件同名的样式
- static：存放所有静态文件，如图片
- data：存放创建站点时 Hugo 使用的其他数据
- public：存放 Hugo 生成的静态网页
- themes：存放主题文件
- hugo.toml：网站配置文件

## hugo 命令

- hugo server：启动本地服务器，预览网站
- hugo new：新建页面
- hugo new site：新建网站
- hugo new theme：新建主题
- hugo new theme --minify：新建主题并压缩
- hugo new theme --minify --force：新建主题并压缩，如果主题已存在，则覆盖

## hugo 配置文件

- baseURL：网站地址
- title：网站标题
- theme：主题名称
- paginate：每页显示的文章数量
- enableEmoji：是否启用表情符号
- enableRobotsTXT：是否启用 robots.txt
- enableGoogleAnalytics：是否启用 Google Analytics
- enableDisqus：是否启用 Disqus 评论
- enableMathJax：是否启用 MathJax 公式
- enablePrettify：是否启用 Prettify 代码高亮
- enableFancybox：是否启用 Fancybox 图片预览

## hugo 主题

- hugo-theme-cactus：简洁的博客主题
- hugo-theme-even：简洁的博客主题
- hugo-theme-hello-friend：简洁的博客主题
- hugo-theme-jane：简洁的博客主题
- hugo-theme-meme：简洁的博客主题
- hugo-theme-minos：简洁的博客主题
- hugo-theme-next：简洁的博客主题
- hugo-theme-quick：简洁的博客主题
- hugo-theme-stack：简洁的博客主题
- hugo-theme-w3layouts：简洁的博客主题

## hugo 主题配置

- theme：主题名称
- baseURL：网站地址
- title：网站标题
- description：网站描述
- keywords：网站关键词
- author：网站作者
- copyright：网站版权信息
- favicon：网站图标
- logo：网站 logo
- avatar：网站头像
- cover：网站封面
- menu：网站菜单
- social：网站社交链接
- analytics：网站分析
- disqus：网站评论
- mathjax：网站公式
- prettify：网站代码高亮
- fancybox：网站图片预览

## hugo 创建示例

```shell

hugo new site hogo-blog
cd hogo-blog
git init

# 示例主题
git submodule add https://github.com/adityatelange/hugo-PaperMod.git themes/PaperMod
echo 'theme = "PaperMod"' >> hugo.toml

# 创建一篇文章
hugo new posts/hello-world.md


# 发布到 github

git remote add origin git@github.com:你的用户名/my-hugo-blog.git
git add .
git commit -m "init blog"
git push -u origin master  # 或 main，视你本地分支名称而定



```

## hugo 本地启动预览

```shell
hugo server	启动本地预览服务器 默认1313端口

hugo server --bind 0.0.0.0 --baseURL=http://localhost --navigateToChanged

--bind 0.0.0.0	让其他设备也能访问（局域网 IP）
--baseURL http://IP:1313	设置站点的基础地址（预览用）
--disableFastRender	禁用快速渲染，解决部分页面刷新异常的问题
--navigateToChanged	自动跳转到刚刚修改的页面
--minify	启动时启用压缩
```

## md 配置

字段 含义
title 标题
date 发布时间
lastmod 最后修改时间（支持主题显示“更新时间”）
draft 草稿状态，true 不会被构建
author 作者名
tags 标签（用于聚合分类）
categories 分类（通常比 tag 粗）
description 简短描述，很多主题支持在首页/列表页显示
slug 自定义文章 URL（/posts/slug/）
images 文章封面图 URL（部分主题支持）
featured 是否是推荐/置顶文章（主题支持才有效）
