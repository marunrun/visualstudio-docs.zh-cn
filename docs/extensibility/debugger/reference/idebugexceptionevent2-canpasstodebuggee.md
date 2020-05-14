---
title: IDebugexception2：：坎帕斯托调试点 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugExceptionEvent2::CanPassToDebuggee
helpviewer_keywords:
- IDebugExceptionEvent2::CanPassToDebuggee
ms.assetid: ae4bbe0a-fbe1-49be-a310-ea64279a434b
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: ab57f599214cfbd7a1f5fcca15fa104b072d1d48
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80729867"
---
# <a name="idebugexceptionevent2canpasstodebuggee"></a>IDebugExceptionEvent2::CanPassToDebuggee
确定调试引擎 （DE） 是否支持在恢复执行时将此异常传递给正在调试的程序的选项。

## <a name="syntax"></a>语法

```cpp
HRESULT CanPassToDebuggee(
   void
);
```

```csharp
int CanPassToDebuggee();
```

## <a name="return-value"></a>返回值
 返回（`S_OK`异常可以传递给程序）或`S_FALSE`（无法传递异常）。

## <a name="remarks"></a>备注
 DE 必须具有传递给调试器的默认操作。 IDE 可能会接收[IDebugExceptionEvent2](../../../extensibility/debugger/reference/idebugexceptionevent2.md)事件，并在不调用`CanPassToDebuggee`该方法的情况下调用["继续"](../../../extensibility/debugger/reference/idebugprocess3-continue.md)方法。 因此，DE 应具有传递异常的默认情况。

## <a name="see-also"></a>请参阅
- [IDebugExceptionEvent2](../../../extensibility/debugger/reference/idebugexceptionevent2.md)
- [继续](../../../extensibility/debugger/reference/idebugprocess3-continue.md)
