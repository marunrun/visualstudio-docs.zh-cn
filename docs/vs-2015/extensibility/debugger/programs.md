---
title: 程序 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], programs
- programs, debugging
ms.assetid: e1f955d8-95da-493b-837e-e97741a26d7e
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 9070b33c7522cdc13fd6217956fcab72cd83f8d1
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68153641"
---
# <a name="programs"></a>Programs
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

在调试器体系结构，方面**程序**:  
  
- 是一组线程和一组模块的容器。 程序在 Windows 操作系统中有任何单个的类比。  
  
     程序是一种类型的子进程。 例如，调试网站时，脚本可视为程序。 脚本引擎进程脚本时，独立于其他脚本，它还具有自己的线程的一组。 调试引擎 (DE) 将附加到程序中，并且不给进程或线程。  
  
- 可以标识本身和它正在运行，并且可以附加到另一个地址，分离，描述创建它，如果任何 DE 的过程。 程序可以执行、 停止、 继续、 终止。  
  
- 可以枚举所有线程。 程序还可以提供其自己的反汇编流，并可以枚举给定的文档位置的所有代码上下文。  
  
- 为由[IDebugProgram2](../../extensibility/debugger/reference/idebugprogram2.md)创建附加程序之前，或附加过程，具体取决于实现的接口。 每个程序时端口枚举进程的程序时，会创建根据相应[IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md)接口传递的参数作为[AddProgramNode](../../extensibility/debugger/reference/idebugportnotify2-addprogramnode.md)。 尽管的调试引擎还创建`IDebugProgram2`接口来表示程序，这些程序不会创建根据程序节点。 `IDebugProgramNode2`那些通过端口仅用于发现进程中运行哪些程序用于实现实际调试接口创建的部署。  
  
## <a name="see-also"></a>请参阅  
 [进程](../../extensibility/debugger/processes.md)   
 [程序节点](../../extensibility/debugger/program-nodes.md)   
 [模块](../../extensibility/debugger/modules.md)   
 [调试器概念](../../extensibility/debugger/debugger-concepts.md)   
 [调试引擎](../../extensibility/debugger/debug-engine.md)   
 [文档位置](../../extensibility/debugger/document-position.md)   
 [代码上下文](../../extensibility/debugger/code-context.md)   
 [IDebugProgram2](../../extensibility/debugger/reference/idebugprogram2.md)   
 [IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md)   
 [AddProgramNode](../../extensibility/debugger/reference/idebugportnotify2-addprogramnode.md)
