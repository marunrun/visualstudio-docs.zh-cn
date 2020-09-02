---
title: IDebugEngine2：： Attach |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngine2::Attach
helpviewer_keywords:
- IDebugEngine2::Attach
ms.assetid: 173dcbda-5019-4c5e-bca9-a071838b5739
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 93890885dbbdfd3cc26984590955681487977200
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80731217"
---
# <a name="idebugengine2attach"></a>IDebugEngine2::Attach
将调试引擎 (DE) 附加到程序或程序。 当 DE 正在进程内运行到 SDM 时，由会话调试管理器调用 (SDM) 。

## <a name="syntax"></a>语法

```cpp
HRESULT Attach( 
   IDebugProgram2**      pProgram,
   IDebugProgramNode2**  rgpProgramNodes,
   DWORD                 celtPrograms,
   IDebugEventCallback2* pCallback,
   ATTACH_REASON         dwReason
);
```

```csharp
int Attach( 
   IDebugProgram2[]     pProgram,
   IDebugProgramNode2[] rgpProgramNodes,
   uint                 celtPrograms,
   IDebugEventCallback2 pCallback,
   Enum_ATTACH_REASON   dwReason
);
```

## <a name="parameters"></a>参数
`pProgram`\
中 [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) 对象的数组，这些对象表示要附加到的程序。 这些是端口程序。

`rgpProgramNodes`\
中 [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md) 对象的数组，这些对象表示程序节点，每个程序各有一个。 此数组中的程序节点表示与中相同的程序 `pProgram` 。 将为程序节点提供，以便 DE 可以标识要附加到的程序。

`celtPrograms`\
中和数组中的程序和/或程序节点 `pProgram` 数 `rgpProgramNodes` 。

`pCallback`\
中要用于向 SDM 发送调试事件的 [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) 对象。

`dwReason`\
中 [ATTACH_REASON](../../../extensibility/debugger/reference/attach-reason.md) 枚举中的一个值，该值指定附加这些程序的原因。 有关详细信息，请参阅“备注”部分。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
 附加到程序有三个原因，如下所示：

- `ATTACH_REASON_LAUNCH` 指示 DE 正在附加到程序，因为用户启动了包含它的进程。

- `ATTACH_REASON_USER` 指示用户已明确请求要附加到程序 (或包含程序) 的进程。

- `ATTACH_REASON_AUTO` 指示 DE 正在附加到特定的程序，因为它已经在特定进程中调试其他程序。 这也称为自动附加。

  调用此方法时，不再需要按顺序发送这些事件：

1. 如果尚未为调试引擎的特定实例发送[IDebugEngineCreateEvent2](../../../extensibility/debugger/reference/idebugenginecreateevent2.md) (，则为) 

2. [IDebugProgramCreateEvent2](../../../extensibility/debugger/reference/idebugprogramcreateevent2.md)

3. [IDebugLoadCompleteEvent2](../../../extensibility/debugger/reference/idebugloadcompleteevent2.md)

   此外，如果附加的原因是，则不再 `ATTACH_REASON_LAUNCH` 需要发送 [IDebugEntryPointEvent2](../../../extensibility/debugger/reference/idebugentrypointevent2.md) 事件。

   一旦取消后，就会获得对应于正在调试的程序的 [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md) 对象，它可以查询任何专用接口。

   在调用或给定的数组中的程序节点的方法之前 `pProgram` `rgpProgramNodes` ，应在表示程序节点的接口上启用模拟（如果需要） `IDebugProgram2` 。 但通常不需要执行此步骤。 有关详细信息，请参阅 [安全问题](../../../extensibility/debugger/security-issues.md)。

## <a name="see-also"></a>另请参阅
- [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)
- [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
- [ATTACH_REASON](../../../extensibility/debugger/reference/attach-reason.md)
- [IDebugEngineCreateEvent2](../../../extensibility/debugger/reference/idebugenginecreateevent2.md)
- [IDebugProgramCreateEvent2](../../../extensibility/debugger/reference/idebugprogramcreateevent2.md)
- [IDebugLoadCompleteEvent2](../../../extensibility/debugger/reference/idebugloadcompleteevent2.md)
- [IDebugEntryPointEvent2](../../../extensibility/debugger/reference/idebugentrypointevent2.md)
