---
title: IDebugFunctionObject::CreateObject |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugFunctionObject::CreateObject
helpviewer_keywords:
- IDebugFunctionObject::CreateObject method
ms.assetid: c4c99dd5-609a-4e7c-8f29-eb728f57e995
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: dc0632f429a547d4b17fe57bec4582fea623ee24
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66320950"
---
# <a name="idebugfunctionobjectcreateobject"></a>IDebugFunctionObject::CreateObject
创建使用构造函数的对象。

## <a name="syntax"></a>语法

```cpp
HRESULT CreateObject( 
   IDebugFunctionObject* pConstructor,
   DWORD                 dwArgs,
   IDebugObject*         pArgs[],
   IDebugObject**        ppObject
);
```

```csharp
int CreateObject(
   IDebugFunctionObject pConstructor,
   uint                 dwArgs,
   IDebugObject[]       pArgs,
   out IDebugObject     ppObject
);
```

## <a name="parameters"></a>参数
`pConstructor`\
[in][IDebugFunctionObject](../../../extensibility/debugger/reference/idebugfunctionobject.md)对象表示要创建的对象的构造函数。

`dwArgs`\
[in]中的参数数量`pArg`数组。 表示传递给构造函数的参数数目。

`pArg`\
[in]一个数组[IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)对象表示的参数传递给构造函数。

`ppObject`\
[out]返回`IDebugObject`表示新创建的对象。

## <a name="return-value"></a>返回值
 如果成功，则返回 S_OK;否则，返回错误代码。

## <a name="remarks"></a>备注
 调用此方法以创建一个对象，表示一个类 （或其他复杂类型，它要求的构造函数） 的实例，它是由表示该函数的参数[IDebugFunctionObject](../../../extensibility/debugger/reference/idebugfunctionobject.md)接口。

 如果对象参数不需要构造函数，调用[CreateObjectNoConstructor](../../../extensibility/debugger/reference/idebugfunctionobject-createobjectnoconstructor.md)方法。

## <a name="see-also"></a>请参阅
- [IDebugFunctionObject](../../../extensibility/debugger/reference/idebugfunctionobject.md)
- [CreateObjectNoConstructor](../../../extensibility/debugger/reference/idebugfunctionobject-createobjectnoconstructor.md)