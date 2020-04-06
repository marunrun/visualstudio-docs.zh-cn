---
title: IDebug函数对象2：：创建对象 |微软文档
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugFunctionObject2::CreateObject
- CreateObject
ms.assetid: 148de615-941e-4b64-ab11-75b692aae465
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 6de1a30a032919a90fbb3d760837d5eeca00feaf
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80728478"
---
# <a name="idebugfunctionobject2createobject"></a>IDebugFunctionObject2::CreateObject
创建使用构造函数给定评估标志设置和超时值的对象。

## <a name="syntax"></a>语法

```cpp
HRESULT CreateObject (
   IDebugFunctionObject* pConstructor,
   DWORD                 dwArgs,
   IDebugObject*         pArgs[],
   DWORD                 dwEvalFlags,
   DWORD                 dwTimeout,
   IDebugObject**        ppObject
);
```

```csharp
int CreateObject (
   IDebugFunctionObject pConstructor,
   uint                 dwArgs,
   IDebugObject[]       pArgs,
   uint                 dwEvalFlags,
   uint                 dwTimeout,
   out IDebugObject**   ppObject
);
```

## <a name="parameters"></a>参数
`pConstructor`\
[在]表示要创建对象的构造函数的[IDebug函数对象](../../../extensibility/debugger/reference/idebugfunctionobject.md)。

`dwArgs`\
[在]数组中的`pArg`参数数。 表示传递给构造函数的参数数。

`pArgs`\
[在][IDebugObject 对象的](../../../extensibility/debugger/reference/idebugobject.md)数组，表示传递给构造函数的参数。

`dwEvalFlags`\
[在][EVALFLAGS](../../../extensibility/debugger/reference/evalflags.md)枚举中的标志组合，用于指定如何执行计算。

`dwTimeout`\
[在]从此方法返回之前等待的最大时间（以毫秒为单位）。 使用**INFINITE**无限期等待。

`ppObject`\
[出]返回表示新创建对象的**IDebugObject。**

## <a name="return-value"></a>返回值
 如果成功，返回`S_OK`;否则，返回错误代码。

## <a name="remarks"></a>备注
 调用此方法以创建表示类实例的对象，或需要构造函数（即参数）的其他复杂类型。

## <a name="see-also"></a>请参阅
- [IDebugFunctionObject2](../../../extensibility/debugger/reference/idebugfunctionobject2.md)
