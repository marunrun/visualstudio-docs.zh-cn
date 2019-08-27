---
title: 自动换行并对齐调用链
description: 了解如何自动换行并对齐方法调用链。
ms.date: 08/13/2019
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jillfra
dev_langs:
- CSharp
ms.workload:
- dotnet
ms.openlocfilehash: 2a5b6bea4c915e029ca3ae448444decce0d7b041
ms.sourcegitcommit: b83fefa8177c5554cbe2c59c4d102cbc534f7cc6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/19/2019
ms.locfileid: "69620009"
---
# <a name="wrap-and-align-call-chains"></a>自动换行并对齐调用链

此重构适用于：

- C#

**功能：** 允许自动换行和对齐方法调用链。

**使用时机：** 有一个长链，由一个语句中的多个方法调用组成。

操作原因：  根据用户首选项进行自动换行或缩进时，长列表会更易于阅读。

## <a name="how-to"></a>操作说明

1. 将光标置于任何调用链中。
2. 按“Ctrl”  + **。** 触发“快速操作和重构”  菜单。
3. 选择“对调用链进行自动换行”或“自动换行并对齐调用链”以接受重构   。

   ![自动换行并对齐调用链](media/wrap-call-chain.png)

## <a name="see-also"></a>请参阅

- [重构](../refactoring-in-visual-studio.md)
