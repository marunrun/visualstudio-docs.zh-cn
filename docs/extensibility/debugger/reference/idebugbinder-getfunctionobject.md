---
title: IDebugBinder：：获取功能对象 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBinder::GetFunctionObject
helpviewer_keywords:
- IDebugBinder::GetFunctionObject method
ms.assetid: 8fb789df-8f30-420d-8ca5-bb496a6738f1
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 01d501367f47e520e9170118da8b6fdfcb326137
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80736009"
---
# <a name="idebugbindergetfunctionobject"></a>IDebugBinder::GetFunctionObject
此方法获取用于创建函数参数的[IDebug函数对象](../../../extensibility/debugger/reference/idebugfunctionobject.md)。

## <a name="syntax"></a>语法

```cpp
HRESULT GetFunctionObject( 
   IDebugFunctionObject **ppFunction
);
```

```csharp
int GetFunctionObject(
   out IDebugFunctionObject ppFunction
);
```

## <a name="parameters"></a>参数
`ppFunction`\
[出]返回用于创建函数参数的[IDebug函数对象](../../../extensibility/debugger/reference/idebugfunctionobject.md)接口。

## <a name="return-value"></a>返回值
 如果成功，返回S_OK;否则，返回错误代码。

## <a name="see-also"></a>请参阅
- [IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md)
- [IDebugFunctionObject](../../../extensibility/debugger/reference/idebugfunctionobject.md)
