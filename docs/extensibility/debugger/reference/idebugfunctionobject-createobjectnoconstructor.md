---
title: IDebugFunctionObject：： CreateObjectNoConstructor |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80728572"
---
# <a name="idebugfunctionobjectcreateobjectnoconstructor"></a>IDebugFunctionObject::CreateObjectNoConstructor
创建不包含构造函数的对象。

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
中一个 [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) 对象，表示要创建的对象的类型。

`ppObject`\
弄返回表示新创建的对象的 [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) 。

## <a name="return-value"></a>返回值
 如果成功，将返回 S_OK;否则，将返回错误代码。

## <a name="remarks"></a>备注
 调用此方法可创建一个对象，该对象表示不需要构造函数的构造函数) 的结构或复杂类型 (，该构造函数由 [IDebugFunctionObject](../../../extensibility/debugger/reference/idebugfunctionobject.md) 接口表示。

 如果对象参数需要构造函数，请调用 [CreateObject](../../../extensibility/debugger/reference/idebugfunctionobject-createobject.md) 方法。

## <a name="see-also"></a>另请参阅
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
- [IDebugFunctionObject](../../../extensibility/debugger/reference/idebugfunctionobject.md)
- [CreateObject](../../../extensibility/debugger/reference/idebugfunctionobject-createobject.md)
