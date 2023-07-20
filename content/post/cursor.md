+++
title = "设置光标主题"
date = 2023-07-19
[taxonomies]
tags = ["cursor","theme"]
[extra]
toc = true
+++

在Hyprland中设置光标主题，通常需要下面的几个步骤：

- 安装光标这主题或下载光标主题
- 通过*hyprland*的配置文件设置光标主题
- 为*xwayland*程序配置光标主题

> 因为笔者使用的是*ArchLinux*系统并且使用*paru*管理软件库，所以下面的软件的安装都以*paru*为主，
其他的系统和软件管理请自行查询。

# 安装/下载光标主题

## 安装光标主题

如果在`Aur`中存在你喜欢的光标主题，可以使用下面的命令来安装它，这里以*oreo*光标主题为例:

```shell
paru -S oreo-cursors-git
```

在安装分成后，就可以使用下面的方法来配置光标主题了。

## 手动下载光标主题

如果在`Aur`中没有你喜欢的光标主题，你可以通过下面的几个光标主题网站来下载你喜欢的光标主题:

- [GNOME Look](https://www.gnome-look.org/browse/cat/107/ord/latest/)
- [Deviant Art](https://www.deviantart.com/browse/all/customization/skins/linuxutil/x11cursors/)
- [Open Desktop](https://www.opendesktop.org/browse/cat/107/)

在手动下载完主题包后，需要把主题包解压到`~/.local/share/icons/`或`~/.icons`目录中。可以使用以下的命令来解压主题压缩包:

```shell
tar xvf foobar-cursor-theme.tar.gz -C ~/.local/share/icons
```

光标主题的目录结构应该为`theme-name/cursors`。请确保解压出的文件是这样的结构。

> 如果软件包包含一个*index.theme*文件，检查里面是否有"Inherits"这一行。如果有，检查继承的主题是否也存在(有必要时重命名)。

# 为*xwayland*程序配置光标主题

如果想要为指定用户配置光标主题，创建并编辑`~/.icons/default/index.theme`;如果想要*系统配置*光标主题,编辑*/usr/share/icons/default/index.theme*。

`[icon theme]`部分的*Inherits*选项必须被设置为X光标主题的目录名*cursor_theme_name*，比如*oreo_spark_green_cursors*:

```
[icon theme]
Inherits=oreo_spark_green_cursors
```

之后编辑`~/.config/gtk-3.0/settings.ini`,将`cursor_theme_name`改为你喜欢的光标主题名称:

```
[Settings]
gtk-cursor-theme-name=oreo_spark_green_cursors
```

重启X以应用更改。
