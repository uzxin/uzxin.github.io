---
title: windows用cmd命令查看主板支持的最大内存
date: 2020-12-31 10:47:44
categories: windows
tags: windows
---

## 1.同时按住键盘上的win+R，打开运行

![](http://114.55.28.2/images/hexo/2020/12/31/1.png)

## 2.输入cmd，按下回车或者点确定

![](http://114.55.28.2/images/hexo/2020/12/31/2.png)

## 3.在dos命令窗口，输入“wmic memphysical get maxcapacity”，按回车

![](http://114.55.28.2/images/hexo/2020/12/31/3.png)

用得出的数值除以1024得出的是M单位，再除以1024得出的是G单位

![](http://114.55.28.2/images/hexo/2020/12/31/4.png)

得出16，说明电脑最大支持16G运行内存