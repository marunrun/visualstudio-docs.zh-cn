---
title: IDebugProcess3 |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80723542"
---
# <a name="idebugprocess3"></a>IDebugProcess3
此接口表示正在运行的进程及其程序。 此接口作为对 [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) 接口中多个方法的替换而存在。 它提供对进程中的所有程序的控制。

> [!NOTE]
> [继续](../../../extensibility/debugger/reference/idebugprogram2-continue.md)、 [执行](../../../extensibility/debugger/reference/idebugprogram2-execute.md)和 [步骤](../../../extensibility/debugger/reference/idebugprogram2-step.md) 方法已弃用，不应再使用。 改为在接口上使用相应的方法 `IDebugProcess3` 。

## <a name="syntax"></a>语法

```
IDebugProcess3 : IDebugProcess2
```

## <a name="notes-for-implementers"></a>实施者注意事项
 此接口由自定义端口提供程序实现，以将程序作为组进行管理。 当程序作为一个组进行管理时，您可以控制其执行并为表达式计算器建立一种语言。 此接口必须由端口提供程序实现。

## <a name="notes-for-callers"></a>调用方说明
 此接口主要由会话调试管理器 (SDM) 调用，以便与在此进程中标识的一组程序进行交互。

 在[IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)接口上调用[QueryInterface](/cpp/atl/queryinterface)以获取此接口。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 除了从 [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)继承的方法之外，还 `IDebugProcess3` 实现以下方法。

|方法|描述|
|------------|-----------------|
|[Continue](../../../extensibility/debugger/reference/idebugprocess3-continue.md)|继续执行或单步执行进程。|
|[执行](../../../extensibility/debugger/reference/idebugprocess3-execute.md)|开始执行进程。|
|[步骤](../../../extensibility/debugger/reference/idebugprocess3-step.md)|单步执行过程中的指令或语句。|
|[GetDebugReason](../../../extensibility/debugger/reference/idebugprocess3-getdebugreason.md)|获取为调试启动进程的原因。|
|[SetHostingProcessLanguage](../../../extensibility/debugger/reference/idebugprocess3-sethostingprocesslanguage.md)|设置托管语言，以便调试引擎可以加载相应的表达式计算器。|
|[GetHostingProcessLanguage](../../../extensibility/debugger/reference/idebugprocess3-gethostingprocesslanguage.md)|检索当前为此进程设置的语言。|
|[DisableENC](../../../extensibility/debugger/reference/idebugprocess3-disableenc.md)|为此进程禁用 (ENC) 的 "编辑并继续"。<br /><br /> 自定义端口供应商不实现此方法 (应始终返回 `E_NOTIMPL`) 。|
|[GetENCAvailableState](../../../extensibility/debugger/reference/idebugprocess3-getencavailablestate.md)|获取此进程的 ENC 状态。<br /><br /> 自定义端口供应商不实现此方法 (应始终返回 `E_NOTIMPL`) 。|
|[GetEngineFilter](../../../extensibility/debugger/reference/idebugprocess3-getenginefilter.md)|检索可用调试引擎的唯一标识符的数组。|

## <a name="requirements"></a>要求
 标头： Msdbg

 命名空间： VisualStudio

 程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>另请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
