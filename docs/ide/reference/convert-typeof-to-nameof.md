---
title: 将 typeof 转换为 nameof
description: 了解如何使用 Visual Studio 中的“快速操作和重构”菜单，在 C# 中将 typeof 转换为 nameof，在 Visual Basic 中将 GetType 转换为 NameOf。
ms.date: 08/12/2020
ms.topic: reference
author: m-redding
ms.author: midumont
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- dotnet
ms.openlocfilehash: ce76b82e2ebc68634be7cf4d463f6b8216d81e06
ms.sourcegitcommit: 3c571f44bfd6402efea5187af43df287bac5b6ac
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/24/2020
ms.locfileid: "97761194"
---
# <a name="convert-typeof-to-nameof"></a>将 `typeof` 转换为 `nameof`

此重构适用于：

- C#
- Visual Basic

**功能：** 使你可以将 `typeof(<QualifiedType>).Name` 实例转换为以 C# 编写的 `nameof(<QualifiedType>)`，并将 `GetType(<QualifiedType>).Name` 实例转换为以 Visual Basic 编写的 `NameOf(<QualifiedType>)`。

**使用时机：** `typeof(<QualifiedType>).Name` 的所有实例，其中 `someType` 不是泛型类型。 此排除是必需的，因为这种情况不返回与 `nameof(<QualifiedType>)` 相同的字符串值。 对于 Visual Basic 实例，也是如此。

操作原因：使用 `nameof` 而不是 `type` 的名称可避免与检索 `type` 对象有关的反射，并且是一种更实用的编写它的方法。

## <a name="how-to"></a>操作说明

1. 将光标置于 C# 的 `typeof(<QualifiedType>).Name` 实例中或 Visual Basic 的 `GetType(<QualifiedType>).Name` 中。

2. 按“Ctrl”+ **。** 触发“快速操作和重构”菜单。

3. 选择以下选项之一：

    - C#
      <br>选择“将 'typeof' 转换为 'nameof'”：![Visual Studio 中“快速操作和重构”菜单的屏幕截图，其中选中了“将 'typeof' 转换为 'nameof'”，并显示了 C# 代码更改。](media/convert-type-of.PNG)

    - Visual Basic
      <br>选择“将 'GetType' 转换为 'NameOf'”：![Visual Studio 中“快速操作和重构”菜单的屏幕截图，其中选中了“将 'GetTyp' 转换为 'NameOf'”，并显示了 Visual Basic 代码更改。](media/convert-get-type.PNG)

## <a name="see-also"></a>另请参阅

- [重构](../refactoring-in-visual-studio.md)
