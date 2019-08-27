---
title: IDebugBinder::ResolveRuntimeType | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBinder::ResolveRuntimeType
helpviewer_keywords:
- IDebugBinder::ResolveRuntimeType method
ms.assetid: 6456ab3e-1c03-4f3c-91f9-16797ab7f5e7
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: b2954b5f2a1ac4dd14485a1b924423ba53fddcb7
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66315168"
---
# <a name="idebugbinderresolveruntimetype"></a>IDebugBinder::ResolveRuntimeType
此方法确定一个对象的运行时类型。

## <a name="syntax"></a>语法

```cpp
HRESULT ResolveRuntimeType( 
   IDebugObject* pObject,
   IDebugField** ppResolved
);
```

```csharp
int ResolveRuntimeType(
   IDebugObject     pObject,
   out IDebugField  ppResolved
);
```

## <a name="parameters"></a>参数
`pObject`\
[in][IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)会得到解决。

`ppResolved`\
[out]返回作为对象的类型[IDebugField](../../../extensibility/debugger/reference/idebugfield.md)。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="remarks"></a>备注
 在编译时，始终不知道对象的运行时类型。 例如，使用多态性，参数可以被传递到函数作为其基本类，如按钮类。 实际自变量可能是派生的类，如单选按钮类。

## <a name="see-also"></a>请参阅
- [IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md)
- [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)