---
title: IDebug拦截例外完成事件2：：获取拦截饼干 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugInterceptExceptionCompleteEvent2::GetInterceptCookie
helpviewer_keywords:
- IDebugInterceptExceptionCompleteEvent2::GetInterceptCookie
ms.assetid: 07b20866-e598-4783-9ecc-6aa8625c8804
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 9065c0b7868efaeb70c10a3ab921a8764694662e
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80727775"
---
# <a name="idebuginterceptexceptioncompleteevent2getinterceptcookie"></a>IDebugInterceptExceptionCompleteEvent2::GetInterceptCookie
当截获的异常的处理完成时调用。

## <a name="syntax"></a>语法

```cpp
HRESULT GetInterceptCookie(
   UINT64* pqwCookie
);
```

```csharp
int GetInterceptCookie(
   out ulong pqwCookie
);
```

## <a name="parameters"></a>参数
`pqwCookie`\
[出]与被截获的异常关联的唯一值。

## <a name="return-value"></a>返回值
 如果成功，返回`S_OK`;否则返回错误代码。

## <a name="remarks"></a>备注
 [拦截异常](../../../extensibility/debugger/reference/idebugstackframe3-interceptcurrentexception.md)方法完成对截取异常的处理后，它将发送[I拦截异常完成事件2。](../../../extensibility/debugger/reference/idebuginterceptexceptioncompleteevent2.md) 处理程序可以使用 方法`GetInterceptCookie`检索与异常关联的唯一值（传递给`InterceptCurrentException`方法的相同值）。

## <a name="see-also"></a>请参阅
- [InterceptCurrentException](../../../extensibility/debugger/reference/idebugstackframe3-interceptcurrentexception.md)
- [IDebugInterceptExceptionCompleteEvent2](../../../extensibility/debugger/reference/idebuginterceptexceptioncompleteevent2.md)
