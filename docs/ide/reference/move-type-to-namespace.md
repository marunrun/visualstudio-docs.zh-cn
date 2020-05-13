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
monikerRange: vs-2019
ms.openlocfilehash: 58d2757fa8798b67c8e597f5f82bc65a279f4a90
ms.sourcegitcommit: 8ff6c6975148ce43bdac21c8995fbab910c312fe
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/28/2020
ms.locfileid: "80375570"
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
