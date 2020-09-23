---
title: 为结构生成 IEquatable 运算符
ms.date: 05/12/2020
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 5ee695169f52036858fc70598f81f375638ab03f
ms.sourcegitcommit: 566144d59c376474c09bbb55164c01d70f4b621c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/19/2020
ms.locfileid: "90808111"
---
# <a name="generate-iequatable-operators-when-generating-equals-for-structs"></a>在为结构生成 Equals 时生成 IEquatable 运算符

此代码生成适用于：

- C#

**功能：** 可便于为[结构](/dotnet/csharp/language-reference/builtin-types/struct)生成 Equals 和 IEquatable 运算符。

**使用时机：** 你有一个结构，我们会为你自动添加 IEquatable 以及 Equals 和 Not Equals 运算符。

操作原因：

- 如果实现值类型，则应考虑重写 Equals 方法，针对 Equals 方法在 ValueType 上的默认实现提升相关性能。

- 实现 IEquatable 接口实现了特定于类型的 Equals() 方法。

## <a name="how-to"></a>操作说明

1. 将光标置于结构声明行上的某个位置。

2. 接下来，执行以下操作之一：

   - 按“Ctrl”+ **。** 触发“快速操作和重构”菜单。

   - 右键单击并选择“快速操作和重构”菜单。

   - 单击 ![左边缘中](../media/screwdriver-icon.png) 显示的螺丝刀图标。

   ![为结构生成 IEquatable 和 Equals](media/generate-equals-structs.png)

3. 在下拉菜单中，选择“生成 Equals(object)”。

## <a name="see-also"></a>请参阅

- [代码生成](../code-generation-in-visual-studio.md)
- [预览更改](../../ide/preview-changes.md)