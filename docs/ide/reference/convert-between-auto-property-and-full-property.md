---
title: 在自动属性和完整属性之间转换
description: 了解如何使用“快速操作和重构”菜单在自动实现的属性和完整属性之间进行转换。
ms.custom: SEO-VS-2020
ms.date: 03/27/2020
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jillfra
dev_langs:
- CSharp
ms.workload:
- dotnet
ms.openlocfilehash: b53f337b538ff1c0aef84272eea7d9e032eb2c1d
ms.sourcegitcommit: 967c2f8c1b3f805cf42c0246389517689d971b53
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/25/2020
ms.locfileid: "96040831"
---
# <a name="convert-between-auto-property-and-full-property"></a>在自动属性和完整属性之间转换

此重构适用于：

- C#

**功能：** 在自动实现的属性和完整属性之间转换。

**使用时机：** 已更改属性的逻辑。

操作原因：  可以手动在自动实现的属性和完整属性之间进行转换，但此功能会自动执行此操作。 

## <a name="how-to"></a>操作说明

1. 将光标置于属性名称上。
2. 按“Ctrl”  + **。** 触发“快速操作和重构”  菜单。
3. 从下列两个选项中进行选择： 

    选择“转换为完整属性”  。

   ![将自动属性转换为完整属性](media/convert-auto-property-to-full-property.png) 

    选择“使用自动属性”  。 

    ![将完整属性转换为自动属性](media/convert-full-property-to-auto-property.png) 

## <a name="see-also"></a>请参阅

- [重构](../refactoring-in-visual-studio.md)
