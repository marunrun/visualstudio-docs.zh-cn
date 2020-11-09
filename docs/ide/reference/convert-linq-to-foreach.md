---
title: 将 LINQ 查询转换为 foreach 语句
ms.custom: SEO-VS-2020
description: 重构代码，以将任何用查询语法编写的 LINQ 查询转换为 foreach 语句。
ms.date: 03/10/2020
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- dotnet
ms.openlocfilehash: 832c4160d743ca35dbe41eb0f0cbafd81d60dd26
ms.sourcegitcommit: f1bb1b66ed141837e992b3352ce68ff24c11f53e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/30/2020
ms.locfileid: "93102540"
---
# <a name="refactoring-to-convert-linq-to-a-foreach-statement"></a>重构以将 LINQ 转换为 foreach 语句

使用此重构将 [LINQ 查询语法](/dotnet/csharp/programming-guide/concepts/linq/query-syntax-and-method-syntax-in-linq)转换为 [foreach](/dotnet/csharp/language-reference/keywords/foreach-in) 语句。

此重构适用于：

- C#

- Visual Basic

## <a name="how-to-use-it"></a>使用方法

1. 选择以 `from` 开头的整个 LINQ 查询。

   > [!NOTE]
   > 此重构只能用于转换用查询语法而不是方法语法表达的 LINQ 查询。

1. 按“Ctrl”  + **。** 或单击代码文件边距中的螺丝刀![螺丝刀图标](../media/screwdriver-icon.png)图标。

   ![将 LINQ 转换为 foreach 快速操作菜单](media/convert-linq-to-foreach.png)

1. 选择“转换为‘foreach’”  。 或者，选择“预览更改”  以打开[“预览更改”](../../ide/preview-changes.md)对话框，然后选择“应用”  。

> [!NOTE]
> 对于 C#，由这些重构生成的代码对 `foreach` 循环的迭代变量使用显式类型或 [var](/dotnet/csharp/language-reference/keywords/var)。 生成代码中的类型（显式或隐式）取决于范围内的代码样式设置。 这些特定的代码样式设置在“工具” > “选项” > “文本编辑器” > “C#” > “代码样式” > “常规” > “var 首选项”\'下以计算机级别进行配置，或在 [EditorConfig](/dotnet/fundamentals/code-analysis/style-rules/language-rules#implicit-and-explicit-types) 文件下以解决方案级别进行配置。 如果在“选项”  中更改了代码样式设置，请重新打开代码文件以使更改生效。

## <a name="see-also"></a>另请参阅

- [LINQ](/dotnet/standard/using-linq)
- [重构](../refactoring-in-visual-studio.md)
- [预览更改](../../ide/preview-changes.md)
