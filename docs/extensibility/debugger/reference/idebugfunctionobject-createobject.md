---
title: IDebug函数对象：：创建对象 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugFunctionObject::CreateObject
helpviewer_keywords:
- IDebugFunctionObject::CreateObject method
ms.assetid: c4c99dd5-609a-4e7c-8f29-eb728f57e995
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: beb00bcf932b19ed4e489456236957c55d909ce4
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80728595"
---
# <a name="idebugfunctionobjectcreateobject"></a>IDebugFunctionObject::CreateObject
使用构造函数创建对象。

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
[在][IDebug函数对象对象](../../../extensibility/debugger/reference/idebugfunctionobject.md)，表示要创建的对象的构造函数。

`dwArgs`\
[在]数组中的`pArg`参数数。 表示传递给构造函数的参数数。

`pArg`\
[在][IDebugObject 对象的](../../../extensibility/debugger/reference/idebugobject.md)数组，表示传递给构造函数的参数。

`ppObject`\
[出]返回表示`IDebugObject`新创建的对象。

## <a name="return-value"></a>返回值
 如果成功，返回S_OK;否则，返回错误代码。

## <a name="remarks"></a>备注
 调用此方法以创建一个对象，该对象表示类（或需要构造函数的其他复杂类型）的实例，该实例是[iDebug函数对象](../../../extensibility/debugger/reference/idebugfunctionobject.md)接口表示的函数的参数。

 如果对象参数不需要构造函数，请调用[CreateObjectNo构造函数](../../../extensibility/debugger/reference/idebugfunctionobject-createobjectnoconstructor.md)方法。

## <a name="see-also"></a>请参阅
- [IDebugFunctionObject](../../../extensibility/debugger/reference/idebugfunctionobject.md)
- [CreateObjectNoConstructor](../../../extensibility/debugger/reference/idebugfunctionobject-createobjectnoconstructor.md)
