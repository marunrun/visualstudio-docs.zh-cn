---
title: 将 foreach 循环转换为 LINQ
descritpion: Convert any foreach loop that uses an IEnumerable to a LINQ query or a LINQ call form (also known as a LINQ method).
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
ms.openlocfilehash: 12c03830ccd37e0970e3c74bc78cdd9c8a8732b7
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "79094216"
---
# <a name="convert-a-foreach-loop-to-linq"></a>将 foreach 循环转换为 LINQ

此重构适用于：

- C#

- Visual Basic

**功能：** 可以将使用 IEnumerables 的 foreach  循环轻松转换为 LINQ 查询或 LINQ 调用窗体（也称为 LINQ 方法）。

**使用时机：** 有一个使用 IEnumerable 的 foreach 循环，并且需要将该循环作为 LINQ 查询读取。

操作原因：  更倾向于使用 LINQ 语法而不是 foreach 循环。 [LINQ](/dotnet/csharp/programming-guide/concepts/linq/introduction-to-linq) 使查询成为 C# 一流语言构造。 LINQ 可以减少文件中的代码量，使代码更易于读取，并允许不同的数据源具有类似的查询表达式模式。

> [!NOTE]
> LINQ 语法的效率通常低于 foreach 循环。 使用 LINQ 来提高代码的可读性时，最好了解可能发生的性能权衡。

## <a name="convert-a-foreach-loop-to-linq-refactoring"></a>将 foreach 循环转换为 LINQ 重构

1. 请将光标置于 `foreach` 关键字。

    ![使用 IEnumerable 的 Foreach 示例](media/convert-foreach-to-LINQ.png)

2. 按“Ctrl”  + **。** 触发“快速操作和重构”  菜单。

   ![转换为 LINQ 菜单示例](media/convert-foreach-to-LINQ-codefix.png)

3. 选择“转换为 LINQ”  或“转换为 Linq (调用窗体)”  。

   ![LINQ 查询结果示例](media/convert-foreach-to-LINQ-result.png)

   ![LINQ 调用窗体结果示例](media/convert-foreach-to-LINQ-callform-result.png)

### <a name="sample-code"></a>示例代码

```csharp
using System.Collections.Generic;

public class Class1
{
    public void MyMethod()
    {
        var greetings = new List<string>()
            { "hi", "yo", "hello", "howdy" };

        IEnumerable<string> enumerable()
        {
            foreach (var greet in greetings)
            {
                if (greet.Length < 3)
                {
                    yield return greet;
                }
            }

            yield break;
        }
    }
}
```

## <a name="see-also"></a>请参阅

- [重构](../refactoring-in-visual-studio.md)
- [预览更改窗口](../../ide/preview-changes.md)
- [针对 .NET 开发人员的提示](../csharp-developer-productivity.md)
