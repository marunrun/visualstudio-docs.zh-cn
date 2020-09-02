---
title: " (Visual Studio SDK) 的断点 |Microsoft Docs"
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- breakpoints
ms.assetid: acfcabed-9f2f-436c-ad18-7ca2f45d631b
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 39c13271bad984291f609ef45505549855bee99f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68146417"
---
# <a name="breakpoints-visual-studio-sdk"></a>断点 (Visual Studio SDK)
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

有三种类型的断点： "挂起"、"绑定" 和 "错误"。  
  
 **挂起的断点：**  
  
- 是一个抽象，其中包含将断点绑定到一个或多个程序中的一个或多个代码上下文所需的所有信息。 每次被调试的程序导致加载代码时，调试引擎都会检查所有挂起的断点，以确定它们是否可以绑定。  
  
   挂起的断点本身从不绑定到代码，而是收集并被视为包含其生成的所有绑定断点。  
  
- 由 [IDebugPendingBreakpoint2](../../extensibility/debugger/reference/idebugpendingbreakpoint2.md) 接口表示。  
  
  **绑定断点：**  
  
- 与关联的断点的抽象，或绑定到单个代码上下文的断点。 每个绑定断点都是为响应挂起断点而生成的。 但挂起的断点可以生成多个绑定断点。  
  
   卸载代码时，绑定断点可以取消绑定并被丢弃。  
  
- 由 [IDebugBoundBreakpoint2](../../extensibility/debugger/reference/idebugboundbreakpoint2.md) 接口表示。  
  
  **错误断点：**  
  
- 用于描述尝试将挂起断点绑定到代码上下文的错误的抽象。 错误断点描述位置或断点表达式本身中的错误。 有关详细信息，请参阅 [绑定断点](../../extensibility/debugger/binding-breakpoints.md)。  
  
   断点错误可以是错误或警告。  
  
- 由 [IDebugErrorBreakpoint2](../../extensibility/debugger/reference/idebugerrorbreakpoint2.md) 接口表示。  
  
## <a name="see-also"></a>另请参阅  
 [程序](../../extensibility/debugger/programs.md)   
 [调试器概念](../../extensibility/debugger/debugger-concepts.md)   
 [代码上下文](../../extensibility/debugger/code-context.md)   
 [IDebugBoundBreakpoint2](../../extensibility/debugger/reference/idebugboundbreakpoint2.md)   
 [IDebugPendingBreakpoint2](../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)   
 [IDebugErrorBreakpoint2](../../extensibility/debugger/reference/idebugerrorbreakpoint2.md)
