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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68153641"
---
# <a name="programs"></a>计划
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

就调试器体系结构而言， **程序**是：  
  
- 是一组线程和一组模块的容器。 在 Windows 操作系统中，程序没有任何一个类比。  
  
     程序是一种子进程。 例如，在调试网站时，可以将脚本视为程序。 尽管脚本在脚本引擎进程中运行（与其他脚本无关），但它还具有自己的一组线程。 调试引擎 (DE) 附加到程序，而不是进程或线程。  
  
- 可以标识自身及其正在其上运行的进程，并可以将其附加到，也可以将其与创建（如果有）。 程序可以执行、停止、继续和终止。  
  
- 可以枚举其所有线程。 程序还可以提供自己的反汇编流，还可以枚举给定文档位置的所有代码上下文。  
  
- 由在附加程序之前创建的 [IDebugProgram2](../../extensibility/debugger/reference/idebugprogram2.md) 接口表示，或作为附加过程的一部分，具体取决于实现。 当端口枚举进程的程序时，将根据作为参数传递到[AddProgramNode](../../extensibility/debugger/reference/idebugportnotify2-addprogramnode.md)的相应[IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md)接口创建每个程序。 尽管调试引擎还 `IDebugProgram2` 会创建接口来表示程序，但不会根据程序节点创建这些程序。 `IDebugProgramNode2`由 DE 创建的接口用于实际调试，而由端口创建的接口仅用于发现进程中运行的程序。  
  
## <a name="see-also"></a>另请参阅  
 [工艺](../../extensibility/debugger/processes.md)   
 [程序节点](../../extensibility/debugger/program-nodes.md)   
 [模块](../../extensibility/debugger/modules.md)   
 [调试器概念](../../extensibility/debugger/debugger-concepts.md)   
 [调试引擎](../../extensibility/debugger/debug-engine.md)   
 [文档位置](../../extensibility/debugger/document-position.md)   
 [代码上下文](../../extensibility/debugger/code-context.md)   
 [IDebugProgram2](../../extensibility/debugger/reference/idebugprogram2.md)   
 [IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md)   
 [AddProgramNode](../../extensibility/debugger/reference/idebugportnotify2-addprogramnode.md)
