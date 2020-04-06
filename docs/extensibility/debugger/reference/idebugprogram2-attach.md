---
title: IDebugProgram2：：附加 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgram2::Attach
helpviewer_keywords:
- IDebugProgram2::Attach
ms.assetid: de069fbf-a565-4905-b102-f5658c55aacd
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 7d0b182ba7a873816e3a7aa32d39beb2c63cc5ce
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80723134"
---
# <a name="idebugprogram2attach"></a>IDebugProgram2::Attach
附加到程序。

## <a name="syntax"></a>语法

```cpp
HRESULT Attach( 
   IDebugEventCallback2* pCallback
);
```

```csharp
int Attach( 
   IDebugEventCallback2 pCallback
);
```

## <a name="parameters"></a>参数
`pCallback`\
[在]用于调试事件通知的[IDebugEvent 回调2](../../../extensibility/debugger/reference/idebugeventcallback2.md)对象。

## <a name="return-value"></a>返回值
 如果成功，返回`S_OK`;否则，返回错误代码。 下表显示了一些可能的错误代码。

|值|说明|
|-----------|-----------------|
|`E_ATTACH_DEBUGGER_ALREADY_ATTACHED`|指定的程序已附加到调试器。|
|`E_ATTACH_DEBUGGEE_PROCESS_SECURITY_VIOLATION`|在附加过程中发生了安全冲突。|
|`E_ATTACH_CANNOT_ATTACH_TO_DESKTOP`|桌面程序无法附加到调试器。|

## <a name="remarks"></a>备注
 调试引擎 （DE） 从不调用此方法附加到程序。 如果 DE 在程序的地址空间中运行，则调用[OnAttach](../../../extensibility/debugger/reference/idebugprogramnodeattach2-onattach.md)方法。 如果 DE 在会话调试管理器 （SDM） 地址空间中运行，则调用[附加](../../../extensibility/debugger/reference/idebugengine2-attach.md)方法。

## <a name="see-also"></a>请参阅
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
- [OnAttach](../../../extensibility/debugger/reference/idebugprogramnodeattach2-onattach.md)
- [Attach](../../../extensibility/debugger/reference/idebugengine2-attach.md)
