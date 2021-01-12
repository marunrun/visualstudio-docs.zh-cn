---
title: 编辑寄存器值 | Microsoft Docs
description: 了解如何通过在“寄存器”窗口（仅在启用了地址级调试时才可用）中编辑寄存器的值来修改寄存器的内容。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- vs.debug.register.edit
dev_langs:
- CSharp
- VB
- FSharp
- C++
- JScript
helpviewer_keywords:
- Registers window, editing register values
- register values
ms.assetid: e27b6bd8-e6d4-4f1d-8a86-9f4047bb1167
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 4f83f67f57e67080f97a6df434f8dfc008e36892
ms.sourcegitcommit: 620d30c60da8f9805fce524fe4951cf40f28297d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/05/2021
ms.locfileid: "97903540"
---
# <a name="how-to-edit-a-register-value-c-c-visual-basic-f"></a>如何：编辑寄存器值（C#、C++、Visual Basic、F#）

只有在“选项”对话框中的“调试”节点下启用了地址级调试后，“寄存器”窗口才可用 。

### <a name="to-change-the-value-of-a-register"></a>更改寄存器值

1. 在“寄存器”窗口中，使用 Tab 或鼠标可以将插入点移到要更改的值的位置。 在开始键入之前，光标必须位于要覆盖的值之前。

2. 键入新值。

    > [!CAUTION]
    > 更改寄存器值（特别是 EIP 和 EBP 寄存器中的值）可能会影响程序的执行。

    > [!CAUTION]
    > 编辑浮点值时，由于要将小数部分从十进制转换为二进制，因此所得的结果可能存在微小误差。 甚至看起来无关紧要的编辑都能引起浮点变量中某些最不重要的数据位发生变化。

## <a name="see-also"></a>请参阅
- [如何：使用“寄存器”窗口](../debugger/how-to-use-the-registers-window.md)