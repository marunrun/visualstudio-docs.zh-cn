---
title: IDebug函数对象：：创建字符串对象 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugFunctionObject::CreateStringObject
helpviewer_keywords:
- IDebugFunctionObject::CreateStringObject method
ms.assetid: fd6070ab-07d4-4ea1-8d71-b16592d6f1a7
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 40a13b9b388caa6a1ae6e3e470e4ea02553fa0ac
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80728515"
---
# <a name="idebugfunctionobjectcreatestringobject"></a>IDebugFunctionObject::CreateStringObject
创建字符串对象。

## <a name="syntax"></a>语法

```cpp
HRESULT CreateStringObject( 
   LPCOLESTR      pcstrString,
   IDebugObject** ppObject
);
```

```csharp
int CreateStringObject(
   string      pcstrString,
   out IDebugObject ppOjbect
);
```

## <a name="parameters"></a>参数
`pcstrString`\
[在]字符串对象的字符串值。

`ppObject`\
[出]返回表示新创建的字符串对象的[IDebugObject 对象](../../../extensibility/debugger/reference/idebugobject.md)。

## <a name="return-value"></a>返回值
 如果成功，返回S_OK;否则，返回错误代码。

## <a name="remarks"></a>备注
 调用此方法以创建一个对象，该对象表示一个字符串，该字符串是[IDebug函数对象](../../../extensibility/debugger/reference/idebugfunctionobject.md)接口表示的函数的参数。

## <a name="see-also"></a>请参阅
- [IDebugFunctionObject](../../../extensibility/debugger/reference/idebugfunctionobject.md)
