---
title: Visual Basic 中的 Stop 语句Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- CSharp
- VB
helpviewer_keywords:
- End statements
- breakpoints, Stop statements
- debugging managed code, Stop statements vs breakpoints
- Stop statements, about Stop statements
- debugging [Visual Basic], Stop statements vs. breakpoints
ms.assetid: 4ad3fe5c-3dfb-4913-b2eb-a0b635751c18
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 8f9ab4ef453a921371ab7ef4f272cd0e38f4108a
ms.sourcegitcommit: 4d2620bee4688fb881e09a07ea4a264b99f0743e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/27/2019
ms.locfileid: "71322537"
---
# <a name="stop-statements-in-visual-basic"></a>Visual Basic 中的 Stop 语句

Visual Basic Stop 语句提供了一种以编程方式设置断点的替换方法。 当调试器遇到 Stop 语句时，它将中断程序的执行（进入中断模式）。 C#程序员可以通过调用来<xref:System.Diagnostics.Debugger.Break%2A?displayProperty=nameWithType>实现同样的效果。

通过编辑源代码来设置或移除 Stop 语句。 不能使用调试器命令设置或清除 Stop 语句，而对于断点却可以使用调试器命令。

不同于 End 语句，Stop 语句不重置变量或返回设计模式。 可以从“调试”菜单中选择“继续”继续运行应用程序。

在调试器外部运行 Visual Basic 应用程序时，如果启用了实时调试，Stop 语句会启动调试器。 如果未启用实时调试，则 Stop 语句的行为就像它是结束语句并终止执行。 没有发生 QueryUnload 或 Unload 事件，因此必须从 Visual Basic 应用程序的发布版本中移除所有的 Stop 语句。 有关详细信息，请参阅[实时调试](just-in-time-debugging-in-visual-studio.md)。

 若要避免移除 Stop 语句，可以使用条件编译：

```vb
#If DEBUG Then
   Stop
#Else
   ' Don't stop
#End If
```

另一种方法是使用<xref:System.Diagnostics.Debug.Assert%2A?displayProperty=nameWithType>语句而不是 Stop 语句。 <xref:System.Diagnostics.Debug.Assert%2A?displayProperty=nameWithType>语句仅在未满足指定条件时中断执行。 <xref:System.Diagnostics.Debug.Assert%2A>生成发布版本时，将自动删除语句。 有关详细信息，请参阅[托管代码中的断言](assertions-in-managed-code.md)。 如果希望<xref:System.Diagnostics.Debug.Assert%2A>语句始终在调试版本中中断执行，可以执行以下操作：

```csharp
Debug.Assert(false);
```

```vb
Debug.Assert(False)
```

另一种<xref:System.Diagnostics.Debug.Fail%2A?displayProperty=nameWithType>方法是使用方法：

```csharp
Debug.Fail("a clever output string goes here");
```

```vb
Debug.Fail("a clever output string goes here")
```

## <a name="see-also"></a>请参阅

- [调试器安全](debugger-security.md)
- [C#, F#, and Visual Basic Project Types](debugging-preparation-csharp-f-hash-and-visual-basic-project-types.md)（C#、F# 和 Visual Basic 项目类型）
- [调试托管代码](debugging-managed-code.md)
