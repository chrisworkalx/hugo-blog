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
