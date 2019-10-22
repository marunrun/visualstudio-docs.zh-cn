---
title: 代码片段 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
f1_keywords:
- vs.ExpansionManagerImport
- vs.codesnippetmanager
helpviewer_keywords:
- code snippets, replacement parameters
- code snippets, surround with
- replacement parameters
- code snippets, expansion
- surround with
- code snippets
ms.assetid: 85976ad9-4c9a-4e7b-896e-66ec6f955199
caps.latest.revision: 17
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 5b41b6e4d4a7635b32edb5697c89ecb1249fb9da
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72619729"
---
# <a name="code-snippets"></a>代码段
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

代码片段是小块可重用的代码，可使用上下文菜单命令或热键组合将其插入代码文件中。 代码片段通常包含常用的代码块（如 try-finally 或 if-else 块），可用于插入整个类或方法。

## <a name="expansion-snippets-and-surround-with-snippets"></a>扩展代码片段和外侧代码片段
 Visual Studio 中有两种类型的代码片段：扩展代码片段和外侧代码片段，前者在指定的插入点添加，并且可以替换代码片段快捷方式，后者仅限 C# 和 C++，在所选代码块的周围添加。

 插入代码片段的示例：在 C# 中，使用快捷方式 tryf 来插入 try-finally 块：

```
try
{

}
finally
{

}

```

 可通过两种方式插入此代码片段：在代码窗口上下文菜单中依次单击“插入代码片段”和“Visual C#”，然后键入 `tryf`，并按 Tab，或者键入 `tryf` 并按 Tab + Tab。

 外侧代码片段的示例：在 C++ 快捷方式中，`if` 可用作插入代码片段，或者可用作外侧代码片段。 如果选择某一个代码行（例如 `return FALSE;`），然后依次单击“外侧代码”和“if”，则代码片段将围绕此行展开：

```
if (true)
{
    return FALSE;
}

```

## <a name="snippet-replacement-parameters"></a>代码片段替换参数
 代码片段可以包含替换参数，这些替换参数是占位符，必须对其进行替换以适应你编写的精确代码。 上例中的 `true` 是替换参数，你可以将其替换为适当的条件。 进行的替换将针对代码片段中同一个替换参数的每个实例重复。

 例如，Visual Basic 中有一个用于插入属性的代码片段。 单击代码窗口上下文菜单中的“插入代码片段”，再依次单击“代码模式”和“属性、过程和事件”，然后定义属性。 插入以下代码：

```
Private newPropertyValue As String
Public Property NewProperty() As String
    Get
        Return newPropertyValue
    End Get
    Set(ByVal value As String)
        newPropertyValue = value
    End Set
End Property

```

 如果将 `newPropertyValue` 更改为 `m_property`，则 `newPropertyValue` 的每个实例都会更改。 如果在属性声明中将 `String` 更改为 `Int`，则 Set 方法中的值也会更改为 `Int`。

## <a name="code-snippet-manager"></a>代码片段管理器
 通过单击“工具/代码片段管理器”可查看当前安装的所有代码片段及其在磁盘中的位置。 代码片段按语言显示。

 可使用“代码片段管理器”对话框中的“添加”和“删除”按钮来添加和删除代码片段指令。 要添加单个代码片段，请使用“导入”按钮。

## <a name="see-also"></a>请参阅
 [演练：创建代码片段](../ide/walkthrough-creating-a-code-snippet.md)[如何：分发代码片段](../ide/how-to-distribute-code-snippets.md)[使用代码片段的最佳做法](../ide/best-practices-for-using-code-snippets.md)[故障排除](../ide/troubleshooting-snippets.md)代码片段[视觉C#对象代码](../ide/visual-csharp-code-snippets.md) [ C++段](../ide/visual-cpp-code-snippets.md)[代码段架构参考](../ide/code-snippets-schema-reference.md)
