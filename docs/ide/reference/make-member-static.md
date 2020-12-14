---
title: 将成员设为静态成员
description: 了解如何使用“快速操作和重构”菜单将成员设为静态成员。
ms.custom: SEO-VS-2020
ms.date: 02/19/2020
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jillfra
dev_langs:
- CSharp
ms.workload:
- dotnet
ms.openlocfilehash: e663d59f47728bc4a7c84290ee0e89ae453f23ae
ms.sourcegitcommit: bbed6a0b41ac4c4a24e8581ff3b34d96345ddb00
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2020
ms.locfileid: "96561014"
---
# <a name="make-member-static"></a>将成员设为静态成员

此重构适用于：

- C#

**功能：** 将成员设为静态成员。

**使用时机：** 在你希望非静态成员为静态成员时。

操作原因：静态成员可提高可读性：已知特定代码是隔离的，使其更易于理解、重新读取和重用。 

## <a name="how-to"></a>操作说明

1. 将脱字号放置在成员名称上。

2. 按“Ctrl”  + **。** （句点）触发“快速操作和重构”菜单。

   ![将成员设为静态成员](media/make-member-static.png)

3. 选择“设为静态”。

## <a name="see-also"></a>另请参阅

- [重构](../refactoring-in-visual-studio.md)
