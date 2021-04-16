<h1 style="text-align: center">VOCALOID™</h1>
<h1 style="text-align: center">Job Plugin API 参考手册</h1>
<div style="text-align: center;">Article ID: VJP-1.0.0.3 / API Version: 3.0.1.0</div>
<div style="text-align: center;">翻译 By <a href="https://space.bilibili.com/180668218">白糖の正义铃</a></div>

---

<!-- @import "[TOC]" {cmd="toc" depthFrom=1 depthTo=6 orderedList=false} -->

<!-- code_chunk_output -->

- [1 介绍](#1-介绍)
  - [1.1 关于任务插件](#11-关于任务插件)
  - [1.2 API版本](#12-api版本)
  - [1.3 Job Plugin API 之所及与不所及](#13-job-plugin-api-之所及与不所及)
    - [1.3.1 Job Plugin API 可以做的事](#131-job-plugin-api-可以做的事)
    - [1.3.2 Job Plugin API 做不到的事](#132-job-plugin-api-做不到的事)
- [2 任务插件的基本结构](#2-任务插件的基本结构)
  - [2.1 语法](#21-语法)
  - [2.2 入口函数(entry point function)](#22-入口函数entry-point-function)
    - [2.2.1 参数列表](#221-参数列表)
    - [2.2.2 返回值](#222-返回值)
    - [2.2.3 代码范例](#223-代码范例)
  - [2.3 任务插件清单信息函数(manifest function)](#23-任务插件清单信息函数manifest-function)
    - [2.3.1 向编辑器提供信息](#231-向编辑器提供信息)
    - [2.3.2 代码范例](#232-代码范例)
- [3 规定](#3-规定)
  - [3.1 命名约定](#31-命名约定)
  - [3.2 数据类型](#32-数据类型)
  - [3.3 定义Table类型变量](#33-定义table类型变量)
  - [3.4 Job Plugin API 原型定义](#34-job-plugin-api-原型定义)
  - [3.5 字符编码](#35-字符编码)
- [4 通过对话框传递参数](#4-通过对话框传递参数)
  - [4.1 动态生成参数输入对话框](#41-动态生成参数输入对话框)
  - [4.2 对话框字段定义](#42-对话框字段定义)
  - [4.3 添加对话框字段](#43-添加对话框字段)
  - [4.4 对话框显示](#44-对话框显示)
  - [4.5 获取输入的参数值](#45-获取输入的参数值)
  - [4.6 消息对话框](#46-消息对话框)
  - [4.7 程序范例](#47-程序范例)
- [5 获取与编辑音符信息](#5-获取与编辑音符信息)
  - [5.1 定义](#51-定义)
  - [5.2 通过游标顺序获取音符信息](#52-通过游标顺序获取音符信息)
  - [5.3 更新音符信息](#53-更新音符信息)
  - [5.4 插入音符](#54-插入音符)
  - [5.5 删除音符](#55-删除音符)
  - [5.6 适用于带表情控制参数的音符的API](#56-适用于带表情控制参数的音符的api)
  - [5.7 程序范例](#57-程序范例)
- [6 获取与编辑控制参数](#6-获取与编辑控制参数)
  - [6.1 定义](#61-定义)
  - [6.2 依据时间点随机操作控制参数](#62-依据时间点随机操作控制参数)
  - [6.3 通过游标顺序操作控制参数](#63-通过游标顺序操作控制参数)
  - [6.4 获取控制参数类型的默认值](#64-获取控制参数类型的默认值)
  - [6.5 程序范例](#65-程序范例)
- [7 获取音轨信息](#7-获取音轨信息)
  - [7.1 定义](#71-定义)
  - [7.2 通过游标顺序获取信息](#72-通过游标顺序获取信息)
  - [7.3 通过时间点随机获取信息](#73-通过时间点随机获取信息)
  - [7.4 获取整个序列的信息](#74-获取整个序列的信息)
  - [7.5 程序范例](#75-程序范例)
- [8 获取与编辑音乐序列信息](#8-获取与编辑音乐序列信息)
  - [8.1 定义](#81-定义)
  - [8.2音乐序列信息获取](#82音乐序列信息获取)
  - [8.3 编辑音乐序列信息](#83-编辑音乐序列信息)
  - [8.4 获取音乐序列虚拟歌手属性信息](#84-获取音乐序列虚拟歌手属性信息)
  - [8.5 程序范例](#85-程序范例)
- [9 获取WAV音频序列信息](#9-获取wav音频序列信息)
  - [9.1 定义](#91-定义)
  - [9.2 获取WAV音频序列信息](#92-获取wav音频序列信息)
  - [9.3 程序范例](#93-程序范例)
- [10 其他提示](#10-其他提示)
  - [10.1 使用文件输入输出标准库](#101-使用文件输入输出标准库)
    - [10.1.1 从对话框传递文件路径参数](#1011-从对话框传递文件路径参数)
    - [10.1.2 程序输出内容至外部文件](#1012-程序输出内容至外部文件)
  - [10.2 在插件中执行外部程序或命令](#102-在插件中执行外部程序或命令)
    - [10.2.1 处理运行外部程序的路径](#1021-处理运行外部程序的路径)
    - [10.2.2 运行DOS命令](#1022-运行dos命令)
  - [10.3 如何确定可用的 Job Plugin API](#103-如何确定可用的-job-plugin-api)
- [11 任务插件的添加与修改](#11-任务插件的添加与修改)
  - [11.1 任务插件的添加](#111-任务插件的添加)
  - [11.2 任务插件的修改](#112-任务插件的修改)
- [12 附录](#12-附录)
  - [12.1 Job Plugin API 列表清单](#121-job-plugin-api-列表清单)
  - [12.2 翻译者](#122-翻译者)

<!-- /code_chunk_output -->

---

# 1 介绍

## 1.1 关于任务插件

Job Plugin 任务插件提供了一种渠道，可以根据用户的需要，通过编写Lua语言脚本（版本5.1.4）扩展VOCALOID编辑器的功能。这个机制是由Job Plugin API提供的，它提供了获取音乐选区参数信息和更改参数的功能。

## 1.2 API版本

本文所描述的的 Job Plugin API 版本号为3.0.1.0

## 1.3 Job Plugin API 之所及与不所及

### 1.3.1 Job Plugin API 可以做的事

- 获取和编辑音乐序列中音符的基本属性
- 获取和编辑音乐序列中音符的控制参数
- 获取和编辑音乐序列中音符的颤音类型
- 获取和编辑音乐序列中音符的颤音长度
- 获取和编辑音乐序列的控制参数
- 获取和编辑音乐序列的基本属性
- 获取当前音轨的节拍信息
- 获取当前音轨的时间拍号信息
- 获取当前序列的属性
- 获取WAV音频序列的属性

### 1.3.2 Job Plugin API 做不到的事

目前，我们没有给 Job Plugin API 开放以下功能

- 获取和编辑序列中音符的颤音控制参数
- 更改当前音轨的节拍信息
- 更改当前音轨的时间拍号信息
- 更改当前序列的属性
- 更改WAV音频序列的属性
- 获取和编辑上面列出的信息以外的信息

> 提示1：音乐序列（Musical Part）和序列（Sequence）是不一样的概念，序列在这里指的是整个工程。音乐序列这个翻译是编辑器自带中文界面给出的，其将 WAV Part 直接翻译为WAV文件，我认为非常不可，于是想了想翻译为WAV音频序列。

> 提示2：在VOCALOID4编辑器主目录的JobPlugin目录下有一个VOCALOID_JobPlugin_SDK的文件夹，里面存放了参考手册原文全文以及范例代码。

# 2 任务插件的基本结构

## 2.1 语法

任务插件遵循了Lua的基本语法，并且可以使用Lua的所有语言特性。Lua的语法不在本文档的讨论范围之内，其内容请参照官方网站和参考手册。

## 2.2 入口函数(entry point function)

**任务插件必须始终包含一个函数名为main的主函数**，它将作为本插件的入口函数(entry point function)。此外，本函数的结尾也是整个插件运行的结尾。
 
### 2.2.1 参数列表

main主函数会被传入两个参数。这两个参数均为Lua的Table类型变量。

第一个参数包含了此时光标在当前音乐序列中的时间点，当前音乐序列选中部分的起始时间点和结束时间点，此参数由VOCALOID编辑器提供信息。时间点的单位为Tick，起始值为0。假如用户在音乐序列没有选中任何部分便运行插件，那么插件运行时，传入的起始时间点是0，结束时间点都会是整个音乐序列的结束时间点。

任务插件可以在音乐序列的整个时间范围内进行数据的检索与更新，另外，由于没有限制插件可更新数据的范围，你也可以在超出本音乐序列的时间范围外进行数据的更新。然而，这是需要尽量避免的，开发者应当在时间范围的边界处以某种机制进行处理，如渐入和渐出。另一方面，开发者也应当提供一些变量可以进行选择来让用户可以灵活地运行插件。


第二个参数则包含了插件运行环境的信息，包括以下信息。

- 放置插件源代码目录的路径：以“\”结尾的放置插件源文件目录的完整路径，另外这也是插件运行时的目录。
- 插件源文件的文件名：其只包含文件名不带路径。
- 插件可操作的临时目录：以“\”结尾的完整目录，插件可以在此目录下自由操作文件和文件夹。
- 插件所使用的 Job Plugin API 版本号：四位数，点号隔开。指定插件运行API的版本。

### 2.2.2 返回值

main主函数必须返回一个确切的数值。

- 返回 0 ：对音乐序列进行数据更新任务并正常结束运行。
- 返回非 0 值：假如你想对插件运行过程中的数据更新内容进行取消或者插件运行出错。关于非0值的取值没有相关规定。

### 2.2.3 代码范例

下面给出的是最简单的插件运行主函数，其没有执行任何操作。

```lua
function main(processParam, envParam)

    -- 获取插件运行的几个时间点信息
    beginPosTick = processParam.beginPosTick -- 选中部分起始时间点
    endPosTick = processParam.endPosTick -- 选中部分结束时间点
    songPosTick = processParam.songPosTick -- 光标当前所在时间点


    -- 获取插件运行环境信息的参数
    scriptDir = envParam.scriptDir -- 插件所在文件夹
    scriptName = envParam.scriptName -- 插件文件名
    tempDir = envParam.tempDir -- 插件运行时可操作的临时文件夹
    apiVersion = envParam.apiVersion -- API版本
    
    -- 插件运行没有执行任何操作
    -- 运行成功，末尾返回0值
    return 0
end
```

## 2.3 任务插件清单信息函数(manifest function)

### 2.3.1 向编辑器提供信息

任务插件的清单信息函数将插件的一些基本信息和开发者信息提供给编辑器。和main主函数一样都是任务插件必须具备的函数，缺一不可。以下为清单信息函数需要提供的信息。

1. 插件名称
2. 插件简介
3. 开发者名称
4. 识别插件唯一性的GUID
5. 本插件的版本号(四位数点号隔开)
6. 插件使用的API版本（目前为3.0.1.0）

需要提醒一下，编辑器通过GUID识别插件，假如俩插件的GUID相同，则编辑器会认为这两个插件是相同的，添加时，会覆盖相同GUID的前一个插件。

### 2.3.2 代码范例

```lua
function manifest()
    myManifest = {
        name = "神调教插件", -- 插件名称
        comment = "一键神调教，人人都想用", -- 插件简介
        author = "V A N", -- 开发者名称
        pluginID = "{AE31E35D-2FD4-4608-8D67-C2B45353192A}", -- 插件GUID（网上找一下GUID生成器）
        pluginVersion = "1.0.0.1", -- 插件版本号
        apiVersion = "3.0.1.0" -- API版本号
    }
    return myManifest
end
```

# 3 规定

## 3.1 命名约定

任务插件可以使用Lua语言所提供的所有语言特性，因此为了避免明显的命名冲突并指明其为 Job Plugin API，有了以下命名约定。

- API函数名称的前缀：Job Plugin API 函数名称前缀为“VS”。
- API的Table类型变量名前缀：Job Plugin API Table类型变量前缀为“VS”。
- 变量名：API的Table类型变量的field命名以小写字母开头。

## 3.2 数据类型

方便起见，Job Plugin API 定义了以下基本数据类型。

- `VSInt32`：32位带符号整型(signed integer)
- `VSFloat`：单精度浮点数
- `VSBool`：布尔值，1为true，0为false
- `VSCString`：字符串常量。编码只能是UTF-8。

> 译者注：这里只需简单了解，不去了解底层原理的话不用深究。

## 3.3 定义Table类型变量

Job Plugin API 使用了Lua的Table类型变量来处理音乐序列数据或者音符数据。为方便起见，我们将先采用类似C++的伪代码来描述定义，然后介绍如何使用Lua的Table类型定义以上的描述。

下面是伪代码描述音符的定义：

```cpp
// 音符类型定义
struct VSLuaNote {
    VSInt32 posTick; -- 音符起始时间点
    VSInt32 durTick; -- 音符时间长度
    VSInt32 noteNum; -- 音高
    VSInt32 velocity; -- 速度
    VSCString lyric; -- 歌词
    VSCString phonemes; -- 音标（空格隔开）
};
```

在任务插件中我们使用Lua来这样定义音符

```lua
-- Lua中的音符定义
note = {} -- 定义Table变量
note.posTick = 1920 -- 定义音符起始时间点
note.durTick = 480 -- 定义音符时间长度
note.noteNum = 69 -- 定义音高
note.velocity = 64 -- 定义速度
note.lyric = "spring" -- 定义歌词
note.phonemes = "s p r I N" -- 定义音标
```

## 3.4 Job Plugin API 原型定义

本文依旧采用类似C++的伪代码来定义 Job Plugin API 的原型。例如下文对对话框获取返回值API的定义：

```cpp
// 从对话框获取整型数据
// 参数:
// fieldName: 此对话框定义的字段名
// 返回:
// result: 成功获取数值，返回VS_TRUE（即1），失败时返回VS_FALSE（即0）
// value: 对话框获取到的返回值
VSBool result, VSInt32 value VSDlgGetIntValue(VSCString fieldname);
```

上面的API，表示了它需要传入一个字符串参数，然后API会返回一个布尔值和32位带符号整型值。下面则展示如何在插件中通过Lua使用这个API。

```lua
-- 从对话框中获取输入的音高值
result, noteNum = VSDlgGetIntValue("noteNum")
```

上文代码片段展示了如何从对话框中获取字段名位noteNum的32位带符号整型的用户输入数值。返回的布尔值表示了此获取动作的成功与否。

## 3.5 字符编码

**Job Plugin 任务插件的字符编码只能是UTF-8**

# 4 通过对话框传递参数

## 4.1 动态生成参数输入对话框

通过使用 Job Plugin API 的参数传递API，我们可以在VOCALOID编辑器中动态的生成可供参数输入的对话框。

## 4.2 对话框字段定义

以下是VOCALOID编辑器中参数传递API的字段的表类型定义：

```cpp
// 对话框中字段类型的定义
enum VSFlexDlgFieldType {
    FT_INTEGER = 0, // 整型数值 0
    FT_BOOL, // 布尔型数值 1
    FT_FLOAT, // 浮点数值 2
    FT_STRING, // 字符串 3
    FT_STRING_LIST // 字符串列表（下拉选择框） 4
};

// 参数对话框字段的定义
struct VSFlexDlgField {
    VSCString name; // 字段名
    VSCString caption; // 字段对话框的显示名称
    VSCString initialVal; // 字段初始值
    VSInt32 type; // 字段类型
};
```

## 4.3 添加对话框字段

> VSBool VSDlgAddField(VSFlexDlgField field)

将要显示的字段信息添加到参数对话框。除此之外，假如指定字段类型为"FT_STRING_LIST"（4），并且初始值为用逗号(",")隔开的字符串，那么该下拉选择框字段会被添加到对话框中，每一项为被逗号隔开的字符串内容。

```cpp
// 向对话框添加字段
// 参数: 参数输入对话框的字段定义
// 返回: 成功返回VS_TRUE（即1），失败返回VS_FALSE（即0）
VSBool VSDlgAddField (VSFlexDlgField field);
```

> void VSDlgSetDialogTitle (VSCString dlgTitle)


```cpp
// 设置对话框的窗口显示标题
// 参数: 对话框的窗口标题字符串
// 返回: None.
void VSDlgSetDialogTitle (VSCString dlgTitle);
```

## 4.4 对话框显示

> VSInt32 VSDlgDoModal()

显示参数输入对话框。在按下“确定”或“取消”按钮之前，控件不会返回值。

```cpp
// 显示对话框
// 参数: None
// 返回: 当确定键按下时返回1，当取消键按下时返回2
VSInt32 VSDlgDoModal();
```

## 4.5 获取输入的参数值

> VSBool result, VSInt32 value VSDlgGetIntValue( VSCString fieldName )

从参数输入对话框的字段中获取整型数值。

```cpp
// 从参数输入对话框的字段中获取整型数值。
// 参数:
// fieldName: 需要获取值的字段的字段名
// 返回:
// result: 获取成功返回VS_TRUE（即1），失败返回VS_FALSE（即0）
// value: 获得到的整型数值
VSBool result, VSInt32 value VSDlgGetIntValue ( VSCString fieldName );
```

> VSBool result, VSBool value VSDlgGetBoolValue( VSCString fieldName )

从参数输入对话框的字段中获取布尔值。

```cpp
// 从参数输入对话框的字段中获取布尔值
// 参数:
// fieldName: 需要获取值的字段的字段名
// 返回:
// result: 获取成功返回VS_TRUE（即1），失败返回VS_FALSE（即0）
// value: 获得到的布尔值
VSBool result, VSBool value VSDlgGetBoolValue ( VSCString fieldName );
```

> VSBool result, VSFloat value VSDlgGetFloatValue(VSCString fieldName)

从参数输入对话框的字段中获取浮点数值。

```cpp
// 从参数输入对话框的字段中获取浮点数值。
// 参数:
// fieldName: 需要获取值的字段的字段名
// 返回:
// result: 获取成功返回VS_TRUE（即1），失败返回VS_FALSE（即0）
// value: 获得到的浮点数值
VSBool result, VSFloat value VSDlgGetFloatValue ( VSCString fieldName );
```

> VSBool result, VSCString value VSDlgGetStringValue ( VSCString fieldName )

从参数输入对话框的字段中获取字符串内容。对于"FT_STRING_LIST"字段类型来说，获取到的值即为下拉选择框选择的那样一项内容。

```cpp
// 从参数输入对话框的字段中获取字符串内容。
// 参数:
// fieldName: 需要获取值的字段的字段名
// Returns:
// result: 获取成功返回VS_TRUE（即1），失败返回VS_FALSE（即0）
// value: 获得到的字符串内容
VSBool result, VSCString value VSDlgGetStringValue ( VSCString fieldName );
```

## 4.6 消息对话框

> VSInt32 VSMessageBox ( VSCString message, VSUint32 type )

在消息对话框中显示消息

```cpp
//     参数: 
//     message: 需要显示的文字信息
//     type: 消息框按钮样式类型，类型代码如下
//             MB_OK               = 0 
//             MB_OKCANCEL         = 1 
//             MB_ABORTRETRYIGNORE = 2 
//             MB_YESNOCANCEL      = 3 
//             MB_YESNO            = 4 
//             MB_RETRYCANCEL      = 5 

//     返回值: 用户点击按钮后的消息代码，各代码内容如下
//             IDOK     = 1 
//             IDCANCEL = 2 
//             IDABORT  = 3 
//             IDRETRY  = 4 
//             IDIGNORE = 5 
//             IDYES    = 6 
//             IDNO     = 7 
VSInt32 VSMessageBox( VSCString message, VSUint32 type );
```

## 4.7 程序范例

- DialogSample.lua

# 5 获取与编辑音符信息

## 5.1 定义

```cpp
// 音符
struct VSLuaNote {
    VSInt32 posTick; // 起始时间
    VSInt32 durTick; // 时间长度
    VSInt32 noteNum; // 音高
    VSInt32 velocity; // 速度
    VSCString lyric; // 歌词
    VSCString phonemes; // 音标（空格隔开）
    VSBool phLock; // 音标锁定标识（默认值: VS_FALSE(0)）
};
```

```cpp
// 音符, 包括表情控制参数(facial control parameters)。
struct VSLuaNoteEx {
	VSInt32 posTick;  // 起始时间
	VSInt32 durTick;  // 时间长度
	VSInt32 noteNum;  // 音高
	VSInt32 velocity;  // 速度
	VSCString lyric;  // 歌词
	VSCString phonemes;  // 音标（空格隔开）
	VSBool phLock;  // 音标锁定标识（默认值: VS_FALSE(0)）
	VSInt32 bendDepth;  // 弯曲深度 (0 - 100)
	VSInt32 bendLength;  // 弯曲长度 (0 - 100)
	VSBool risePort;  // Addition of portamento flag on line form
	VSBool fallPort;  // Portamento additional flag in the descending form
	VSInt32 decay;  // 衰变 (0 - 100)
	VSInt32 accent;  // 重音 (0 - 100)
	VSInt32 opening;  // 开口度 (0 - 127)

	// 颤音长度（舍入到整数值）
	VSInt32 vibratoLength;  
	
	// 颤音类型
	// 0: 无颤音
	// 1 - 4: Normal // 5 - 8: Extreme // 9 -12: Fast // 13 - 16: Slight
	VSInt32 vibratoType;
};
```

> 译者注：这个表情控制参数，说白了就是对音符信息进行拓展。基本版的音符信息定义已满足大部分的开发需求。

音标锁定标识是一个来防止编辑器的自动转换机制改变已经自定义的音标内容。当设置为VS_TRUE(1)时，歌词改变触发的VOCALOID编辑器自动歌词转音标机制不会改变当前音符的音标；当设置为VS_TRUE(0)，输入新歌词，那么你自定义的音标将会被自动转换的音标内容覆盖。

## 5.2 通过游标顺序获取音符信息

![](img/note.png)
<div style="text-align: center;">通过游标顺序获取音符信息</div>

可以通过游标，从音乐序列起始处顺序获取音符信息。首先，通过VSSeekToBeginNote()，将游标放置到音乐序列的第一个音符之前。接着，通过VSGetNextNote()，你就可以获取到音乐序列第一个音符，并从中获取到它的参数。之后，通过不断重复VSGetNextNote()，你可以接连获取到之后的音符信息。假如游标走到最后一个音符了，那么再次调用VSGetNextNote()时会返回VS_FALSE(0)。

> void VSSeekToBeginNote()

将游标放置到当前音乐序列第一个音符之前。

```cpp
// 将游标放置到第一个音符之前。
// 参数: None.
// 返回: None.
void VSSeekToBeginNote();
```

> VSBool result, VSLuaNote note VSGetNextNote()

将游标移至下一个音符，并获取音符信息

```cpp
// 将游标移至下一个音符，并获取音符信息
// 参数: None.
// 返回:
// result: 获取成功返回VS_TRUE（即1），失败返回VS_FALSE（即0）
// value: 获得到的音符信息
VSBool result, VSLuaNote note VSGetNextNote();
```


## 5.3 更新音符信息

> VSBool VSUpdateNote(VSLuaNote note)

更新音符中的数值信息

先通过VSGetNextNote()获取到音符信息，然后依据需求对其中的字段值进行更改，之后通过调用VSUpdateNote()更新改动的音符信息。

```cpp
// 更新音符中的数值信息
// 参数: 更新过数值信息的音符
// 结果: 更新成功返回VS_TRUE（即1），失败返回VS_FALSE（即0）
VSBool VSUpdateNote( VSLuaNote note );
```

## 5.4 插入音符

> VSBool VSInsertNote(VSLuaNote note)

你可以添加具备参数值的音符。被添加的音符必须每一项都正确的填写，然而，phLock这一项可以被省略，省略在添加时将会置为默认值VS_FALSE(0)。

```cpp
// 插入一个音符
// 参数: 需要被添加的音符
// 返回: 添加成功返回VS_TRUE（即1），失败返回VS_FALSE（即0）
VSBool VSInsertNote( VSLuaNote note );
```

## 5.5 删除音符

> VSBool VSRemoveNote(VSLuaNote note)

删除当前音乐序列中的音符。需要注意的是，删除的音符只能先通过调用VSGetNextNote()获取，然后作为参数传入VSRemoveNote()来进行删除。

```cpp
// 删除音符
// 参数: 需要被删除的音符
// 返回: 删除成功返回VS_TRUE（即1），失败返回VS_FALSE（即0）
VSBool VSRemoveNote(VSLuaNote note);
```

## 5.6 适用于带表情控制参数的音符的API

> VSBool result, VSLuaNoteEx noteEx VSGetNextNoteEx()

获取下一个带有表情控制参数的音符。

```cpp
// 获取下一个带有表情控制参数的音符
// 参数: None
// result: 获取成功返回VS_TRUE（即1），失败返回VS_FALSE（即0）
// noteEx: 带有表情控制参数的音符信息
VSBool result, VSLuaNoteEx noteEx VSGetNextNoteEx();
```

> VSBool VSUpdateNoteEx(VSLuaNoteEx noteEx)

本API可以更新带有表情控制参数的音符。先通过VSGetNextNoteEx()获取到音符信息，然后依据需求对其中的字段值进行更改，之后通过调用VSUpdateNoteEx()更新改动的音符信息。

```cpp
// 更新带有表情控制参数的音符信息
// 参数: noteEx, 带有表情控制参数的音符
// 返回值: 获取成功返回VS_TRUE（即1），失败返回VS_FALSE（即0）
VSBool VSUpdateNoteEx( VSLuaNoteEx noteEx );
```

> VSBool VSInsertNoteEx(VSLuaNoteEx noteEx)

你可以添加具备参数值的带有表情控制参数音符。被添加的音符必须每一项都正确的填写，然而，phLock这一项可以被省略，省略在添加时将会置为默认值VS_FALSE(0)。

```cpp
// 插入带有表情控制参数的音符
// 参数: noteEx，带有表情控制参数的音符
// 返回值: 插入成功返回VS_TRUE（即1），失败返回VS_FALSE（即0）
VSBool VSInsertNoteEx( VSLuaNoteEx noteEx );
```

## 5.7 程序范例

- NoteSample1.lua
- NoteSample2.lua

# 6 获取与编辑控制参数

## 6.1 定义

控制参数采用Table类型进行定义

```cpp

// 控制参数类型（字符串常量）
// "DYN": 动态
// "BRE": 呼吸度
// "BRI": 明亮度
// "CLE": 清晰度
// "GEN": 性别
// "PIT": 滑音
// "PBS": 滑音敏感度
// "POR": 滑音时间
// "XSY": 交叉演奏参数
// "GWL": 咆哮声

// 控制参数断点定义
struct VSLuaControl {
    VSInt32 posTick; // 控制参数断点所在的时间点
    VSInt32 value; // 控制参数断点的参数值
    VSCString type; // 控制参数断点的参数类型
};

```

## 6.2 依据时间点随机操作控制参数

控制参数在时间轴上以断点(break point)的形式离散排布着。相较于繁琐的通过游标获取信息的音符获取方式，控制参数断点则可以通过传入时间点来直接获取访问控制参数信息，简单明了。

通过下方的图片介绍一下通过时间点随机获取控制参数的方法。时间轴上分布着控制参数断点，两个断点之间通过直线进行插值。

- 假如指定的时间点在第一个控制参数断点之前，那么获取到的参数值是该控制参数类型的默认值
- 假如指定的时间点是某个控制参数断点所在的时间点，那么获取到的是那个控制参数断点的参数值
- 假如指定的时间点在最后一个控制参数断点之后，那么获取到的是最后一个控制参数断点的参数值

![](img/control.png)
<center>依据时间点随机获取控制参数</center>

> VSBool result, VSInt32 value VSGetControlAt(VSCString controlType, VSInt32 posTick)

通过音乐序列上的时间点随机获取控制参数

```cpp
// 获取控制参数
// 参数:
// controlType: 想要获取值的参数类型
// posTick: 控制参数所在时间点
// 返回值:
// result: 获取成功返回VS_TRUE（即1），失败返回VS_FALSE（即0）
// value: 获得到的控制参数数值
VSBool result, VSInt32 value VSGetControlAt(VSCString controlType, VSInt32 posTick);
```

> VSBool VSUpdateControlAt(VSCString controlType, VSInt32 posTick, VSInt32 value)

通过音乐序列上的时间点更新控制参数数值

```cpp
// 更新控制参数数值
// 参数:
// controlType: 控制参数类型
// posTick: 控制参数时间点
// value: 要更新的数值
// 返回值: 更新成功返回VS_TRUE（即1），失败返回VS_FALSE（即0）
VSBool VSUpdateControlAt( VSCString controlType, VSInt32 posTick, VSInt32 value );
```

## 6.3 通过游标顺序操作控制参数

当想要更改控制参数数值却不知道它的具体时间点时，你依旧可以像音符一样通过游标的形式顺序获取控制参数。

> VSBool VSSeekToBeginControl(VSCString controlType)

将游标放置在当前音乐序列第一个控制参数断点之前

```cpp
// 将游标放置在第一个控制参数断点之前
// 参数:
// controlType: 控制参数类型
// 返回值: 成功返回VS_TRUE（即1），失败返回VS_FALSE（即0）
VSBool VSSeekToBeginControl( VSCString controlType );
```

> VSBool result, VSLuaControl control VSGetNextControl(VSCString controlType)

获取音乐序列下当前游标位置的下一个控制参数断点

```cpp
// 参数:
// controlType: 控制参数类型
// 返回值:
// result: 获取成功返回VS_TRUE（即1），失败返回VS_FALSE（即0）
// control: 获取到的控制参数断点
VSBool result, VSLuaControl control VSGetNextControl(VSCString controlType);
```

> VSBool VSUpdateControl(VSLuaControl control)

传入控制参数断点并更新控制参数。你需要通过VSGetNextControl()获取控制参数断点，并对其中的属性值依据需求进行更改，之后传入VSUpdateControl()进行更新。

```cpp
// 更新控制参数断点
// 参数: 更新数值后的控制参数断点
// 返回值: 更新成功返回VS_TRUE（即1），失败返回VS_FALSE（即0）
VSBool VSUpdateControl( VSLuaControl control );
```

> VSBool VSInsertControl(VSLuaControl control)

插入控制参数断点。你需要定义一个控制参数断点并对其中的属性进行合理的赋值，之后调用VSInsertControl()便可以插入。

```cpp
// 插入控制参数断点
// 参数: 需要插入的控制参数断点
// 返回值: 插入成功返回VS_TRUE（即1），失败返回VS_FALSE（即0）
VSBool VSInsertControl( VSLuaControl control );
```

> VSBool VSRemoveControl(VSLuaControl control)

删除音乐序列上的控制参数断点。你需要通过VSGetNextControl()获取想要删除控制参数断点，之后传入VSRemoveControl()即可删除。

```cpp
// 删除控制参数断点
// 参数: 想要删除的控制参数断点
// 返回值: 删除成功返回VS_TRUE（即1），失败返回VS_FALSE（即0）
VSBool VSRemoveControl( VSLuaControl control );
```

## 6.4 获取控制参数类型的默认值

> VSBool result, VSInt32 value VSGetDefaultControlValue(VSCString controlType)

依据特定的的控制参数类型获取其默认值

```cpp
// 参数:
// controlType: 控制参数的类型
// 返回值:
// result: 获取成功返回VS_TRUE（即1），失败返回VS_FALSE（即0）
// value: 控制参数默认值
VSBool result, VSInt32 value VSGetDefaultControlValue( VSCString controlType );
```

## 6.5 程序范例

- ControlSample1.lua
- ControlSample2.lua
- ControlSample3.lua
- Delete Selection.lua

# 7 获取音轨信息

## 7.1 定义

下方是音轨信息的Table类型定义。要注意，下方两个定义里面的时间点(posTick)是全局的时间点（与音乐序列里面的不同时间点，每个音乐序列里面的时间点是相对与其各自内部的）


```cpp
// 节拍/速率 (Tempo)
struct VSLuaTempo {
    VSInt32 posTick; // 时间点 (全局时间点)
    VSFloat tempo; // BPM值
};
// 时间拍号 (Time signature)
struct VSLuaTimeSig {
    VSInt32 posTick; // Beat time (全局时间点)
    VSInt32 numerator; // 拍号分子
    VSInt32 denominator; // 拍号分母
};
```

## 7.2 通过游标顺序获取信息

和音符一样，我们可以通过游标来顺序获取节拍和时间拍号信息。先以获取节拍信息为例。首先通过VSSeekToBeginTempo()将游标置于第一个节拍之前，然后通过VSGetNextTempo()获取第一个节拍，之后通过重复调用VSGetNextTempo()顺序获取之后的节拍信息，当获取最后一个节拍信息后，再次调用VSGetNextTempo()则返回VS_FALSE(0)。对于时间拍好信息的获取过程和以上同理。

> void VSSeekToBeginTempo()

将游标置于第一个节拍之前

```cpp
// 参数: None.
// 返回: None.
void VSSeekToBeginTempo();
```

> void VSSeekToBeginTimeSig()

将游标置于第一个时间拍号之前

```cpp
// 参数: None.
// 返回: None.
void VSSeekToBeginTimeSig();
```

> VSBool result, VSLuaTempo tempo VSGetNextTempo()

将游标置于下一个节拍，并且获取其信息

```cpp
// 参数: None.
// 返回:
// result: 获取成功返回VS_TRUE（即1），失败返回VS_FALSE（即0）
// tempo: 获取到的节拍
VSBool result, VSLuaTempo tempo VSGetNextTempo();
```

> VSBool result, VSLuaTimeSig timeSig VSGetNextTimeSig()

将游标置于下一个时间拍号，并且获取其信息

```cpp
// 参数: None.
// 返回:
// result: 获取成功返回VS_TRUE（即1），失败返回VS_FALSE（即0）
// timeSig: 获取到的时间拍号
VSBool result, VSLuaTimeSig timeSig VSGetNextTimeSig();
```

## 7.3 通过时间点随机获取信息

和控制参数一样，你也可以依据某时间点来随机获取音轨的信息

> VSBool result, VSFloat tempo VSGetTempoAt(VSInt32 posTick)

通过特定时间点获取节拍信息

```cpp
// 参数:
// posTick: 获取的时间点
// 返回:
// result: 获取成功返回VS_TRUE（即1），失败返回VS_FALSE（即0）
// tempo: 单精度浮点数类型的BPM值
VSBool result, VSFloat tempo VSGetTempoAt( VSInt32 posTick );
```
> VSBool result, VSInt32 numerator, VSInt32 denominator VSGetTimeSigAt(VSInt32 posTick)

通过特定时间点获取时间拍号信息

```cpp
// 参数:
// posTick: 获取时间点
// 返回:
// result: 获取成功返回VS_TRUE（即1），失败返回VS_FALSE（即0）
// numerator: 时间拍号分子
// denominator: 时间拍号分母
VSBool result, VSInt32 numerator, VSInt32 denominator VSGetTimeSigAt( VSInt32 posTick );
```

## 7.4 获取整个序列的信息

> VSCString VSGetSequenceName()

获取当前打开序列的文件名

```cpp
// 参数: None.
// 返回值: 当前打开序列的文件名
VSCString VSGetSequenceName();
```

> VSCString VSGetSequencePath()

获取当前打开序列的文件位置

```cpp
// 参数: None.
// 返回: 序列的文件位置
VSCString VSGetSequencePath();
```

> VSInt32 VSGetResolution()

获取当前打开序列的时间分辨率

```cpp
// 参数: None.
// 返回: 当前打开序列的时间分辨率
VSInt32 VSGetResolution();
```

> VSInt32 VSGetPreMeasure()

获取当前打开序列的前置测度

```cpp
// 参数: None.
// 返回: Pre-measure. Units of the sequence currently open bar.
VSInt32 VSGetPreMeasure();
```

- VSInt32 VSGetPreMeasureInTick()

获取以Tick为单位的前置测度

```cpp
// 参数: None.
// 返回: Pre-measure. Units of the sequence currently open Tick.
VSInt32 VSGetPreMeasureInTick();
```

> 译者注：这里的序列约等于工程，前置测度是比较学术的测量值，我们不用理会。

## 7.5 程序范例

- MasterTrackSample.lua

# 8 获取与编辑音乐序列信息

## 8.1 定义

下面是音乐序列信息的Table类型定义

```cpp
// 音乐序列
struct VSLuaMusicalPart {
    VSInt32 posTick; // 音乐序列的起始时间点（全局时间点）
    VSInt32 playTime; // 音乐序列的播放时间（起始点到结束点）
    VSInt32 durTick; // 音乐序列的非空播放时间（即playTime去除在最后一个音符之后部分的时间）
    VSCString name; // 音乐序列的名称
    VSCString comment; // 音乐序列的注释
};

// 虚拟歌手属性
struct VSLuaMusicalSinger {

	// 声库属性
    VSInt32 vBS; // Virtual Bank Select
    VSInt32 vPC; // Virtual Program Change.
    VSCString compID; // Component ID.

    // 声音参数
    VSInt32 breathiness; // 呼吸度
    VSInt32 brightness; // 明亮度
    VSInt32 clearness; // 清晰度
    VSInt32 genderFactor; // 性别
    VSInt32 opening; // 开口度
```

## 8.2音乐序列信息获取

> VSBool result, VSLuaMusicalPart part VSGetMusicalPart()

获取当前音乐序列信息

```cpp
// 参数: None.
// 返回:
// result: 获取成功返回VS_TRUE（即1），失败返回VS_FALSE（即0）
// part: 获取到的音乐序列信息
VSBool result, VSLuaMusicalPart part VSGetMusicalPart();
```

## 8.3 编辑音乐序列信息

> VSBool VSUpdateMusicalPart(VSLuaMusicalPart part)

编辑当前音乐序列的信息。你需要先通过VSGetMusicalPart()获取到想要的音乐序列，然后对其中的属性进行更改，之后传入VSUpdateMusicalPart()中进行数据的更新。

```cpp
// 参数: 更新信息的音乐序列
// 返回: 更新成功返回VS_TRUE（即1），失败返回VS_FALSE（即0）
VSBool VSUpdateMusicalPart( VSLuaMusicalPart part );
```

## 8.4 获取音乐序列虚拟歌手属性信息

> VSBool result, VSLuaMusicalSinger singer VSGetMusicalPartSinger()

获取当前音乐序列的虚拟歌手属性信息

```cpp
// 参数: None.
// 返回:
// result: 获取成功返回VS_TRUE（即1），失败返回VS_FALSE（即0）
// singer: 获取到的虚拟歌手属性信息
VSBool result, VSLuaMusicalSinger singer VSGetMusicalPartSinger();
```

## 8.5 程序范例

- MusicalPartSample.lua

# 9 获取WAV音频序列信息

## 9.1 定义

```cpp
// WAV音频序列
struct VSLuaWAVPart {
    VSInt32 posTick; // WAV音频序列的起始时间点(全局时间点)
    VSInt32 playTime; // 播放时间
    VSInt32 sampleRate; // 音频采样率
    VSInt32 sampleReso; // 音频位深
    VSInt32 channels; // 音频声道数
    VSCString name; // 音频序列名
    VSCString comment; // 音频序列注释
    VSCString filePath; // WAV音频的绝对路径
};
```

## 9.2 获取WAV音频序列信息

> VSBool result, VSLuaWAVPart wavPart VSGetStereoWAVPart()

获取立体声WAV音频序列的信息。立体声音轨上只能有一个WAV音频序列。

```cpp
// 参数: None.
// 返回:
// result: 成功返回VS_TRUE（即1），失败返回VS_FALSE（即0）
// wavPart: 立体声WAV音频序列的信息
VSBool result, VSLuaWAVPart wavPart VSGetStereoWAVPart();
```

> void VSSeekToBeginMonoWAVPart()

将游标放置在第一个单声道WAV音频序列之前

```cpp
// 参数: None.
// 返回: None.
void VSSeekToBeginMonoWAVPart();
```

> VSBool result, VSLuaWAVPart wavPart VSGetNextMonoWAVPart()

将游标移至下一个单声道WAV音频序列，并获取其信息

```cpp
// 参数: None.
// 返回:
// result: 成功返回VS_TRUE（即1），失败返回VS_FALSE（即0）
// wavPart: 获取到的单声道WAV音频序列信息
VSBool result, VSLuaWAVPart wavPart = VSGetNextMonoWAVPart();
```

## 9.3 程序范例

- WAVPartSample.lua

# 10 其他提示

## 10.1 使用文件输入输出标准库

前面已经说明，任务插件只支持UTF-8编码，所以在使用Lua的文件IO标准库时，需要检查文件内容是否符合要求。以下是Lua的几个文件输入输出的方法。

1. io.open()
2. io.input()
3. io.output()


### 10.1.1 从对话框传递文件路径参数

通过VSDlgGetStringValue()获取到的对话框字符串会被编码为UTF-8，所以你可以正常地将该字符串用于文件的输入和输出操作。下面展示一个例子。

```lua
-- 新建一个要求用户提供输出文件位置的对话框
field = {}
field.name = "outFilePath"
field.caption = "Output file path"
field.initialVal = ""
field.type = 3

dlgStatus = VSDlgAddField(field)

-- 获取到该文件目录的字符串值
dlgStatus = VSDlgDoModal()
dlgStatus, outFilePath = VSDlgGetStringValue("outFilePath")

-- 文件输出
outFile, errMsg = io.open(outFilePath, "w")

if (outFile) then 
    outFile:write("Hello, World!!\n")
end
```


### 10.1.2 程序输出内容至外部文件

输出文件的编码格式也是UTF-8

```lua
function main(processParam, envParam)
    -- 直接指定输出文件位置
    io.output(envParam.tempDir .. "\\Hello.txt")

    -- 输出内容至外部文件
    io.write("Hello,World!!\n") 
    return 0
end
```


## 10.2 在插件中执行外部程序或命令

得益于Lua的OS标准库，你可以在任务插件中运行外部程序或者DOS命令

> os.execute()

### 10.2.1 处理运行外部程序的路径

外部程序的路径只能用UTF-8的编码

```lua
-- 运行笔记本应用
os.execute("notepad.exe")
```

### 10.2.2 运行DOS命令

你也可以通过Lua的os.execute()方法运行DOS命令

CMD /C "DOS Command"

```lua
-- 要创建的文件夹位置
newDir = "C:\\Temp\\myDir"

-- 通过DOS创建一个文件夹
-- CMD /C "MKDIR "C:\Temp\myDir""
os.execute("CMD /C \"MKDIR \"" .. newDir .. "\"\"")
```

> 译者注：以上总结——全部用UTF-8

## 10.3 如何确定可用的 Job Plugin API

可用的 Job Plugin API 列表均被记录在Lua的一个叫做"_G"的全局变量中，于是你可以通过以下的方法判断在当前环境下某API是否可用。

```lua
-- I examine Job plug-in API is whether available.
-- Argument apiName: Job plug-in API name to find out
-- Return value available: true Not available: false
function isAvailableAPI(apiName)
    local isAvailable = false
    local key, val
    for key, val in pairs(_G) do
        if ((key == apiName) and (type(val) == "function")) then
            -- apiName Functions that match in there (available).
            isAvailable = true
            break
        end
    end
    return isAvailable
end
```

# 11 任务插件的添加与修改

## 11.1 任务插件的添加

在VOCALOID编辑器中，通过选择菜单栏上的“任务”->“管理任务插件”，可以打开任务插件管理器。你可以通过添加按钮选中添加你想要的任务插件，也可以删除不想要的任务插件。

在选择任务插件的脚本文件并添加后，任务插件管理器会加载文件并读取脚本文件里面的清单信息函数所提供的插件信息，并验证任务插件的合法性。此时，管理器会计算插件脚本文件的SHA-1哈希值然后一并注册到管理器之中。

![任务插件管理器界面](img/register.jpg)
<center>任务插件管理器界面</center>

## 11.2 任务插件的修改

VOCALOID编辑器的内置数据库维护着已经添加的任务插件的信息。当你的脚本文件代码改动时，文件的SHA-1哈希值也会随着变动，内部数据库匹配不上，于是编辑器便会认为其非法，阻止任务插件运行，这样做主要是防止插件遭到恶意篡改，此时在任务插件管理器界面你会发现相应的插件备注那一栏出现了'N/A'的字样。假如你还想继续使用那个插件，只需将其从中删除然后重新添加即可。

# 12 附录

## 12.1 Job Plugin API 列表清单

| API Name                 | Support API version |
| ------------------------ | ------------------- |
| VSDlgSetDialogTitle      | 3.0.0.1 ~           |
| VSDlgAddField            | 3.0.0.1 ~           |
| VSDlgGetIntValue         | 3.0.0.1 ~           |
| VSDlgGetBoolValue        | 3.0.0.1 ~           |
| VSDlgGetFloatValue       | 3.0.0.1 ~           |
| VSDlgGetStringValue      | 3.0.0.1 ~           |
| VSDlgDoModal             | 3.0.0.1 ~           |
| VSMessageBox             | 3.0.0.1 ~           |
| VSGetSequenceName        | 3.0.0.1 ~           |
| VSGetSequencePath        | 3.0.0.1 ~           |
| VSGetResolution          | 3.0.0.1 ~           |
| VSGetPreMeasure          | 3.0.1.0 ~           |
| VSGetPreMeasureInTick    | 3.0.1.0 ~           |
| VSSeekToBeginTempo       | 3.0.0.1 ~           |
| VSGetNextTempo           | 3.0.0.1 ~           |
| VSSeekToBeginTimeSig     | 3.0.0.1 ~           |
| VSGetNextTimeSig         | 3.0.0.1 ~           |
| VSGetTempoAt             | 3.0.0.1 ~           |
| VSGetTimeSigAt           | 3.0.0.1 ~           |
| VSGetMusicalPart         | 3.0.0.1 ~           |
| VSUpdateMusicalPart      | 3.0.0.1 ~           |
| VSGetMusicalPartSinger   | 3.0.0.1 ~           |
| VSSeekToBeginNote        | 3.0.0.1 ~           |
| VSGetNextNote            | 3.0.0.1 ~           |
| VSGetNextNoteEx          | 3.0.0.1 ~           |
| VSUpdateNote             | 3.0.0.1 ~           |
| VSUpdateNoteEx           | 3.0.0.1 ~           |
| VSInsertNote             | 3.0.0.1 ~           |
| VSInsertNoteEx           | 3.0.0.1 ~           |
| VSRemoveNote             | 3.0.0.1 ~           |
| VSGetControlAt           | 3.0.0.1 ~           |
| VSUpdateControlAt        | 3.0.0.1 ~           |
| VSSeekToBeginControl     | 3.0.0.1 ~           |
| VSGetNextControl         | 3.0.0.1 ~           |
| VSUpdateControl          | 3.0.0.1 ~           |
| VSInsertControl          | 3.0.0.1 ~           |
| VSRemoveControl          | 3.0.0.1 ~           |
| VSGetDefaultControlValue | 3.0.0.1 ~           |
| VSSeekToBeginMonoWAVPart | 3.0.0.1 ~           |
| VSGetNextMonoWAVPart     | 3.0.0.1 ~           |
| VSGetStereoWAVPart       | 3.0.0.1 ~           |
| VSGetAudioDeviceName     | 3.0.1.0 ~           |

## 12.2 翻译者

- 白糖の正义铃：V/SV调校师、初级混音师、初级码农
- B站个人主页：https://space.bilibili.com/180668218