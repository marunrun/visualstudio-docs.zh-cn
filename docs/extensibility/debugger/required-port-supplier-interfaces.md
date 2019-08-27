---
title: 所需端口提供程序接口 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- port suppliers, required interfaces
- debugging [Debugging SDK], port suppliers
ms.assetid: 0c2cdd40-9f6f-425e-b305-858f7734161e
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: dfc7b25a54bd17ecf759a25d603997380076c5d1
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2019
ms.locfileid: "67823414"
---
# <a name="required-port-supplier-interfaces"></a>所需的端口提供程序接口
端口提供程序必须实现[IDebugPortSupplier2](../../extensibility/debugger/reference/idebugportsupplier2.md)接口。[IDebugPortSupplier2](../../extensibility/debugger/reference/idebugportsupplier2.md)

 端口供应商提供的端口，并实现它们。 因此，它必须运行以下接口：

- [IDebugPort2](../../extensibility/debugger/reference/idebugport2.md)

  描述该端口，并枚举在端口上运行的所有进程。

- [IDebugPortEx2](../../extensibility/debugger/reference/idebugportex2.md)

  提供用于启动和终止进程的端口上。

- [IDebugPortNotify2](../../extensibility/debugger/reference/idebugportnotify2.md)

  提供了一种机制，通知程序节点创建和析构的此端口的上下文中运行的程序。 有关详细信息，请参阅[程序节点](../../extensibility/debugger/program-nodes.md)。

- `IConnectionPointContainer`

  提供的连接点[IDebugPortEvents2](../../extensibility/debugger/reference/idebugportevents2.md)。

## <a name="port-supplier-operation"></a>端口供应商操作
 [IDebugPortEvents2](../../extensibility/debugger/reference/idebugportevents2.md)接收器时接收通知过程和程序创建和销毁上一个端口。 发送所需的端口[IDebugProcessCreateEvent2](../../extensibility/debugger/reference/idebugprocesscreateevent2.md)时创建一个进程并[IDebugProcessDestroyEvent2](../../extensibility/debugger/reference/idebugprocessdestroyevent2.md)端口上一个进程被销毁时。 一个端口也需要发送[IDebugProgramCreateEvent2](../../extensibility/debugger/reference/idebugprogramcreateevent2.md)程序创建时和[IDebugProgramDestroyEvent2](../../extensibility/debugger/reference/idebugprogramdestroyevent2.md)程序中的端口上运行的进程被销毁时。

 端口通常发送程序创建和销毁事件以响应[AddProgramNode](../../extensibility/debugger/reference/idebugportnotify2-addprogramnode.md)并[RemoveProgramNode](../../extensibility/debugger/reference/idebugportnotify2-removeprogramnode.md)方法，分别。

 因为一个端口可以启动和终止进程的物理和逻辑的程序，还必须调试引擎中实现以下接口：

- [IDebugProcess2](../../extensibility/debugger/reference/idebugprocess2.md)

  介绍了物理过程。 至少必须实现以下方法：

  - [EnumPrograms](../../extensibility/debugger/reference/idebugprocess2-enumprograms.md)

  - [GetName](../../extensibility/debugger/reference/idebugprocess2-getname.md)

  - [GetServer](../../extensibility/debugger/reference/idebugprocess2-getserver.md)

  - [GetPhysicalProcessId](../../extensibility/debugger/reference/idebugprocess2-getphysicalprocessid.md)

  - [GetProcessId](../../extensibility/debugger/reference/idebugprocess2-getprocessid.md)

  - [GetAttachedSessionName](../../extensibility/debugger/reference/idebugprocess2-getattachedsessionname.md)

- [IDebugProcessEx2](../../extensibility/debugger/reference/idebugprocessex2.md)

  提供有关 SDM，附加和分离本身从进程的方法。

- [IDebugProgram2](../../extensibility/debugger/reference/idebugprogram2.md)

  描述逻辑的程序。 至少必须实现以下方法：

  - [GetName](../../extensibility/debugger/reference/idebugprogram2-getname.md)

  - [GetProcess](../../extensibility/debugger/reference/idebugprogram2-getprocess.md)

  - [GetProgramId](../../extensibility/debugger/reference/idebugprogram2-getprogramid.md)

- [IDebugProgramEx2](../../extensibility/debugger/reference/idebugprogramex2.md)

  提供有关 SDM，附加到此程序的方法。

## <a name="see-also"></a>请参阅
- [实现端口提供程序](../../extensibility/debugger/implementing-a-port-supplier.md)
