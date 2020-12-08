---
title: 必需的端口提供商接口 |Microsoft Docs
description: 了解端口提供程序必须运行的接口。 端口供应商提供端口并实现它们。
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: 13e3ac8dc0c229f0c0a00bd22131251c71893224
ms.sourcegitcommit: ce85cff795df29e2bd773b4346cd718dccda5337
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/08/2020
ms.locfileid: "96847125"
---
# <a name="required-port-supplier-interfaces"></a>必需的端口提供商接口
端口供应商必须实现 [IDebugPortSupplier2](../../extensibility/debugger/reference/idebugportsupplier2.md) 接口。[IDebugPortSupplier2](../../extensibility/debugger/reference/idebugportsupplier2.md)

 端口供应商提供端口并实现它们。 因此，它必须运行以下接口：

- [IDebugPort2](../../extensibility/debugger/reference/idebugport2.md)

  描述端口并枚举端口上运行的所有进程。

- [IDebugPortEx2](../../extensibility/debugger/reference/idebugportex2.md)

  提供用于在端口上启动和终止进程的。

- [IDebugPortNotify2](../../extensibility/debugger/reference/idebugportnotify2.md)

  为在此端口的上下文中运行的程序提供一种机制，以便在程序节点创建和销毁时向其发送通知。 有关详细信息，请参阅 [Program 节点](../../extensibility/debugger/program-nodes.md)。

- `IConnectionPointContainer`

  为 [IDebugPortEvents2](../../extensibility/debugger/reference/idebugportevents2.md)提供连接点。

## <a name="port-supplier-operation"></a>端口供应商操作
 在端口上创建并销毁进程和程序时， [IDebugPortEvents2](../../extensibility/debugger/reference/idebugportevents2.md) 接收器会接收通知。 创建进程时，需要使用端口发送 [IDebugProcessCreateEvent2](../../extensibility/debugger/reference/idebugprocesscreateevent2.md) ，并在端口上销毁进程时发送 [IDebugProcessDestroyEvent2](../../extensibility/debugger/reference/idebugprocessdestroyevent2.md) 。 创建程序时，还需要使用端口来发送 [IDebugProgramCreateEvent2](../../extensibility/debugger/reference/idebugprogramcreateevent2.md) ，并在端口上运行的进程中销毁程序时进行 [IDebugProgramDestroyEvent2](../../extensibility/debugger/reference/idebugprogramdestroyevent2.md) 。

 端口通常会分别发送程序创建和销毁事件以响应 [AddProgramNode](../../extensibility/debugger/reference/idebugportnotify2-addprogramnode.md) 和 [RemoveProgramNode](../../extensibility/debugger/reference/idebugportnotify2-removeprogramnode.md) 方法。

 由于端口可以启动和终止物理进程和逻辑程序，因此调试引擎还必须实现以下接口：

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

## <a name="see-also"></a>请参阅
- [实现端口供应商](../../extensibility/debugger/implementing-a-port-supplier.md)
