---
title: “命中断点时”对话框 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.debug.whenbreakpointishit
dev_langs:
- CSharp
- VB
- FSharp
- C++
- JScript
- SQL
ms.assetid: 476e3d98-cf35-4338-b124-cd0f3010d854
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 53b19f4dd0d4b0cb97bb33e4895f36c4dc8f670c
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72728143"
---
# <a name="when-breakpoint-is-hit-dialog-box"></a>“命中断点时”对话框
借助此对话框，你可以自定义命中断点时执行的操作。

## <a name="uielement-list"></a>UIElement 列表
 **打印消息**：使用 DebuggerDisplay 语法打印消息。 有关详细信息，请参阅[使用 DebuggerDisplay 属性](../debugger/using-the-debuggerdisplay-attribute.md)。

 此文本框还支持可单独使用或在 DebuggerDisplay 表达式的大括号内使用的特殊关键字（例如 $ADDRESS）。 可用关键字在对话框中列出。

 **继续执行**：仅在选择“打印消息”时启用此控件。 选择此控件后，可以使用断点作为跟踪点来跟踪程序执行，而不是在命中位置时中断。

## <a name="see-also"></a>请参阅
- [使用断点](../debugger/using-breakpoints.md)
- [使用 DebuggerDisplay 特性](../debugger/using-the-debuggerdisplay-attribute.md)