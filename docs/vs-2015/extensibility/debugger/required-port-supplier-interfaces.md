---
title: 必需的端口提供商接口 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- port suppliers, required interfaces
- debugging [Debugging SDK], port suppliers
ms.assetid: 0c2cdd40-9f6f-425e-b305-858f7734161e
caps.latest.revision: 14
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: a065389a6b9b67b8bce82394569ce65afb0f8d55
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "67821435"
---
# <a name="required-port-supplier-interfaces"></a>所需的端口提供程序接口
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

端口供应商必须实现 [IDebugPortSupplier2](../../extensibility/debugger/reference/idebugportsupplier2.md) 接口。[IDebugPortSupplier2](../../extensibility/debugger/reference/idebugportsupplier2.md)  
  
 由于端口供应商提供端口，因此还必须实现它们。 因此，它必须实现以下接口：  
  
- [IDebugPort2](../../extensibility/debugger/reference/idebugport2.md)  
  
     描述端口，并可以枚举在该端口上运行的所有进程。  
  
- [IDebugPortEx2](../../extensibility/debugger/reference/idebugportex2.md)  
  
     提供用于在端口上启动和终止进程的。  
  
- [IDebugPortNotify2](../../extensibility/debugger/reference/idebugportnotify2.md)  
  
     为在此端口的上下文中运行的程序提供一种机制，以便在程序节点创建和销毁时向其发送通知。 有关详细信息，请参阅 [Program 节点](../../extensibility/debugger/program-nodes.md)。  
  
- `IConnectionPointContainer`  
  
     为 [IDebugPortEvents2](../../extensibility/debugger/reference/idebugportevents2.md)提供连接点。  
  
## <a name="port-supplier-operation"></a>端口供应商操作  
 在端口上创建并销毁进程和程序时， [IDebugPortEvents2](../../extensibility/debugger/reference/idebugportevents2.md) 接收器会接收通知。 创建进程时，需要使用端口发送 [IDebugProcessCreateEvent2](../../extensibility/debugger/reference/idebugprocesscreateevent2.md) ，并在端口上销毁进程时发送 [IDebugProcessDestroyEvent2](../../extensibility/debugger/reference/idebugprocessdestroyevent2.md) 。 创建程序时，还需要使用端口来发送 [IDebugProgramCreateEvent2](../../extensibility/debugger/reference/idebugprogramcreateevent2.md) ，并在端口上运行的进程中销毁程序时进行 [IDebugProgramDestroyEvent2](../../extensibility/debugger/reference/idebugprogramdestroyevent2.md) 。  
  
 端口通常会分别发送程序创建和销毁事件以响应 [AddProgramNode](../../extensibility/debugger/reference/idebugportnotify2-addprogramnode.md) 和 [RemoveProgramNode](../../extensibility/debugger/reference/idebugportnotify2-removeprogramnode.md) 方法。  
  
 由于端口可以启动和终止物理进程和逻辑程序，因此这些接口还必须由调试引擎实现：  
  
- [IDebugProcess2](../../extensibility/debugger/reference/idebugprocess2.md)  
  
  描述物理进程。 至少必须实现以下方法：  

  - [EnumPrograms](../../extensibility/debugger/reference/idebugprocess2-enumprograms.md)  

  - [GetName](../../extensibility/debugger/reference/idebugprocess2-getname.md)  

  - [GetServer](../../extensibility/debugger/reference/idebugprocess2-getserver.md)  

  - [GetPhysicalProcessId](../../extensibility/debugger/reference/idebugprocess2-getphysicalprocessid.md)  

  - [GetProcessId](../../extensibility/debugger/reference/idebugprocess2-getprocessid.md)  

  - [GetAttachedSessionName](../../extensibility/debugger/reference/idebugprocess2-getattachedsessionname.md)  

- [IDebugProcessEx2](../../extensibility/debugger/reference/idebugprocessex2.md)  
  
    为 SDM 提供一种附加和分离进程的方法。  
  
- [IDebugProgram2](../../extensibility/debugger/reference/idebugprogram2.md)  
  
  介绍逻辑程序。 至少必须实现以下方法：  

  - [GetName](../../extensibility/debugger/reference/idebugprogram2-getname.md)  

  - [GetProcess](../../extensibility/debugger/reference/idebugprogram2-getprocess.md)  

  - [GetProgramId](../../extensibility/debugger/reference/idebugprogram2-getprogramid.md)  
  
- [IDebugProgramEx2](../../extensibility/debugger/reference/idebugprogramex2.md)  
  
     为 SDM 附加到此程序提供了一种方法。  
  
## <a name="see-also"></a>另请参阅  
 [实现端口提供程序](../../extensibility/debugger/implementing-a-port-supplier.md)
