---
title: Flutter 输入框 TextField 笔记
published: 2025-07-28
updated: 2025-07-28
pinned: false
tags: ["Flutter", "输入框", "TextField"]
category: Flutter
draft: true
slug: flutter/textfield
---

```dart
(new) TextField({
  Key? key,
  Object groupId = EditableText,
  TextEditingController? controller,
  FocusNode? focusNode,
  UndoHistoryController? undoController,
  InputDecoration? decoration = const InputDecoration(),
  TextInputType? keyboardType,
  TextInputAction? textInputAction,
  TextCapitalization textCapitalization = TextCapitalization.none,
  TextStyle? style,
  StrutStyle? strutStyle,
  TextAlign textAlign = TextAlign.start,
  TextAlignVertical? textAlignVertical,
  TextDirection? textDirection,
  bool readOnly = false,
  ToolbarOptions? toolbarOptions,
  bool? showCursor,
  bool autofocus = false,
  WidgetStatesController? statesController,
  String obscuringCharacter = '•',
  bool obscureText = false,
  bool? autocorrect,
  SmartDashesType? smartDashesType,
  SmartQuotesType? smartQuotesType,
  bool enableSuggestions = true,
  int? maxLines = 1,
  int? minLines,
  bool expands = false,
  int? maxLength,
  MaxLengthEnforcement? maxLengthEnforcement,
  void Function(String)? onChanged,
  void Function()? onEditingComplete,
  void Function(String)? onSubmitted,
  void Function(String, Map<String, dynamic>)? onAppPrivateCommand,
  List<TextInputFormatter>? inputFormatters,
  bool? enabled,
  bool? ignorePointers,
  double cursorWidth = 2.0,
  double? cursorHeight,
  Radius? cursorRadius,
  bool? cursorOpacityAnimates,
  Color? cursorColor,
  Color? cursorErrorColor,
  BoxHeightStyle? selectionHeightStyle,
  BoxWidthStyle? selectionWidthStyle,
  Brightness? keyboardAppearance,
  EdgeInsets scrollPadding = const EdgeInsets.all(20.0),
  DragStartBehavior dragStartBehavior = DragStartBehavior.start,
  bool? enableInteractiveSelection,
  bool? selectAllOnFocus,
  TextSelectionControls? selectionControls,
  void Function()? onTap,
  bool onTapAlwaysCalled = false,
  void Function(PointerDownEvent)? onTapOutside,
  void Function(PointerUpEvent)? onTapUpOutside,
  MouseCursor? mouseCursor,
  Widget? Function(BuildContext, {required int currentLength, required bool isFocused, required int? maxLength})? buildCounter,
  ScrollController? scrollController,
  ScrollPhysics? scrollPhysics,
  Iterable<String>? autofillHints = const <String>[],
  ContentInsertionConfiguration? contentInsertionConfiguration,
  Clip clipBehavior = Clip.hardEdge,
  String? restorationId,
  bool scribbleEnabled = true,
  bool stylusHandwritingEnabled = EditableText.defaultStylusHandwritingEnabled,
  bool enableIMEPersonalizedLearning = true,
  Widget Function(BuildContext, EditableTextState)? contextMenuBuilder = _defaultContextMenuBuilder,
  bool canRequestFocus = true,
  SpellCheckConfiguration? spellCheckConfiguration,
  TextMagnifierConfiguration? magnifierConfiguration,
  List<Locale>? hintLocales,
})
```

---

## KeyBoardType

控制输入框的键盘类型，常用类型如下

| 枚举值 | 说明 |
|-------------|------|
| text        | 普通文本输入 |
| number      | 数字输入 |
| phone       | 电话号码输入 |
| email       | 邮箱输入 |
| url         | URL输入 |
| datetime    | 日期时间输入 |

## maxLengthEnforcement

文本超过 maxLength 时的截断策略。

| 枚举值 | 说明 |
|--------|------|
| none   | 不限制输入长度，允许超出 maxLength |
| enforced | 强制执行最大长度限制，用户无法输入超过最大长度的字符，包括粘贴操作，<br/>且使用中文输入法内嵌候选时，超出长度会直接截断。<br/>适用于输入验证码、手机号等纯数字场景 |
| truncateAfterCompositionEnds | 在中文输入法内嵌候选时，超出长度会在候选结束后截断。<br/>适用于输入中文、英文单词等文本场景 |

```dart
// 6位验证码
TextField(
  keyboardType: TextInputType.number,
  maxLength: 6,
  maxLengthEnforcement: MaxLengthEnforcement.enforced,
)

// 普通文本输入
TextField(
  maxLength: 20,
  maxLengthEnforcement: MaxLengthEnforcement.truncateAfterCompositionEnds,
)
```
