---
title: 断点时命中对话框 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug.whenbreakpointishit
dev_langs:
- FSharp
- VB
- CSharp
- C++
- JScript
- SQL
- VB
- CSharp
- C++
ms.assetid: 476e3d98-cf35-4338-b124-cd0f3010d854
caps.latest.revision: 14
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 9a7cd140a22c435df0875c089a69476d3e1e61cf
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68149407"
---
# <a name="when-breakpoint-is-hit-dialog-box"></a>“命中断点时”对话框
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

使用此对话框，您可以自定义命中断点时，会发生的操作。  
  
## <a name="uielement-list"></a>UIElement 列表  
 **打印消息**  
 打印一条消息，使用 DebuggerDisplay 语法。 有关详细信息，请参阅[使用 DebuggerDisplay 特性](../debugger/using-the-debuggerdisplay-attribute.md)。  
  
 此文本框还支持可用于单独或 DebuggerDisplay 表达式的大括号内的特殊关键字 （如 $ADDRESS)。 在对话框中列出了可用的关键字。  
  
 **继续执行**  
 仅在选择“打印消息”时启用此控件  。 选择此控件，可以使用断点与跟踪点跟踪程序执行，而不是重大时命中位置。  
  
## <a name="see-also"></a>请参阅  
 [使用断点](../debugger/using-breakpoints.md)   
 [使用 DebuggerDisplay 特性](../debugger/using-the-debuggerdisplay-attribute.md)
