---
title: 断点时命中对话框 |Microsoft Docs
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
ms.openlocfilehash: d4cc3c2366ca20328f591b0661e8c2b3e5af1e45
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62929194"
---
# <a name="when-breakpoint-is-hit-dialog-box"></a>“命中断点时”对话框
使用此对话框，您可以自定义命中断点时，会发生的操作。

## <a name="uielement-list"></a>UIElement 列表
 **打印消息**打印一条消息，使用 DebuggerDisplay 语法。 有关详细信息，请参阅[使用 DebuggerDisplay 特性](../debugger/using-the-debuggerdisplay-attribute.md)。

 此文本框还支持可用于单独或 DebuggerDisplay 表达式的大括号内的特殊关键字 （如 $ADDRESS)。 在对话框中列出了可用的关键字。

 **继续执行**启用此控件时，才**打印一条消息**处于选中状态。 选择此控件，可以使用断点与跟踪点跟踪程序执行，而不是重大时命中位置。

## <a name="see-also"></a>请参阅
- [使用断点](../debugger/using-breakpoints.md)
- [使用 DebuggerDisplay 特性](../debugger/using-the-debuggerdisplay-attribute.md)