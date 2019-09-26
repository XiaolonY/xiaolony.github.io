---
title: VsCode 终端中文乱码解决办法
categories: 学习笔记
tags:
  - 开发工具
copyright: false
---
{% cq %}
最近换了 Debian 9 的系统，重新部署了一下开发环境。在安装完 VsCode 之后，发现在终端里输出中文文件名时出现一堆 ??? 。
{% endcq %}
<!-- more -->
### 原因分析
不能正确输出你想要的文字时，一是可能你写错了，二是计算机不认识。所以如果能保证自己没写错，那就是计算机不认识你写的东西了，也就是说编码或者相关语言配置不对了。
### 问题解决
既然知道了大概的原因了，那就看一下目前在 VsCode 终端里是使用的什么语言和编码吧。
使用 `locale` 命令 或者 `echo` 输出一下要查看的环境变量。
<br>
我这里用的是 `locale` 命令查看全部的语言环境设置，发现设置的值是 `en_US.UTF-8`，编码没问题，但是语言却是英语（美国）而不是中文（简体）。
<br>
使用 `LANG="zh_CN.UTF-8` 临时设置一下环境变量， 重新输出一下中文文件名，发现输出正常了。
<br>
找到解决办法了，但是这是一种临时生效的方法，怎样才能让它长期生效呢？
<br>
VsCode 配置文件里有一个配置项 `terminal.integrated.env.*` 可以添加环境变量到 VsCode 进程中, 因为我是 `linux` 系统，所以在配置文件 `setting.json` 中使用 `terminal.integrated.env.linux` 来配置：
``` json
"terminal.integrated.env.linux": {
    "LC_ALL": "zh_CN.UTF-8"
}
```
配置后保存，重启 VsCode 终端， 生效。
### 举一反三
如果在使用 linux 的时候发现内置终端的中文乱码，也是可以采用这种方法来解决的，修改 `.bashrc` 文件可以长期修改环境变量。
