---
title: IDebugProcessEx2：：附加 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProcessEx2::Attach
helpviewer_keywords:
- IDebugProcessEx2::Attach method
ms.assetid: f3334ed7-39bf-4d02-a338-36f567b9b287
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: d70da2530a1677367a22968436a17eba809fd24a
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80723381"
---
# <a name="idebugprocessex2attach"></a>IDebugProcessEx2::Attach
此方法通知进程会话正在调试该过程。

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
[在]唯一标识附加到此过程的会话的值。

## <a name="return-value"></a>返回值
 如果成功，返回`S_OK`;否则，返回错误代码。

## <a name="remarks"></a>备注
 传入的`pSession`接口将仅被视为 Cookie，该值唯一标识附加到此过程的会话调试管理器;提供的接口上没有任何方法正常工作。

## <a name="see-also"></a>请参阅
- [IDebugProcessEx2](../../../extensibility/debugger/reference/idebugprocessex2.md)
