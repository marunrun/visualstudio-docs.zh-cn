---
title: IDebugPort事件2：：事件 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPortEvents2::Event
helpviewer_keywords:
- IDebugPortEvents2::Event
ms.assetid: 5cc813f7-04a1-4462-9ea7-fbddcf0e0143
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 931be468f6321250481aec79688f7f326abcfcac
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80725249"
---
# <a name="idebugportevents2event"></a>IDebugPortEvents2::Event
此方法发送表示在端口上创建和销毁进程和程序的事件。

## <a name="syntax"></a>语法

```cpp
HRESULT Event(
   IDebugCoreServer2* pServer,
   IDebugPort2*       pPort,
   IDebugProcess2*    pProcess,
   IDebugProgram2*    pProgram,
   IDebugEvent2*      pEvent,
   REFIID             riidEvent
);
```

```csharp
int Event(
   IDebugCoreServer2 pServer,
   IDebugPort2       pPort,
   IDebugProcess2    pProcess,
   IDebugProgram2    pProgram,
   IDebugEvent2      pEvent,
   ref Guid          riidEvent
);
```

## <a name="parameters"></a>参数
`pMachine`\
[在][IDebugCoreServer2](../../../extensibility/debugger/reference/idebugcoreserver2.md)对象，表示发生该事件的每个实例都有一个[!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)]调试服务器。

`pPort`\
[在]表示事件发生的端口的[IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)对象。

`pProcess`\
[在][IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)对象，表示事件发生的进程。

`pProgram`\
[在][IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)对象，表示事件发生的程序。

`pEvent`\
[在]标识事件的[IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)对象。 可能的事件如下：

- [IDebugProcessCreateEvent2](../../../extensibility/debugger/reference/idebugprocesscreateevent2.md)

- [IDebugProcessDestroyEvent2](../../../extensibility/debugger/reference/idebugprocessdestroyevent2.md)

- [IDebugProgramCreateEvent2](../../../extensibility/debugger/reference/idebugprogramcreateevent2.md)

- [IDebugProgramDestroyEvent2](../../../extensibility/debugger/reference/idebugprogramdestroyevent2.md)

`riidEvent`\
[在]事件的 GUID。 由于在调用此方法之前将事件强制转换为[IDebugEvent2，](../../../extensibility/debugger/reference/idebugevent2.md)因此此标识符可以更轻松地确定正在发送的事件。

## <a name="return-value"></a>返回值
 如果成功，返回`S_OK`;否则，返回错误代码。

## <a name="see-also"></a>请参阅
- [IDebugPortEvents2](../../../extensibility/debugger/reference/idebugportevents2.md)
- [IDebugCoreServer2](../../../extensibility/debugger/reference/idebugcoreserver2.md)
- [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)
- [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
