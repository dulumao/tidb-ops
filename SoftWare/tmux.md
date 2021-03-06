---
title: Tmux 快捷键 & 速查表
toc: true
tags:
  - Tmux
date: 2009-01-01 21:40:52
updated: 2009-01-01 21:40:52
categories:
  - software
---
# Tmux 快捷键 & 速查表

## 扩展阅读

- [Tmux 使用手册](http://louiszhai.github.io/2017/09/30/tmux/)
- [Arch linux Tmux (简体中文)](https://wiki.archlinux.org/index.php/Tmux_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87))
- [man Tmux](http://man7.org/linux/man-pages/man1/tmux.1.html)

## Tmux 介绍

#### 安装

- Ubuntu

`sudo apt-get install tmux`

- Centos

`yum install tmux -y`

#### 会话，窗口，面板

根据 tmux 的定义，在开启了 tmux 服务器后，会首先创建一个会话，而这个会话则会首先创建一个 窗口，其中仅包含一个面板；也就是说，这里看到的所谓终端控制台应该称作 tmux 的一个面板， 虽然其使用方法与终端控制台完全相同。

tmux 使用 C/S 模型构建，主要包括以下单元模块：

- server 服务器。输入 tmux 命令时就开启了一个服务器。
- session 会话。一个服务器可以包含多个会话
- window 窗口。一个会话可以包含多个窗口。
- pane 面板。一个窗口可以包含多个面板。

#### 初体验

启动新会话

    tmux [new -s 会话名 -n 窗口名]
    tmux new -s test -n tmux

保存会话退出

    tmux detach # 断开当前会话，会话在后台运行
    Ctrl + b  d # 快捷键保存退出当前会话

列出所有会话

    tmux list-session
    tmux ls

恢复会话

    tmux a [-t 会话名]
    tmux attach-session -t session-name     # 连接指定会话
    tmux a -t session-name                  # 连接指定会话
    tmux a                                  # 在上次保存退出位置登陆

关闭会话

    tmux kill-session           # 关闭服务，所有会话退出
    tmux kill-session -t 会话名  # 指定会话退出
    Ctrl + c                    # 在会话内强制退出

关闭所有会话

    tmux ls | grep : | cut -d. -f1 | awk '{print substr($1, 0, length($1)-1)}' | xargs kill

## Tmux 快捷键

> tmux 的所有指令，都包含同一个前缀，默认为 Ctrl+b，输入完前缀过后，控制台激活，命令按键才能生效。

### 系统快捷键

前缀 | 指令 | 描述
------- | ------- | -------
Ctrl+b | ? | 显示快捷键帮助文档；按 q 返回
Ctrl+b | d | 断开当前会话；这样可以暂时返回 Shell 界面，输入 tmux attach 能够重新进入之前的会话
Ctrl+b | D | 选择要断开的会话；在同时开启了多个会话时使用
Ctrl+b | Ctrl+z | 挂起当前会话
Ctrl+b | r | 强制重载当前会话
Ctrl+b | s | 显示会话列表用于选择并切换；在同时开启了多个会话时使用
Ctrl + b  | $ | 重命名当前会话
Ctrl+b | : | 进入命令行模式；此时可以输入支持的命令，例如 kill-server 可以关闭服务器
Ctrl+b | [ | 进入复制模式；此时的操作与 vi/emacs 相同，按 q 退出
Ctrl+b | ] | 粘贴复制模式中复制的文本
Ctrl+b | ~ | 列出提示信息缓存；其中包含了之前 tmux 返回的各种提示信息

### 窗口快捷键

前缀 | 指令 | 描述
------- | ------- | -------
Ctrl+b | c | 新建窗口
Ctrl+b | & | 关闭当前窗口（关闭前需输入 y or n 确认）
Ctrl+b | 0 ~ 9 | 切换到指定窗口
Ctrl+b | p | 切换到上一窗口
Ctrl+b | n | 切换到下一窗口
Ctrl+b | w | 打开窗口列表，用于且切换窗口
Ctrl+b | , | 重命名当前窗口
Ctrl+b | . | 修改当前窗口编号（适用于窗口重新排序）
Ctrl+b | f | 快速定位到窗口（输入关键字匹配窗口名称）

### 面板快捷键

前缀 | 指令 | 描述
------- | ------- | -------
Ctrl+b | " | 当前面板上下一分为二，下侧新建面板
Ctrl+b | % | 当前面板左右一分为二，右侧新建面板
Ctrl+b | o | 选择下一面板
Ctrl+b | x | 关闭当前面板（关闭前需输入 y or n 确认）
Ctrl+b | z | 最大化当前面板，再重复一次按键后恢复正常（v1.8 版本新增）
Ctrl+b | ! | 将当前面板移动到新的窗口打开（原窗口中存在两个及以上面板有效）
Ctrl+b | ; | 切换到最后一次使用的面板
Ctrl+b | q | 显示面板编号，在编号消失前输入对应的数字可切换到相应的面板
Ctrl+b | { | 向前置换当前面板
Ctrl+b | } | 向后置换当前面板
Ctrl+b | Ctrl+o | 顺时针旋转当前窗口中的所有面板
Ctrl+b | alt +o | 逆时针旋转当前窗口中的所有面板
Ctrl+b | 方向键 | 移动光标切换面板
Ctrl+b | 空格键 | 在自带的面板布局中循环切换；依次包括even-horizontal、even-vertical、main-horizontal、main-vertical、tiled
Ctrl+b | Alt + 方向键 | 以 5 个单元格为单位调整当前面板边缘
Ctrl+b | Ctrl + 方向键 | 以 1 个单元格为单位调整当前面板边缘（Mac 下被系统快捷键覆盖）
Ctrl+b | t | 显示时钟

### 调整窗口排序

    swap-window -s 3 -t 1  交换 3 号和 1 号窗口
    swap-window -t 1       交换当前和 1 号窗口
    move-window -t 1       移动当前窗口到 1 号

### 同步窗格

这么做可以切换到想要的窗口，输入 Tmux 前缀和一个冒号呼出命令提示行，然后输入：

```bash
:setw synchronize-panes
```

你可以指定开或关，否则重复执行命令会在两者间切换。
这个选项值针对某个窗口有效，不会影响别的会话和窗口。
完事儿之后再次执行命令来关闭。[帮助](http://blog.sanctum.geek.nz/sync-tmux-panes/)

### 调整窗格尺寸

如果你不喜欢默认布局，可以重调窗格的尺寸。虽然这很容易实现，但一般不需要这么干。这几个命令用来调整窗格：

    PREFIX : resize-pane -D          当前窗格向下扩大 1 格
    PREFIX : resize-pane -U          当前窗格向上扩大 1 格
    PREFIX : resize-pane -L          当前窗格向左扩大 1 格
    PREFIX : resize-pane -R          当前窗格向右扩大 1 格
    PREFIX : resize-pane -D 20       当前窗格向下扩大 20 格
    PREFIX : resize-pane -t 2 -L 20  编号为 2 的窗格向左扩大 20 格

### 文本复制模式：

按下 ** 前缀 [** 进入文本复制模式。可以使用方向键在屏幕中移动光标。默认情况下，方向键是启用的。在配置文件中启用 Vim 键盘布局来切换窗口、调整窗格大小。Tmux 也支持 Vi 模式。要是想启用 Vi 模式，只需要把下面这一行添加到 .tmux.conf 中：

    setw -g mode-keys vi

启用这条配置后，就可以使用 h、j、k、l 来移动光标了。

想要退出文本复制模式的话，按下回车键就可以了。一次移动一格效率低下，在 Vi 模式启用的情况下，可以辅助一些别的快捷键高效工作。

例如，可以使用 w 键逐词移动，使用 b 键逐词回退。使用 f 键加上任意字符跳转到当前行第一次出现该字符的位置，使用 F 键达到相反的效果。

    vi             emacs        功能
    ^              M-m          反缩进
    Escape         C-g          清除选定内容
    Enter          M-w          复制选定内容
    j              Down         光标下移
    h              Left         光标左移
    l              Right        光标右移
    L                           光标移到尾行
    M              M-r          光标移到中间行
    H              M-R          光标移到首行
    k              Up           光标上移
    d              C-u          删除整行
    D              C-k          删除到行末
    $              C-e          移到行尾
    :              g            前往指定行
    C-d            M-Down       向下滚动半屏
    C-u            M-Up         向上滚动半屏
    C-f            Page down    下一页
    w              M-f          下一个词
    p              C-y          粘贴
    C-b            Page up      上一页
    b              M-b          上一个词
    q              Escape       退出
    C-Down or J    C-Down       向下翻
    C-Up or K      C-Up         向下翻
    n              n            继续搜索
    ?              C-r          向前搜索
    /              C-s          向后搜索
    0              C-a          移到行首
    Space          C-Space      开始选中
                   C-t          字符调序

### 杂项：

    d  退出 tmux（tmux 仍在后台运行）
    t  窗口中央显示一个数字时钟
    ?  列出所有快捷键
    :  命令提示符

### 配置选项：

    # 鼠标支持 - 设置为 on 来启用鼠标
    * setw -g mode-mouse off
    * set -g mouse-select-pane off
    * set -g mouse-resize-pane off
    * set -g mouse-select-window off

    # 设置默认终端模式为 256color
    set -g default-terminal "screen-256color"

    # 启用活动警告
    setw -g monitor-activity on
    set -g visual-activity on

    # 居中窗口列表
    set -g status-justify centre

    # 最大化 / 恢复窗格
    unbind Up bind Up new-window -d -n tmp \; swap-pane -s tmp.1 \; select-window -t tmp
    unbind Down
    bind Down last-window \; swap-pane -s tmp.1 \; kill-window -t tmp

### 配置文件（~/.tmux.conf）：

```bash
# 基础设置
set -g default-terminal "screen-256color"
set -g display-time 3000
set -g escape-time 0
set -g history-limit 65535
set -g base-index 1
set -g pane-base-index 1

# 前缀绑定 (Ctrl+a)
set -g prefix ^a
unbind ^b
bind a send-prefix

# 分割窗口
unbind '"'
bind - splitw -v
unbind %
bind | splitw -h

# 选中窗口
bind-key k select-pane -U
bind-key j select-pane -D
bind-key h select-pane -L
bind-key l select-pane -R

# copy-mode 将快捷键设置为 vi 模式
setw -g mode-keys vi

# 启用鼠标 (Tmux v2.1)
set -g mouse on

# 更新配置文件
bind r source-file ~/.tmux.conf \; display "已更新"

#<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<
# Tmux Plugin Manager(Tmux v2.1)
# Tmux Resurrect
set -g @plugin 'tmux-plugins/tmux-resurrect'

# List of plugins
set -g @plugin 'tmux-plugins/tpm'
set -g @plugin 'tmux-plugins/tmux-sensible'

# Other examples:
# set -g @plugin 'github_username/plugin_name'
# set -g @plugin 'git@github.com/user/plugin'
# set -g @plugin 'git@bitbucket.com/user/plugin'

# Initialize TMUX plugin manager (keep this line at the very bottom of tmux.conf)
run '~/.tmux/plugins/tpm/tpm'
#>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>
```
