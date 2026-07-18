---
title: scrcpy简易使用手册
published: 2025-07-27
pinned: false
description: "scrcpy简易使用手册"
tags: ["scrcpy", "手册"]
category: scrcpy
draft: false
---

#### 快速上手

``````
scrcpy --video-codec=h265 --max-size=1920 --max-fps=60 --no-audio --keyboard=uhid

scrcpy --video-codec=h265 -m1920 --max-fps=60 --no-audio -K  # short version

scrcpy --no-audio -S  # 默认熄屏
``````

在新的虚拟显示器中启动VLC：

```scrcpy --new-display=1920x1080 --start-app=org.videolan.vlc```

#### 无线连接

修改无线调试端口：

```adb tcpip 5555```

连接：

```scrcpy --video-cache=h265 -m1920 --max-fps=60 --no-audio -K```

或者

```scrcpy --serial=192.168.1.1:5555```

其中，端口可以省略，此时默认为5555端口

#### 快捷键

|           操作           |                快捷键                |
| :----------------------: | :----------------------------------: |
|         切换全屏         |            ```alt + f```             |
|     左/右旋转显示屏      | ```alt + left arrow / right arrow``` |
|      暂停或重新显示      |            ```alt + z```             |
|       取消暂停显示       |        ```alt + shift + z```         |
|          home键          |       ```alt + h``` / 中键单击       |
|          back键          |       ```alt + b``` / 右键单击       |
|         多任务键         |            ```alt + s```             |
|         解锁屏幕         |            ```alt + m```             |
|         音量+/-          |  ```alt + up arrow / down arrow```   |
|          电源键          |            ```alt + p```             |
| 关闭设备屏幕（保持镜像） |            ```alt + o```             |
|       打开设备屏幕       |        ```alt + shift + o```         |



