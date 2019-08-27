---
title: Split 或 merge if 语句
ms.date: 06/12/2019
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jillfra
dev_langs:
- CSharp
ms.workload:
- dotnet
ms.openlocfilehash: 405ccd4bc0197ce06aa14982a16dc02f6d13a537
ms.sourcegitcommit: d4920babfc3d24a3fe1d4bf446ed3fe73b344467
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2019
ms.locfileid: "67160733"
---
# <a name="split-or-merge-if-statements"></a>Split 或 merge if 语句

此重构适用于：

- C#

**功能：** **功能：** 拆分或合并 [if](/dotnet/csharp/language-reference/keywords/if-else) 语句。

**使用时机：** 希望将使用 `&&` 或 `||` 运算符的 `if` 语句拆分为嵌套的 `if` 语句，或者将 `if` 语句与外部 `if` 语句合并。

操作原因：  这是一个样式偏好问题。  

## <a name="how-to"></a>操作说明

如果想要拆分 `if` 语句：

1. 将光标置于 `&&` 或 `||` 运算符的 `if` 语句中。

2. 按“Ctrl”  + **。** 触发“快速操作和重构”  菜单。

    ![拆分 If 语句](../media/split-if-statement.png)

3. 选择“拆分到嵌套的 if 语句”  。

    ![拆分 If 语句完成](../media/split-if-statement-complete.png)

如果想要将内部 `if` 语句和外部 `if` 语句合并： 

1. 将光标置于内部 `if` 关键字。

2. 按“Ctrl”  + **。** 触发“快速操作和重构”  菜单。

    ![合并 If 语句](../media/merge-if-statement.png)

3. 选择“与外部 if 语句合并”  。

    ![合并 If 语句完成](../media/merge-if-statement-complete.png)

## <a name="see-also"></a>请参阅

- [重构](../refactoring-in-visual-studio.md)