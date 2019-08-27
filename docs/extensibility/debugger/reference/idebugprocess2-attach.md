---
title: IDebugProcess2::Attach | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProcess2::Attach
helpviewer_keywords:
- IDebugProcess2::Attach
ms.assetid: 40d78417-fde2-45c3-96c9-16e06bd9008d
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 24a83c13d8953e3725a5fc5a4e55153b9ade88c4
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66353252"
---
# <a name="idebugprocess2attach"></a>IDebugProcess2::Attach
将会话调试管理器 (SDM) 附加到进程。

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
[in][IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)用于调试事件通知的对象。

`rgguidSpecificEngines`\
[in]Guid 的数组的调试引擎以用于调试的进程中运行的程序。 此参数可以为 null 值。 有关详细信息，请参阅备注。

`celtSpecificEngines`\
[in]引擎中，调试数`rgguidSpecificEngines`数组和大小`rghrEngineAttach`数组。

`rghrEngineAttach`\
[in、 out]HRESULT 代码的调试引擎返回的数组。 此数组的大小指定为`celtSpecificEngines`参数。 每个代码通常是`S_OK`或`S_ATTACH_DEFERRED`。 后者表示 DE 当前附加到任何程序。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。 下表显示了其他可能的值。

|值|描述|
|-----------|-----------------|
|`E_ATTACH_DEBUGGER_ALREADY_ATTACHED`|指定的进程已附加到调试器。|
|`E_ATTACH_DEBUGGEE_PROCESS_SECURITY_VIOLATION`|在附加过程中发生了安全冲突。|
|`E_ATTACH_CANNOT_ATTACH_TO_DESKTOP`|桌面的过程不能附加到调试器。|

## <a name="remarks"></a>备注
 附加到进程将 SDM 附加到可调试的调试引擎 (DE) 中指定该进程中运行的所有程序`rgguidSpecificEngines`数组。 设置`rgguidSpecificEngines`参数为 null 值或包含`GUID_NULL`数组中要将附加到进程中的所有程序。

 在过程中发生的所有调试事件都发送到给定[IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)对象。 这`IDebugEventCallback2`SDM 调用此方法时提供对象。

## <a name="see-also"></a>请参阅
- [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)