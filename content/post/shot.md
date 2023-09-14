+++
title = "截图"
date = 2023-07-19
[taxonomies]
tags = ["截图","工具"]
[extra]
toc = true
+++

# 在Hyprland中截图

在Hyprland中截图有多种选择，在这里，我们选择使用`grim`+`slurp`的方式.

## 安装软件

在使用之前，我们需要先安装`grim`和`slurp`:

```shell
paru -S grim slurp
```

## 配置Hyprland快捷键以截图

在`~/.config/hypr/hyprland.conf`中添加以下内容:

```
$ShiftMod = SUPER_SHIFT
$Shift = SHIFT
$ALT = ALT
$screen_file=${HOME}/Pictures/Screenshots/screen_shot_$(date +%Y-%m-%d_%H-%M-%S).png
bind=$ShiftMod, S, exec, grim -g "$(slurp)" - | wl-copy
bind=,Print, exec, grim $screen_file
bind=$SHIFT, Print, exec, grim -g "$(slurp)" $screen_file
bind=$ALT, Print, exec, grim - | wl-copy
```

如果需要把截图文件保存到其他的地方可以修改`$screen_file`的值。

## 总结

这就是使用`grim`+`slurp`截图的方法。
