---
title: IDebug属性2：：设置价值作为参考 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProperty2::SetValueAsReference
helpviewer_keywords:
- IDebugProperty2::SetValueAsReference method
ms.assetid: 341b1b89-4ab8-4e1c-abe2-fb955df5c6b0
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 73d00ccedc6985061448170735e9ebcaac42f530
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80721250"
---
# <a name="idebugproperty2setvalueasreference"></a>IDebugProperty2::SetValueAsReference
将此属性的值设置为给定引用的值。

## <a name="syntax"></a>语法

```cpp
HRESULT SetValueAsReference(
   IDebugReference2** rgpArgs,
   DWORD              dwArgCount,
   IDebugReference2*  pValue,
   DWORD              dwTimeout
);
```

```csharp
int SetValueAsReference(
   IDebugReference2[] rgpArgs,
   uint               dwArgCount,
   IDebugReference2   pValue,
   uint               dwTimeout
);
```

## <a name="parameters"></a>参数
`rgpArgs`\
[在]要传递给托管代码属性设置器的参数数组。 如果属性设置器不采用参数，或者此[IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)对象不引用此类属性设置器，`rgpArgs`则应为 null 值。 此参数通常是空值。

`dwArgCount`\
[在]数组中的`rgpArgs`参数数。

`pValue`\
[在]以[IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)对象的形式对用于设置此属性的值的引用。

`dwTimeout`\
[在]设置值需要多长时间（以毫秒为单位）。 典型的值是`INFINITE`。 这会影响任何可能的评估可能需要的时间长度。

## <a name="return-value"></a>返回值
 如果成功，返回`S_OK`;否则将返回错误代码，通常为以下代码之一：

|错误|描述|
|-----------|-----------------|
|`E_SETVALUEASREFERENCE_NOTSUPPORTED`|不支持从引用中设置值。|
|`E_SETVALUE_VALUE_CANNOT_BE_SET`|无法设置该值，因为此属性引用方法。|
|`E_SETVALUE_VALUE_IS_READONLY`|该值为只读，无法设置。|
|`E_NOTIMPL`|该方法未实现。|

## <a name="see-also"></a>请参阅
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
- [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)
