---
title: IDebugThread2：：获取ThreadId |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugThread2::GetThreadId
helpviewer_keywords:
- IDebugThread2::GetThreadId
ms.assetid: db8b1c07-6b86-47f9-b292-bac19c276d36
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: a7788cc09d92ff4c784fbcb7004393fe0d3074c8
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80718702"
---
# <a name="idebugthread2getthreadid"></a>IDebugThread2::GetThreadId
获取系统线程标识符。

## <a name="syntax"></a>语法

```cpp
HRESULT GetThreadId (
    DWORD* pdwThreadId
);
```

```csharp
int GetThreadId (
    out uint pdwThreadId
);
```

## <a name="parameters"></a>参数
`pdwThreadId`\
[出]返回系统线程标识符。

## <a name="return-value"></a>返回值
如果成功，返回`S_OK`;否则，返回错误代码。

## <a name="remarks"></a>备注
线程 ID 用于标识进程中所有其他线程之间的线程。

## <a name="example"></a>示例
下面的示例演示如何实现[IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)接口的简单`CProgram`对象实现此方法。

```cpp
HRESULT CProgram::GetThreadId(DWORD* pdwThreadId) {
    *pdwThreadId = GetCurrentThreadId();
    return NOERROR;
}
```

## <a name="see-also"></a>请参阅
- [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)
