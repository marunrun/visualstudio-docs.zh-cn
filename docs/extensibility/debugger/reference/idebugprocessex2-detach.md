---
title: IDebugProcessEx2::Detach | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProcessEx2::Detach
helpviewer_keywords:
- IDebugProcessEx2::Detach method
ms.assetid: 66d54c2c-9302-47c8-9975-f30ed988ab29
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 2f016c078fcf19ec244fc4c0682d2caee81a2062
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66311620"
---
# <a name="idebugprocessex2detach"></a>IDebugProcessEx2::Detach
此方法将通知该过程在会话不再调试进程。

## <a name="syntax"></a>语法

```cpp
HRESULT Detach( 
   IDebugSession2* pSession
);
```

```csharp
int Detach(
   IDebugSession2 pSession
);
```

## <a name="parameters"></a>参数
`pSession`\
[in]一个值，唯一标识要分离从的此进程的会话。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="remarks"></a>备注
 接口传入`pSession`仅作为 cookie 处理，用于唯一标识会话调试管理器最初的值附加到此过程; 上提供的接口的方法不起作用。

## <a name="see-also"></a>请参阅
- [IDebugProcessEx2](../../../extensibility/debugger/reference/idebugprocessex2.md)