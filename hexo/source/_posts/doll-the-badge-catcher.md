---
title: "打造小而美，Doll - 菜单栏小助手"
date: 2022-01-28
categories:
- [gallery]
tags:
- Doll
- Menu bar
- Productivity
featured_image: https://s2.loli.net/2022/05/19/yhvJYpoaSHuMXcD.jpg
---

今天给大家分享（~~安利~~）我最近开发的一个 macOS app - **Doll**，它能改善你的 Mac 菜单栏体验。


## 解决什么问题？
如果你的 Mac 使用习惯也和我一样，喜欢【自动隐藏 Dock + 窗口全屏】进行日常工作，那么时不时地 **_遗漏工作消息_** 一定是你的日常。

为什么总会遗漏消息？因为全屏的时候，Menu Bar 会隐藏，自动隐藏的 Dock 又很不好调出来（甚至可能划拉了五六下都出不来）。这两个 App 常驻的位置都看不到了，那一旦你没有看到一开始的消息通知（分神了或者喝茶喝水去了），等你回来继续工作，你根本不会意识到需要去调出 Dock 看看有没有红点点（当然离开座位要锁屏噢朋友）。

非全屏模式也并非高枕无忧，我常用的 **Slack**，**Mail**，**Microsoft Teams** 之类的应用是没有菜单栏常驻图标的，只能通过 Dock 确认有没有新消息，你专心写代码的时候也不会时常调出 Dock。

![dock-only](https://s2.loli.net/2022/05/19/XbqsVyT3EYFeMJU.png)

如果应用提供了菜单栏常驻图标，那这个问题就可以很大程度上缓解，因为就算没有新消息的时候，为了看时间你也会时不时地喵上几眼菜单栏，而菜单栏比 Dock 更易见得多，就算隐藏了也只需要把鼠标移动到屏幕上方即可快速显示。

**Doll** 解决的就是这么一个小小小小小...众需求，它可以帮你把 Dock 上的图标和未读消息同步到菜单栏上！

![showcase](https://s2.loli.net/2022/05/19/moFvwhnVE7iUbjt.png)

## 如何获取
我把 **Doll** 开源并托管在了 Github 上，你可以去这个[页面下载 dmg 安装文件](https://github.com/xiaogdgenuine/Doll/releases)

## 如何安装
双击 dmg 文件，把 Doll.app 拖到 Application 目录
![install](https://s2.loli.net/2022/05/19/15VfosQmnRw2Ppc.png)

双击打开 Doll，此时系统应该会提示你这是未被验证的开发者发布的程序，不允许你打开，这是正常的因为我只是简单地发布了个未签名的 dmg 文件，并没有准备上架 App Store，点击 OK 继续。
![prevent-open](https://s2.loli.net/2022/05/19/Tj5WC2XLZ6EgFzi.png)

Command + Space 打开 System Preferences > Security > General > Open anyway
![open-anyway](https://s2.loli.net/2022/05/19/STHDeVWO1UJ5igy.png)

## 如何使用
使用方法很简单，App 启动后会要求你选择一个 App 进行观测，同时你也可以进行搜索:

![usage](https://s2.loli.net/2022/05/19/6GmFulcTeUJsNIX.png)

当你选择好要观测的 App 后，**Doll** 会请求你授予 **Accessibility API** 权限: 
![ask-for-permission](https://s2.loli.net/2022/05/19/ZfTzyiFx1r2PpkL.png)

确保你授予了 **Doll.app** 使用 **Accessibility API** 的权限否则观测不会起任何作用。
![grant-permission](https://s2.loli.net/2022/05/19/geSnwF1Y6DRItW4.png)

搞定!
**Doll** 现在会自动同步 Dock 的 App Badge 信息到菜单栏对应的图标，你不用再担心漏回消息了!

# 切换当前观测的 App
如果被观测的 App 正在运行, 点击菜单栏图标只会简单地打开那个 App。

如果你想更改设置，只需要按住 "**_Option 键(⌥)_**" 然后点击图标.

![config](https://s2.loli.net/2022/05/19/vZRXOU2AqTMlNiI.png)

# 同时监测多个 App
没有问题，点击这个小加号就行。
![multiple-monitor](https://s2.loli.net/2022/05/19/G4cgpbK9sajNSWh.png)

## 为什么需要 Accessibility API 权限？不会有安全隐患吧？
**_绝对！不要！相信！互联网！_**

当然有风险当然有隐患，没事不要瞎装软件。

[**Doll**](https://github.com/xiaogdgenuine/Doll) 是开源的，如果你不放心我提供的 dmg 包，随时欢迎你克隆，审查，修改代码然后编译属于你自己的安装包。

## **Doll**？什么怪名字。

**Doll** 这个名字来自我很喜欢的动画[《黑之契约者》](https://zh.wikipedia.org/wiki/DARKER_THAN_BLACK), 动画里如果一个 **_契约者_** 一直使用他的超能力但却从不支付 **代价**, 那么最终他的能力会失控，丧失自我成为毫无感情的 **_Doll_**，终日面无表情（误.

![doll](https://s2.loli.net/2022/05/19/yhvJYpoaSHuMXcD.jpg)

如果我们工作中使用了太多的 **专注能力** 却从来不支付 **代价**，我们会变成什么呢～ >>__<<.


## 怎么实现的？
整个项目的 UI 完全由 SwiftUI 实现。

核心的获取 Badge 信息的代码存放在单独的一个叫 [MonitorCore](https://github.com/xiaogdgenuine/Doll/tree/main/MonitorCore) 的 Swift Package 中，使用了 macOS 的 Accessibility API，因为 API 的限制，**Doll** 只能通过 Polling 的方式每隔 1s 同步一次 Badge 信息，不过无需担心性能，因为每个轮询操作只是简单的读取和设置文本，而且一天最多执行 86400 次，对 Mac 来说洒洒水而已啦。

具体细节就有劳各位自己看代码啦。


## 近来的一些些感想

### 学习一门新语言的建议
因为最近刚加入了很优秀的 iOS 开发团队，为了不拖后腿一直在恶补 Swift 各种语法和新特性，这个学习的过程也有一些心得想分享一下。

我以前是专职前端开发的，最近一年多才慢慢接触 iOS 开发，这个小项目也是我为了用熟 Swift 语言的各种新特性给自己找的课题。

以前学一门计算机语言时我喜欢把一整本教程书啃完再动手实践，一边看书一边心里还会默念类似 “啊这都要单独写出来吗谁不懂啊”，“不就是个尾递归优化嘛又在这水页数” 的话，可每每到了看完书要动手的时候就抓瞎了，好像什么语法都懂，但就是没有兴趣用这门语言写点东西，最后往往就不了了之，过个一年半载语法又忘光了，学 Java, Python，Ruby 都是这样。

但其实我也有学得蛮好的语言，C# 尽管多年没复习了每年还是能用它写点自娱自乐的 Windows 软件，JavaScript 更不用说是看家吃饭的手艺，轮子一个接一个造，近两年来 Swift 也是用得越来越熟练，甚至还开发了一个广受好评的 [App](https://apps.apple.com/cn/app/%E5%8F%AF%E8%BE%BE%E6%BC%AB%E7%94%BB-%E6%9C%AC%E5%9C%B0%E6%BC%AB%E7%94%BB%E9%98%85%E8%AF%BB%E5%99%A8/id1545372338)。

回顾一下我用得最好的这三门语言，发觉我反而没有系统地学过它们，
- C# 能学起来是因为想用 WPF 实现一个炫酷的桌面聊天软件。
- JavaScript 能学起来是因为第一家公司的宣传网站是我一个人搭的。
- Swift 能学起来是因为我买了 iPad 想好好看漫画而不得。

基本上稍微系统地学习这些语言都是在我已经做出了一点成果之后了，需要更精进的时候我才会去买一些书来看，而且此时我的针对性很强，我要解决的就是开发过程中遇到的非常具体的问题，要买什么书要学什么技术我基本也都门清了。

而怎么也学不好的那几门语言，是因为我就从没想好用它们做点什么，学习的动力来源非常单一：“这么火应该学”。

说出来不怕大伙笑话，什么异步多线程编程，竞态资源，自旋锁，信号量，Async Await，内存泄露排查，性能调优，我这种半路出家的刚入行那几年根本连概念都看不懂，书也看不下去。

可一旦开始写一个感兴趣的项目了，我就想提高它的稳定性，改善它的性能，各种变着法想让它更好用，于是这个过程里我就什么语言特性都学到了，用得也更扎实了，成就感是非常强的，经常解决完问题后激动地原地跺 JoJo！

说到底计算机科学还是更偏向实践一些，因此对于语言初学者，不管你在学什么语言，我的建议是学完简单的基础后就先把书合起来吧，马上动手去做点东西才能保住你那份热情，前期多做，后期多学，会是正反馈周期比较合理的方式。

### iOS 开发的效率
搞 iOS 开发的同学们，SwiftUI 现在必须立刻马上武装到你的技能树上，投资回报率是近几年最高的了！

**Doll** 仅仅花了我 3 个晚上就写完了，90% 的时间其实花在了查 macOS 的 API 文档上，UI 部分可以说毫无阻力，想哪写哪，随时预览随时调节。

虽然因为用了较新的 SwiftUI 所以 **Doll** 只能跑在 macOS 11.0(Big Sur) 以上的系统，但这个牺牲完全值得！如果我为了兼容老系统改用 UIKit 实现界面，我这会儿应该还在纠结为什么 UICollectionViewDataSource 就是不更新，Layout Constraints 应该 Enable 哪几个，Disable 哪几个，要怎么实现数据绑定。。。等我实现出一版 UIKit，竞品早已经迭代了好几版 UI 了。
    

### 规划
虽然说有想法就赶紧上机开码的感觉特别爽（谁开机谁知道），但该缓一缓的时候还是得及时刹车。

开发 **Doll** 的时候我就犯了急性子的大错，想当然觉得全屏模式时，应该在有新消息的时候显示一个小小的通知 Popover 好让用户注意到。为了实现这个 Popover 又花了一小时查怎么确定当前窗口是全屏模式（实名吐槽 Apple 烂文档，交了那么多钱就这体验），然后又一顿调试终于实现了。

最后当我在全屏模式下发了一条测试消息的时候，我傻眼了：

![useless](https://s2.loli.net/2022/05/19/QuxcpK2rw6URBez.png)

你说这一个多小时能找谁要回来？其实脑子只要停下来想一想马上就能意识到这个功能鸡肋至极，可是脑子说不行，你不能停，这个 idea 太棒了用户一定会赞不绝口的！

这种错我还是偶尔会犯，对抗本能太难了，这个鸡肋功能就留在 **Doll** 里作为提醒吧。


## 最后
希望 **Doll** 这个小作品能小小地提高大家的工作体验，也祝愿各位大姑娘小伙子们能找回那种开发软件解决问题的纯粹乐趣。
