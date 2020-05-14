---
title: DEBUG_PROPERTY_INFO |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- DEBUG_PROPERTY_INFO
helpviewer_keywords:
- DEBUG_PROPERTY_INFO structure
ms.assetid: 5a085d18-62c6-4740-b9e9-3f5db6bfdf7f
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 34fc1b5103949a767a3ee448618cbb708ea6a48b
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80737446"
---
# <a name="debug_property_info"></a>DEBUG_PROPERTY_INFO
包含有关调试属性的信息。

## <a name="syntax"></a>语法

```cpp
typedef struct tagDEBUG_PROPERTY_INFO {
    DEBUGPROP_INFO_FLAGS dwValidFields;
    BSTR                 bstrFullName;
    BSTR                 bstrName;
    BSTR                 bstrType;
    BSTR                 bstrValue;
    IDebugProperty2*     pProperty;
    DBG_ATTRIB_FLAGS     dwAttrib;
} DEBUG_PROPERTY_INFO;
```

```csharp
public struct DEBUG_PROPERTY_INFO {
    public uint            dwValidFields;
    public string          bstrFullName;
    public string          bstrName;
    public string          bstrType;
    public string          bstrValue;
    public IDebugProperty2 pProperty;
    public ulong           dwAttrib;
};
```

## <a name="members"></a>成员
`dwValidFields`\
[DEBUGPROP_INFO_FLAGS](../../../extensibility/debugger/reference/debugprop-info-flags.md)枚举中的标志的组合，用于指定填充哪些字段。

`bstrFullName`\
属性的全名。

`bstrName`\
上下文中的属性名称。

`bstrType`\
属性类型作为格式化字符串。

`bstrValue`\
属性值作为格式化字符串。

`pProperty`\
此结构描述的[IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)对象。

`dwAttrib`\
描述此属性属性[DBG_ATTRIB_FLAGS](../../../extensibility/debugger/reference/dbg-attrib-flags.md)枚举的标志的组合。

## <a name="remarks"></a>备注
属性是具有名称、类型和值的分层性质的对象。 例如，属性可以描述局部变量、参数、监视变量和表达式以及寄存器。

此结构传递给填写该结构的[GetPropertyInfo](../../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md)方法。 此结构还作为此结构列表的一部分从[IEnumDebugPropertyInfo2](../../../extensibility/debugger/reference/ienumdebugpropertyinfo2.md)接口返回，该接口又从调用[Enum 子项](../../../extensibility/debugger/reference/idebugproperty2-enumchildren.md)和[枚举属性](../../../extensibility/debugger/reference/idebugstackframe2-enumproperties.md)方法返回。

## <a name="requirements"></a>要求
标题： msdbg.h

命名空间：微软.VisualStudio.调试器.互通

程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)
- [DEBUGPROP_INFO_FLAGS](../../../extensibility/debugger/reference/debugprop-info-flags.md)
- [DBG_ATTRIB_FLAGS](../../../extensibility/debugger/reference/dbg-attrib-flags.md)
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
- [获取财产信息](../../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md)
- [IEnumDebugPropertyInfo2](../../../extensibility/debugger/reference/ienumdebugpropertyinfo2.md)
- [EnumChildren](../../../extensibility/debugger/reference/idebugproperty2-enumchildren.md)
- [EnumProperties](../../../extensibility/debugger/reference/idebugstackframe2-enumproperties.md)
