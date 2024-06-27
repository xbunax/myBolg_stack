---
title: "Spotify Tui"
description: 
date: 2024-03-06T13:17:22+08:00
image: https://raw.githubusercontent.com/xbunax/blogImg/main/spotify_tui/cover.png 
math: 
license: 
categories : [
"Spotify",
"Macos",
"Beautify"
]
hidden: false
comments: true
toc: true
draft: false
---

对于使用Spotify作为主力音乐流媒体的人来说，Spotify官方的桌面app体验并不是很好，无法看歌词，而且UI水平对于我个人审美来说感觉并不是很好看。

![spotify_desktop](https://raw.githubusercontent.com/xbunax/blogImg/main/spotify_tui/spotify_desktop.png )

***
### Spotify 第三方客户端

#### Spotify webUI
这时候就要选择第三方的Spotify客户端了，或者也可以使用Spotify的webUI然后使用美化插件，我webUI使用的Arc浏览器搭配上Gallery美化，其实最后的效果还可以，而且很轻量化，除了没法看歌词都很完美。

![spotify_web](https://raw.githubusercontent.com/xbunax/blogImg/main/spotify_tui/spotify_web.png )

#### Spotify TUI
但是webUI到底还是官方的UI而且没法看歌词，而且作为重度终端使用者，还是希望在终端上使用Spotify。我选择使用的是[`spotify_player`](https://github.com/aome510/spotify-player)一个用rust开发的开源的Spotify TUI，使用vim的键位并且在`iTerm2`中可以显示专辑封面，同时也可以在配置文件`~/.config/spotify-player/app.toml`中进行自定义。

![spotify_tui_playback](https://raw.githubusercontent.com/xbunax/blogImg/main/spotify_tui/spotify_tui_playback.png)
### Spotify Lyrics

接下来要解决官方客户端无法看歌词的问题，我们可以使用[`sptlrx`](https://github.com/raitonoberu/sptlrx.git)这个开源的终端歌词同步软件，搭配`spotify_player`使用可以看当前歌曲的歌词。

![sptlrx](https://raw.githubusercontent.com/xbunax/blogImg/main/spotify_tui/sptlrx.gif)

### Custom Your TUI

这样我们就实现了在终端上使用Spotify并且显示滚动歌词，同时搭配[`cava`](https://github.com/karlstav/cava#macos-1)(一个Audio Visualizer，依赖[`backgroud Music`](https://github.com/kyleneideck/BackgroundMusic)实现)，最后使用[`tty-clock`](https://github.com/xorg62/tty-clock)为整个布局点缀一下，就可以实现封面的效果了。

![Spotify](https://raw.githubusercontent.com/xbunax/blogImg/main/spotify_tui/cover.png)

### Optimization

虽然这样布局很不错，但是每次都要手动分屏很麻烦，能不能实现在终端敲一个命令自动分屏布局并且每个`pane`自动执行对应的命令呢，当然是可以的啦。

我一开始选择使用`tmux`和`tmuxp`这样就可以用`yml`配置文件写好`tmux session`布局并且在对应的`pane`执行不同的命令，但是研究了一下`tmuxp`发现好像无法实现封面那样的复杂布局，只有几个预设的布局，而且`tmux`无法显示超过1M大小的图片所以`spotify_player`无法显示图片。

所以最后另辟蹊径，使用`AppleScript`直接对`iTerm2`进行布局。


```AppleScript
tell application "iTerm"
	tell current window
		tell current session of current tab
			split vertically with default profile
			split vertically with default profile
		end tell
		tell third session of current tab
			split horizontally with default profile
		end tell
		tell first session of current tab
			write text "spotify_player"
		end tell
		tell second session of current tab
			write text "sptlrx"
		end tell
		tell third session of current tab
			write text "tty-clock -c -s"
		end tell
		tell fourth session of current tab
			write text "cava"
		end tell
	end tell
end tell
```

这样将`AppleScript`保存为`scpt`文件，只需要在终端中用`osascript scpt文件路径`执行`AppleScript`脚本就可以实现一键布局啦。如果嫌每次输`osascript`命令很麻烦，在`~/.zshrc`中用`alias`映射一下命令或者写个`shell`脚本添加到环境变量就可以啦。


<video width="720" height="480" controls>
  <source src="https://raw.githubusercontent.com/xbunax/blogImg/main/spotify_tui/result.mp4" type="video/mp4">
</video>

这就是最后的效果啦。

***
> - 如果要使用本教程需要会一点`Unix-like`系统的操作，最基础的`ls cd`这些需要会使用，如果是Mac则要安装`Homebrew`作为包管理器，方便管理和安装。
> - 如果要使用`spotify_player`需要一个Spotify的会员账号，并且去[dev spotify](https://developer.spotify.com/documentation/web-api)申请一个`client id`。
