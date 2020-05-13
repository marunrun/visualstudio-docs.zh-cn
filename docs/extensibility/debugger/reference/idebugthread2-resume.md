---
title: IDebugThread2：恢复 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugThread2::Resume
helpviewer_keywords:
- IDebugThread2::Resume
ms.assetid: 36aad682-b0b9-40a2-b3fc-f0e61d41cdbc
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 3899dea7c33946588de4308f42b948ede703361a
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80718685"
---
# <a name="idebugthread2resume"></a>IDebugThread2::Resume
恢复线程的执行。

## <a name="syntax"></a>语法

```cpp
HRESULT Resume ( 
   DWORD *pdwSuspendCount
);
```

```csharp
int Resume ( 
   out uint pdwSuspendCount
);
```

## <a name="parameters"></a>参数
`pdwSuspendCount`\
[出]返回恢复操作后的挂起计数。

## <a name="return-value"></a>返回值
 如果成功，返回`S_OK`;否则，返回错误代码。

## <a name="remarks"></a>备注
 对此方法的每个调用都会取消挂起计数，直到它达到 0，此时实际恢复执行。 此挂起计数显示在**线程**调试窗口中。

 对于对此方法的每个调用，必须对[挂起](../../../extensibility/debugger/reference/idebugthread2-suspend.md)方法进行以前的调用。 挂起计数确定到目前为止调用`IDebugThread2::Suspend`该方法的次数。

## <a name="see-also"></a>请参阅
- [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)
- [暂停](../../../extensibility/debugger/reference/idebugthread2-suspend.md)
