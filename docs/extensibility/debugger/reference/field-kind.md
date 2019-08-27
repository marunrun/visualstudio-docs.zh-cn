---
title: FIELD_KIND | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- FIELD_KIND
helpviewer_keywords:
- FIELD_KIND enumeration
ms.assetid: fd522b9c-52e2-42fa-939d-343347d5c3b1
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 9ff49f0723153880e88a21376aadec26b250a62b
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66344475"
---
# <a name="fieldkind"></a>FIELD_KIND
指定字段中包含的种类[IDebugField](../../../extensibility/debugger/reference/idebugfield.md)对象。

## <a name="syntax"></a>语法

```cpp
enum enum_FIELD_KIND {
    FIELD_KIND_NONE       = 0x00000000,

    // Type of field
    FIELD_KIND_TYPE       = 0x00000001,
    FIELD_KIND_SYMBOL     = 0x00000002,

    // Storage type of the field
    FIELD_TYPE_PRIMITIVE  = 0x00000010,
    FIELD_TYPE_STRUCT     = 0x00000020,
    FIELD_TYPE_CLASS      = 0x00000040,
    FIELD_TYPE_INTERFACE  = 0x00000080,
    FIELD_TYPE_UNION      = 0x00000100,
    FIELD_TYPE_ARRAY      = 0x00000200,
    FIELD_TYPE_METHOD     = 0x00000400,
    FIELD_TYPE_BLOCK      = 0x00000800,
    FIELD_TYPE_POINTER    = 0x00001000,
    FIELD_TYPE_ENUM       = 0x00002000,
    FIELD_TYPE_LABEL      = 0x00004000,
    FIELD_TYPE_TYPEDEF    = 0x00008000,
    FIELD_TYPE_BITFIELD   = 0x00010000,
    FIELD_TYPE_NAMESPACE  = 0x00020000,
    FIELD_TYPE_MODULE     = 0x00040000,
    FIELD_TYPE_DYNAMIC    = 0x00080000,
    FIELD_TYPE_PROP       = 0x00100000,
    FIELD_TYPE_INNERCLASS = 0x00200000,
    FIELD_TYPE_REFERENCE  = 0x00400000,
    FIELD_TYPE_EXTENDED   = 0x00800000,

    // Specific information about symbols
    FIELD_SYM_MEMBER      = 0x01000000,
    FIELD_SYM_LOCAL       = 0x02000000,
    FIELD_SYM_PARAM       = 0x04000000,
    FIELD_SYM_THIS        = 0x08000000,
    FIELD_SYM_GLOBAL      = 0x10000000,
    FIELD_SYM_PROP_GETTER = 0x20000000,
    FIELD_SYM_PROP_SETTER = 0x40000000,
    FIELD_SYM_EXTENDED    = 0x80000000,

    FIELD_KIND_MASK       = 0x0000000f,
    FIELD_TYPE_MASK       = 0x00fffff0,
    FIELD_SYM_MASK        = 0xff000000,

    FIELD_KIND_ALL        = 0xffffffff
};
typedef DWORD FIELD_KIND;
```

```csharp
public enum enum_FIELD_KIND {
    FIELD_KIND_NONE       = 0x00000000,

    // Type of field
    FIELD_KIND_TYPE       = 0x00000001,
    FIELD_KIND_SYMBOL     = 0x00000002,

    // Storage type of the field
    FIELD_TYPE_PRIMITIVE  = 0x00000010,
    FIELD_TYPE_STRUCT     = 0x00000020,
    FIELD_TYPE_CLASS      = 0x00000040,
    FIELD_TYPE_INTERFACE  = 0x00000080,
    FIELD_TYPE_UNION      = 0x00000100,
    FIELD_TYPE_ARRAY      = 0x00000200,
    FIELD_TYPE_METHOD     = 0x00000400,
    FIELD_TYPE_BLOCK      = 0x00000800,
    FIELD_TYPE_POINTER    = 0x00001000,
    FIELD_TYPE_ENUM       = 0x00002000,
    FIELD_TYPE_LABEL      = 0x00004000,
    FIELD_TYPE_TYPEDEF    = 0x00008000,
    FIELD_TYPE_BITFIELD   = 0x00010000,
    FIELD_TYPE_NAMESPACE  = 0x00020000,
    FIELD_TYPE_MODULE     = 0x00040000,
    FIELD_TYPE_DYNAMIC    = 0x00080000,
    FIELD_TYPE_PROP       = 0x00100000,
    FIELD_TYPE_INNERCLASS = 0x00200000,
    FIELD_TYPE_REFERENCE  = 0x00400000,
    FIELD_TYPE_EXTENDED   = 0x00800000,

    // Specific information about symbols
    FIELD_SYM_MEMBER      = 0x01000000,
    FIELD_SYM_LOCAL       = 0x02000000,
    FIELD_SYM_PARAM       = 0x04000000,
    FIELD_SYM_THIS        = 0x08000000,
    FIELD_SYM_GLOBAL      = 0x10000000,
    FIELD_SYM_PROP_GETTER = 0x20000000,
    FIELD_SYM_PROP_SETTER = 0x40000000,
    FIELD_SYM_EXTENDED    = 0x80000000,

    FIELD_KIND_MASK       = 0x0000000f,
    FIELD_TYPE_MASK       = 0x00fffff0,
    FIELD_SYM_MASK        = 0xff000000,

    FIELD_KIND_ALL        = 0xffffffff
};
```

## <a name="fields"></a>字段
`FIELD_KIND_TYPE`\
指示该字段是仅的类型。

`FIELD_KIND_SYMBOL`\
指示该字段是一个符号，与类型、 名称和其他信息。

`FIELD_TYPE_PRIMITIVE`\
指示该字段为基元数据类型。

`FIELD_TYPE_STRUCT`\
指示该字段是一种结构。

`FIELD_TYPE_CLASS`\
指示该字段是一个类。

`FIELD_TYPE_INTERFACE`\
指示该字段是一个接口。

`FIELD_TYPE_UNION`\
指示该字段是一个联合。

`FIELD_TYPE_ARRAY`\
指示该字段是一个数组。

`FIELD_TYPE_METHOD`\
指示该字段是一种方法。

`FIELD_TYPE_BLOCK`\
指示该字段是一个块。

`FIELD_TYPE_POINTER`\
指示该字段是一个指针。

`FIELD_TYPE_ENUM`\
指示该字段是枚举的数据类型。

`FIELD_TYPE_LABEL`\
指示该字段是一个标签。

`FIELD_TYPE_TYPEDEF`\
指示该字段是其 typedef。

`FIELD_TYPE_BITFIELD`\
指示该字段是一组标志。

`FIELD_TYPE_NAMESPACE`\
指示该字段是一个命名空间。

`FIELD_TYPE_MODULE`\
指示该字段是一个模块。

`FIELD_TYPE_DYNAMIC`\
指示该字段是动态。

`FIELD_TYPE_PROP`\
指示该字段是一个属性。

`FIELD_TYPE_INNERCLASS`\
指示该字段是一个内部类。

`FIELD_TYPE_REFERENCE`\
指示该字段是一个引用。

`FIELD_TYPE_EXTENDED`\
留待将来使用。

`FIELD_SYM_MEMBER`\
指示该字段是成员。

`FIELD_SYM_LOCAL`\
指示该字段是本地。

`FIELD_SYM_PARAMETER`\
指示该字段是一个参数。

`FIELD_SYM_THIS`\
指示该字段是"this"指针。

`FIELD_SYM_GLOBAL`\
指示该字段是全局。

`FIELD_SYM_PROP_GETTER`\
指示该字段检索属性。

`FIELD_SYM_PROP_SETTER`\
指示该字段将设置属性。

`FIELD_SYM_EXTENDED`\
留待将来使用。

`FIELD_KIND_MASK`\
指示字段类型的掩码。

`FIELD_TYPE_MASK`\
指示字段类型的掩码。

`FIELD_SYM_MASK`\
指示符号信息的掩码。

## <a name="remarks"></a>备注
从调用返回[GetKind](../../../extensibility/debugger/reference/idebugfield-getkind.md)方法。

具体取决于类型的字段中， [QueryInterface](/cpp/atl/queryinterface)可以在调用[IDebugField](../../../extensibility/debugger/reference/idebugfield.md)更特定形式的接口的接口。 例如，如果[GetKind](../../../extensibility/debugger/reference/idebugfield-getkind.md)返回`FIELD_TYPE_METHOD`，然后，可以调用`QueryInterface`上我`DebugField`若要获取[IDebugMethodField](../../../extensibility/debugger/reference/idebugmethodfield.md)接口。

## <a name="requirements"></a>要求
标头： sh.h

命名空间:Microsoft.VisualStudio.Debugger.Interop

程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [FIELD_MODIFIERS](../../../extensibility/debugger/reference/field-modifiers.md)
- [GetKind](../../../extensibility/debugger/reference/idebugfield-getkind.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
