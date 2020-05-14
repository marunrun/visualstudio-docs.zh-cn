---
title: IDebugStackFrame2：：枚举属性 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugStackFrame2::EnumProperties
helpviewer_keywords:
- IDebugStackFrame2::EnumProperties
ms.assetid: 334bb95e-c7e0-4008-9f06-8c3999e47ee8
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: f822f20cf4fb7a6fd5aa71b9cc1ec26bcd90e234
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80719897"
---
# <a name="idebugstackframe2enumproperties"></a>IDebugStackFrame2::EnumProperties
为与堆栈框架关联的属性（如局部变量）创建枚举器。

## <a name="syntax"></a>语法

```cpp
HRESULT EnumProperties ( 
   DEBUGPROP_INFO_FLAGS      dwFieldSpec,
   UINT                      nRadix,
   REFIID                    refiid,
   DWORD                     dwTimeout,
   ULONG*                    pcelt,
   IEnumDebugPropertyInfo2** ppEnum
);
```

```csharp
int EnumProperties ( 
   enum_DEBUGPROP_INFO_FLAGS   dwFieldSpec,
   uint                        nRadix,
   ref Guid                    refiid,
   uint                        dwTimeout,
   out uint                    pcelt,
   out IEnumDebugPropertyInfo2 ppEnum
);
```

## <a name="parameters"></a>参数
`dwFieldSpec`\
[在][DEBUGPROP_INFO_FLAGS](../../../extensibility/debugger/reference/debugprop-info-flags.md)枚举中的标志的组合，指定要填充枚举[DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md)结构中的字段。

`nRadix`\
[在]用于格式化任何数值信息的半径。

`refiid`\
[在]用于选择要枚[举DEBUG_PROPERTY_INFO结构](../../../extensibility/debugger/reference/debug-property-info.md)的筛选器的 GUID，例如`guidFilterLocals`。

`dwTimeout`\
[在]从此方法返回之前等待的最大时间（以毫秒为单位）。 用于`INFINITE`无限期等待。

`pcelt`\
[出]返回枚举的属性数。 这与调用[GetCount](../../../extensibility/debugger/reference/ienumdebugpropertyinfo2-getcount.md)方法相同。

`ppEnum`\
[出]返回包含所需属性列表的[IEnumDebugPropertyInfo2](../../../extensibility/debugger/reference/ienumdebugpropertyinfo2.md)对象。

## <a name="return-value"></a>返回值
 如果成功，返回`S_OK`;否则，返回错误代码。

## <a name="remarks"></a>备注
 由于此方法允许使用单个调用检索所有选定的属性，因此比按顺序调用[GetDebugProperty](../../../extensibility/debugger/reference/idebugstackframe2-getdebugproperty.md)和[Enum 儿童](../../../extensibility/debugger/reference/idebugproperty2-enumchildren.md)方法要快。

## <a name="see-also"></a>请参阅
- [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)
- [DEBUGPROP_INFO_FLAGS](../../../extensibility/debugger/reference/debugprop-info-flags.md)
- [IEnumDebugPropertyInfo2](../../../extensibility/debugger/reference/ienumdebugpropertyinfo2.md)
- [GetCount](../../../extensibility/debugger/reference/ienumdebugpropertyinfo2-getcount.md)
- [GetDebugProperty](../../../extensibility/debugger/reference/idebugstackframe2-getdebugproperty.md)
- [EnumChildren](../../../extensibility/debugger/reference/idebugproperty2-enumchildren.md)
