---
title: IDebugProgram2：：终止 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgram2::Terminate
helpviewer_keywords:
- IDebugProgram2::Terminate
ms.assetid: 4d3127d3-b1e9-4b28-ac22-2f2eea255f86
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 913c90e34e308ce5bb4ceecface739afc8d03f3d
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80722742"
---
# <a name="idebugprogram2terminate"></a>IDebugProgram2::Terminate
终止程序。

## <a name="syntax"></a>语法

```cpp
HRESULT Terminate( 
   void 
);
```

```csharp
int Terminate();
```

## <a name="return-value"></a>返回值
 如果成功，返回`S_OK`;否则，返回错误代码。

## <a name="remarks"></a>备注
 如果可能，程序将被终止并从进程卸载;否则，调试引擎 （DE） 将执行任何必要的清理。

 此方法或[终止](../../../extensibility/debugger/reference/idebugprocess2-terminate.md)方法由 IDE 调用，通常是响应用户停止所有调试。 理想情况下，此方法的实现应在进程中终止程序。 如果这是不可能的，DE 应阻止程序在此进程中再运行任何（并进行任何必要的清理）。 如果`IDebugProcess2::Terminate`IDE 调用了该方法，则整个进程将在调用`IDebugProgram2::Terminate`该方法后的某个时间终止。

## <a name="see-also"></a>请参阅
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [终止](../../../extensibility/debugger/reference/idebugprocess2-terminate.md)
