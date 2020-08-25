---
title: “选项”>“文本编辑器”>“基本(VB)”>“高级”
ms.date: 08/12/2020
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.Visual_Basic.Editor
- VS.ToolsOptionsPages.Text_Editor.Basic.Editor
- VS.ToolsOptionsPages.Visual_Basic_Editor.Editor
- VS.ToolsOptionsPages.Text_Editor.Basic.SimplifiedEditorPage
- VS.ToolsOptionsPages.Text_Editor.Basic
- VS.ToolsOptionsPages.Text_Editor.Basic.Advanced
- VS.ToolsOptionsPages.Text_Editor.Basic.VB_Specific
helpviewer_keywords:
- Basic Text Editor Options dialog box
ms.assetid: 5a8cafca-f7b4-4a2d-92ce-6894a7673d00
author: akhera99
ms.author: midumont
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 778cd1f9c126b176cafad8b33a147d284bea1b67
ms.sourcegitcommit: 2946d802aec1418e87bfa779d81834eeb7be5c9d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/14/2020
ms.locfileid: "88214643"
---
# <a name="options-text-editor-basic-visual-basic-advanced"></a>“选项”>“文本编辑器”>“基本(Visual Basic)”>“高级”
在“选项”  （“工具”  菜单）对话框中“文本编辑器”  文件夹的“基本”  文件夹内，“VB 专用”  属性页包含以下属性：

## <a name="analysis"></a>分析

- 实时代码分析或背景分析范围

   配置托管代码的背景分析范围。 有关详细信息，请参阅[如何：配置托管代码的实时代码分析范围](../../code-quality/configure-live-code-analysis-scope-managed-code.md)。

## <a name="using-directives"></a>Using 指令

- 对 using 排序时将“System”指令排在第一位

   当你选择右键单击菜单中的“删除和排序 Using”命令后，它会对 `using` 指令进行排序，并将“System”命名空间置于列表顶部  。

- 单独的 using 指令组

   当你选择右键单击菜单中的“删除和排序 Using”  命令后，它会在具有相同根命名空间的指令组之间插入空行，以将 `using` 指令分隔开来。

- 建议对引用程序集中的类型使用 using
- 建议对 NuGet 包中的类型使用 using

   选择这些选项时，[快速操作](../quick-actions.md)可用于安装 NuGet 包，并为未引用的类型添加 `using` 指令。

   ![用于在 Visual Studio 中安装 NuGet 包的快速操作](media/nuget-lightbulb.png)

## <a name="highlighting"></a>Highlighting

 **启用突出显示引用和关键字**

文本编辑器可以突出显示所有符号实例或子句中的所有关键字，如 `If..Then`、`While...End While` 或 `Try...Catch...Finally`。 可以在突出显示的引用或关键字之间进行导航，具体方法为按 Ctrl   + Shift   + 向下箭头  ，或按 Ctrl   + Shift   + 向上箭头  。

## <a name="outlining"></a>大纲显示

**启用大纲显示模式**

在代码编辑器中打开文件时，可在大纲显示模式下查看该文档。 有关详细信息，请参阅[大纲显示](../../ide/outlining.md)。 选定此选项后，打开文件即会激活大纲显示功能。

**显示过程行分隔符**

文本编辑器指示过程的可视范围。 在项目的 .vb  源文件中，在下表列出的位置处绘制行：

|.vb 源文件中的位置|行位置示例|
|---------------------------------|------------------------------|
|在块声明构造结束之后|-   在类、结构、模块、接口或枚举的末尾<br />-   在属性、函数或子类之后<br />-   不在属性中的 get 和 set 子句之间|
|在一组单行构造之后|-   在类文件中的导入语句之后，在类型定义之前<br />-   在类中声明的变量之后，在所有过程之前|
|在单行声明（非块级声明）之后|-   在导入语句、继承语句、变量声明、事件声明、委托声明和 DLL 声明语句之后|

## <a name="block-structure-guides"></a>块结构指南

如果你选中此选项，与结构化代码块对齐的竖线就会在编辑器中显示，这样你就能轻松识别各个代码块了。 例如，在 `Sub` 语句中的 `Sub` 和 `EndSub` 之间会出现一条线。

## <a name="editor-help"></a>编辑器帮助

::: moniker range=">=vs-2019"
**内联参数名称提示**    
如果选择此选项，则会在函数调用中的每个参数之前插入文本、强制转换文本和对象实例化的参数名称提示。  

![Visual Basic 的内联参数名称提示](media/inline-parameter-name-hints-visualbasic.png)
::: moniker-end

**整齐排列代码（重新设置格式）** 文本编辑器会适当地重新设置代码格式。 选定此选项后，代码编辑器会：

- 将代码与正确的制表符位置对齐

- 重新确定关键字、变量和对象的大小写，以符合正确的形式

- 向 `If...Then` 语句添加缺少的 `Then`

- 在函数调用中添加括号

- 在字符串中添加缺少的结束引号

- 重新设置指数表示法格式

- 重新设置日期格式

**自动插入最终构造**

例如，如果你键入过程声明的第一行 `Sub Main` 并按 Enter，文本编辑器就会添加匹配的 `End Sub` 行。 同样，如果添加一个 [For](/dotnet/visual-basic/language-reference/statements/for-next-statement) 循环，文本编辑器会添加一个匹配的 `Next` 语句。 选定此选项后，代码编辑器会自动添加最终构造。

**自动插入 Interface 和 MustOverride 成员**

为类提交 `Implements` 语句或 `Inherits` 语句时，文本编辑器分别为必须实现或必须替代的成员插入原型。

**启用错误纠正建议**

文本编辑器可以建议常见错误的解决方案，并且允许选择适当的更正，然后将该更正应用于代码。

## <a name="see-also"></a>请参阅

- [“选项”对话框 ->“环境”->“常规”](../../ide/reference/general-environment-options-dialog-box.md)
- [“选项”->“文本编辑器”->“所有语言”->“选项卡”](../../ide/reference/options-text-editor-all-languages-tabs.md)
