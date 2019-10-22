---
title: “选项”->“文本编辑器”->“C#”->“高级”| Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.Text_Editor.CSharp.Outlining
- VS.ToolsOptionsPages.Text_Editor.Visual_JSharp.Advanced
- VS.ToolsOptionsPages.Text_Editor.Visual_JSharp.Outlining
- VS.ToolsOptionsPages.Text_Editor.CSharp.Advanced
helpviewer_keywords:
- XML comments
- XML documentation, generating
- outlining options [C#]
- outlining options [J#]
- XML documentation, creating
ms.assetid: 947f9d9a-b0f3-408d-9866-d82895bcee31
caps.latest.revision: 26
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 4f2d11e78c2402a6541bc87748ed6ba348ba80fc
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72662324"
---
# <a name="options-text-editor-c-advanced"></a>选项，文本编辑器，C#，高级
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

使用此对话框可修改 Visual C# 的编辑器格式设置、代码重构设置和 XML 文档注释设置。 若要访问此对话框，请在“工具菜单”  上单击“选项”  ，展开“文本编辑器”  文件夹，再展开“C#”  ，然后单击“高级”  。

> [!NOTE]
> 显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于你现用的设置或版本。 若要更改设置，请在 **“工具”** 菜单上选择 **“导入和导出设置”** 。 有关详细信息，请参阅[在 Visual Studio 中自定义开发设置](https://msdn.microsoft.com/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。

## <a name="outlining"></a>大纲显示
 进入大纲模式选中此选项后打开文件时，会自动概述代码文件，该文件创建可折叠的代码块。 首次打开文件时，#region 块和非活动代码块处于折叠状态。

## <a name="editor-help"></a>编辑器帮助
 编辑器中的下划线错误标识代码中的生成错误。 选中此选项后，不同颜色的波浪下划线具有不同的特定含义：

- 分析错误为红色。

- 生成错误为蓝色。

- 生成警告为绿色。

- 无效的[编辑并继续](../../debugger/edit-and-continue.md)编辑为紫色。

  将指针移到用下划线标出的代码段，可查看包含错误相关信息的工具提示。

  显示实时语义错误标识某些编译错误，无需显式编译，例如声明和使用未知类型或引用未知属性。

  当光标位于符号内时，突出显示对光标下的符号的引用，或者单击某个符号时，将突出显示代码文件中该符号的所有实例。

## <a name="refactoring"></a>重构
 验证重构结果在您尝试重构包含生成错误的代码时显示 "验证结果" 对话框，或者当重构将导致代码引用绑定到与其原始绑定不同的内容时显示 "**验证结果**" 对话框。

 如果在具有编译器生成的引用的成员上发出警告，则在尝试重构与编译器生成的引用同名的成员时，将显示警告对话框。

## <a name="xml-documentation-comments"></a>XML 文档注释
 如果选择了 "生成 XML 文档注释"，则在键入///注释简介后，会自动为 XML 文档注释插入 \<summary > 开始标记和结束标记。 有关 XML 文档注释的详细信息，请参阅 [XML 文档注释](https://msdn.microsoft.com/library/803b7f7b-7428-4725-b5db-9a6cff273199)。

## <a name="implement-interface"></a>实现接口
 使用 #region 将生成的代码括起来，在使用 "实现接口" 或 "实现接口" 时，将 #region \<*接口名称*> 成员插入成员。

## <a name="organize-usings"></a>组织用法
 将 "System" 指令排入第一次在选定时进行排序时，`System` using 指令显示在其他 using 指令之前。 有关详细信息，请参阅 [对 Using 排序](../../misc/sort-usings.md)。

## <a name="see-also"></a>另请参阅
 [XML 文档注释](https://msdn.microsoft.com/library/803b7f7b-7428-4725-b5db-9a6cff273199)[设置特定于语言的编辑器选项](../../ide/reference/setting-language-specific-editor-options.md) [Visual C# IntelliSense](../../ide/visual-csharp-intellisense.md)
