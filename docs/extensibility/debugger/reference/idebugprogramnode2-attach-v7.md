---
title: IDebugProgramNode2：：Attach_V7 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramNode2::Attach
helpviewer_keywords:
- IDebugProgramNode2::Attach_V7
- IDebugProgramNode2::Attach
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: bdee5b224ae38c3474009aeaf26e783ebc5dd139
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80722136"
---
# <a name="idebugprogramnode2attach_v7"></a>IDebugProgramNode2::Attach_V7

> [!Note]
> 废弃。 请勿使用。

## <a name="syntax"></a>语法

```cpp
HRESULT Attach_V7 (
   IDebugProgram2*       pMDMProgram,
   IDebugEventCallback2* pCallback,
   DWORD                 dwReason
);
```

```csharp
int Attach_V7 (
   IDebugProgram2       pMDMProgram,
   IDebugEventCallback2 pCallback,
   uint                 dwReason
);
```

## <a name="parameters"></a>参数

`pMDMProgram`\
[在][IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)接口，表示要附加到的程序。

`pCallback`\
[在]用于将调试事件发送到 SDM 的[IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)接口。

`dwReason`\
[在]ATTACH_REASON[枚举中](../../../extensibility/debugger/reference/attach-reason.md)指定附加原因的值。

## <a name="return-value"></a>返回值

实现应始终返回`E_NOTIMPL`。

## <a name="remarks"></a>备注

> [!WARNING]
> 自 Visual Studio 2005 起，此方法不再使用，应始终返回`E_NOTIMPL`。 如果程序节点需要指示它不能附加到，或者程序节点只是设置程序`GUID`，请参阅[IDebugProgramNodeAttach2](../../../extensibility/debugger/reference/idebugprogramnodeattach2.md)接口，了解替代方法。 否则，实现[附加](../../../extensibility/debugger/reference/idebugengine2-attach.md)方法。

## <a name="prior-to-visual-studio-2005"></a>2005年之前的视觉工作室

仅当 DE 在正在调试的程序的地址空间中运行时，才需要实现此方法。 否则，此方法应返回`S_FALSE`。

调用此方法时，如果尚未为[IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)接口的此实例发送[IDebugEngineCreateEvent2](../../../extensibility/debugger/reference/idebugenginecreateevent2.md)事件对象，以及[IDebugProgramCreateEvent2](../../../extensibility/debugger/reference/idebugprogramcreateevent2.md)和[IDebugLoadCompleteEvent2](../../../extensibility/debugger/reference/idebugloadcompleteevent2.md)事件对象，则 DE 必须发送 IDebugEngineCreateEvent2 事件对象。 如果`dwReason`参数为`ATTACH_REASON_LAUNCH`，则发送[IDebugentryPointEvent2](../../../extensibility/debugger/reference/idebugentrypointevent2.md)事件对象。

DE`IDebugProgram2`必须在[IDebugProgramCreateEvent2](../../../extensibility/debugger/reference/idebugprogramcreateevent2.md)事件对象提供的[IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)对象上调用[GetProgramId](../../../extensibility/debugger/reference/idebugprogram2-getprogramid.md)方法，并且必须将该程序的 GUID 存储在 DE 实现的对象的实例数据中。

## <a name="see-also"></a>请参阅

- [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)
- [IDebugProgramNodeAttach2](../../../extensibility/debugger/reference/idebugprogramnodeattach2.md)
- [Attach](../../../extensibility/debugger/reference/idebugengine2-attach.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
- [IDebugEngineCreateEvent2](../../../extensibility/debugger/reference/idebugenginecreateevent2.md)
- [IDebugProgramCreateEvent2](../../../extensibility/debugger/reference/idebugprogramcreateevent2.md)
- [IDebugLoadCompleteEvent2](../../../extensibility/debugger/reference/idebugloadcompleteevent2.md)
- [IDebugEntryPointEvent2](../../../extensibility/debugger/reference/idebugentrypointevent2.md)
- [ATTACH_REASON](../../../extensibility/debugger/reference/attach-reason.md)
