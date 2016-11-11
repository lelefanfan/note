#Git与Github入门教程
Git，即源代码管理工具。它是一个开源的分布式版本控制系统，可以有效、高速的处理从很小到非常大的项目版本管理。

[TOC]

##资源

1. 阮一峰git教程：http://www.ruanyifeng.com/blog/2015/12/git-cheat-sheet.html
2. 廖雪峰git教程：http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/

##下载

1. 这是我在网上找到的一个国内Git镜像：https://github.com/waylau/git-for-win 可以从该页面下载各个版本的Git安装文件。
2. 还有一个是自己经常用的版本，不过是64位版本的，下载地址：http://pan.baidu.com/s/1jHAKs1w 密码：uyxh，这个版本的方便之处在于不需要安装，安装后即可使用。

##安装

1. 安装过程中，按照默认设置下一步下一步即可完成安装。
2. 安装完成后，注意设置环境变量。

##常用命令

###初始化
命令：`git init`

###查看状态
命令：`git status` 还可以输出简要日志，命令：`git status -s`

###添加文件到暂存区
命令：`git add <file>`,将工作文件添加到暂存区；`git add .`，将所有文件添加到暂存区

**忽略清单功能**

1. 在代码库跟文件夹添加一个.gitignore文件，该文件用于说明`git add .`命令不需要跟踪的文件
2. 在.gitignore文件中只要直接写被忽略的文件，一行一个即可
3. .gitignore文件中写入`/dist`，表示只忽略根目录中的dist目录

###将暂存区文件提交到仓库区
命令：`git commit -m '提交说明'`

###显示暂存区与仓库区的区别
命令：`git diff`,diff命令还有许多高级用法，可以查阅手册。

###重置

1. 重置当前分支的HEAD为指定commit，同时重置暂存区和工作区，与指定commit一致
命令：`$ git reset --hard [commit]`,[commit]为commit哈希值，可以通过`git log`命令查看哈希值

###增加一个新的远程仓库，并命名
命令：`git remote add [shortname] [url]`，shortname表示别名，url表示要添加的远程仓库

###上传本地指定分支到远程仓库
命令：`git push -u [shortname] [branch]`，-u可有可无，有表示流上传，速度会快一些;branch表示要上传到的分支

###下载文件
命令：`git pull [shortname] [branch]`

###上传文件
命令：`git push [shortname] [branch]`

##注意事项

1. 第一次使用必须设置邮箱与用户名，分别用到两个命令：`git config --global user.email "你的email"`，`git config --global user.name "你的名称"`,完成这个步骤后才能正常提交。
2. Sublime编辑器GitGutter插件可以在代码编辑区显示Git状态。









<style>
    h1,h2,h3,h4,p,strong { font-family: "Helvetica Neue",Arial,"Hiragino Sans GB","STHeiti","Microsoft YaHei","WenQuanYi Micro Hei",SimSun,Song,sans-serif }
    p { font-size: 16px; }
    code { color: #c7254e; background-color:#f9f2f4 !important; }
    .toc ul { list-style-type: none; margin-bottom: 15px; font-size:18px; font-family:"Helvetica Neue",Arial,"Hiragino Sans GB","STHeiti","Microsoft YaHei","WenQuanYi Micro Hei",SimSun,Song,sans-serif;  }
</style>
<link href="http://cdn.bootcss.com/highlight.js/9.7.0/styles/vs.min.css" rel="stylesheet">
<script src="http://cdn.bootcss.com/highlight.js/9.7.0/highlight.min.js"></script>
<script>hljs.initHighlightingOnLoad();</script>