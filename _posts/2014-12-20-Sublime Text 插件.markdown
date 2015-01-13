---
layout: post
title:  "Sublime Text 插件"
date:   2014-12-20 04:56:54
categories: [DevStudy,Tools]
---
# Sublime Text 插件
_——All for one,one for all_
Tags:Tools Sublime DevStudy

---

**转载请注明出处** [https://www.zybuluo.com/BookThief/note/56463](https://www.zybuluo.com/BookThief/note/56463)  --by [BookThief](http://weibo.com/nonboat/)

[TOC]

## 前言

　　之前安装`Sublime`后，各种插件狂安。结果就是好多按键冲突……无奈之下，连同系统一并格掉重做。当然，其实主要是想格掉系统的。
　　如果更换环境，总是去网上找这些基础的配置真的好蛋疼。因此，在这里把自己常用的设置写一下，也希望能帮助到一样对这有需求的人。

---

## Packages

　　先介绍一下可能会用到的基本操作，通用式安装、快捷键修改位置和更新、删除插件：

　　1、与其说叫安装有点……其实就是把下载后缀为`.sublime-package`的包，放到 `$ PATH/Installed Packages` 里面(`$ PATH`就是你自己的安装目录),以下我会在每个插件介绍前放置官方的下载链接(有些是官方git上给的zip包，自己解压以下哦)；

　　2、在`Preferences => Key Bindings - User`添加自己想要的快捷键。

　　3、更新和删除插件的命令，`Ctrl + Shift + P`输入:`upgrade package`、`remove package`

### [Package Control](https://sublime.wbond.net/installation)
　　
　　[.sublime-package 文件](https://sublime.wbond.net/Package%20Control.sublime-package)

　　`Sublime`必备的插件，用来方便安装其他插件的插件。首先按`Ctrl + ｀`调出控制台：
　　
![Console](https://raw.githubusercontent.com/BookThief-D/pictures/master/Sublime/Console.JPG) 

　　然后在控制台上输入以下命令：


	// Sublime Text 3
	import urllib.request,os; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); urllib.request.install_opener( urllib.request.build_opener( urllib.request.ProxyHandler()) ); open(os.path.join(ipp, pf), 'wb').write(urllib.request.urlopen( 'http://sublime.wbond.net/' + pf.replace(' ','%20')).read())


	// Sublime Text 2
	import urllib2,os; pf='Package Control.sublime-package'; ipp = sublime.installed_packages_path(); os.makedirs( ipp ) if not os.path.exists(ipp) else None; urllib2.install_opener( urllib2.build_opener( urllib2.ProxyHandler( ))); open( os.path.join( ipp, pf), 'wb' ).write( urllib2.urlopen( 'http://sublime.wbond.net/' +pf.replace( ' ','%20' )).read()); print( 'Please restart Sublime Text to finish installation')


　　以后再遇到想下的插件而不方便去找`.sublime-package`包的时候，直接按`Ctrl + Shift + P`,输入`install package`(支持模糊查询，简单输一个instal就能看到，如下图)，稍等片刻就进入包管理器了，想找啥就随你了。

![Packages](https://raw.githubusercontent.com/BookThief-D/pictures/master/Sublime/packages.jpg)

### [Markdown Preview](https://sublime.wbond.net/packages/Markdown%20Preview)

　　[.sublime-package 文件](https://github.com/revolunet/sublimetext-markdown-preview/archive/master.zip)

　　一个`Markdown`的插件支持，包括本篇笔记的书写，越来越多的人选择`Markdown`来书写Blog、书刊。在我看来，是因为写作的时候不需要考虑排版，依赖已写好的`.css`就可以了。当然，还有许多诸如代码高亮、流程图、数学公式等非常方便的功能也都在逐渐扩充。

　　`Sublime`中可以装的Markdown插件有很多，例如`MarkdownEditing`除了实现代码高亮等功能，还可以想`Emmet`一样对`Markdown`进行了快捷键封装。不过不知道是我错觉还是什么，觉得安装`MarkdownEditing`之后，速度慢了好多。另外，快捷键多了引起与其他插件的冲突……

　　这个`Markdown Preview`，除了代码高亮、数学公式等功能以外，有一个 `preview in bowser` ( `Ctrl + Shift + P` 后查找 `Markdown Preview` )可以在浏览器中查看文档的阅读模式。阅读模式分两种，`github`上有些`Markdwon`的插件并不支持，例如[TOC]显示目录(如本文开始的目录，就是用的[TOC]),所以想在`github`上写`readme`或者建立自己的`gitpage`时可以用这个预览一下。
　　这个是没有快捷键的，可自行添加：

    {   //  Ctrl + Shift + M 可自行更换自己喜欢的快捷键
        "keys": ["Ctrl + Shift + M"], "command": "markdown_preview", "args": { "target": "browser"}
    }

　　高亮的设置在`Preferences => Package Settings => Markdown Preview => Setting Default`可以找到，里面有很多属性都默认不开启，有需要的可以阅读下官方文档选择自己想要的。另外，建议所有属性都不要在`Default`里修改，放在`~ => Setting User`里：

    "enable_highlight": false,

　　_当然,在网络良好的情况下，我会选择本文所在地的[作业部落](https://www.zybuluo.com/)来写`Markdown`文档(相信你用过也会喜欢)。本地情况下我也会用`Atom`，虽然被诟病说占用内存多，但是`Ctrl + Shift + M`的即写即读和作业部落这一点一样，让编写过程显得直观。_



### [TrailingSpacer](https://github.com/SublimeText/TrailingSpaces)

　　这个没有`.sublime-package`文件，有的是一个[ZIP包](https://github.com/SublimeText/TrailingSpaces/archive/master.zip)，还是用`Package Control`安装更方便。

　　这是一个高亮显示、删除多余空格和Tab的插件，个人觉得还是蛮喜欢的。其实对于现在的编译器，空格和Tab基本没有什么影响，无非就是一个美观而已，可能对于强迫症患者来说比较必须。

　　这个一样是没有快捷键的：

    // 删除多余空格和Tab
    { "keys": ["Ctrl + Alt + D"], "command": "delete_trailing_spaces" },
    // 高亮显示开关
    { "keys": ["Ctrl + Alt + T"], "command": "toggle_trailing_spaces" }


### [CSS Comb](http://csscomb.com/)

　　一样只有[ZIP包](https://github.com/csscomb/csscomb-for-sublime/archive/master.zip)。

　　快捷键是`Ctrl + Shitf + C`,可以将CSS属性重新排序，又是强迫症的一大福音……
　　
### [ColorPicker](https://github.com/weslly/ColorPicker)

　　[ZIP包](https://github.com/weslly/ColorPicker/archive/master.zip)

　　一个便捷的颜色选择其，传说中前端会经常用且很好用的插件。我这吊丝还没真正用过呢……

　　这个有个单疼的是，快捷键也是`Ctrl + Shitf + C`。只能自己根据需要去改keymap了。


### [Emmet](http://emmet.io/)

　　[ZIP包](https://github.com/sergeche/emmet-sublime/archive/master.zip)

　　这是一个连`Vim`和`Emacs`都支持的插件，`Atom`、`Eclipse`、`EditPlus`甚至还有在线的`CodePen`都可使用。强大的html、css编辑插件，前提是你需要花点时间去了解快捷键。

　　***以上是现在我用到的插件，在未来的学习过程中，如果有新的发现，我会不断更新完善这篇Blog的。***


---


　　
　　
## 参考资料

[1]. [Sublime Text 3 安装Package Control](http://www.cnblogs.com/luoshupeng/archive/2013/09/09/3310777.html)

[2]. [sublime text 2 下的Markdown写作](http://www.jianshu.com/p/378338f10263)

[3]. [Sublime Text 3 能用支持的插件推荐](http://dengo.org/archives/923)


**转载请注明出处** [https://www.zybuluo.com/BookThief/note/56463](https://www.zybuluo.com/BookThief/note/56463)  --by [BookThief](http://weibo.com/nonboat/)
2