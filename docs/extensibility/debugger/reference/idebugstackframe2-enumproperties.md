---
title: IDebugStackFrame2::EnumProperties | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugStackFrame2::EnumProperties
helpviewer_keywords:
- IDebugStackFrame2::EnumProperties
ms.assetid: 334bb95e-c7e0-4008-9f06-8c3999e47ee8
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: ba4cf74c41d321cc03684ec6717a9eea74e9a622
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66321855"
---
# <a name="idebugstackframe2enumproperties"></a>IDebugStackFrame2::EnumProperties
创建与该堆栈帧，如本地变量关联的属性的枚举器。

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
[in]中的标志的组合[DEBUGPROP_INFO_FLAGS](../../../extensibility/debugger/reference/debugprop-info-flags.md)枚举，用于指定哪些字段中枚举[DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md)结构是必填。

`nRadix`\
[in]用于格式化数值的任何信息的基数。

`refiid`\
[in]筛选器用于选择其中一个 GUID [DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md)结构是否进行枚举，如`guidFilterLocals`。

`dwTimeout`\
[in]最大时间 （毫秒），此方法返回前等待。 使用`INFINITE`无限期等待。

`pcelt`\
[out]返回枚举的属性的数目。 这是调用相同[GetCount](../../../extensibility/debugger/reference/ienumdebugpropertyinfo2-getcount.md)方法。

`ppEnum`\
[out]返回[IEnumDebugPropertyInfo2](../../../extensibility/debugger/reference/ienumdebugpropertyinfo2.md)对象，其中包含所需属性的列表。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="remarks"></a>备注
 此方法允许一次调用检索所有所选的属性，因为它是比按顺序调用更快[GetDebugProperty](../../../extensibility/debugger/reference/idebugstackframe2-getdebugproperty.md)并[EnumChildren](../../../extensibility/debugger/reference/idebugproperty2-enumchildren.md)方法。

## <a name="see-also"></a>请参阅
- [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)
- [DEBUGPROP_INFO_FLAGS](../../../extensibility/debugger/reference/debugprop-info-flags.md)
- [IEnumDebugPropertyInfo2](../../../extensibility/debugger/reference/ienumdebugpropertyinfo2.md)
- [GetCount](../../../extensibility/debugger/reference/ienumdebugpropertyinfo2-getcount.md)
- [GetDebugProperty](../../../extensibility/debugger/reference/idebugstackframe2-getdebugproperty.md)
- [EnumChildren](../../../extensibility/debugger/reference/idebugproperty2-enumchildren.md)