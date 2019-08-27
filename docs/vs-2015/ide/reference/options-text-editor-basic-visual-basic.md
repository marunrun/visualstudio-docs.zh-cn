---
title: “选项”->“文本编辑器”->“Basic”(Visual Basic) | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.Visual_Basic.Editor
- VS.ToolsOptionsPages.Text_Editor.Basic.Editor
- VS.ToolsOptionsPages.Visual_Basic_Editor.Editor
- VS.ToolsOptionsPages.Text_Editor.Basic.SimplifiedEditorPage
- VS.ToolsOptionsPages.Text_Editor.Basic
- VS.ToolsOptionsPages.Text_Editor.Basic.VB_Specific
helpviewer_keywords:
- Basic Text Editor Options dialog box
ms.assetid: 5a8cafca-f7b4-4a2d-92ce-6894a7673d00
caps.latest.revision: 20
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 461af4c3c8e811c989bc296b6f8f55f398bc5bd5
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65674514"
---
# <a name="options-text-editor-basic-visual-basic"></a>选项，文本编辑器，基本 (Visual Basic)
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

在“选项”（“工具”菜单）对话框的“文本编辑器”文件夹下的“Basic”文件夹中，“VB 专用”属性页包含以下属性：  
  
 **自动插入最终构造**  
 键入一个过程声明的第一行（如 `Sub Main—`）并按 Enter 时，文本编辑器会添加一个匹配的 `End Sub` 行。 同样，如果添加一个 [For](https://msdn.microsoft.com/library/f5fc0d51-67ce-4c36-9f09-31c9a91c94e9) 循环，文本编辑器会添加一个匹配的 `Next` 语句。 选定此选项后，代码编辑器会自动添加最终构造。  
  
 **整齐排列代码（重新设置格式）**  
 文本编辑器会适当地重新设置代码格式。 选定此选项后，代码编辑器会：  
  
- 将代码与正确的制表符位置对齐  
  
- 重新确定关键字、变量和对象的大小写，以符合正确的形式  
  
- 向 `If...Then` 语句添加缺少的 `Then`  
  
- 在函数调用中添加括号  
  
- 在字符串中添加缺少的结束引号  
  
- 重新设置指数表示法格式  
  
- 重新设置日期格式  
  
  **启用大纲显示模式**  
  在代码编辑器中打开文件时，可在大纲显示模式下查看该文档。 有关详细信息，请参阅[大纲显示](../../ide/outlining.md)。 选定此选项后，打开文件即会激活大纲显示功能。  
  
  **自动插入 Interface 和 MustOverride 成员**  
  为类提交 `Implements` 语句或 `Inherits` 语句时，文本编辑器分别为必须实现或必须替代的成员插入原型。  
  
  **显示过程行分隔符**  
  文本编辑器指示过程的可视范围。 在项目的 .vb 源文件中，在下表列出的位置绘制行：  
  
|.vb 源文件中的位置|行位置示例|  
|---------------------------------|------------------------------|  
|在块声明构造结束之后|-   在类、结构、模块、接口或枚举的末尾<br />-   在属性、函数或子类之后<br />-   不在属性中的 get 和 set 子句之间|  
|在一组单行构造之后|-   在类文件中的导入语句之后，在类型定义之前<br />-   在类中声明的变量之后，在所有过程之前|  
|在单行声明（非块级声明）之后|-   在导入语句、继承语句、变量声明、事件声明、委托声明和 DLL 声明语句之后|  
  
 **启用错误纠正建议**  
 文本编辑器可以建议常见错误的解决方案，并且允许选择适当的更正，然后将该更正应用于代码。  
  
 **启用突出显示引用和关键字**  
 文本编辑器可突出显示符号的所有实例或子句中的所有关键字，例如 `If..Then`、`While...End While` 或 `Try...Catch...Finally`。 可通过按下 Ctrl+Shift+向下键或 Ctrl+Shift+向上键在突出显示的引用或关键字之间浏览。  
  
## <a name="see-also"></a>请参阅  
 [“选项”对话框 ->“环境”->“常规”](../../ide/reference/general-environment-options-dialog-box.md)   
 [“选项”->“文本编辑器”->“所有语言”->“选项卡”](../../ide/reference/options-text-editor-all-languages-tabs.md)
