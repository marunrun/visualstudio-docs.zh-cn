---
title: “删除无法访问的代码”重构
ms.date: 01/26/2018
ms.topic: reference
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- CSharp
ms.workload:
- dotnet
ms.openlocfilehash: b1c88fbeb9daf293df868a835247098e2ce999e3
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62576013"
---
# <a name="remove-unreachable-code-refactoring"></a>“删除无法访问的代码”重构

此重构适用于：

- C#

**功能：** 删除永远不执行的代码。

**使用时机：** 程序无法访问代码片段，使得该代码片段没有存在的必要性时。

操作原因：通过删除永远不会执行的多余代码来提高可读性和可维护性。

## <a name="how-to"></a>操作说明

1. 将无法访问的代码淡化后，将光标置于其中的任意位置：

![淡化后的无法访问的代码](media/unreachablecode-faded-cs.png)

1. 接下来，执行以下操作之一：

   - **键盘**
      - 按“Ctrl”+**。** 触发“快速操作和重构”菜单，然后从“预览”弹出窗口选择“删除无法访问的代码”。
   - **鼠标**
      - 右键单击代码，选择“快速操作和重构”菜单，然后从“预览”弹出窗口选择“删除无法访问的代码”。

1. 对更改感到满意时，按 Enter 或单击菜单中的修复，即可提交所做的更改。

示例:

```csharp
// Before
private void Method()
{
    throw new Exception(nameof(Method));
    Console.WriteLine($"Exception for method {nameof(Method)}");
}

// Remove unreachable code

// After
private void Method()
{
    throw new Exception(nameof(Method));
}
```

## <a name="see-also"></a>请参阅

- [重构](../refactoring-in-visual-studio.md)
- [预览更改](../../ide/preview-changes.md)