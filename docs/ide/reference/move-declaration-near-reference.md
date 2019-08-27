---
title: 将变量声明移动到引用附近
ms.date: 01/26/2018
ms.topic: reference
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- CSharp
ms.workload:
- dotnet
ms.openlocfilehash: e23c5c8d6ea0895f9e5a78e726bb7a7cede071bb
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62540591"
---
# <a name="move-declaration-near-reference-refactoring"></a>将变量声明移动到引用附近

此重构适用于：

- C#

**功能：** 将变量声明移至靠近其用法的位置。

**使用时机：** 具有可存在于较窄范围中的变量声明时。

操作原因：可以将其保留不变，但这可能会导致可读性问题或信息隐藏。 可以进行重构，以提高可读性。

## <a name="how-to"></a>操作说明

1. 将光标置于变量声明中。

1. 接下来，执行以下操作之一：

   - **键盘**
      - 按“Ctrl”+**。** 触发“快速操作和重构”菜单，然后从“预览”弹出窗口中选择“移动声明至引用附近”。
   - **鼠标**
      - 右键单击代码，选择“快速操作和重构”菜单，然后从“预览”弹出窗口中选择“移动声明至引用附近”。

1. 对更改感到满意时，按 Enter 或单击菜单中的修复，即可提交所做的更改。

示例:

```csharp
// Before
int x;
if (condition)
{
    x = 1;
    Console.WriteLine(x);
}

// Move declaration near reference

// After
if (condition)
{
    int x = 1;
    Console.WriteLine(x);
}
```

## <a name="see-also"></a>请参阅

- [重构](../refactoring-in-visual-studio.md)
- [预览更改](../../ide/preview-changes.md)