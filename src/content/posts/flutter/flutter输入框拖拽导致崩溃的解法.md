---
title: 安卓中 Flutter 输入框拖拽导致崩溃的解法
published: 2026-07-31
description: 'ReorderableListView 中的 TextField 拖拽导致崩溃的解决方案'
tags: ['Flutter', '输入框', 'TextField', '安卓', 'Android']
category: Flutter
draft: false
slug: flutter/textfield-crash-on-drag
---

# 问题原因

这种问题通常是因为在 `ReorderableListView` 中使用 `TextField` 时，拖拽操作会触发 `TextField` 的焦点变化，从而导致 Flutter 的渲染引擎在处理焦点变化时出现异常，最终导致应用崩溃。

# 解决方案

1. 在 `ReorderableListView` 中，将 `buildDefaultDragHandles` 设置为 `false`，避免长按触发拖拽。
2. 自定义拖拽手柄 `ReorderableDragStartListener`，只在特定区域触发拖拽。
3. 在拖拽代理之前清除焦点，调用 `FocusManager.instance.primaryFocus?.unfocus();`。

```dart
return Listener(
  onPointerDown: (_) {
    // 清除焦点，避免拖拽时触发 TextField 的焦点变化
    FocusManager.instance.primaryFocus?.unfocus();
  },
  child: ReorderableListView(
    buildDefaultDragHandles: false,
    children: items.map((item) {
      return ListTile(
        key: ValueKey(item),
        title: TextField(
          controller: TextEditingController(text: item),
        ),
        // 自定义拖拽手柄，点击时可清除焦点
        trailing: ReorderableDragStartListener(
          index: items.indexOf(item),
          child: Icon(Icons.drag_handle),
        ),
      );
    }).toList(),
    onReorder: (oldIndex, newIndex) {
      setState(() {
        if (newIndex > oldIndex) newIndex -= 1;
        final item = items.removeAt(oldIndex);
        items.insert(newIndex, item);
      });
    },
  ),
);
```