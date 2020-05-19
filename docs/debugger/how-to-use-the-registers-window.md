---
title: 在调试器中查看寄存器值 | Microsoft Docs
ms.custom: seodec18
ms.date: 11/19/2018
ms.topic: conceptual
f1_keywords:
- vs.debug.registers
dev_langs:
- CSharp
- VB
- FSharp
- C++
- JScript
helpviewer_keywords:
- registers, debugging
- register contents
- flags, Registers window
- register groups
- debugging [Visual Studio], Registers window
- Registers window
ms.assetid: 2918ffa2-562f-40d6-9053-ef321bbeb767
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: afcada407060af2072e3cf1c30e86153762890b5
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62905996"
---
# <a name="view-register-values-in-the-registers-window-c-c-visual-basic-f"></a>在“寄存器”窗口中查看寄存器值（C#、C++、Visual Basic、F#）

在 Visual Studio 调试期间，“寄存器”窗口显示寄存器内容。 有关寄存器和“寄存器”窗口背后概念的高级别介绍，请参阅[调试器基础知识：“寄存器”窗口](../debugger/debugging-basics-registers-window.md)。

> [!NOTE]
> 寄存器信息对于脚本或 SQL 应用不可用。

在调试过程中，寄存器值会随着代码在应用中执行而更改。 最近更改过的值在“寄存器”窗口中显示为红色。

为了减少混乱，“寄存器”窗口将寄存器组织成组，具体情况随平台和处理器类型的不同而不同。 可以显示或隐藏寄存器组。 有关详细信息，请参阅[如何：显示和隐藏寄存器组](../debugger/how-to-display-and-hide-register-groups.md)。

有关在“寄存器”窗口中看到的标志的信息，请参阅[关于“寄存器”窗口](../debugger/debugging-basics-registers-window.md)

您可以编辑寄存器的值。 有关详细信息，请参阅[如何：编辑寄存器值](../debugger/how-to-edit-a-register-value.md)。

打开“寄存器”窗口

1. 启用地址级调试，方法是在“工具”（或“调试”）>“选项” > “调试”中选择“启用地址级调试”。

1. 当调试正在运行或处于某个断点时，请选择“调试” > “窗口” > “寄存器”，或按 Alt+5。

>[!NOTE]
>对话框和菜单命令可能有所不同，具体取决于 Visual Studio 版本或设置。 若要更改设置，请在 Visual Studio“工具”菜单上选择“导入和导出设置” 。 有关详细信息，请参阅[重置设置](../ide/environment-settings.md#reset-settings)。

### <a name="see-also"></a>请参阅

- [调试基础知识：“寄存器”窗口](../debugger/debugging-basics-registers-window.md)
- [查看调试器中的数据](../debugger/viewing-data-in-the-debugger.md)
