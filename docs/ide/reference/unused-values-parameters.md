---
title: 未使用的值和参数
description: 了解未使用的值分配、变量和参数以及它们在 Visual Studio 代码编辑器中的显示方式。
ms.custom: SEO-VS-2020
ms.date: 02/15/2019
ms.topic: reference
author: kendrahavens
ms.author: kehavens
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- dotnet
ms.openlocfilehash: 8768992ce3ef9f40ab0adba1724d43b32e5bde5c
ms.sourcegitcommit: bbed6a0b41ac4c4a24e8581ff3b34d96345ddb00
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2020
ms.locfileid: "96560702"
---
# <a name="unused-value-assignments-variables-and-parameters"></a>未使用的值分配、变量和参数

此重构适用于：

- C#
- Visual Basic

**功能：** 渐隐未使用的参数并为未使用的表达式值生成警告。 编译器也执行流分析，以查找任何未使用的值分配。 渐隐未使用的值分配，然后显示包含[快速操作](../quick-actions.md)的灯泡，以删除多余的分配。 未使用的变量（带有未知值）显示[快速操作](../quick-actions.md)建议，以改用[弃元](/dotnet/csharp/discards)。 （弃元是一种在应用程序代码中人为取消使用的临时虚拟变量。 它们可以减少内存分配，使代码易于读取。）

**使用时机：** 具有从未使用的值分配、参数或表达式值。

操作原因：有时很难判断是否不再使用某个值分配、变量或参数。 通过渐隐这些值或发出警告，可以直观地了解可删除的代码。

## <a name="unused-expression-values-and-parameters-diagnostic"></a>未使用的表达式值和参数诊断

1. 具有任何未使用的值分配、变量或参数。
2. 未使用的分配值或参数渐隐。未使用的表达式值会生成一条警告。

  ![未使用的参数](media/unused-parameter.png)
  ![Unused value](media/unused-value.png)
  ![未使用的值分配](media/unused-value-assignment.png)
  ![Unused value discard](media/unused-value-discard.png)

## <a name="see-also"></a>另请参阅

- [重构](../refactoring-in-visual-studio.md)
- [针对 .NET 开发人员的提示](../csharp-developer-productivity.md)
