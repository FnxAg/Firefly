---
title: Flutter 教程与资料收录
published: 2026-07-29
updated: 2026-07-29
pinned: false
tags: ["Flutter", "教程", "资料"]
category: Flutter
draft: true
sourceLink: https://juejin.cn/post/6910163213778681864
slug: flutter/tutorials-and-resources
---

# TextField

## 1

[稀土掘金 https://juejin.cn/post/6910163213778681864](https://juejin.cn/post/6910163213778681864)

### 效果

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/11d5cd08fd7c40c0a21823bf7b508f62~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.webp)

> 终于还是对`TextField`下手了，这个属性最多、功能点最多的Widget。

### 基本属性

`TextField`是一个`material design`风格的输入框，本身有多种属性，除此之外装饰器`InputDecoration`也有多种属性，但都比较简单，所以不必担心，且听我娓娓道来。

先看一下源码，重要或常用的属性会有注释。

#### TextField

```dart
  const TextField({
    Key key,
    this.controller,//控制器
    this.focusNode,//焦点
    this.decoration = const InputDecoration(),//装饰
    TextInputType keyboardType,//键盘类型，即输入类型
    this.textInputAction,//键盘按钮
    this.textCapitalization = TextCapitalization.none,//大小写
    this.style,//样式
    this.strutStyle,
    this.textAlign = TextAlign.start,//对齐方式
    this.textDirection,
    this.autofocus = false,//自动聚焦
    this.obscureText = false,//是否隐藏文本，即显示密码类型
    this.autocorrect = true,//自动更正
    this.maxLines = 1,//最多行数，高度与行数同步
    this.minLines,//最小行数
    this.expands = false,
    this.maxLength,//最多输入数，有值后右下角就会有一个计数器
    this.maxLengthEnforced = true,
    this.onChanged,//输入改变回调
    this.onEditingComplete,//输入完成时，配合TextInputAction.done使用
    this.onSubmitted,//提交时,配合TextInputAction
    this.inputFormatters,//输入校验
    this.enabled,//是否可用
    this.cursorWidth = 2.0,//光标宽度
    this.cursorRadius,//光标圆角
    this.cursorColor,//光标颜色
    this.keyboardAppearance,
    this.scrollPadding = const EdgeInsets.all(20.0),
    this.dragStartBehavior = DragStartBehavior.start,
    this.enableInteractiveSelection,
    this.onTap,//点击事件
    this.buildCounter,
    this.scrollPhysics,
  }) 

```

参数很多，其实日常开发中连一半的属性都用不到，但还是会尽量多的介绍。

#### InputDecoration

```dart
  const InputDecoration({
    this.icon,//左侧外的图标
    this.labelText,//悬浮提示，可代替hintText
    this.labelStyle,//悬浮提示文字的样式
    this.helperText,//帮助文字
    this.helperStyle,
    this.hintText,//输入提示
    this.hintStyle,
    this.hintMaxLines,
    this.errorText,//错误提示
    this.errorStyle,
    this.errorMaxLines,
    this.hasFloatingPlaceholder = true,//是否显示悬浮提示文字
    this.isDense,
    this.contentPadding,//内填充
    this.prefixIcon,//左侧内的图标
    this.prefix,
    this.prefixText,//左侧内的文字
    this.prefixStyle,
    this.suffixIcon,//右侧内图标
    this.suffix,
    this.suffixText,
    this.suffixStyle,
    this.counter,//自定义计数器
    this.counterText,//计数文字
    this.counterStyle,//计数样式
    this.filled,//是否填充
    this.fillColor,//填充颜色
    this.errorBorder,
    this.focusedBorder,
    this.focusedErrorBorder,
    this.disabledBorder,
    this.enabledBorder,
    this.border,//边框
    this.enabled = true,
    this.semanticCounterText,
    this.alignLabelWithHint,
  })

```

参数很多，多为一个小功能点的图标、文字和样式，并不复杂。

> ok，基本属性大概过一遍，脑子里有个印象就行了。下面开始实操。

### 样式

#### 基础样式

```dart
			TextField(),

```

很简单，无任何参数，当然效果也很简单。

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/6b55c769c743419386a818adcd9aacd2~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.webp)

style可以修改样式。

#### 隐藏文本

修改`obscureText`属性值

```dart
              TextField(
                obscureText: true,
              ),

```

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/bd99d47dc568493f92dab6b818553786~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.webp)

可以看到输入的内容已经不可见了，变成常见的密码类型了。

#### 键盘类型

键盘类型 即 可输入的类型，比如`number`就只能输入数字

```dart
              TextField(
                keyboardType: TextInputType.number,
              ),

```

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/a4d021de348048ee9a812aba51d5b502~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.webp)

`TextInputType`可选类型：

* text
* multiline
* number
* phone
* datetime
* emailAddress
* url

#### 键盘按钮

即键盘右下角的按钮，常见的比如完成，右下角是一个完成的对号按钮，上图即是。

```dart
              TextField(
                textInputAction: TextInputAction.done,
              ),

```

`TextInputAction`其他选项：

* none
* unspecified
* done
* go
* search
* send
* next
* previous
* continueAction
* join
* route
* emergencyCall
* newline

#### 大小写

即控制输入的英文字母大小写，比如单词首字母大写

```dart
              TextField(
                textCapitalization: TextCapitalization.words,
              ),

```

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/6022f771bf6f42a08230bf3676d94f92~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.webp)

`TextCapitalization`的其他选项：

* words：单词首字母大写
* sentences：句子的首字母大写
* characters：所有字母大写
* none：默认无

#### 光标

默认是一个蓝色的竖线

```dart
              TextField(
                cursorColor: Colors.orange,
                cursorWidth: 15,
                cursorRadius: Radius.circular(15),
              ),

```

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/7eeb8724788948fcadfbf388ce39538f~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.webp)

#### 最多行数

设置最多3行

```dart
              TextField(
                maxLines: 3,
              ),

```

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/a077af9a15474f0b99f11245404e0ee7~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.webp)

从效果可以看出，TextField高度已经变成了3行。但是我只是想最多输入3行，默认还是1行的高度怎么办呢？ 不用慌，加一个参数就行了： `minLines`

```dart
              TextField(
                maxLines: 3,
                minLines: 1,
              ),

```

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/5db65d76e2a94c8db108b1ecfb887b7c~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.webp)

可以看到，TextField的高度是会自适应的。

#### 计数器

即右下角会有一个计数

```dart
              TextField(
                maxLength: 8,
              ),

```

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/8ac7385200e74265ac30f8e615d9b590~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.webp)

默认：当前输入长度/最大长度，那这个地方我们能不能改呢，当然可以，下面简单操作一下

```dart
              TextField(
                maxLength: 8,
                decoration: InputDecoration(
                  counter: Text("自定义计数 0/100"),
                ),
              ),

```

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/ef1633ae021541aea3343a2b39682e37~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.webp)

这里我用到了装饰`InputDecoration`下的`counter`，类型是`widget`，那扩展度就相当高了，我只用了一个`Text`，别的widget也是可以的。

如果只是纯文字的话，InputDecoration下还有一个`counterText`属性和`counterStyle`。

#### 图标

图标有3种：

* 左侧外的图标

```dart
              TextField(
                decoration: InputDecoration(
                  icon: Icon(Icons.person),
                ),
              ),

```

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/557bfefc48524b2d88456e39bc5ddf01~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.webp)

* 左侧内图标

```dart
              TextField(
                decoration: InputDecoration(
                  prefixIcon: Icon(Icons.phone_android),
                ),
              ),

```

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/d2e67372352c4d0a86d7c54b4c4811f9~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.webp)

* 右侧内图标

```dart
              TextField(
                decoration: InputDecoration(
                  suffixIcon: IconButton(
                    icon: Icon(Icons.close),
                    onPressed: () {
                      controller.clear();
                    },
                  ),
                ),
              ),

```

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/75dea73657a740ceb29ac8b33b55654b~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.webp)

在右侧图标加了一个`IconButton`，因为带有点击事件，我们可以在点击的时候清除TextField中的内容。

以上就是图标的介绍，其实除了图标之外，对应的位置也可以显示文字或者自定义显示其他widget 比如出了`prefixIcon`之外还有其他3个属性，用法跟上面介绍到的自定义计数器是一样的。

```dart
    this.prefix,
    this.prefixText,
    this.prefixStyle,

```

#### 提示文字

提示文字有4种：

* 输入提示文字

```dart
              TextField(
                controller: controller,
                decoration: InputDecoration(
                  hintText: '请输入账号aaa',
                ),
              ),

```

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/e5c2e21438b84d92bc1107206c203da5~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.webp)

* 悬浮提示文字

```dart
              TextField(
                controller: controller,
                decoration: InputDecoration(
                  hintText: '请输入账号aaa',
                  labelText: '请输入账号',
                ),
              ),

```

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/51a4ebac05b8464c9a5a36a574b2c91a~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.webp)

可以看到，默认显示`labelText`，聚焦之后才显示`hintText`，所以labelText是可以取代hintText的。

* 帮助提示文字

```dart
              TextField(
                controller: controller,
                decoration: InputDecoration(
                  helperText: "帮助文字",
                  helperStyle: TextStyle(color: Colors.blue)
                ),
              ),

```

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/3cdca68a124440ed8a3aa4841783d310~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.webp)

一直显示在左下方

* 错误提示文字

```dart
              TextField(
                controller: controller,
                decoration: InputDecoration(
                  errorText: "你没有输入任何内容",
                ),
              ),

```

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/357c1f940aef46208b4933ab890c7b82~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.webp)

#### 去除下划线

```dart
              TextField(
                decoration: InputDecoration.collapsed(hintText: "无下划线的输入框"),
              ),

```

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/d2be0149698f4e4d8a54497b6a52093b~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.webp)

也可以`decoration: null`, 差别就是没有hintText了

#### 边框

```dart
              TextField(
                decoration: InputDecoration(
                  border: OutlineInputBorder(),
                ),
              ),

```

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/d58f57cec889492f8e66d7fa79fb2044~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.webp)

如果这个圆角不喜欢的话，也可以改一下的，比如：

```dart
              TextField(
                decoration: InputDecoration(
                  border: OutlineInputBorder(
                    borderRadius: BorderRadius.all(Radius.circular(30)),
                  ),
                ),
              ),

```

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/b42040c483564ca6a27ce501747facb0~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.webp)

### 获取输入内容

有两种方式：

* onChanged `onChanged`是输入内容改变时的回调，返回一个`String`类型的数值，可以用一个变量记一下

```dart
              TextField(
                onChanged: (text) {
                  print("输入改变时" + text);
                },
              ),

```

* controller 即控制器，初始化：

```dart
  var controller;

  @override
  void initState() {
    super.initState();
    controller = TextEditingController();
    controller.addListener(() {});
  }

```

配置给TextField

```dart
              TextField(
                controller: controller,
              ),

```

获取内容

```dart
controller.text

```

在事件中调用`controller.text`即返回输入内容。

### 关闭软键盘

往往我们在事件中提交的时候，是需要关闭软键盘的

这里我们就用到了`focusNode`

初始化：

```dart
FocusNode userFocusNode = FocusNode();

```

配置：

```dart
              TextField(
                focusNode: userFocusNode,
              ),

```

然后在需要的地方调用：

```dart
userFocusNode.unfocus();

```

### 校验

校验的话其实有个`inputFormatters`属性

```dart
  final List<TextInputFormatter> inputFormatters;

```

继续看TextInputFormatter源码，有3个子类：

* BlacklistingTextInputFormatter
* WhitelistingTextInputFormatter
* LengthLimitingTextInputFormatter

黑名单、白名单和长度限制，我们随便找一个看一下源码是怎么实现校验的：

往下看会看到这么一段代码：

```dart
  static final BlacklistingTextInputFormatter singleLineFormatter
      = BlacklistingTextInputFormatter(RegExp(r'\n'));

```

关键词在`RegExp`，其实就是我们一般用的正则表达式而已。

这样的话，我们也可以自定义校验规则了，比如校验手机号：

```dart
  String validateMobile(String value) {
    String patttern = r'(^[0-9]*$)';
    RegExp regExp = new RegExp(patttern);
    if (value.length == 0) {
      return "手机号为空";
    } else if (!regExp.hasMatch(value)) {
      return "手机号格式不正确";
    }
    return null;
  }

```

> 以上只是我们一般的校验，表单的话还是建议使用`From`包裹`TextFormField`

### 异常

* 软键盘弹出之后遮盖
* 软键盘弹出之后高度溢出

**解决办法**：用滑动组件包裹起来（ListView等），这样软键盘弹出的时候，输入框也会自动向上滑。
