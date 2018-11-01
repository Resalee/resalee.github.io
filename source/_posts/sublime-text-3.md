---
title: 配置sublime text 3
date: 2017-11-01 22:24:00
tags: [tools]
---

## 0、目前需求：

- 编辑css/html/JavaScript页面
- 用Markdown写文章
- 在多台终端上同步使用

<!-- more -->

## 1、安装sublime text 3

[下载sublime text 3](http://www.sublimetext.com/3)，解压到自己想放软件的地方。
PS.测试通过坚果云同步软件，但会带来使用不便，有时候会有文件冲突，所以做好基本配置后，可以打包一份上传到云，需要时再下载，后期的改动基本上是插件方面的。Atom可以同步，不过没怎么倒腾。

## 2、基本设置

点击菜单栏Preferences-Settings，会弹出默认设置文件和用户设置文件，可以在用户设置文件里进行一些选项的设置：

```
{
    // 设置主题，下载主题后，可以通过Preferences-Color Schemes选择主题
    "color_scheme": "Packages/Boxy Theme/schemes/Boxy Monokai.tmTheme",
    // 设置Sans-serif（无衬线）等宽字体，以便阅读
    "font_face": "YaHei Consolas Hybrid",
    "font_size": 12,
    // 使光标闪动更加柔和
    "caret_style": "phase",
    // 高亮当前行
    "highlight_line": true,
    // 高亮有修改的标签
    "highlight_modified_tabs": true,
    // 设置tab的大小为2
    "tab_size": 2,
    // 使用空格代替tab
    "translate_tabs_to_spaces": true,
    // 添加行宽标尺
    "rulers": [80, 100],
    // 显示空白字符
    "draw_white_space": "all",
    // 保存时自动去除行末空白
    "trim_trailing_white_space_on_save": true,
    // 保存时自动增加文件末尾换行
    "ensure_newline_at_eof_on_save": true,
    "ignored_packages":
    [
        "Vintage",
        "Markdown"
    ]
}
```

sublime key settings设置光标跳出括号Preferences-Key Bindings，在右侧的user文件内输入：

```
[
    {"keys": ["enter"], "command": "move", "args": {"by": "characters", "forward": true}, "context":
        [
            { "key": "following_text", "operator": "regex_contains", "operand": "^[)\\]\\>\\'\\\"\\ %>\\}\\;\\,]", "match_all": true },
            { "key": "preceding_text", "operator": "not_regex_match", "operand": "^.*\\{$", "match_all": true  },
            { "key": "auto_complete_visible", "operator": "equal", "operand": false }
        ]
    }
]
```

## 3、安装插件

### 3.1 安装package control

参考[Package Control](https://packagecontrol.io/installation)官网页面进行安装，在线方法为：打开sublime，`Ctrl+``调出控制台，复制下列代码，Enter：

```
import urllib.request,os,hashlib; h = '6f4c264a24d933ce70df5dedcf1dcaee' + 'ebe013ee18cced0ef93d5f746d80ef60'; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); urllib.request.install_opener( urllib.request.build_opener( urllib.request.ProxyHandler()) ); by = urllib.request.urlopen( 'http://packagecontrol.io/' + pf.replace(' ', '%20')).read(); dh = hashlib.sha256(by).hexdigest(); print('Error validating download (got %s instead of %s), please try manual install' % (dh, h)) if dh != h else open(os.path.join( ipp, pf), 'wb' ).write(by)
```

我没有装成功，采用官网右侧Manual提示的方法：

- 在官网下载[Package Control.sublime-package](https://packagecontrol.io/Package%20Control.sublime-package)
- 点击sublime菜单栏：`Preferences - Browse Packages`，回到文件夹的上一级菜单，打开`Installed Packages`文件夹
- 把下载的Package Control.sublime-package放进Installed Packages文件夹
- 重启sublime

这个方法成功了，点击菜单栏Preferences可以看到Package Control选项了。

### 3.2 下载安装插件

`Ctrl+Shift+P`呼出命令板，点击Package Control: Install Package（或输入PCI快速定位），安装自己需要的插件、主题等。下面是我参考挑的一些自己可能需要的：

[ColorPicker](http://weslly.github.io/ColorPicker/)：
颜色选择器，快捷键`Ctrl / Cmd + Shift + C `

[SublimeLinter插件](https://github.com/SublimeLinter)：高亮提示用户编写的代码中存在的不规范和错误的写法。具体的使用可以参见：[借助 SublimeLinter 编写高质量的 JavaScript & CSS 代码](http://www.cnblogs.com/lhb25/archive/2013/05/02/sublimelinter-for-js-css-coding.html)

[HTML-CSS-JS Prettify](https://github.com/victorporof/Sublime-HTMLPrettify)：集成了格式化（美化）html、css、js三种文件类型的插件。插件依赖于nodejs，因此需要事先安装nodejs，然后才可以正常运行。插件安装完成后，快捷键ctrl+shift+H完成当前文件的美化操作。使用可以参见[这篇](http://frontenddev.org/article/sublime-does-text-three-plug-ins-html-and-css-js-prettify.html)介绍。

[CSScomb CSS属性排序](https://github.com/csscomb/CSScomb-for-Sublime)：选中要排序的CSS代码，按`Ctrl+Shift+C`，即可对CSS属性重新排序了，代码从此简洁有序易维护，如果不款选代码则插件将排序文件中所有的CSS属性。当然，可以自己自定义CSS属性排序规则，打开插件目录里的CSScomb.sublime-settings文件，更改里面的CSS属性顺序就行了。因为这个插件使用PHP写的，要使他工作需要在环境变量中添加PHP的路径，具体请看github上的说明。

[DocBlockr](https://github.com/spadgos/sublime-jsdocs:) 代码块注释：可以快速的对函数进行注释。保持代码规范。

- /*:回车创建一个代码块注释
- /**:回车在自动查找函数中的形参等等。

[advancedNewFile](https://github.com/skuroda/Sublime-AdvancedNewFile) ：快速创建文件，运用快捷键`command+alt+n`(win: `ctrl+alt+n`)，Sublime Text底部会弹出输入框；我们只需在这个输入框里输入我们需要新建的文件名回车即可（我们甚至可以带路径,譬如:*src/components/perfect.vue*;这就会在当前项目目录下，建立该文件；需要注意的是这路径前面不可加 ‘/‘, 这会使得建立的路径成为用户目录，而非改项目目录）。默认情况下文件会存储在当前目录，如果当前没有目录，会存储在用户的家目录。

[Emmet](https://github.com/emmetio/emmet)：在线没安装成功，下载GitHub上的zip文件，解压到安装文件夹中的Packages文件夹内（可通过Preferences-Browser Packages打开文件夹）。使用emmet需要安装PyV8，如果在线自动安装失败，也可以通过手动[下载安装](https://github.com/emmetio/pyv8-binaries)，解压到`Installed Packages/PyV8（PyV8这个文件夹要新建）`。使用参考：[使用Emmet加速Web前端开发](http://www.w3cplus.com/tools/using-emmet-speed-front-end-web-development.html)

[JsFormat](https://github.com/jdc0589/JsFormat)：将JS格式化的插件，可在JS文件中通过鼠标右键->JsFormat或键盘快捷键Ctrl+Alt+F对JS进行格式化。

Markdown Editing + MarkdownLivePreview：安装这两款插件后，重启sublime，进行设置：Preferences-Package Settings-MarkdownLivePreview-Setting，设置Markdown GFM Settings - User（也可以这样设置standard和multi的，这里的主题是我下载的sublime主题，可以换成你自己喜欢的主题）：

```
{   
    // 修改主题，应用sublime主题，而不是markdownediting原有的主题
    "color_scheme": "Packages/Boxy Theme/schemes/Boxy Monokai.tmTheme",
    // Layout
    "draw_centered": false, // 改为false，原始值为true，使页面靠左显示
    "word_wrap": true,
    "wrap_width": 120, // 每行字符数上限
    "rulers": [],
}
```
使用快捷键`alt+M`可以实时预览markdown文件，赶脚有点卡。

## 4、接下来需要
- 熟悉插件的快捷使用方法
- 熟悉更多sublime快捷键的使用

## 参考资料：

[Sublime Text 全程指南](http://zh.lucida.me/blog/sublime-text-complete-guide/)
[如何优雅地使用Sublime Text3](https://jeffjade.com/2015/12/15/2015-04-17-toss-sublime-text/#)
[Sublime Text 3前端开发常用优秀插件介绍](http://www.cnblogs.com/hykun/p/sublimeText3.html)
[Sublime Text的心得经验](https://github.com/jikeytang/sublime-text)
[Sublime Text3 + Markdown + 实时预览](http://www.cnblogs.com/james-lee/p/6847906.html)
[Sublime Text 3 MarkdownEditing布局设置](http://blog.csdn.net/hfut_jf/article/details/52853868)
[Sublime Text主题在线修改](http://tmtheme-editor.herokuapp.com)
