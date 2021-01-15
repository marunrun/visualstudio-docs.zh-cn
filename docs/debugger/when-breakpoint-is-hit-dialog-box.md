---
title: “命中断点时”对话框 | Microsoft Docs
description: 使用“命中断点时”指定中断时的操作。 可以指定打印消息，且随后应继续执行。
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: a528709769f599219a7b3df2b8157b0ee3a605b1
ms.sourcegitcommit: 957da60a881469d9001df1f4ba3ef01388109c86
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/13/2021
ms.locfileid: "98149308"
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