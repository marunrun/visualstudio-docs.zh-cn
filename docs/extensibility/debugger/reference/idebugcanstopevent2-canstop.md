---
title: IDebugCanStopEvent2::CanStop |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCanStopEvent2::CanStop
helpviewer_keywords:
- IDebugCanStopEvent2::CanStop
ms.assetid: 7d61adbe-6b3d-41f3-86a1-45d9cc01a7f8
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: ab59cf5d077c4e397373c4c86b864ed17749fc19
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66351254"
---
# <a name="idebugcanstopevent2canstop"></a>IDebugCanStopEvent2::CanStop
通知在当前代码位置停止，或只需继续执行调试引擎 (DE)。

## <a name="syntax"></a>语法

```cpp
HRESULT CanStop ( 
   BOOL fCanStop
);
```

```csharp
int CanStop ( 
   int fCanStop
);
```

## <a name="parameters"></a>参数
`fCanStop`\
[in]非零 (`TRUE`) 如果 DE 应停止在当前代码位置; 否则为零 (`FALSE`)。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="remarks"></a>备注
 此事件的接收方通常会调用[GetReason](../../../extensibility/debugger/reference/idebugcanstopevent2-getreason.md)方法，以确定 DE 想要停止的原因，然后调用`IDebugCanStopEvent2::CanStop`与适当的响应的方法。

 如果 DE 停止，它将发送事件，介绍了停止的原因。 通常有两个发送的事件，表示用户或信号中断[IDebugBreakEvent2](../../../extensibility/debugger/reference/idebugbreakevent2.md)接口，并且表示的断点事件[IDebugBreakpointEvent2](../../../extensibility/debugger/reference/idebugbreakpointevent2.md)接口。

## <a name="see-also"></a>请参阅
- [IDebugCanStopEvent2](../../../extensibility/debugger/reference/idebugcanstopevent2.md)
- [IDebugBreakEvent2](../../../extensibility/debugger/reference/idebugbreakevent2.md)
- [IDebugBreakpointEvent2](../../../extensibility/debugger/reference/idebugbreakpointevent2.md)
- [GetReason](../../../extensibility/debugger/reference/idebugcanstopevent2-getreason.md)