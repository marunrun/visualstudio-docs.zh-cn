---
title: 重构代码以将 for 循环转换为 foreach 语句
ms.date: 05/10/2018
ms.topic: reference
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- CSharp
ms.workload:
- dotnet
ms.openlocfilehash: d61e79055b2158115b459e643a36170304b7f655
ms.sourcegitcommit: b468d71052a1b8a697f477ab23a3644de139f1e9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2019
ms.locfileid: "67261709"
---
# <a name="refactoring-to-convert-between-a-for-loop-and-a-foreach-statement"></a>重构，以便在 for 循环和 foreach 语句之间进行转换

本文介绍了在两个循环结构之间转换的快速操作重构。 它包含了一些你可能希望代码中的 [for](/dotnet/csharp/language-reference/keywords/for) 循环和 [foreach](/dotnet/csharp/language-reference/keywords/foreach-in) 语句之间转换的原因。

## <a name="convert-a-for-loop-to-a-foreach-statement"></a>将 for 循环转换为 foreach 语句

如果代码中有 [for](/dotnet/csharp/language-reference/keywords/for) 循环，可使用此重构将其转换为 [foreach](/dotnet/csharp/language-reference/keywords/foreach-in) 语句。

此重构适用于：

- C#

> [!NOTE]
> 转换为 foreach  快速操作重构仅适用于包含全部三部分的 [for](/dotnet/csharp/language-reference/keywords/for) 循环：初始化表达式、条件和迭代器。

### <a name="why-convert"></a>转换原因

需要将 [for](/dotnet/csharp/language-reference/keywords/for) 循环转换为 [foreach](/dotnet/csharp/language-reference/keywords/foreach-in) 语句的原因包括：

- 未在循环内使用本地循环变量（用作索引的情况除外）来访问项。

- 想要简化代码，并降低初始化表达式、条件以及迭代器部分中出现逻辑错误的可能性。

### <a name="how-to-use-it"></a>使用方法

1. 将插入点置于 `for` 关键字中。

1. 按“Ctrl”  + **。** 或单击代码文件边距中的螺丝刀![螺丝刀图标](../media/screwdriver-icon.png)图标。

   ![转换为 foreach 菜单](media/convert-to-foreach.png)

1. 选择“转换为‘foreach’”  。 或者，选择“预览更改”  以打开[“预览更改”](../../ide/preview-changes.md)对话框，然后选择“应用”  。

## <a name="convert-a-foreach-statement-to-a-for-loop"></a>将 foreach 语句转换为 for 循环

如果代码中有 [foreach (C#)](/dotnet/csharp/language-reference/keywords/foreach-in) 或 [For Each...Next (Visual Basic)](/dotnet/visual-basic/language-reference/statements/for-each-next-statement) 语句，则可使用此重构将其转换为 [for](/dotnet/csharp/language-reference/keywords/for) 循环。

此重构适用于：

- C#

- Visual Basic

### <a name="why-convert"></a>转换原因

需要将 [foreach](/dotnet/csharp/language-reference/keywords/foreach-in) 语句转换为 [for](/dotnet/csharp/language-reference/keywords/for) 循环的原因包括：

- 想在循环中使用本地循环变量，且不止用于访问项，还用于更多操作。

- 要[循环访问多维数组](/dotnet/csharp/programming-guide/arrays/using-foreach-with-arrays)，且希望实现对数组元素更多的控制。

### <a name="how-to-use-it"></a>使用方法

1. 将插入点置于 `foreach` 或 `For Each` 关键字中。

1. 按“Ctrl”  + **。** 或单击代码文件边距中的螺丝刀![螺丝刀图标](../media/screwdriver-icon.png)图标。

   ![转换为 for 菜单](media/convert-to-for.png)

1. 选择“转换为‘for’”  。 或者，选择“预览更改”  以打开[“预览更改”](../../ide/preview-changes.md)对话框，然后选择“应用”  。

1. 因为重构会引入一个新迭代计数变量，因此，“重命名”  框将出现在编辑器的右上角。 如果想要为变量选择不同名称，键入该名称，然后按“Enter”  或选择“重命名”  框中的“应用”  。 如果不想选择新名称，按“Esc”  或选择“应用”  以关闭“重命名”  框。

> [!NOTE]
> 对于 C#，由这些重构生成的代码对集合中的项目类型使用显式类型或 [var](/dotnet/csharp/language-reference/keywords/var)。 生成代码中的类型（显式或隐式）取决于范围内的代码样式设置。 这些特定的代码样式设置在“工具”   > “选项”   > “文本编辑器”   > “C#”   > “代码样式”   > “常规”   > “var 首选项”\'  下以计算机级别进行配置，或在 [EditorConfig](../../ide/editorconfig-language-conventions.md#implicit-and-explicit-types) 文件下以解决方案级别进行配置。 如果在“选项”  中更改了代码样式设置，请重新打开代码文件以使更改生效。

## <a name="see-also"></a>请参阅

- [重构](../refactoring-in-visual-studio.md)
- [预览更改](../../ide/preview-changes.md)