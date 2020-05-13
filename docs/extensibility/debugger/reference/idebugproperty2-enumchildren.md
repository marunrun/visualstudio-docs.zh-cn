---
title: IDebug属性2：：枚举儿童 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProperty2::EnumChildren
helpviewer_keywords:
- IDebugProperty2::EnumChildren
ms.assetid: cf79f666-65d1-417c-af7c-9271bac9a267
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: d6d3908c469b489eb16e4662f7515ea624825e3b
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80721510"
---
# <a name="idebugproperty2enumchildren"></a>IDebugProperty2::EnumChildren
检索属性的子项列表。

## <a name="syntax"></a>语法

```cpp
HRESULT EnumChildren ( 
   DEBUGPROP_INFO_FLAGS      dwFields,
   DWORD                     dwRadix,
   REFGUID                   guidFilter,
   DBG_ATTRIB_FLAGS          dwAttribFilter,
   LPCOLESTR                 pszNameFilter,
   DWORD                     dwTimeout,
   IEnumDebugPropertyInfo2** ppEnum
);
```

```csharp
int EnumChildren ( 
   enum_DEBUGPROP_INFO_FLAGS   dwFields,
   uint                        dwRadix,
   ref Guid                    guidFilter,
   uint                        dwAttribFilter,
   string                      pszNameFilter,
   uint                        dwTimeout,
   out IEnumDebugPropertyInfo2 ppEnum
);
```

## <a name="parameters"></a>参数
`dwFields`\
[在][DEBUGPROP_INFO_FLAGS](../../../extensibility/debugger/reference/debugprop-info-flags.md)枚举中的标志的组合，指定要填充枚举[DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md)结构中的字段。

`dwRadix`\
[在]指定用于格式化任何数值信息的半径。

`guidFilter`\
[在]与`dwAttribFilter`和`pszNameFilter`参数一起使用的筛选器的 GUID，`DEBUG_PROPERTY_INFO`用于选择要枚举的子级。 例如，`guidFilterLocals`局部变量的筛选器。

`dwAttribFilter`\
[在][DBG_ATTRIB_FLAGS](../../../extensibility/debugger/reference/dbg-attrib-flags.md)枚举中的标志的组合，用于指定要枚举的对象类型，例如`DBG_ATTRIB_METHOD`，对于可能是此属性子级的所有方法。 与 和`guidFilter``pszNameFilter`参数结合使用。

`pszNameFilter`\
[在]与`guidFilter`和`dwAttribFilter`参数一起使用的筛选器的名称，用于选择要枚`DEBUG_PROPERTY_INFO`举的子级。 例如，为所有名为"MyX"的子级设置此参数为"MyX"筛选器。

`dwTimeout`\
[在]指定从此方法返回之前等待的最大时间（以毫秒为单位）。 用于`INFINITE`无限期等待。

`ppEnum`\
[出]返回包含子属性列表的[IEnumDebugPropertyInfo2](../../../extensibility/debugger/reference/ienumdebugpropertyinfo2.md)对象。

## <a name="return-value"></a>返回值
 如果成功，返回`S_OK`;否则返回错误代码。

## <a name="see-also"></a>请参阅
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
- [DEBUGPROP_INFO_FLAGS](../../../extensibility/debugger/reference/debugprop-info-flags.md)
- [DBG_ATTRIB_FLAGS](../../../extensibility/debugger/reference/dbg-attrib-flags.md)
- [IEnumDebugPropertyInfo2](../../../extensibility/debugger/reference/ienumdebugpropertyinfo2.md)
