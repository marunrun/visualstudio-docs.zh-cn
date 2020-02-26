---
title: 将 if 语句转换为 switch 语句或 switch 表达式
ms.date: 02/12/2020
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jillfra
dev_langs:
- CSharp
ms.workload:
- dotnet
ms.openlocfilehash: cb0c06fe0493f973ea9cf0a566ffda45a49eeeff
ms.sourcegitcommit: 68f893f6e472df46f323db34a13a7034dccad25a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/15/2020
ms.locfileid: "77283459"
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
3. 选择“转换为 'switch' 语句”  。

   ![将 if 语句转换为 switch 语句或 switch 表达式](media/convert-if-statement-to-switch-statement-or-switch-expression.png) 

## <a name="see-also"></a>请参阅

- [重构](../refactoring-in-visual-studio.md)
