---
title: IDebug函数对象：：评估 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugFunctionObject::Evaluate
helpviewer_keywords:
- IDebugFunctionObject::Evaluate method
ms.assetid: 29349ea3-d5c1-4135-aa76-ced073ab9683
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 529a5f67c808efa258bc0cb9899f546dbb90d431
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80728508"
---
# <a name="idebugfunctionobjectevaluate"></a>IDebugFunctionObject::Evaluate
调用函数并将结果值作为对象返回。

## <a name="syntax"></a>语法

```cpp
HRESULT Evaluate( 
   IDebugObject** ppParams,
   DWORD          dwParams,
   DWORD          dwTimeout,
   IDebugObject** ppResult
);
```

```csharp
int Evaluate(
   IDebugObject[]   ppParams,
   IntPtr           dwParams,
   uint             dwTimeout,
   out IDebugObject ppResult
);
```

## <a name="parameters"></a>参数
`ppParams`\
[在]表示输入参数的[IDebugObject 对象的](../../../extensibility/debugger/reference/idebugobject.md)数组。 每个参数都是使用[IDebug函数对象](../../../extensibility/debugger/reference/idebugfunctionobject.md)接口中的`Create`一种方法创建的。

`dwParams`\
[在]数组中的`ppParams`参数数。

`dwTimeout`\
[在]指定从此方法返回之前等待的最大时间（以毫秒为单位）。 用于`INFINITE`无限期等待。

`ppResult`\
[出]返回表示函数值为对象的[IDebugObject。](../../../extensibility/debugger/reference/idebugobject.md)

## <a name="return-value"></a>返回值
 如果成功，返回S_OK;否则，返回错误代码。

## <a name="remarks"></a>备注
 此方法设置并执行对[IDebug函数对象](../../../extensibility/debugger/reference/idebugfunctionobject.md)表示的函数的调用。

## <a name="see-also"></a>请参阅
- [IDebugFunctionObject](../../../extensibility/debugger/reference/idebugfunctionobject.md)
