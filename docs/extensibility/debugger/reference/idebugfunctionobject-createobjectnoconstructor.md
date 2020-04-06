---
title: IDebug函数对象：：创建对象无构造函数 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugFunctionObject::CreateObjectNoConstructor
helpviewer_keywords:
- IDebugFunctionObject::CreateObjectNoConstructor method
ms.assetid: 4e2bd6d5-f4bd-4c10-a998-3db451c9a0c8
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: ad95f9273276830b59ebc77214f3920a687d41ed
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80728572"
---
# <a name="idebugfunctionobjectcreateobjectnoconstructor"></a>IDebugFunctionObject::CreateObjectNoConstructor
创建没有构造函数的对象。

## <a name="syntax"></a>语法

```cpp
HRESULT CreateObjectNoConstructor( 
   IDebugField*   pClassObject,
   IDebugObject** ppObject
);
```

```csharp
int CreateObjectNoConstructor(
   IDebugField      pClassField,
   out IDebugObject ppObject
);
```

## <a name="parameters"></a>参数
`pClassObject`\
[在]表示要创建的对象类型的[IDebugField](../../../extensibility/debugger/reference/idebugfield.md)对象。

`ppObject`\
[出]返回表示新创建对象的[IDebugObject。](../../../extensibility/debugger/reference/idebugobject.md)

## <a name="return-value"></a>返回值
 如果成功，返回S_OK;否则，返回错误代码。

## <a name="remarks"></a>备注
 调用此方法以创建表示结构或复杂类型的实例的对象（不需要构造函数），该实例是[IDebugAtheObject](../../../extensibility/debugger/reference/idebugfunctionobject.md)接口表示的函数的参数。

 如果对象参数需要构造函数，请调用[CreateObject](../../../extensibility/debugger/reference/idebugfunctionobject-createobject.md)方法。

## <a name="see-also"></a>请参阅
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
- [IDebugFunctionObject](../../../extensibility/debugger/reference/idebugfunctionobject.md)
- [CreateObject](../../../extensibility/debugger/reference/idebugfunctionobject-createobject.md)
