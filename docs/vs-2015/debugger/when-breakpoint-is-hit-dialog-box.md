---
title: “命中断点时”对话框 | Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68149407"
---
# <a name="when-breakpoint-is-hit-dialog-box"></a>“命中断点时”对话框
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

借助此对话框，你可以自定义命中断点时执行的操作。  
  
## <a name="uielement-list"></a>UIElement 列表  
 **打印消息**  
 使用 DebuggerDisplay 语法打印一条消息。 有关详细信息，请参阅[使用 DebuggerDisplay 属性](../debugger/using-the-debuggerdisplay-attribute.md)。  
  
 此文本框还支持可单独使用或在 DebuggerDisplay 表达式的大括号内使用的特殊关键字（例如 $ADDRESS）。 可用关键字在对话框中列出。  
  
 **继续执行**  
 仅在选择“打印消息”时启用此控件****。 选择此控件后，可以使用断点作为跟踪点来跟踪程序执行，而不是在命中位置时中断。  
  
## <a name="see-also"></a>另请参阅  
 [使用断点](../debugger/using-breakpoints.md)   
 [使用 DebuggerDisplay 特性](../debugger/using-the-debuggerdisplay-attribute.md)
