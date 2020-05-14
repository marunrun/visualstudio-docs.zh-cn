---
title: 将匿名类型转换为元组
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
ms.openlocfilehash: f7e89c5b5a05900fe42af62ef87f70292e94e662
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "79094281"
---
# <a name="convert-anonymous-type-to-tuple"></a>将匿名类型转换为元组

此重构适用于：

- C#

- Visual Basic

**功能：** 将匿名类型转换为元组。

**使用时机：** 有符合元组资格的匿名类型。

操作原因：  [元组](/dotnet/csharp/tuples)有助于保持语法轻量级。 此快速操作可以更容易地利用此 C# 功能。

## <a name="how-to"></a>操作说明

1. 请将光标放置在匿名类型中。
2. 按“Ctrl”  + **。** 触发“快速操作和重构”  菜单。

   ![将匿名类型转换为元组](media/convert-anon-to-tuple.png)

2. 按 Enter 接受重构  。

   ![将匿名类型转换为元组](media/convert-anon-to-tuple-complete.png)

## <a name="see-also"></a>请参阅

- [重构](../refactoring-in-visual-studio.md)
