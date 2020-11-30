---
title: 添加显式强制转换
description: 了解如何根据代码的上下文自动向表达式添加显式强制转换。
ms.custom: SEO-VS-2020
ms.date: 03/26/2020
ms.topic: reference
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: a8208ec9c84eb076ab5c313b3078d3853619fb06
ms.sourcegitcommit: 935e4d9a20928b733e573b6801a6eaff0d0b1b14
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/25/2020
ms.locfileid: "95870841"
---
# <a name="add-explicit-cast"></a>添加显式强制转换

此代码生成适用于：

- C#

**功能：** 允许根据使用情况，自动向表达式添加显式强制转换。

**使用时机：** 需要向表达式添加显式强制转换，并希望正确地自动分配它。

操作原因：  可以手动向表达式添加显式强制转换，但此功能会根据代码上下文自动添加它。

## <a name="how-to-use-it"></a>使用方法

1. 将脱字号放置在错误上。
2. 按“Ctrl”  + **。** 触发“快速操作和重构”  菜单。
3. 选择“添加显式强制转换”  。

   ![在 Visual Studio 中添加显式强制转换快速操作](media/add-explicit-cast.png)

## <a name="see-also"></a>请参阅

- [代码生成](../code-generation-in-visual-studio.md)
- [重构](../refactoring-in-visual-studio.md)
