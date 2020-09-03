---
title: IDebugProgramNode2：： Attach_V7 |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80722136"
---
# <a name="idebugprogramnode2attach_v7"></a>IDebugProgramNode2::Attach_V7

> [!Note]
> 弃用. 请勿使用。

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
中表示要附加到的程序的 [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) 接口。

`pCallback`\
中要用于向 SDM 发送调试事件的 [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) 接口。

`dwReason`\
中 [ATTACH_REASON](../../../extensibility/debugger/reference/attach-reason.md) 枚举中的一个值，该值指定附加的原因。

## <a name="return-value"></a>返回值

实现应总是返回 `E_NOTIMPL` 。

## <a name="remarks"></a>备注

> [!WARNING]
> 在 Visual Studio 2005 中，此方法不再使用，应始终返回 `E_NOTIMPL` 。 如果程序节点需要指示它无法连接到，或者如果程序节点只是设置程序，则请参阅 [IDebugProgramNodeAttach2](../../../extensibility/debugger/reference/idebugprogramnodeattach2.md) 接口以获取替代方法 `GUID` 。 否则，实现 [Attach](../../../extensibility/debugger/reference/idebugengine2-attach.md) 方法。

## <a name="prior-to-visual-studio-2005"></a>Visual Studio 2005 之前

仅当在正在调试的程序的地址空间中运行时，才需要实现此方法。 否则，此方法应返回 `S_FALSE` 。

调用此方法时，如果尚未为[IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)接口的此实例发送[IDebugEngineCreateEvent2](../../../extensibility/debugger/reference/idebugenginecreateevent2.md)事件对象，以及[IDebugProgramCreateEvent2](../../../extensibility/debugger/reference/idebugprogramcreateevent2.md)和[IDebugLoadCompleteEvent2](../../../extensibility/debugger/reference/idebugloadcompleteevent2.md)事件对象，则 DE 必须发送该对象。 如果参数为，则发送 [IDebugEntryPointEvent2](../../../extensibility/debugger/reference/idebugentrypointevent2.md) 事件对象 `dwReason` `ATTACH_REASON_LAUNCH` 。

DE 必须对[IDebugProgramCreateEvent2](../../../extensibility/debugger/reference/idebugprogramcreateevent2.md)事件对象提供的[IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)对象调用[GetProgramId](../../../extensibility/debugger/reference/idebugprogram2-getprogramid.md)方法，并且必须在 `IDebugProgram2` 由 DE 实现的对象的实例数据中存储该程序的 GUID。

## <a name="see-also"></a>另请参阅

- [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)
- [IDebugProgramNodeAttach2](../../../extensibility/debugger/reference/idebugprogramnodeattach2.md)
- [附加](../../../extensibility/debugger/reference/idebugengine2-attach.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
- [IDebugEngineCreateEvent2](../../../extensibility/debugger/reference/idebugenginecreateevent2.md)
- [IDebugProgramCreateEvent2](../../../extensibility/debugger/reference/idebugprogramcreateevent2.md)
- [IDebugLoadCompleteEvent2](../../../extensibility/debugger/reference/idebugloadcompleteevent2.md)
- [IDebugEntryPointEvent2](../../../extensibility/debugger/reference/idebugentrypointevent2.md)
- [ATTACH_REASON](../../../extensibility/debugger/reference/attach-reason.md)
