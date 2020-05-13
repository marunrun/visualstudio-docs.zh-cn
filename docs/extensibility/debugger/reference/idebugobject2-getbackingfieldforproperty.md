---
title: IDebugObject2：：获取属性的"背景" |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugObject2::GetBackingFieldForProperty
helpviewer_keywords:
- IDebugObject2::GetBackingFieldForProperty method
ms.assetid: e72c6338-5573-4fad-8075-f3ade3435424
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: b5b9fed9b071f34c119c8e4a5af12c1df7990f4c
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80726240"
---
# <a name="idebugobject2getbackingfieldforproperty"></a>IDebugObject2::GetBackingFieldForProperty
获取可能支持此对象表示的属性的字段或变量（如果有）。

## <a name="syntax"></a>语法

```cpp
HRESULT GetBackingFieldForProperty(
   IDebugObject2** ppObject
);
```

```csharp
int GetBackingFieldForProperty(
   out IDebugObject2 ppObject
);
```

## <a name="parameters"></a>参数
`ppObject`\
[出]描述备份字段的[IDebugObject2](../../../extensibility/debugger/reference/idebugobject2.md)对象。

## <a name="return-value"></a>返回值
 如果成功，返回S_OK;否则，返回错误代码。

## <a name="remarks"></a>备注
 [IDebugObject2](../../../extensibility/debugger/reference/idebugobject2.md)对象表示托管代码类属性，即具有 get 和/或设置访问器的方法。 此类属性通常需要变量来包含属性操作的值。 此变量称为后备字段。 如果对象没有支持字段，请确保返回 null 值：某些调用方可能不会注意返回值，而是查看是否在 中`ppObject`返回了 null 值。

## <a name="see-also"></a>请参阅
- [IDebugObject2](../../../extensibility/debugger/reference/idebugobject2.md)
