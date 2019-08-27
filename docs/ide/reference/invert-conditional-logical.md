---
title: 反转条件表达式和逻辑运算
ms.date: 02/19/2019
ms.topic: reference
author: kendrahavens
ms.author: kehavens
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- dotnet
ms.openlocfilehash: 3931ae53fc29b0ffd8b8b6e96951a0f4786ff756
ms.sourcegitcommit: 614d5b99576ea27a41957cd94062dc95cbd29c1c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2019
ms.locfileid: "65531680"
---
# <a name="invert-conditional-expressions-and-conditional-andor-operators"></a>反转条件表达式和条件 AND/OR 运算符

此重构适用于：

- C#
- Visual Basic

**功能：** 可以反转条件表达式或条件 AND/OR 运算符。

**使用时机：** 如果进行反转，条件表达式或条件 AND/OR 运算符将更好被理解。

操作原因：手动反转表达式或条件 AND/OR 运算符可能需要更长的时间并可能引入错误。 此代码修补程序可帮助你自动执行此重构。

## <a name="invert-conditional-expressions-and-conditional-andor-operators-refactoring"></a>反转条件表达式和条件 AND/OR 重构

1. 请将光标置于条件表达式或条件 AND/OR 运算符。
2. 按“Ctrl”+**。** 触发“快速操作和重构”菜单。
3. 选择“反转条件”或“将 '&&' 替换为 '||'”

    ![反转条件](media/invert-conditional.png)

    ![反转条件](media/invert-logical-operator.png)

## <a name="see-also"></a>请参阅

- [重构](../refactoring-in-visual-studio.md)
- [针对 .NET 开发人员的提示](../csharp-developer-productivity.md)
