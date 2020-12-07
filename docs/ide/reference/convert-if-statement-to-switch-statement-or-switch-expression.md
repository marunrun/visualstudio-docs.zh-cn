---
title: 将 if 语句转换为 switch 语句或表达式
description: 了解如何使用“快速操作和重构”菜单将 if 语句转换为 switch 语句或 C# 8.0 switch 表达式。
ms.custom: SEO-VS-2020
ms.date: 03/10/2020
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jillfra
dev_langs:
- CSharp
ms.workload:
- dotnet
ms.openlocfilehash: e19314b8bf73f5859fdf2cef7d281f142c643b68
ms.sourcegitcommit: 2244665d5a0e22d12dd976417f2a782e68684705
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2020
ms.locfileid: "96305557"
---
# <a name="convert-if-statement-to-switch-statement-or-switch-expression"></a>将 if 语句转换为 switch 语句或 switch 表达式

此重构适用于：

- C#

**功能：** 将 if 语句转换为 [switch 语句](/dotnet/csharp/language-reference/keywords/switch)或 C# 8.0 [switch 表达式](/dotnet/csharp/whats-new/csharp-8#switch-expressions)。

**使用时机：** 最好将 `if` 语句转换为 `switch` 语句或 `switch` 表达式，反之亦然。

操作原因：  如果使用 `if` 语句，通过此重构可将其轻松转换为 `switch` 语句或 `switch` 表达式。

## <a name="how-to"></a>操作说明

1. 请将光标置于 `if` 关键字。
2. 按“Ctrl”  + **。** 触发“快速操作和重构”  菜单。
3. 从下列两个选项中进行选择：

    选择“转换为 'switch' 语句”  。

   ![将 if 语句转换为 switch 语句](media/convert-if-to-switch-statement.png)

    选择“转换为 "switch" 表达式”  。

    ![将 If 语句转换为 Switch 表达式](media/convert-if-to-switch-expression.png)

## <a name="see-also"></a>请参阅

- [重构](../refactoring-in-visual-studio.md)
