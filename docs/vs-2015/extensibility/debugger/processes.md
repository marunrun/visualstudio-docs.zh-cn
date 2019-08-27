---
title: 进程 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], processes
ms.assetid: a6a1efdc-b243-40c8-a778-6f69f6b018be
caps.latest.revision: 15
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 82718a7ceb7a18f9978840f35ca0c5fce5628e81
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68153672"
---
# <a name="processes"></a>进程
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

在调试器体系结构，方面**进程**:  
  
- 是一组程序的容器。 它是非常类似于 Windows 进程，这是一组线程的容器。  
  
- 可以将自己标识的名称、 标识符或物理标识符。  
  
- 可以枚举所有正在运行的程序 （和其线程）。  
  
- 可以描述本身、 在中，运行的端口和包含它的计算机。  
  
- 可以创建一个或多个程序终止的任何程序创建，或导致程序停止。  
  
- 为由[IDebugProcess2](../../extensibility/debugger/reference/idebugprocess2.md)接口，这启动进程时创建的。 通过任一会话调试管理器 (SDM) 启动进程或[LaunchSuspended](../../extensibility/debugger/reference/idebugenginelaunch2-launchsuspended.md)。  
  
  调试包可以附加调试引擎 (DE) 到的进程通过调用[附加](../../extensibility/debugger/reference/idebugprocess2-attach.md)。 这意味着，DE 将附加到所有可能的程序可以处理的进程中运行。 例如，如果公共语言运行时 DE 会附加到进程，它附加到正在运行托管的代码的程序仅。  
  
## <a name="see-also"></a>请参阅  
 [程序](../../extensibility/debugger/programs.md)   
 [线程](../../extensibility/debugger/threads.md)   
 [调试器概念](../../extensibility/debugger/debugger-concepts.md)   
 [调试包](../../extensibility/debugger/debug-package.md)   
 [调试引擎](../../extensibility/debugger/debug-engine.md)   
 [IDebugProcess2](../../extensibility/debugger/reference/idebugprocess2.md)   
 [LaunchSuspended](../../extensibility/debugger/reference/idebugenginelaunch2-launchsuspended.md)   
 [附加](../../extensibility/debugger/reference/idebugprocess2-attach.md)
