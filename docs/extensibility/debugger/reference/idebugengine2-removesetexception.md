---
title: IDebugEngine2::RemoveSetException | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngine2::RemoveSetException
helpviewer_keywords:
- IDebugEngine2::RemoveSetException
ms.assetid: bdd25097-0e9d-4218-b417-0497ea48d2e8
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 45c3cec5ab0511ea80a6b04d9b3ee575afd9d149
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66352552"
---
# <a name="idebugengine2removesetexception"></a>IDebugEngine2::RemoveSetException
以便不再由调试引擎中移除指定的异常。

## <a name="syntax"></a>语法

```cpp
HRESULT RemoveSetException( 
   EXCEPTION_INFO* pException
);
```

```csharp
int RemoveSetException( 
   EXCEPTION_INFO[] pException
);
```

## <a name="parameters"></a>参数
`pException`\
[in][EXCEPTION_INFO](../../../extensibility/debugger/reference/exception-info.md)结构描述要删除的异常。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="remarks"></a>备注
 要删除的异常必须之前已设置到的早期调用[SetException](../../../extensibility/debugger/reference/idebugengine2-setexception.md)方法。

 若要立即删除组的所有异常，请调用[RemoveAllSetExceptions](../../../extensibility/debugger/reference/idebugengine2-removeallsetexceptions.md)方法。

## <a name="see-also"></a>请参阅
- [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)
- [EXCEPTION_INFO](../../../extensibility/debugger/reference/exception-info.md)