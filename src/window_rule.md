# 窗口规则

> ⚠️ 窗口规则是区分大小写的。如(firefox!=Firefox);

到目前为止，Hyprland的窗口规则分为*V1*和*V2*两个版本的规则。其基本语法为：
```ini
windowrule=RULE,WINDOW
windowrulev2=RULE,(WINDOW)+
```

- RULE 是一个[规则](#rule)
- WINDOW 是一个正则表达式,用于匹配窗口

其中*V2*对比*V1*对于规则没有变化，主要是WINDOW的匹配有了变化。有了更多的支持。其中*V1*版本的窗口匹配如下:

- 一个正则表达式，用于匹配窗口的class属性
- `title:` 后跟一个正则表达式，用于匹配窗口的title属性

而*V2*版本的窗口匹配就比较多了，可以查看下面的[详情](#v2版窗口匹配).

# V2版窗口匹配

在窗口匹配的V2版本中，可以使用多个表达式对窗口进行匹配，只有可以同时满足指定的多个匹配的窗口才可以应用规则。如:

```ini
windowrulev2 = float, class:^(kitty)$, title:^(kitty)$
```

在上面的例子中,只有title和class属性都为*kitty*的窗口才会应用*float*(浮动)效果。

到目前为止，V2版本的窗口匹配支持以下内容:

字段 | 描述
---|---
class:\[regex] | 指定正则表达式匹配*class*属性的窗口
title:\[regex] | 指定正则表达式匹配*title*属性的窗口
initialClass:\[regex] | 指定正则表达式匹配*initialClass*属性的窗口
initialTitle:\[regex] | 指定正则表达式匹配*initialTitle*属性的窗口
tag:\[name] | 匹配*tag*属性的窗口
xwayland:\[0/1] | *xwayland*为指定值的窗口
floating:\[0/1] | *floating*为指定值的窗口
fullscreen:\[0/1] | *fullscreen*为指定值的窗口
pinned:\[0/1] | *pinned*为指定值的窗口
focus:\[0/1] | *focus*为指定值的窗口
workspace:\[w] | 在指定workspace上的窗口。其中,*w*可以是*id*或*name:string*
onworkspace:\[w] | 在指定workspace上的窗口。其中,*w*可以是*id*或*name:string*或*workspace selector*
fullscreenstate:\[internal] \[client] | 符合指定全屏状态的窗口。*internal*和*client*可以为 全屏状态[^1] 的值。

[^1]: `*` -any, `0` - none, `1` - 最大化, `2` - 全屏, `3` - 最大化和全屏


# rule

## 静态规则

只在窗口打开时执行一次，之后不再执行的规则称之为静态规则。下面是一些具体的规则：

规则 | 描述
---|---
float | 浮动窗口
tile | 平铺窗口
fullscreen | 窗口全屏
maximize | 最大化窗口
fullscreenstate \[internal] \[client] | 设置窗口的全屏模式[^1]和发送给客户端的模式
move \[x] \[y] | 移动浮动窗口到指定位置。x和y的值可以支持整型或百分比。如20%或100。同时还支持计算，如*100%-20*.此外，还允许窗口宽度进入计算，如*100%-w-20*，其中的*w*就表示窗口的宽度。
size \[x] \[y] | 调整浮动窗口的大小，*x*和*y*的值可以是整型或百分比。
center ([opt]) | 设置激光器窗口居中，如果*opt*参数为*1*，可以确保窗口居中时不会侵入到显示器的保留区域[^2]。
pseudo | 伪平铺窗口
monitor \[id] | 指定窗口打开于哪个显示器。*id*值可以是显示器id或显示器名称,比如`1`或`DP-1`。
workspace \[w] | 指定窗口打开于哪个工作区。对于*w*的命令可以参考[工作区](./workspace.md)。此外，还可以设置*w*为*unset*，以取消之前应用于此窗口的所有工作区规则。还可以设置*w*为*slient*，以使应用在指定的工作区静默打开。
noinitialfocus | 禁用窗口的初始化焦点
pin | 钉住窗口，比如让窗口在所有工作区显示
unset | 取消窗口之前的所有规则
nomaxsize | 取消窗口的最大化限制
stayfocused | 只有窗口可见，就强制聚集该窗口
group \[options] | 设置窗口的组属性
suppressevent \[types...] | 让窗口忽略指定事件,多个事件以空格分隔，可用的事件包括:*fullscreen*,*maximize*,*activate*,*activatefocus*

[^2]: 显示器的保留区域是指在显示器屏幕边缘的一定区域内不进行窗口排列和管理的区域。这个概念通常出现在桌面环境或窗口管理器中，目的是为了提供一个清晰、整洁且易于管理的桌面体验。保留区域的设置可以防止窗口过于靠近屏幕边缘，从而避免用户在点击或操作窗口时不小心触发屏幕边缘的滚动或其他系统级行为。

## 动态规则

TODO
