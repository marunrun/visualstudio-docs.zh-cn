---
title: “删除无法访问的代码”重构
description: 了解如何使用“快速操作和重构”菜单删除永远不执行的代码。
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: 3af9d0a14b600773c5025fcaad68380c7bb82b29
ms.sourcegitcommit: 2cf87f79762906ccaa133a7645aa4c77a0bed7da
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/05/2020
ms.locfileid: "96616702"
---
# <a name="remove-unreachable-code-refactoring"></a>“删除无法访问的代码”重构

此重构适用于：

- C#

- Visual Basic

功能：删除永远不执行的代码

时机：程序无法访问代码片段，使得该代码片段没有存在的必要性时。

原因：通过删除永远不会执行的多余代码来提高可读性和可维护性。

## <a name="how-to"></a>操作说明

1. 将无法访问的代码淡化后，将光标置于其中的任意位置：

![淡化后的无法访问的代码](media/unreachablecode-faded-cs.png)

1. 接下来，执行以下操作之一：

   - **键盘**
      - 按“Ctrl”+ **。** 触发“快速操作和重构”菜单，然后从“预览”弹出窗口选择“删除无法访问的代码”。
   - **鼠标**
      - 右键单击代码，选择“快速操作和重构”菜单，然后从“预览”弹出窗口选择“删除无法访问的代码”。

1. 对更改感到满意时，按 Enter 或单击菜单中的修复，即可提交所做的更改。

例如：

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

## <a name="see-also"></a>另请参阅

- [重构](../refactoring-in-visual-studio.md)
- [预览更改](../../ide/preview-changes.md)
