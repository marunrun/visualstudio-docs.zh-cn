---
title: DEBUG_PROPERTY_INFO | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- DEBUG_PROPERTY_INFO
helpviewer_keywords:
- DEBUG_PROPERTY_INFO structure
ms.assetid: 5a085d18-62c6-4740-b9e9-3f5db6bfdf7f
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 7804cfad48d5029e16619b5ae524fa6e761f11b4
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66346172"
---
# <a name="debugpropertyinfo"></a>DEBUG_PROPERTY_INFO
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
中的标志的组合[DEBUGPROP_INFO_FLAGS](../../../extensibility/debugger/reference/debugprop-info-flags.md)枚举，用于指定哪些字段填充。

`bstrFullName`\
属性的完整名称。

`bstrName`\
在上下文中的属性名称。

`bstrType`\
形式的格式化字符串的属性类型。

`bstrValue`\
形式的格式化字符串的属性值。

`pProperty`\
[IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)此结构所描述的对象。

`dwAttrib`\
中的标志的组合[DBG_ATTRIB_FLAGS](../../../extensibility/debugger/reference/dbg-attrib-flags.md)描述此属性的特性的枚举。

## <a name="remarks"></a>备注
属性是层次结构性质具有名称、 类型和值的对象。 例如，属性可以描述本地变量、 参数、 监视变量和表达式和寄存器。

此结构传递给[GetPropertyInfo](../../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md)填写其中的方法。 作为一系列从此结构的一部分，也会返回此结构[IEnumDebugPropertyInfo2](../../../extensibility/debugger/reference/ienumdebugpropertyinfo2.md)接口，反过来，通过调用将返回该值[EnumChildren](../../../extensibility/debugger/reference/idebugproperty2-enumchildren.md)和[EnumProperties](../../../extensibility/debugger/reference/idebugstackframe2-enumproperties.md)方法。

## <a name="requirements"></a>要求
标头： msdbg.h

命名空间:Microsoft.VisualStudio.Debugger.Interop

程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)
- [DEBUGPROP_INFO_FLAGS](../../../extensibility/debugger/reference/debugprop-info-flags.md)
- [DBG_ATTRIB_FLAGS](../../../extensibility/debugger/reference/dbg-attrib-flags.md)
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
- [GetPropertyInfo](../../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md)
- [IEnumDebugPropertyInfo2](../../../extensibility/debugger/reference/ienumdebugpropertyinfo2.md)
- [EnumChildren](../../../extensibility/debugger/reference/idebugproperty2-enumchildren.md)
- [EnumProperties](../../../extensibility/debugger/reference/idebugstackframe2-enumproperties.md)
