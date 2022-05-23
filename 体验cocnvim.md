# 体验cocnvim
在[coc.nvim](https://github.com/neoclide/coc.nvim)上查看文档，根据提示安装。

### 安装

注意，需要安装vim-plug。GitHub仓库里的指引看了也没看明白，重新找了别的文档:[VIM学习笔记 插件管理器(vim-plug)](https://zhuanlan.zhihu.com/p/56910536)，写得挺好，一看就懂了。

安装好后，coc默认可以根据上下文补全单词。参考这篇文章：[VIM——自动补全插件coc.nvim的安装与使用](https://blog.csdn.net/bojin4564/article/details/105832148)，要使coc发挥期望功效，还需要安装语言处理后端。**语言处理后端实际上很好安装，没必要去编辑配置文件，根据[coc-clangd](https://github.com/clangd/coc-clangd)中的步骤输入命令就可以了。**

### coc的默认配置文件

~~添加了coc推荐的vim配置之后，估计是改了什么配色，在termius里无法在vim分屏的时候看到文件名，所以我就把它去掉了。（并且自动高亮光标文本的功能也不好用，高亮颜色跟字体颜色差不多，看不清楚。）~~

还是需要添加配置文件，它里面带了很多快捷键和功能，例如代码格式化、引用跳转以及文档显示等。

### Modify Highlight settings

The default highlight background color is too light, so I can hardly see the text in Termius; while in iTerm on my Mac, the text becomes absolutely invisible.

Use `highlight CursorColumn cterm=bold cuter bag=DarkGrey` in `vimrc` file.

Ref: 
[vim 光标高亮行列的颜色设置](https://blog.csdn.net/iynu17/article/details/51509830) 
[vim的颜色修改，高亮设置。](https://blog.csdn.net/u010727765/article/details/77333803)

### 美化status bar

由于设置默认设置后status bar不显示内容了，我希望找个status bar的美化插件，解决显示文字问题的同时把status bar弄好看点。

安装了vim-airline，以便显示更好的文件信息。但是显示出来的状态栏是纯黑底色，啥也看不到。尝试安装powerline字体[powerline-fonts](https://github.com/powerline/fonts)。

### 重启vim前保存session，以便恢复

修改字体后需要重启vim以查看效果，但是我已经打开了一堆windows，我不希望一个个记住他们并在重启vim后再一个个手动打开，那太傻了。所以我需要保存浏览的session，并在下次启动时恢复。
我查到了这篇文章，很好地解决了我的问题：[VIM学习笔记 会话(Session)](https://zhuanlan.zhihu.com/p/84959887)

使用apt装上了，同时在vimrc里添加了`let g:airline_powerline_fonts = 1`，但还是不行，字体显示出来了，可是没有底色。

### tmux的终端模拟器设置

经过检查，发现应该是tmux没搞对，使用`echo $TERM`命令得到的输出是`screen`；而在tmux之外的默认terminal中，得到的输出是`xterm-256color`。参考：[iPad上的最强开发环境——1，iPad上学习编程的首选方式](https://zhuanlan.zhihu.com/p/373100540)，其中的第二节“美化tmux”介绍了更改terminal的方式。

**注意⚠️**： 使用文中的配置不管用，我改成了`set-option -g default-terminal 'xterm-256color'`，好使。

### tmux保存session

现在问题又来了，美化完tmux，还得重启才能生效。可是我已经打开了一大堆windows，重启后需要重新打开，太麻烦了。我需要保存session，重启并恢复。

参考：[Tmux会话保存与恢复](https://blog.csdn.net/qq_38789531/article/details/122846475)

安装好插件后，可以按`<C-b>, <C-s>`保存，按`<C-b>, <C-r>`恢复。

### Vim配色看不清

默认情况下，vim语法高亮的配色，给注释用了很不明显的深蓝色，在黑色terminal底色的配合下，非常费眼睛。

在`vimrc`文件中，添加/取消注释这一行配置：`set background=dark`，使配色为深底色terminal优化。

### Adding user-defined keyword highlight
[vim 添加自己的关键字高亮](http://blog.chinaunix.net/uid-23767307-id-3019546.html) According to this article, I added “NOTE”, “QUESTION” and “ANSWER” self-defined keyword highlights.

Steps to go:

- Note that, except for copy command line `syn keyword cTodo contained TODO FIXME XXX` to make a new syntax entry,
- and append the entry to the end of `syn cluster cCommentGroup contains=cTodo,cBadContinuation` syntax cluster. 
- Then, we need to add a highlight setting, e.g. `hl def link cNote    Todo` to make cNote just like Todos.
