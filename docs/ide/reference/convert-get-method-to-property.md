---
title: 将 Get 方法转换为属性；将属性转换为 Get 方法
ms.date: 01/26/2018
ms.topic: reference
ms.devlang: csharp
author: jillre
ms.author: jillfra
manager: jillfra
f1_keywords:
- vs.csharp.refactoring.convertmethodtoproperty
dev_langs:
- CSharp
ms.workload:
- dotnet
ms.openlocfilehash: ac33db013a8cea11b373e4104bf2d58a1b22cef4
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72654529"
---
# <a name="convert-get-method-to-property--convert-property-to-get-method-refactorings"></a>将 Get 方法转换为属性或反向转换

这些重构适用于：

- C#

## <a name="convert-get-method-to-property"></a>将 Get 方法转换为属性

**功能：** 将 Get 方法转换为属性（或 Set 方法）。

**使用时机：** 有不包含任何逻辑的 Get 方法时。

### <a name="how-to"></a>操作说明

1. 将光标置于 Get 方法名称中。

1. 接下来，执行以下操作之一：

   - **键盘**
      - 按“Ctrl”  + **。** 触发“快速操作和重构”菜单，然后从“预览”弹出窗口中选择“用属性替换方法”   。
   - **鼠标**
      - 右键单击代码，选择“快速操作和重构”菜单，然后从“预览”弹出窗口中选择“用属性替换方法”   。

1. （可选）如果拥有 Set 方法，此时还可通过选择“用属性替换 Get 方法和 Set 方法”来转换 Set 方法  。

1. 如果对代码预览中的更改感到满意，请按“Enter”  或单击菜单中的“修复”，即可提交所做的更改。

示例：

```csharp
private int MyValue;

// Before
public int GetMyValue()
{
    return MyValue;
}

// Replace 'GetMyValue' with property

// After
public int MyValue
{
    get { return MyValue; }
}
```

## <a name="convert-property-to-get-method"></a>将属性转换为 Get 方法

**功能：** 将属性转换为 Get 方法

**使用时机：** 有涉及多个立即设置或获取值的属性时

### <a name="how-to"></a>操作说明

1. 将光标置于 Get 方法名称中。

1. 接下来，执行以下操作之一：

   - **键盘**
      - 按“Ctrl”  + **。** 触发“快速操作和重构”  菜单，然后从“预览”弹出窗口中选择“用方法替换属性”  。
   - **鼠标**
      - 右键单击代码，选择“快速操作和重构”  菜单，然后从“预览”弹出窗口中选择“用方法替换属性”  。

1. 如果对代码预览中的更改感到满意，请按“Enter”  或单击菜单中的“修复”，即可提交所做的更改。

## <a name="see-also"></a>请参阅

- [重构](../refactoring-in-visual-studio.md)
- [预览更改](../../ide/preview-changes.md)