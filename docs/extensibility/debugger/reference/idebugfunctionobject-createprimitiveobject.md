---
title: IDebugFunctionObject：： CreatePrimitiveObject |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugFunctionObject::CreatePrimitiveObject
helpviewer_keywords:
- IDebugFunctionObject::CreatePrimitiveObject method
ms.assetid: 6e9dc8b6-b4e1-4abf-b6e0-e885910775bc
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 24b26a072a3bebda2d01a89baaf2910de96e77d1
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80728529"
---
# <a name="idebugfunctionobjectcreateprimitiveobject"></a>IDebugFunctionObject::CreatePrimitiveObject
创建一个基元数据对象，如简单整数。

## <a name="syntax"></a>语法

```cpp
HRESULT CreatePrimitiveObject( 
   OBJECT_TYPE    ot,
   IDebugObject** ppObject
);
```

```csharp
int CreatePrimitiveObject(
   enum_OBJECT_TYPE ot,
   out IDebugObject ppObject
);
```

## <a name="parameters"></a>参数
`ot`\
中 [OBJECT_TYPE](../../../extensibility/debugger/reference/object-type.md) 枚举中的一个值，表示要创建的基元类型。

`ppObject`\
弄返回表示新创建的对象的 [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) 。

## <a name="return-value"></a>返回值
 如果成功，将返回 S_OK;否则，将返回错误代码。

## <a name="remarks"></a>备注
 调用此方法可创建一个对象，该对象表示一个基元对象，该对象是由 [IDebugFunctionObject](../../../extensibility/debugger/reference/idebugfunctionobject.md) 接口表示的函数的参数。 例如，如果表达式字符串为 "myString (5) "，则此方法将用于创建表示整数5的对象。

## <a name="see-also"></a>另请参阅
- [IDebugFunctionObject](../../../extensibility/debugger/reference/idebugfunctionobject.md)
