---
title: IDebugProgramEx2：：附加 |微软文档
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
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
[在][IDebugEvent回调2](../../../extensibility/debugger/reference/idebugeventcallback2.md)对象，表示附加的调试引擎向其发送事件的回调函数。

`dwReason`\
[在]描述附加操作原因[ATTACH_REASON](../../../extensibility/debugger/reference/attach-reason.md)枚举中的值。

`pSession`\
[在]唯一标识附加到程序的会话的值。

## <a name="return-value"></a>返回值
 如果成功，返回`S_OK`;否则返回错误代码。 如果程序已附加`E_ATTACH_DEBUGGER_ALREADY_ATTACHED`，此方法应返回。

## <a name="remarks"></a>备注
 包含该程序的端口可以使用 中`pSession`的值来确定尝试附加到该程序的会话。 例如，如果端口一次只允许一个调试会话附加到进程，则端口可以确定同一会话是否已附加到进程中的其他程序。

> [!NOTE]
> 传入的`pSession`接口将仅被视为 Cookie，该值唯一标识附加到此程序的会话调试管理器;提供的接口上没有任何方法正常工作。

## <a name="see-also"></a>请参阅
- [IDebugProgramEx2](../../../extensibility/debugger/reference/idebugprogramex2.md)
