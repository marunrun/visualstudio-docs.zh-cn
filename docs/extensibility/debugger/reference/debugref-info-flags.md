---
title: DEBUGREF_INFO_FLAGS |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- DEBUGREF_INFO_FLAGS
helpviewer_keywords:
- DEBUGREF_INFO_FLAGS enumeration
ms.assetid: 1b043327-302a-4f6d-b51d-f94f9d7c7f9d
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: cb10ae5d3b4ce9f8aa777f643d412e075bd5293f
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80737386"
---
# <a name="debugref_info_flags"></a>DEBUGREF_INFO_FLAGS
指定要检索的有关调试引用对象的哪些信息。

## <a name="syntax"></a>语法

```cpp
enum enum_DEBUGREF_INFO_FLAGS {
    DEBUGREF_INFO_NAME             = 0x00000001,
    DEBUGREF_INFO_TYPE             = 0x00000002,
    DEBUGREF_INFO_VALUE            = 0x00000004,
    DEBUGREF_INFO_ATTRIB           = 0x00000008,
    DEBUGREF_INFO_REFTYPE          = 0x00000010,
    DEBUGREF_INFO_REF              = 0x00000020,
    DEBUGREF_INFO_VALUE_AUTOEXPAND = 0x00010000,
    DEBUGREF_INFO_NONE             = 0x00000000,
    DEBUGREF_INFO_ALL              = 0xffffffff
};
typedef DWORD DEBUGREF_INFO_FLAGS;
```

```csharp
public enum enum_DEBUGREF_INFO_FLAGS {
    DEBUGREF_INFO_NAME             = 0x00000001,
    DEBUGREF_INFO_TYPE             = 0x00000002,
    DEBUGREF_INFO_VALUE            = 0x00000004,
    DEBUGREF_INFO_ATTRIB           = 0x00000008,
    DEBUGREF_INFO_REFTYPE          = 0x00000010,
    DEBUGREF_INFO_REF              = 0x00000020,
    DEBUGREF_INFO_VALUE_AUTOEXPAND = 0x00010000,
    DEBUGREF_INFO_NONE             = 0x00000000,
    DEBUGREF_INFO_ALL              = 0xffffffff
};
```

## <a name="fields"></a>字段
`DEBUGREF_INFO_NAME`\
初始化/使用结构`bstrName`中的字段。

`DEBUGREF_INFO_TYPE`\
初始化/使用结构`bstrType`中的字段。

`DEBUGREF_INFO_VALUE`\
初始化/使用结构`bstrValue`中的字段。

`DEBUGREF_INFO_ATTRIB`\
初始化/使用结构`dwAttrib`中的字段。

`DEBUGREF_INFO_REFTYPE`\
初始化/使用结构`dwRefType`中的字段。

`DEBUGREF_INFO_REF`\
初始化/使用结构`pReference`中的字段。

`DEBUGREF_INFO_VALUE_AUTOEXPAND`\
值字段应包含此类型对象的自动展开值（如果可用）。

`DEBUGREF_INFO_NONE`\
指示未设置任何标志。

`DEBUGREF_INFO_ALL`\
指示标志的蒙版。

## <a name="remarks"></a>备注
这些标志将传递给[Enum 子项](../../../extensibility/debugger/reference/idebugreference2-enumchildren.md)和[GetReferenceInfo](../../../extensibility/debugger/reference/idebugreference2-getreferenceinfo.md)方法，以指示要初始化[DEBUG_REFERENCE_INFO](../../../extensibility/debugger/reference/debug-reference-info.md)结构的字段。

用于`dwFields``DEBUG_REFERENCE_INFO`结构的成员，用于指示在返回结构时使用哪些字段并有效。

这些值可以稍微结合`OR`。

## <a name="requirements"></a>要求
标题： msdbg.h

命名空间：微软.VisualStudio.调试器.互通

程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [DEBUG_REFERENCE_INFO](../../../extensibility/debugger/reference/debug-reference-info.md)
- [EnumChildren](../../../extensibility/debugger/reference/idebugreference2-enumchildren.md)
- [GetReferenceInfo](../../../extensibility/debugger/reference/idebugreference2-getreferenceinfo.md)
