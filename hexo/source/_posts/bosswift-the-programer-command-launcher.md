---
title: "Bosswift - 为 Git 用户设计的命令启动器"
date: 2022-07-10
categories:
- [gallery]
tags:
- Bosswift
- Command Launcher
- Productivity
- Git
featured_image: https://s2.loli.net/2022/07/10/AOeoQdW5Nk7pliG.jpg
---

## 一件麻烦事
朋友，在你的开发生涯中，是否经常有过这样的经历：

> 你正工作在某个开发任务上，同事紧急让你帮忙定位一下另一个已上线的功能为什么表现怪异，是不是代码有什么问题。

你说好，然后熟练地打开命令行窗口，打下一大串让人心疼的命令：

```bash
# 暂存当前的工作
git stash -u
# 切换到线上分支
git checkout release/v1
# 拉取线上分支最新代码
git pull
# 安装依赖，配置运行环境等
npm install...
# 启动，定位问题
npm run...
```

折腾五六分钟后终于把环境跑起来，定位问题结束后，你又打开命令行窗口，打下另一串让人心疼的命令，继续你原本的开发任务:

```bash
# 切换回工作分支
git checkout feature/in-development
# 恢复工作变更
git stash apply
# 安装依赖，配置运行环境等
npm install...
# 启动，继续开发
npm run...
```

如果一天内这样的事情多次出现，你的工作效率会相当低效，时间都耗费在没必要的上下文切换上了.

想象一下如果我们可以同时 Checkout 多个分支，每个分支有自己专属的工作文件夹，是不是就不用这么折腾了？

确实是这样子的，这个频繁上下文切换的问题 git 团队也注意到了，为了解决它，git 2.5 版本开始支持 [multiple worktrees](https://git-scm.com/docs/git-worktree)，你可以在一个 git repo 里同时创建多个 worktree 拷贝，每个 worktree 都有专属于自己的分支, 类似下图：

![bosswift-git-worktree-explain](https://s2.loli.net/2022/07/11/bqQ4cdguWPxza3Z.webp)
有了 git worktree，分支切换就变成了 cd 到不同的 worktree 目录，每个分支都可以拥有自己的独立工作目录，东西不会揉在一起，stash 命令也用不上了：

![bosswift-new-fashion](https://s2.loli.net/2022/07/11/U62tEvT1gIrsKlY.jpg)

更重要的是，你不需要重新安装项目依赖，因为你的工作代码没有任何改动！

git worktree 也可以帮我们确保本地一直有一个可以运行的分支，不会受你当前工作的影响，这一点有时候很重要。

## 一个东西能解决问题，那它一定会带来新的问题
纯命令行使用 git worktree 有以下问题：
- 创建和删除 worktree 要手打的东西实在太多了, 得指定 worktree 路径，指定新分支名等，经常写错要删了 worktree 重来
- 切换分支要 cd 来 cd 去，常常忘了自己在哪里要干什么，也比较容易切错目录
- 磁盘占用多，每个 worktree 里第三方依赖都得单独拷贝一份

## ✨✨✨ Bosswift ✨✨✨
为了解决命令行使用 git worktree 的这些痛点，**Bosswift** 应运而生。

**Bosswift** 与 git worktree 深度集成，帮助你用 UI 的方式轻松管理 worktree。
![bosswift-introduction](https://s2.loli.net/2022/07/11/dQnKzR5gjMTA718.png)

# 安装 + 配置
从[这里下载](https://github.com/xiaogdgenuine/bosswift/releases/latest)最新的安装包，双击安装。
![bosswift-install](https://s2.loli.net/2022/07/11/E9tuLSBJAUX6bjd.png)
第一次打开 **Bosswift** 需要一点配置，主要就是选一下你平时的工作目录，这样 **Bosswift** 就可以随时同步 Worktree 状态，我习惯是创建一个 dev 目录存放所有工作项目：
![bosswift-on-boarding](https://s2.loli.net/2022/07/11/WJIgGTZHxsq92ak.png)

# 使用
配置完成后，按下 Option + Space (默认快捷键)，**Bosswift** 的快速启动框就打开了。
![bosswift-quick-launch-bar](https://s2.loli.net/2022/07/11/BA4dlWFDEuaqjVe.png)
输入关键字搜索想要执行命令的分支（各代表一个 worktree），回车或者按 Tab 键选中：
![bosswift-quick-launch-search-branch](https://s2.loli.net/2022/07/11/icIqUQ8T3s9m1jX.png)
搜索想要执行的命令，**Bosswift** 里已经自带了一些常用命令，回车即可执行：
![bosswift-quick-pick-command](https://s2.loli.net/2022/07/11/9tc7LSs6mf5IJMQ.png)

## 创建新的 Worktree
当你需要新的 worktree 时，执行这个命令：
![bosswift-create-worktree](https://s2.loli.net/2022/07/11/6EXZYkdlr5Pa2Jv.png)
此命令可基于选中的分支创建新的 worktree，你只需要输入分支名即可：
![bosswift-create-worktree-branch-name](https://s2.loli.net/2022/07/11/N7PVZYqS6zlv2nC.png)
该命令会自动处理好以下几种 case
- 本地已经有同名分支：将新 worktree 切换到该分支。
- 本地没有对应分支，但是远端有：拉取该分支到本地，创建新 worktree 并切换到该分支。
- 本地和云端均没有同名分支：创建新 worktree 并创建新分支。

你可以修改该命令，在末尾添加诸如 "**从源分支 worktree 拷贝 node_modules**" 等操作，避免新 worktree 需要重新安装第三方依赖浪费时间。
## 删除 Worktree
当你不再需要某个 worktree 时，执行这个命令删除对应的 worktree 文件夹：
![bosswift-delete-worktree](https://s2.loli.net/2022/07/11/KXynVNlpHodg69h.png)
你可以修改该命令，在末尾添加清理操作，比如删除对应的 Xcode Derived Data 目录节省磁盘占用。

# 编写自定义命令
如果连自己的命令都不能编写还算什么 Boss 呢~
我鼓励你编写适用于你项目的各种命令，**Bosswift** 会给你提供力所能及的帮助，一些可以使用的变量会在脚步运行时提供：
![bosswift-command-glossary](https://s2.loli.net/2022/07/11/rvRZuxigzPkdTVJ.png)

以选中了 /Users/huikai/dev 下 Doll Repo 的 feature 分支为例，以下是各变量的解释和对应值:
|  变量名 | 意义 | 值  |
|  ----  | ----  | ----  |
| $BOSSWIFT_WORK_FOLDER  |  Bosswift 的工作目录  | /Users/huikai/dev |
| $BOSSWIFT_PROJECT_NAME |  当前选中的 Repo 文件夹名  | Doll |
| $BOSSWIFT_BRANCH_NAME |  当前选中的 Branch 名  | feature |
| $BOSSWIFT_WORKTREE_PATH |  当前 Worktree 的路径  | /Users/huikai/dev/Bosswift_Work/Doll/feature |
| $BOSSWIFT_DEFAULT_WORKTREE_PATH |  Repo 默认 Worktree 的路径 | /Users/huikai/dev/Doll |
| $BOSSWIFT_XCODE_DERIVED_PATH |  Worktree 对应的 Xcode Derived Data 路径（Apple 开发者特供）  | /Users/huikai/Library/Developer/Xcode/DerivedData/Doll-cikiwqgnfwrbgzgebttnrazqigks |
| $BOSSWIFT_XCODE_WORKSPACE_FILE |  当前 Worktree 里的 xcworkspace 文件名（Apple 开发者特供）  | Doll.xcworkspace |
| $BOSSWIFT_XCODE_PROJECT_FILE |  当前 Worktree 里的 xcodeproj 文件名（Apple 开发者特供）  | Doll.xcodeproj |

# Dashboard 查看运行中的命令
可以在 Dashboard 管理正在运行中的任务：
![bosswift-dashboard](https://s2.loli.net/2022/07/11/sdKzgDEtYRvQj5N.png)

# 作为常用命令管理器 (Universal Command)
有一些命令是全局的，时不时就得跑一下，比如为了解决 Xcode 认不出手机的问题，我常需要重启 usb 服务，但是我总是忘了怎么写，需要去各种笔记软件里拷贝出来很麻烦。

有了 **Bosswift**，这些命令都可以统一存放到 Universal Command 里了：
![bosswift-universal-commands](https://s2.loli.net/2022/07/11/ivKCaHUuGOwADyX.png)
在快速启动框输入 “/” 就可以选择 Universal Command 去执行了：
![bosswift-select-universal-command](https://s2.loli.net/2022/07/11/tkEiXnsAhY9Bxcb.png)

# 作为临时命令启动器
在快速启动框输入的关键字如果没有任何匹配项，就可以直接回车作为临时命令执行：
![bosswift-temporary-commands](https://s2.loli.net/2022/07/11/UIE45RKTbSrCiNg.png)

## 命令行 还是 GUI
或许是命令行打得太少的缘故，我从没有体会过那种键指如飞框框框一回车就把活干完的快感，反而是很多命令我都要仔细检查，生怕打错一个字，把文件写到不该写的地方，把不该删的文件删了，确认没问题后我才敢回车，效率并没有很高。

说一句违背祖宗的话，作为一个程序员，我一直对命令行喜欢不起来，甚至有点怕命令行，diff 还有合并冲突这些事都喜欢用死贵的 GUI 工具（如 JetBrains 系列）来完成。

可是 GUI 在重复任务自动化方面是完全不行的，各个程序的界面设计也良莠不齐，遇到难用的真还不如手打命令。

很幸运，这不是一个非此即彼的问题，把格局打开，GUI 里可以有命令行，命令行也可以调 GUI 嘛。

命令行在自动化和功能可造性上都是碾压 GUI 的，**Bosswift** 离不开命令行，它背后的核心是 _screen_ 命令（用来分发任务），为了实现任务管理，_ps_, _grep_, _pkill_ 等命令也是必不可少的，把这些命令和易用的 GUI 结合在一起，配合一些巧妙的引导，GUI 能帮助用户毫无心理压力地执行任务（一些优秀的防呆设计可以做到这点），最后命令行默默把活干了就行。

# 代码地址
https://github.com/xiaogdgenuine/bosswift

免责声明：
我一向风格就是能跑就行，把活干了再来扯别的，所以代码洁癖千万不要看，血压会上来，Repo 里充满了丑陋的全局变量，不合理的模块划分，以及各种自以为是的环境假设。
