---
title: IDebugProgramEx2：： Attach |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramEx2::Attach
helpviewer_keywords:
- IDebugProgramEx2::Attach
ms.assetid: 33b22b2f-431e-4205-9441-d28a9c928c97
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: fcb52a96074b783043af1e908cf454466df74c30
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80722388"
---
# <a name="idebugprogramex2attach"></a>IDebugProgramEx2::Attach
将会话附加到程序。

## <a name="syntax"></a>语法

```cpp
HRESULT Attach( 
   IDebugEventCallback2* pCallback,
   DWORD                 dwReason,
   IDebugSession2*       pSession
);
```

```csharp
int Attach( 
   IDebugEventCallback2 pCallback,
   uint                 dwReason,
   IDebugSession2       pSession
);
```

## <a name="parameters"></a>参数
`pCallback`\
中一个 [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) 对象，该对象表示附加的调试引擎将事件发送到的回调函数。

`dwReason`\
中 [ATTACH_REASON](../../../extensibility/debugger/reference/attach-reason.md) 枚举中的一个值，该值描述附加操作的原因。

`pSession`\
中一个值，该值唯一标识附加到程序的会话。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。 如果已附加该程序，则此方法应返回 `E_ATTACH_DEBUGGER_ALREADY_ATTACHED` 。

## <a name="remarks"></a>备注
 包含程序的端口可以使用中的值 `pSession` 来确定尝试将哪个会话附加到该程序。 例如，如果一个端口一次只允许一个调试会话附加到一个进程，则该端口可以确定是否已将同一会话附加到进程中的其他程序。

> [!NOTE]
> 传入的接口将 `pSession` 仅被视为 cookie，这是唯一标识会话调试管理器附加到此程序的值; 提供的接口上的任何方法都不起作用。

## <a name="see-also"></a>另请参阅
- [IDebugProgramEx2](../../../extensibility/debugger/reference/idebugprogramex2.md)
