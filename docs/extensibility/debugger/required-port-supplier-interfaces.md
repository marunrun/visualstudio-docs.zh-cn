---
title: 所需的端口供应商接口 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- port suppliers, required interfaces
- debugging [Debugging SDK], port suppliers
ms.assetid: 0c2cdd40-9f6f-425e-b305-858f7734161e
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: bf2aeb1f26f81d773e171aa3fed6b0f2ef976c91
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80713155"
---
# <a name="required-port-supplier-interfaces"></a>所需的端口供应商接口
端口供应商必须实现[IDebugPort 供应商2](../../extensibility/debugger/reference/idebugportsupplier2.md)接口。[IDebugPort供应商2](../../extensibility/debugger/reference/idebugportsupplier2.md)

 端口供应商提供端口并实现它们。 因此，它必须运行以下接口：

- [IDebugPort2](../../extensibility/debugger/reference/idebugport2.md)

  描述端口并枚举在端口上运行的所有进程。

- [IDebugPortEx2](../../extensibility/debugger/reference/idebugportex2.md)

  提供在端口上启动和终止进程。

- [IDebugPortNotify2](../../extensibility/debugger/reference/idebugportnotify2.md)

  为在此端口上下文中运行的程序提供一种机制，以通知其程序节点的创建和销毁。 有关详细信息，请参阅[程序节点](../../extensibility/debugger/program-nodes.md)。

- `IConnectionPointContainer`

  为[IDebugPortEvents2](../../extensibility/debugger/reference/idebugportevents2.md)提供连接点。

## <a name="port-supplier-operation"></a>港口供应商运营
 在端口上创建和销毁进程和程序时[，IDebugPortEvents2](../../extensibility/debugger/reference/idebugportevents2.md)接收器会接收通知。 创建进程时需要端口发送[IDebugProcessCreateEvent2;](../../extensibility/debugger/reference/idebugprocesscreateevent2.md)在端口上销毁进程时，需要[IDebugProcessCreateEvent2。](../../extensibility/debugger/reference/idebugprocessdestroyevent2.md) 创建程序时，还需要端口发送[IDebugProgramCreateEvent2;](../../extensibility/debugger/reference/idebugprogramcreateevent2.md)在端口上运行的进程中销毁程序时，需要[发送 IDebugProgramCreateEvent2。](../../extensibility/debugger/reference/idebugprogramdestroyevent2.md)

 端口通常分别发送程序创建和销毁事件以响应[AddProgramNode](../../extensibility/debugger/reference/idebugportnotify2-addprogramnode.md)和[RemoveProgramNode](../../extensibility/debugger/reference/idebugportnotify2-removeprogramnode.md)方法。

 由于端口可以启动和终止物理进程和逻辑程序，因此调试引擎还必须实现以下接口：

- [IDebugProcess2](../../extensibility/debugger/reference/idebugprocess2.md)

  描述物理过程。 至少必须实现以下方法：

  - [EnumPrograms](../../extensibility/debugger/reference/idebugprocess2-enumprograms.md)

  - [GetName](../../extensibility/debugger/reference/idebugprocess2-getname.md)

  - [GetServer](../../extensibility/debugger/reference/idebugprocess2-getserver.md)

  - [GetPhysicalProcessId](../../extensibility/debugger/reference/idebugprocess2-getphysicalprocessid.md)

  - [获取进程 Id](../../extensibility/debugger/reference/idebugprocess2-getprocessid.md)

  - [GetAttachedSessionName](../../extensibility/debugger/reference/idebugprocess2-getattachedsessionname.md)

- [IDebugProcessEx2](../../extensibility/debugger/reference/idebugprocessex2.md)

  为 SDM 提供一种从进程中附加和分离自身的方法。

- [IDebugProgram2](../../extensibility/debugger/reference/idebugprogram2.md)

  描述逻辑程序。 至少必须实现以下方法：

  - [GetName](../../extensibility/debugger/reference/idebugprogram2-getname.md)

  - [获取过程](../../extensibility/debugger/reference/idebugprogram2-getprocess.md)

  - [GetProgramId](../../extensibility/debugger/reference/idebugprogram2-getprogramid.md)

- [IDebugProgramEx2](../../extensibility/debugger/reference/idebugprogramex2.md)

  为 SDM 提供了一种附加到此程序的方法。

## <a name="see-also"></a>请参阅
- [实施端口供应商](../../extensibility/debugger/implementing-a-port-supplier.md)
