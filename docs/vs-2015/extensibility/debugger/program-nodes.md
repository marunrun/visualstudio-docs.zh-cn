---
title: 程序节点 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- program nodes, debugging context
- debugging [Debugging SDK], program nodes
- program nodes, adding
- program nodes, superceding
ms.assetid: 1c5a5c13-c14d-42c3-af11-4c63f1032c8d
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 3a06be4ef0a69ec173f171ba202f1f479448b1ca
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68153650"
---
# <a name="program-nodes"></a>程序节点
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

就调试器体系结构而言， **程序节点**：  
  
- 是对程序的轻型说明。  
  
- 可以标识自身及其在其中运行的进程，并可以将其附加到，也可以将其与创建的调试引擎 (DE) （如果有）。  
  
- 由 [IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md) 接口表示，通常由 DE 或端口创建。 通过调用 [AddProgramNode](../../extensibility/debugger/reference/idebugportnotify2-addprogramnode.md)将程序节点添加到端口。 将程序节点添加到端口后，会将该节点添加到包含此程序节点所表示的程序的进程中。  
  
  在调试会话启动之后的某个时间段，根据调试包的实现，程序节点用于创建相应的程序。 查询进程时，会枚举程序，每个程序节点各有一个。  
  
  将程序附加到之前，IDE 只需要程序的轻型说明。 可以从程序节点获取此信息。 将程序附加到后，IDE 需要显示更多详细信息，如程序中运行的所有线程的列表。 此信息是从程序本身获取的。  
  
## <a name="see-also"></a>另请参阅  
 [程序](../../extensibility/debugger/programs.md)   
 [工艺](../../extensibility/debugger/processes.md)   
 [调试引擎](../../extensibility/debugger/debug-engine.md)   
 [调试器概念](../../extensibility/debugger/debugger-concepts.md)   
 [IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md)   
 [AddProgramNode](../../extensibility/debugger/reference/idebugportnotify2-addprogramnode.md)
