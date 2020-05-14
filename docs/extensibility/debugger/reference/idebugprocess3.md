---
title: IDebugProcess3 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProcess3
helpviewer_keywords:
- IDebugProcess3 interface
ms.assetid: 7bd6b952-cf34-4e66-b8f6-d472dac3748f
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: b423ee2cb95ad55296c452cfdc4b891ee4cd26a0
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80723542"
---
# <a name="idebugprocess3"></a>IDebugProcess3
此接口表示正在运行的进程及其程序。 此接口作为[IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)接口中多种方法的替换而存在。 它提供对流程中所有程序的控制。

> [!NOTE]
> [将弃用"继续](../../../extensibility/debugger/reference/idebugprogram2-continue.md)["、执行](../../../extensibility/debugger/reference/idebugprogram2-execute.md)和[步骤](../../../extensibility/debugger/reference/idebugprogram2-step.md)方法，不应再使用。 而是在`IDebugProcess3`接口上使用相应的方法。

## <a name="syntax"></a>语法

```
IDebugProcess3 : IDebugProcess2
```

## <a name="notes-for-implementers"></a>实施者说明
 此接口由自定义端口供应商实现，以作为一个组管理程序。 当程序作为一个组进行管理时，您可以控制其执行并为表达式赋值器建立语言。 此接口必须由端口供应商实现。

## <a name="notes-for-callers"></a>呼叫者备注
 此接口主要由会话调试管理器 （SDM） 调用，以便与在此过程中标识的一组程序进行交互。

 在[IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)接口上调用[查询接口](/cpp/atl/queryinterface)以获取此接口。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 除了从[IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)继承的方法外，`IDebugProcess3`还实现了以下方法。

|方法|描述|
|------------|-----------------|
|[继续](../../../extensibility/debugger/reference/idebugprocess3-continue.md)|继续执行或逐步执行流程。|
|[执行](../../../extensibility/debugger/reference/idebugprocess3-execute.md)|开始执行进程。|
|[步骤](../../../extensibility/debugger/reference/idebugprocess3-step.md)|在此过程中向前走一条指令或语句。|
|[GetDebugReason](../../../extensibility/debugger/reference/idebugprocess3-getdebugreason.md)|获取进程启动以进行调试的原因。|
|[SetHostingProcessLanguage](../../../extensibility/debugger/reference/idebugprocess3-sethostingprocesslanguage.md)|设置托管语言，以便调试引擎可以加载相应的表达式赋值器。|
|[GetHostingProcessLanguage](../../../extensibility/debugger/reference/idebugprocess3-gethostingprocesslanguage.md)|检索当前为此过程设置的语言。|
|[DisableENC](../../../extensibility/debugger/reference/idebugprocess3-disableenc.md)|禁用此过程的编辑并继续 （ENC）。<br /><br /> 自定义端口供应商不实现此方法（应始终返回`E_NOTIMPL`）。|
|[GetENCAvailableState](../../../extensibility/debugger/reference/idebugprocess3-getencavailablestate.md)|获取此过程的 ENC 状态。<br /><br /> 自定义端口供应商不实现此方法（应始终返回`E_NOTIMPL`）。|
|[GetEngineFilter](../../../extensibility/debugger/reference/idebugprocess3-getenginefilter.md)|检索可用调试引擎的唯一标识符数组。|

## <a name="requirements"></a>要求
 标题： Msdbg.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
