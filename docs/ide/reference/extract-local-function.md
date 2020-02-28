---
title: 提取本地函数
description: 通过选择代码并按 Ctrl+R、Ctrl+M，将代码片段转换为自己的方法。
ms.date: 02/19/2020
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jillfra
dev_langs:
- CSharp
ms.workload:
- dotnet
ms.openlocfilehash: 031fbe22ec61837d489df7a6af923ef0cd2454c7
ms.sourcegitcommit: 260d093d2287ba791f28bdc7103493beabf80b2e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/20/2020
ms.locfileid: "77519325"
---
# <a name="extract-local-function-refactoring"></a>提取本地函数重构

此重构适用于：

- C#

**功能：** 将代码片段从现有方法转换为本地函数。

**使用时机：** 需要从本地函数调用某些方法中现有的代码片段时。

操作原因：可以复制/粘贴该代码，但这样会导致重复。 更好的解决方案是将此片段重构为其自己的本地函数。

## <a name="how-to"></a>操作说明

1. 突出显示要提取的代码。

2. 按“Ctrl”+**。** 触发“快速操作和重构”菜单。 

3. 选择“提取本地函数”。

    ![提取本地函数](media/extract-local-function.png)

## <a name="see-also"></a>请参阅

- [重构](../refactoring-in-visual-studio.md)
- [预览更改](../../ide/preview-changes.md)
