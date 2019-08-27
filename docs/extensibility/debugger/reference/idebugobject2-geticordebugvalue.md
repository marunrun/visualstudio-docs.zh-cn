---
title: IDebugObject2::GetICorDebugValue | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugObject2::GetICorDebugValue
helpviewer_keywords:
- IDebugObject2::GetICorDebugValue method
ms.assetid: bcd4355d-3fbe-483f-bb23-a44348323c6a
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: edbacbaeac9a5172d8c3bb5b54ee38fff201a2bf
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66317367"
---
# <a name="idebugobject2geticordebugvalue"></a>IDebugObject2::GetICorDebugValue
获取表示与此对象关联的值的托管的代码对象。

## <a name="syntax"></a>语法

```cpp
HRESULT GetICorDebugValue(
   IUnknown** ppUnk
);
```

```csharp
int GetICorDebugValue(
   out object ppUnk
);
```

## <a name="parameters"></a>参数
`ppUnk`\
[out]`IUnknown`接口，表示此别名。 此接口可以查询有关`ICorDebugValue`接口。

## <a name="return-value"></a>返回值
 如果成功，则返回 S_OK;否则，返回错误代码。

## <a name="remarks"></a>备注
 `ICorDebugValue`对象是一个公共语言运行时接口，表示的值。

## <a name="see-also"></a>请参阅
- [IDebugObject2](../../../extensibility/debugger/reference/idebugobject2.md)