---
title: 将临时变量替换为其值
ms.date: 01/26/2018
ms.topic: reference
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- dotnet
ms.openlocfilehash: a7c691efcc507212aa0649b6c4b4179fb8288f06
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62423154"
---
# <a name="inline-a-temporary-variable-refactoring"></a>“内联临时变量”重构

此重构适用于：

- C#

- Visual Basic

**功能：** 删除临时变量并将其替换为其值。

**使用时机：** 使用临时变量会使代码难以理解时。

操作原因：删除临时变量可使代码更易于理解。

## <a name="how-to"></a>操作说明

1. 突出显示要内联的临时变量，或将文本光标置于其中：

   - C#：

       ![突出显示的代码 - C#](media/inline-highlight-cs.png)

   - Visual Basic：

       ![突出显示的代码 - Visual Basic](media/inline-highlight-vb.png)

2. 接下来，执行以下操作之一：

   - **键盘**
      - 按“Ctrl”+**。** 触发“快速操作和重构”菜单。
   - **鼠标**
      - 右键单击代码，然后选择“快速操作和重构”菜单。

3. 从“预览”弹出窗口选择“内联临时变量”。

   将删除此变量，且在使用它的位置改用变量的值。

   - C#：

      ![内联结果 - C#](media/inline-result-cs.png)

   - Visual Basic：

      ![内联结果 - Visual Basic](media/inline-result-vb.png)

## <a name="see-also"></a>请参阅

- [重构](../refactoring-in-visual-studio.md)