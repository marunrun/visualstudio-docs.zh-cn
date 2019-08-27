---
title: 将类型移到命名空间
ms.date: 06/17/2019
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jillfra
dev_langs:
- CSharp
ms.workload:
- dotnet
ms.openlocfilehash: 821e915a0b66f25c5b89a83b31e93b01aea6f400
ms.sourcegitcommit: b593bb889f049fcbdff502c30b73178ed17dbdf0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/20/2019
ms.locfileid: "67292696"
---
# <a name="move-type-to-namespace"></a>将类型移到命名空间

此重构适用于：

- C#

**功能：** 将类型移到命名空间。

**使用时机：** 想要将类型移动到其他命名空间或文件夹。 

操作原因：  想要重构部分解决方案的某些部分，并快速将类型移动到其他命名空间或文件夹。 

## <a name="how-to"></a>操作说明

1. 请将光标置于类名称。
2. 按“Ctrl”  + **。** 触发“快速操作和重构”  菜单。
3. 选择“移动到命名空间”。 

   ![“移动到命名空间”重构](media/move-to-namespace.png)

4. 在打开的对话框中，选择想要将类型移动到的目标命名空间。 

   ![“选择命名空间”对话框](media/select-target-namespace.png)

## <a name="see-also"></a>请参阅

- [重构](../refactoring-in-visual-studio.md)
