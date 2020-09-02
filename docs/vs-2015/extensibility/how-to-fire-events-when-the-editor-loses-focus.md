---
title: 如何：在编辑器失去焦点时激发事件 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - fire events on losing focus
ms.assetid: 64d40695-6917-468a-8037-a253453ac159
caps.latest.revision: 9
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 2ebca733798636ca32787b88b8874c31a2ffffdb
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68204196"
---
# <a name="how-to-fire-events-when-the-editor-loses-focus"></a>如何：在编辑器失去焦点时触发事件
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

有时，有必要知道编辑器何时失去窗口框架焦点。 例如，你可能需要将代码从代码窗口中提取出来，然后再将其集中于该编辑器。 下面的过程提供了接收编辑器失去焦点通知的步骤。  
  
### <a name="to-fire-an-event-in-response-to-an-editor-losing-focus"></a>触发事件以响应失去焦点的编辑器  
  
1. 通过从获取对象来监视选择事件 <xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection> <xref:Microsoft.VisualStudio.Shell.Interop.SVsShellMonitorSelection> 。  
  
2. 调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection.AdviseSelectionEvents%2A> 并为其提供你的 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSelectionEvents> 对象。  
  
3. 在对的调用中 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSelectionEvents.OnElementValueChanged%2A> ，查找 `elementid==SEID_WindowFrame` 。  
  
4. `varValueNew`针对以下两项测试参数：  
  
    1. 要查找的窗口框架。  
  
    2. 程序将所选内容丢失到该窗口框架的点。
