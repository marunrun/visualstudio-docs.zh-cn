---
title: Split 或 merge if 语句
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
ms.openlocfilehash: a3b42f83faacda6be34b282150cf4fb4c0f379f1
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "79093678"
---
# <a name="split-or-merge-if-statements"></a>Split 或 merge if 语句

此重构适用于：

- C#

- Visual Basic

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