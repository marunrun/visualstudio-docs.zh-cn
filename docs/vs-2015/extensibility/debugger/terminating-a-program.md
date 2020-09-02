---
title: 终止程序 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- programs, termination events
- debugging [Debugging SDK], terminating a program
ms.assetid: eedda0a3-5e05-44fe-841d-a2f4866ac72d
caps.latest.revision: 8
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: f0b9ad248751af0885fa4edc0275be2ede5ddd9f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "62421858"
---
# <a name="terminating-a-program"></a>终止程序
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

下面说明了单个程序的终止，其中包含一个线程。  
  
## <a name="termination-process"></a>终止进程  
  
1. DE 发送具有有效[IDebugThread2](../../extensibility/debugger/reference/idebugthread2.md)的[IDebugThreadDestroyEvent2](../../extensibility/debugger/reference/idebugthreaddestroyevent2.md) 。  
  
2. DE 发送具有有效[IDebugProgram2](../../extensibility/debugger/reference/idebugprogram2.md)的[IDebugProgramDestroyEvent2](../../extensibility/debugger/reference/idebugprogramdestroyevent2.md) 。  
  
   IDE 进入设计模式。 调试引擎或运行时环境调用 [IDebugPortNotify2：： RemoveProgramNode](../../extensibility/debugger/reference/idebugportnotify2-removeprogramnode.md) 从端口中删除程序。  
  
## <a name="see-also"></a>另请参阅  
 [调用调试器事件](../../extensibility/debugger/calling-debugger-events.md)
