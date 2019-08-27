---
title: IDebugProcessEx2::Attach | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProcessEx2::Attach
helpviewer_keywords:
- IDebugProcessEx2::Attach method
ms.assetid: f3334ed7-39bf-4d02-a338-36f567b9b287
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 5932535810f28e6f5da96ab69457f7364563d622
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66325332"
---
# <a name="idebugprocessex2attach"></a>IDebugProcessEx2::Attach
此方法将通知过程会话现在正在调试的进程。

## <a name="syntax"></a>语法

```cpp
HRESULT Attach( 
   IDebugSession2* pSession
);
```

```csharp
int Attach(
   IDebugSession2 pSession
);
```

## <a name="parameters"></a>参数
`pSession`\
[in]一个值，唯一标识附加到此进程的会话。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="remarks"></a>备注
 接口传入`pSession`仅视为 cookie 中，用于唯一标识会话调试管理器附加到此进程; 的值上提供的接口的方法不起作用。

## <a name="see-also"></a>请参阅
- [IDebugProcessEx2](../../../extensibility/debugger/reference/idebugprocessex2.md)