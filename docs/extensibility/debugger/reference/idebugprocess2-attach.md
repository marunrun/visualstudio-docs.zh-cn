---
title: IDebugProcess2：：附加 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProcess2::Attach
helpviewer_keywords:
- IDebugProcess2::Attach
ms.assetid: 40d78417-fde2-45c3-96c9-16e06bd9008d
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: fb6ea896285c784021402400597ba168f6ccf716
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80724191"
---
# <a name="idebugprocess2attach"></a>IDebugProcess2::Attach
将会话调试管理器 （SDM） 附加到进程。

## <a name="syntax"></a>语法

```cpp
HRESULT Attach( 
   IDebugEventCallback2* pCallback,
   GUID*                 rgguidSpecificEngines,
   DWORD                 celtSpecificEngines,
   HRESULT*              rghrEngineAttach
);
```

```csharp
int Attach( 
   IDebugEventCallback2 pCallback,
   Guid[]               rgguidSpecificEngines,
   uint                 celtSpecificEngines,
   int[]                rghrEngineAttach
);
```

## <a name="parameters"></a>参数
`pCallback`\
[在]用于调试事件通知的[IDebugEvent 回调2](../../../extensibility/debugger/reference/idebugeventcallback2.md)对象。

`rgguidSpecificEngines`\
[在]用于调试进程中运行的程序的调试引擎 GUID 数组。 此参数可以是空值。 有关详细信息，请参阅备注。

`celtSpecificEngines`\
[在]数组中的`rgguidSpecificEngines`调试引擎数和`rghrEngineAttach`数组的大小。

`rghrEngineAttach`\
[进出]调试引擎返回的 HRESULT 代码数组。 此数组的大小在`celtSpecificEngines`参数中指定。 每个代码通常是 或`S_OK``S_ATTACH_DEFERRED`。 后者表示 DE 当前未附加到任何程序。

## <a name="return-value"></a>返回值
 如果成功，返回`S_OK`;否则，返回错误代码。 下表显示了其他可能的值。

|值|说明|
|-----------|-----------------|
|`E_ATTACH_DEBUGGER_ALREADY_ATTACHED`|指定的进程已附加到调试器。|
|`E_ATTACH_DEBUGGEE_PROCESS_SECURITY_VIOLATION`|在附加过程中发生了安全冲突。|
|`E_ATTACH_CANNOT_ATTACH_TO_DESKTOP`|桌面进程无法附加到调试器。|

## <a name="remarks"></a>备注
 附加到进程将 SDM 附加到该进程中运行的所有程序，这些程序可以由`rgguidSpecificEngines`阵列中指定的调试引擎 （DE） 调试。 将`rgguidSpecificEngines`参数设置为 null 值，或在`GUID_NULL`数组中包括附加到进程中的所有程序。

 进程中发生的所有调试事件都发送到给定的[IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)对象。 当`IDebugEventCallback2`SDM 调用此方法时，将提供此对象。

## <a name="see-also"></a>请参阅
- [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
