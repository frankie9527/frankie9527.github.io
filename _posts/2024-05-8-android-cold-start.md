---
title: android 冷启动优化
description: android 冷启动优化
author: cotes
date: 2024-05-8 2:53:00 +0800
categories: [ android, mac ]
tags: [ mac ]
render_with_liquid: false


---
# 抓去trace 文件
- adb 抓取命令 adb shell atrace -b 25600 --async_start wm am gfx dalvik binder_lock binder_driver sched
- adb 保存命令 adb shell atrace --async_stop -o /data/local/tmp/boot_trace
- 把手机上的boot-trace 导入到电脑
- 打开网页并分析 http://ui.perfetto.dev/


# 其他
- 显示隐藏文件 shift +command + 。
- 截屏 shift +command + 3/4/5/6
- 关闭当前窗口 command + Q
- 文件排序 control +command +1/2/3
- 打开某个文件（Terminal 输入） open + 文件名
- 安装git（Terminal 输入）git
